# Remove-Files-Git-History

1. Install git filter-repo:

First, ensure that git filter-repo is installed. You can install it using pip (Python package manager) if you don't have it installed yet. 

Go to the official Python website and download the latest version of Python for Windows (make sure to download Python 3.x).

Run the Python installer and during installation, make sure to check the box that says "Add Python to PATH". This ensures that Python and pip are available from the command line.

Install git filter-repo using pip:

```
pip install git-filter-repo
```
If you're using Homebrew on macOS, you can install it like this:
```
brew install git-filter-repo
```
You can verify the installation with:
```
git filter-repo --version
```
2. Clone the Repository (if not already in the local repo):
If you haven't cloned your repository yet, do so using:
```
git clone https://github.com/your-username/your-repository.git
cd your-repository
```
3. Create a Backup (Important!):
Since git filter-repo rewrites your Git history, it’s important to create a backup of your repository first, just in case anything goes wrong. You can create a backup using:
```
git clone --mirror https://github.com/your-username/your-repository.git your-repository-backup.git
```
4. Run git filter-repo to Remove .env:
Once you're inside the local copy of your Git repository, use git filter-repo to remove all .env files from the entire history.
```
git filter-repo --path .env --invert-paths
```
This will delete the .env file from all commits in the repository history. The --invert-paths flag ensures that .env files are removed (as opposed to just kept).

Note: If .env is in multiple subdirectories, this command will handle that as well.
5. Clean Up the Repository:
After running the git filter-repo command, it’s important to run Git garbage collection to clean up the repository and remove any dangling references to deleted files.
```
git reflog expire --expire=now --all=now
git gc --prune=now --aggressive
```
6. Force Push the Changes to GitHub:
Since you’ve rewritten the Git history, you'll need to force push the changes to your GitHub repository.
```
git push --force
```
This will overwrite the history on GitHub with the new, cleaned history.
