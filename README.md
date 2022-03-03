# git cheat-sheet

The git command-line utility has plenty of inconsistencies
http://steveko.wordpress.com/2012/02/24/10-things-i-hate-about-git/

A GUI like http://sourcetreeapp.com is often helpful, but staying on the command line usually quicker.
This is a list of the commands I use most frequently, listed by functional category:

### current state
`git status`					list which (unstaged) files have changed  
`git diff`						list (unstaged) changes to files  
`git log`						list recent commits  


### adding files to repo
`git add fn`					stage file  
`git commit -m 'message'`			commit file  
`git commit -am 'message'`		add/commit all changes from all tracked files (no untracked files) in one go  

### undoing previous actions
http://git-scm.com/book/en/Git-Tools-Rewriting-History  
`git reset filename`				unstage file  
`git commit --amend -m 'message'`	alter the last commit (add any staged files, new comment)  
`git reset --soft HEAD^`			undo previous commit, put changes in staging  
`git reset --hard HEAD^`			Undo last commit and all changes  
`git reset --hard HEAD^^`			Undo two (^^) last commits and all changes  
`git checkout -- cats.html index.html`	Undo all changes that were made to files cats.html and index.html  
`git rebase --onto <commit-id>\^ <commit-id> HEAD`	remove specific commit from repository. the \ in \^ is just an escape   char to make zsh play nice and is not necessary if using bash.  

### remote repositories
`git remote add origin git@example.com:example/petshop.git` add a remote repository  
`git push -u origin master`			push current local repo to remote. -u sets it to default for the future  
`git remote -v show`				show the available remote repositories that have been added  
`git pull`						checkout and merge remote changes in one go  
`git fetch origin`						update the local cache of the remote repository  
`git remote -v update`				bring remote refs up to date (and -v show which branches were updated)  
`git status -uno` will tell you whether the branch you are tracking is ahead, behind or has diverged. If it says nothing, the local and remote are the same.  
`git show-branch *master` will show you the commits in all of the branches whose names end in master (eg master and origin/master).  
`git show remote origin`			show local<->remote branch tracking and sync status  


### Examine changes on remote, without pulling them
`git fetch origin`  
`git log HEAD..origin/master --oneline` shows commit messages  
`git diff HEAD..origin/master` shows all changes on remote compared to local HEAD  


### Branches
`git branch`						list currently existing branches  
`git branch [branchname]`			create new branch  
`git checkout branchname`			move to that branch  
`git checkout -b branchname`			create and checkout new branch in one go  
`git branch -d branchname`			remove branch  

#### merging branch back to master
`git checkout master; git merge branchname;`	conditions for fast-forward merge - nothing new on master between branch start/end points  

### branches on remote
`git fetch origin``git branch -r` 		list remote branches (after a fetch)  
`git push origin :branchname`		delete remote branch 'branchname'  
`git remote prune origin`			clean up deleted remote branches (let's say someone else deleted a branch on the remote)  
`git remote show origin`			show local<->remote branch tracking and sync status (duplicate info under "remote repositories")  


#### push local branch to differently named remote branch. Eg Heroku only deploys master
`git push heroku yourbranch:master`       simple form  
`git push heroku-staging staging:master` 	(localBranchName:remoteBranchName)  

### tagging
`git tag`	list all tags  
`git checkout v0.0.1`	checkout code  
`git tag -a v0.0.3`	-m 'Version 0.0.3'	add new tag  
`git push --tags`	push new tags to remote  

### dealing with large files - keep them outside the repo on an ssh machine.
http://stackoverflow.com/questions/540535/managing-large-binary-files-with-git  
http://git-annex.branchable.com/walkthrough/ #see ssh section  

`git annex add mybigfile`  
`git commit -m 'add mybigfile'`  
`git push myremote` 
`git annex copy --to myremote mybigfile` this command copies the actual content to myremote  
`git annex drop mybigfile`  remove content from local repo  
`git annex get mybigfile`   retrieve the content  
`git annex copy --from myremote mybigfile`specify the remote from which to get the file  


### connect through remove url using ssh key

`Create a new repository, or reuse an existing one on git.` <br/>
`Generate a new SSH key:`

`ssh-keygen -t rsa -C "your_email@example.com"` <br/>
`Copy the contents of the file ~/.ssh/id_rsa.pub to your SSH keys in your GitHub account settings.`

`Test SSH key:` <br/>

`$ ssh -T git@github.***.***.corp` <br/>
`Hi developius! You've successfully authenticated, but GitHub does not provide shell access.` <br/>
`Change directory into the local clone of your repository (if you're not already there) and run:` <br/>

`git remote set-url origin git@github.com:username/your-repository.git`


### Local vs Remote Command

#`git Local repository command `

`git init`			 				initialize local git repository <br/>
`git status`							Stage check for file <br/>
`git add file_name`						Add file for stage <br/>
`git add .`							Add all file for stage <br/>
`git commit -m "message"`					Commit file <br/>
`git log `							History of commit  <br/>
`git diff file_name `						Compare committed file and current file <br/>
`git checkout file_name`					Rollback previous version <br/>
`git branch branch_name` 					Create new branch in git local <br/>
`git branch`							List down number of branches <br/>
`git checkout branch_name`					Change branch in cmd <br/>
`git merge branch-name`						Merge branch_name to master <br/>
			

#`git Remote repository command `

`git remote add origin  git_repo_name`    			set remote repository  <br/>
`git push -u origin master`					Push local file to remote in master branch <br/>
`create file name .gitignore `					Add filename inside .gitignore to ignore stage and commit  <br/>
`git rm --cached -r .`						Remove all file from staging area <br/>
`git clone git_repo_name`					Clone the project to local machine <br/>
`git clone --branch <branchname> url`				Clone from specific branch1 <br/>


*****************


### BTP Commands

`Create a new Account in SAPÂ® BTP
`https://account.hana.ondemand.com/
 
`Install CF CLI
`https://github.com/cloudfoundry/cli/wiki/V6-CLI-Installation-Guide
 
`Important and Basic CF CLI Commands:
https://cli.cloudfoundry.org/en-US/v6/
	
`$ cf version
`Version of CF CLI
	
`$ cf login
`Login to Cloud Foundry via CLI
 
`Flags:
`	-a API_URL Example: https://api.cf.eu10.hana.ondemand.com
`	-u USERNAME Example: Email ID
`	-o ORG
`	-s SPACE
`$ cf marketplace
`Getting services from marketplace	
`$ cf buildpacks
`Check What are all the App Buildpacks  Can be used
`$ cf apps
`List all apps in the target space
`$ cf start|stop|restart <app-name>
`Start or Stop or Restart an App
`$  cf logs <app-name> --recent
`Check Logs of the App
`$ sudo cf app <App Name>
`Check health and status for the app
`$ sudo cf scale <App Name> -i INSTANCES
`Number of Instance of the App with i in integer
`$ sudo cf scale <App Name> -m 
`Memory limit example 256M, 1024G, 1G etc.
`$ sudo cf scale <App Name> -k
`Disk Limit example 256M, 1024G, 1G etc.
`$ sudo cf delete <App Name>
`Delete the App and -f for forced 
`Checked Backedn connectivity - 
`$ curl -v -i "<Destination_Name>.dest/sap/opu/odata/iwfnd/catalogservice;v=2/ServiceCollection?%24top=1"

