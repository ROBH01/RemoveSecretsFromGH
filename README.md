# Removing secrets from GH
This repo is more of a guidance on how to remove secrets e.g. passwords and keys from GitHub History on a specific repo.

<br />

### 🙋 Is this for me?
If you accidentally or unknowingly pushed sensitive information such as passwords and keys to GH, across multiple commits, a new commit with the 'masked' changes will not help. This is because files have a history and sensitive information can still be seen in previous versions of the files. There are, however, different ways to address this:

- Change all credentials, without committing the new ones (add them to .gitignore). This way, previous passwords or api keys won't work, and the new credentials will only be known to you.

Although old credentials won't work, they can still be seen which in some situations may not help much as it could give hints on future passwords or formats used.
To completely address this, the safest and quickest way that worked for me is to mask them altogether from all the commit history by replacing them with something else.
To achieve this, the **bfg tool** can be used.

<br />

### 💻 Replacing sensitive info using **BFG Repo Cleaner** tool and VSCode
1. Download the BFG Repo Cleaner (requires java runtime in your system): [BFG Repo Cleaner](https://rtyley.github.io/bfg-repo-cleaner/).
2. Ensure that the repo needing change is cloned locally in VSCode (or any Editor) and is in a clean state.
3. Remove/Replace all the desired sensitive information and Stage -> Commit -> Push all those changes.
4. Create a new file in the root folder of your local repo and name it **password.txt**. Once created, insert all the secrets that you want to remove from the repo, ensuring that **every** secret is on a new line.

        1 ThisIsMyPa$$10
        2 This is something else I want to remove

5. Open a new cmd line and navigate to the root of your repo and run the following command `java -jar [PATH_TO_BFG e.g. C:\Users\Mike\Desktop\Tools\bfg-1.14.0.jar] --replace-text password.txt`.
6. Locally, all the commit history is now re-written, replacing each secret from password.txt with a **REMOVED** text. To make those changes available in your GH repo, you need to force push those local changes using `git push --force origin [branch e.g. main]`. To apply the changes to all the branches, it is necessary to run the command for each branch.
The option `--force` is needed because the history rewrite made every commit hash change starting with the first commit that contained any secret from the password.txt file.
7. All is now completed and the password.txt file is no longer needed.

<br />

*Note: A copy of BFG (v1.14.0) is attached to this repo.*

<br />

#### 🔗 References:
- [BFG Repo Cleaner download page](https://rtyley.github.io/bfg-repo-cleaner/)
- [Remove GH History article](https://www.claudiobernasconi.ch/2021/06/04/how-to-remove-secrets-from-git-history/)
