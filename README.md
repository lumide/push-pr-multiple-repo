# Push Pull Request to multiple repos in your organization

### The main aim here is to use GH Cli to create a PR to multiple repository in Github using a for loop statement from your local environment following the git workflow below

- Clone git branch
- Checkout to development branch
- Create a feature branch
- Make changes to code
- Add and commit changes
- Push 
- Create PR

## **Prerequisite**

* Basic experience with Linux commands and Scripting
* Basic experience with Git (Pull, Push, Commit, Add ...)

## **Tools Needed**

* GH Cli
* Code Editor - [Terminal, Visual Code Studio]
* Git
* JQ - optional, to filter JSON outputs

## **First Step (Installation of Tools)**

* [Install GH Cli -> ](https://cli.github.com/manual/installation)
* [Install Git -> ](https://git-scm.com/downloads)
* [Install JQ : Optional -> ](https://stedolan.github.io/jq/download/)


After installations, you have to authenticate gh cli by running the command 
`gh auth login` 

## You can find the extensive gh cli commands [Here -> ](https://cli.github.com/manual/)
-
<img width="611" alt="image" src="https://user-images.githubusercontent.com/24320233/232786524-a38dbd33-8295-498b-97b7-0a8042e14e61.png">
-

Sign in with credentials and paste the code generated and authorize

Ensure other tools are installed also

Script to be ran locally:
```
for repo in $(gh repo list <git.username> --no-archived -L 5 --json "owner,name" --template '{{range .}}{{tablerow (.name) }}{{end}}'); do
 
        git clone https://github.com/<git.username>/${repo}.git
        cd ${repo}
        git checkout development
        git checkout -b Feature-branch
        cp /path/to/file/test.txt .
        git add .
        git commit -m "Add test config file"
        git push -u origin Feature-branch
        gh pr create --base development --head Feature-branch --title "Add test config file" --body "Add test config file" 
        cd ..
 
done
```
<git.username> should be replace with your username on git

* **gh repo list <git.username>** - The script above runs a for loop statement checking your github account for repos 
* **--no-archived:** Excludes archived repos
* **-L:** 5 repos are checked
* **--json:** Output format
* Clones the repo
* Changes Directory to the clone repo
* Checkout to development branch
* Create a feture branch from the development branch
* Copys the file 
* Runs git add 
* Runs git commit
* Runs git push
* And cretaes the PR
* Changes directly to run the script all over until it is ran for all the 5 repo
