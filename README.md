# Bash Cheat Sheet 
Most important bash commands for researchers and data scientists. 

The set-up of this cheat sheet is inspired by an existing [cheat sheet](https://github.com/tiimgreen/github-cheat-sheet) initated by [Tim Green](https://github.com/tiimgreen).

****************************************************
****************************************************
## Table of Contents
 - [Managing processes](#managing-processes)
  - [First-aid procedure for killing a running process](#first-aid-procedure-for-killing-a-running-process)
  - [Cronjobs and Crontab](#cronjobs-and-crontab)
  - [Tmux sessions](#tmux-sessions)
  - [Bash profiles](#bash-profiles)
  - [Git](#git)
 - [Python](#python)
 	- [Virtual environments](#virtual-environments)
	- [Check which python packages are installed](#check-which-python-packages-are-installed)
	- [Start scrapy project](#start-scrapy-project)
 - [R](#r)
 - [SQL and SQLite](#sql-and-sqlite)
 - [Text editing and LaTeX](#text-editing-and-latex)
  - [Calculate the number of words in a Latex file](#calculate-the-number-of-words-in-a-latex-file)

****************************************************
****************************************************
## Managing processes

****************************************************
### First-aid procedure for killing a running process
* open new terminal window
* type `ps + enter`
* identify PID (processid) of the process
* type `kill -9 <PID>`

OR:
* `control + C` (twice if needed)


****************************************************
### Cronjobs and Crontab

#### Schedule crontab task
* If you want to run the cronjob on a server: enter the server
* enter `crontab -e` in the terminal
* enter `<minutes> <hours> <day of month> <month> <day of week>`
 * for example `6 0 * * 1-6 cd /home/annerose/Python/continuousscraper/ && python processcontrol.py new`
 * this signifies that the process will start to run Monday through Saturday at 6 minutes past midnight.

For more information, see 
* [http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html](http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html) and 
* [http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment](http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment)

#### Kill an existing cronjob
* enter `ps -e` in the terminal to see all existing processes.
* termine which processid your process has.
* enter `kill -9 <processid>`


****************************************************
### Tmux sessions
Tmux allows to keep processes running after ending an ssh session. For more detailed explanation, see [here](http://askubuntu.com/questions/8653/how-to-keep-processes-running-after-ending-ssh-session).

* ssh into the remote machine
* start tmux by typing `tmux` into the shell
* start the process you want inside the started tmux session
* leave/detach the tmux session by typing `Ctrl+B` and then `D`

You can now safely logoff from the remote machine, your process will keep running inside tmux. When you come back again and want to check the status of your process you can use `tmux attach` to attach to your tmux session.

If you want to have multiple session running side-by-side you should name each session using `Ctrl-B` and `$`. You can get a list of the currently running sessions using `tmux list-sessions`.

Some more useful tmux commands (see also this [video](https://www.youtube.com/watch?v=BHhA_ZKjyxo)):

| Command        | Significance          |
| ------------- |-------------| 
| `control + -b <command>`      | to tell the shell that it's for tmux and not just normal shell. | 
| `control + -b  p`    | previous window      | 
| `control + -b  n` | next window |
|`control + -b  c` | create window |
|`control + -b  w` | list windows |
|`control + -b %` |split window vertically into two parts |
|`control + -b` | split-horizontally : split window horizontally |
|`tmux - new s <sessionname>` | create a new tmux session |
|`control + -x`  | close (kill) tmux pane|
|`control + -b d` | detach from tmux session. (without stopping the process) |
| `tmux list-sessions` | List all tmux sessions|
|`tmux attach -t <sessionname>` | attach to a certain tmux session|
|`tmux attach` |attach all tmux sessions/ any tmux session |

****************************************************
### Bash profiles
#### Create bash profile
`touch ~/.bash_profile; open ~/.bash_profile`

`touch` creates the file, so no need to run this command when the file already exists.  
`open ~/.bashrc` is also possible.

For editing the .bash_profile. opens in a text editor. See [here](http://stackoverflow.com/questions/30461201/how-do-i-edit-path-bash-profile-on-osx)

****************************************************
### Git
#### Clone repository from GitHub to local machine
* create new repository on GitHub
* go to the directory on your local machine where the cloned repository should be saved.
* type `git clone https://github.com/your-name/repository-name.git`
* the repository should no appear in the local folder on your machine.

#### Commit file from terminal
* go to the directory of your repository inside the terminal
* type `git add .` . This recurses into sub-directories. Alternative: `git add` or `git commit -a`
* `git commit -m “your commit message”`. Commit the changes.
* `git push`. Push the changes.

To see the status of your repository: `git status`.

See [this](http://shaun.boyblack.co.za/blog/2009/03/14/getting-started-with-git-on-mac-os-x/) useful blog.

#### global .gitignore file
See [here](http://stackoverflow.com/questions/7335420/global-git-ignore)

Create a global .gitignore file (file types to be excluded from every git project):  
`git config --global core.excludesfile ~/.gitignore_global`

The file is found under Documents/Username (as a hidden file). Open it in a text editor to edit it and add files you don’t want to
sync with git/GitHub.

#### local .gitignore file
enter  
`touch .gitignore`  
in the terminal under the working environment of the project you want to commit to github. 

The file is found locally in the working environment of the project. Open it in a text editor to edit it and add files.

****************************************************
****************************************************
## Python

****************************************************
### Virtual environments

#### Change virtual environment: 

```bash
workon <name of virtual environment>
workon annerose2015-11  # python 2 environment
workon annerose_python3_2016-07 # python 3 environment
```

How to set up and manage virtual environments in Ubuntu:   [http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu](http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu)


#### Configure Pycharm to use a virtual environment

`touch ~/.pycharmrc; open ~/.pycharmrc`  
See [here](see http://stackoverflow.com/questions/22288569/how-do-i-activate-a-virtualenv-inside-pycharms-terminal).

Then set the shell Preferences->Tools->Terminal->Shell path to  
`/bin/bash --rcfile ~/.pycharmrc`


****************************************************
### Check which python packages are installed

```bash
pip freeze
```

****************************************************
### Start scrapy project
Start [scrapy](http://scrapy.org) project for webscraping: enter the following command
in the terminal (in the directory where you want to start your project).

`scrapy startproject name_of_project`


****************************************************
****************************************************
## R
* Open new RStudio window from terminal (e.g. when one RStudio needs to run for an extended period of time):
 * enter `open -n -a "rstudio"` in terminal
* How to add an RStudio project to Github: [https://www.r-bloggers.com/rstudio-and-github/](https://www.r-bloggers.com/rstudio-and-github/)

Add the following commands in shell after having created the project in Github:
```bash
git remote add origin https://github.com/your-name/repository-name.git  
git config remote.origin.url git@github.com:your-name/repository-name.git  
git pull -u origin master  
git push -u origin master  
```

****************************************************
****************************************************
## SQL and SQLite

****************************************************
### Repair corrupt database
How to repair db database: see 
[stackoverflow](http://stackoverflow.com/questions/5274202/sqlite3-database-or-disk-is-full-the-database-disk-image-is-malformed)

```bash  
echo '.dump'|sqlite3 corrupt.db|sqlite3 corrupt_fixed.db  
cat <( sqlite3 corrupt.db .dump | grep "^ROLLBACK" -v ) <( echo "COMMIT;" ) | sqlite3 corrupt_fixed.db
```

****************************************************
### Merge two SQLite databases
http://stackoverflow.com/questions/3689694/merge-sqlite-files-into-one-db-file-and-begin-commit-question    
http://stackoverflow.com/questions/80801/how-can-i-merge-many-sqlite-databases    
Leaving out duplicates:
http://sqlite.1065341.n5.nabble.com/Merging-two-SQLites-leaving-out-duplicates-td46337.html



****************************************************
****************************************************
## Text editing and LaTeX

****************************************************
### Calculate the number of words in a Latex file
* change the working directory of your terminal to where the LaTeX TeX file is located.
* enter `detex <document_name>.tex | wc -w -c -l` or just `detex <document_name>.tex | wc`
* to calculate word count in pdf document: `pdftotext <document_name>.pdf - | wc -w`
