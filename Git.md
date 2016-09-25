Git

Thursday, July 02, 2015

15:09

 

Mydu : my@43du

Git : git@123

Tntuser : tntuser@123

 

**git clone <promonuser@10.155.104.110:/opt/git/promos.git> **

** **

Pass: pro@123

 

getent group &lt;groupname&gt; : list users

> **Create new empty shared Git repository**
>
> Steps cover:

-   set up of an empty bare Git repository,

-   clone of it from remote machine,

-   push and pull to remote repository from local development machine

<!-- -->

-   Set up new local group that would be allowed to push new changes and
    > empty Git bare repo:\
    > **addgroup &lt;groupname&gt;\
    > git init --bare --shared=group &lt;nameofrepo&gt;.git**

-   Set up ownership and permissions correctly\
    > **chgrp -R &lt;groupname&gt; &lt;nameofrepo&gt;.git**

-   Set up user(s) and add it to &lt;groupname&gt; group:\
    > **adduser &lt;username&gt;\
    > usermod -aG &lt;groupname&gt; &lt;username&gt;**

-   Clone shared repository to local machine\
    > **git clone
    > &lt;username&gt;@&lt;server&gt;:/path/to/git/repo\[.git\]
    > &lt;directory\_name&gt;**

-   Push and pull changes test\
    > **pull origin\
    > push origin master**

> **Create shared git repository for exiting project**
>
> Steps cover:

-   set up of bare repository for existing project on the same server

<!-- -->

-   turn existing project into Git repository\
    > **cd /path/to/project\
    > git init**

-   clone this repository on the same server into bare Git repository
    > that will be shared - main bare repository for this project\
    > **git clone --bare --no-hardlinks /path/to/exiting/git/repo
    > path/to/new/bare/git/&lt;reponame&gt;.git**

-   To make a private bare repo group shared: edit config file and
    > add **sharedRepository = group** to the \[core\] section

-   Fix permissions and ownership:\
    > **chgrp -R &lt;groupname&gt; &lt;reponame&gt;.git\
    > cd &lt;reponame&gt;.git\
    > find . -type f | xargs chmod g+w\
    > find . -type d | xargs chmod g+ws**

> When creating shared Git repository make sure that:

-   File permissions and ownership is set correctly on the shared
    > repository

-   In config file under \[core\] section we have line that says:
    > "sharedRepository = group" or true

-   Shared remote repository should be bare repository and should end
    > with .git extension

>  
>
> From
> &lt;<http://webdevsphere.com/article/create-shared-git-repository>&gt;
>
>  

-   Initialize to non empty directory

>  
>
> git init\
> git remote add origin PATH/TO/REPO\
> git fetch\
> git checkout -t origin/master
>
>  
>
> From
> &lt;<http://stackoverflow.com/questions/2411031/how-do-i-clone-into-a-non-empty-directory>&gt;
>
>  
>
>  
>
>  
>
> Git:
>
>  
>
> git remote show origin
>
> git remote
>
> git remote add origin git@tvmatp236424d:/opt/git/pms.git
>
> git remote rm origin
>
>  
>
> git add --all
>
> git commit -m "Modules"
>
> git push origin master
>
> git clone git@tvmatp236424d:/opt/git/pms.git
>
> git pull origin master
>
> find . -type d -exec chmod g+s '{}' +
>
>  
>
> git diff --stat --cached origin/master
>
> git reset
>
>  

 

New git root pass: invisible
