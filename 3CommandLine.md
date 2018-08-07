# Introduction to Git and GitHub: Git on the command line

####Before class:
* set up shell:
	* enlarge text size
	* `export PS1='$ '`
	* `export PROMPT_COMMAND="history 1 >> ~/Dropbox/GitHistory.txt"`
* check software installation for git AND account with GitHub
* need proxy?
* get slides setup
* remind students to register for GitHub account
* XKCD comic: https://xkcd.com/1597/

####Reources
* class website: http://ouinformatics.github.io/2015-05-27-osu 
* etherpad: https://etherpad.mozilla.org/2015-05-27-osu
* Kate's history: https://www.dropbox.com/s/nvpwfcrjgen60z4/GitHistory.txt?dl=0 
* Git for beginners: http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide 
* fixing detached head: http://stackoverflow.com/questions/10228760/fix-a-git-detached-head 
	
####SETUP
**Objectives:** get system set up for proper attribution of your work

* Slides: run locally, Git.pdf
* open shell, can be anywhere
* specify your name, to be recorded in commits
* `git config --global user.name "k8hertweck"`
	* specify your email, to be recorded in commits
* `git config --global user.email "k8hertweck@gmail.com"`
	* specify text editor, to be used in committing
	* nano: `git config --global core.editor "nano -w"`
	* text wrangler: `git config --global core.editor "edit -w"`
	* notepad++: `git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`
	* kate: `git config --global core.editor "kate"`
* `--global` means will apply for every command entered afterward
* check settings: `git config –list`
* syntax for git: `git VERB`	

####CREATING A REPO (WORKING LOCALLY)
**Objectives:** start tracking versions in a particular folder/directory (repository)

* start in home directory
* create directory and change directories
* `mkdir planets`
* `cd planets`
* tell git where to store old records and versions of file
	* `git init`
* list contents: `ls`
* list everything (including hidden files)
	* `ls -a`
* result is a subdirectory with information about project
* if this is removed, we don't have access to versioning anymore
* ask status of project
* `git status`
* output also adds helpful comments
* Socrative question 1

####TRACKING CHANGES: 
**Objectives:** practice workflow (modify-add-commit), explain where information is stored

* create new file: nano mars.txt
* copy and add text, exit and save, `ls`, `cat mars.txt`
* show status of project: `git status`
	* draw attention to "untracked files": there's something not being tracked
* add file: `git add mars.txt`
* `git status` draw attention to "Changes to be committed": it's tracking, but the changes aren't recorded
* commit file: `git commit -m "creating script"`
	* commits record to history in .git, called a revision, with short identifier
	* run without -m and will open editor to add comment (you've specified your preference earlier today)
	* good commits: brief (<50 characters), for more info, add empty line (adds in separate field)
* `git status`
* check history: `git log`
	* lists all revisions in reverse chronological order: full identifier (relate to short identifier, same initial characters),
	* when created, log message
* make another change (this is just one way): `nano mars.txt`, `cat mars.txt`
* check status: `git status`
* look at differences: `git diff`
first line: old and new version of files, similar to diff command in Unix
second line: labels for revisions
third and fourth: name of file changing
last lines: actual changes
commit changes: git commit -m "adding change"
but change hasn't been added!: git add, git commit
working through staging
nano morning.txt, make change, cat morning.txt
look at differences: git diff
stage file: git add morning.txt, git diff (no output)
git diff –staged (shows differences)
git commit -m, git status, git log
git commit workflow
Socrative question 2

####EXPLORING HISTORY
Objectives: identify and use Git commit numbers, compare versions, restore old versions

compare different versions of commits
HEAD~1 (HEAD minus 1) and HEAD~2 refer to old commits: most recent end of chain is HEAD
git diff HEAD~1 mars.txt
git diff HEAD~2 mars.txt
git log gives strings of digits and letters: git diff XXXXXXXX mars.txt
can also just use first few characters: git diff XXX mars.txt
how to revert to old version?
make another change, git status
git checkout to remove unstaged changes (default to previous committed version)
git checkout XXX mars.txt
remember that you want changes before most recent commit 
Socrative question3

####IGNORING THINGS
Objectives: ignore some files, why ignoring is useful

sometimes backup files are created by other programs, or intermediate files we don't want to track
create dummy files 
mkdir results, touch a.dat b.dat c.dat results/a.out results b.out
git status: lots of stuff needs to be committed, but we don't want to!
nano .gitignore, add *.dat and results/
git status: now .gitignore is the only thing there!
git add .gitignore, git commit -m “add ignore file”, git status
git add a.dat: error
git status --ignored

####REMOTES IN GITHUB
Objectives: explain why remote repos, clone remote repos, push/pull

Github is cool because collaboration!
we've been working in local repo, so we're the only ones who can see our work
GitHub is a remote repo that can be published for other folks to see
log in to GitHub, click icon in top right corner, create repo called “planets”
resulting page has info about configuring repository, it's done the mkdir planets, cd planets, git init process remotely
connect the two repos: copy https url to clipboard
go to local repo (in shell): git remote add origin https://github.com/k8hertweck/planets
git remote -v: check that it worked
origin is a nickname for remote repo
now send local changes to remote repo: git push origin master
check remote repo, changes should be there.
create README file and add brief comment about the purpose of the materials, commit change, go back to terminal: git pull origin master

## Wrapping up