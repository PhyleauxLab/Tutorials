### Very Brief Introduction to Command Line Git Version Control

***

**Version**: 0.3.2

**Last Updated**: Sunday, 10 September 2017 

By: **[Lyndon Coghill](@lcoghill)**

***

#### Table of Contents

1. [About Git](#about)
1. [Installing Git](#install)
1. [Configuring Git](#configure)
1. [Tracking Changes](#track)
1. [Remote Servers](#remote)
1. [Branches](#branches)
1. [Useful Resources](#useful)

***


<a name="about"></a>
#### About Git

Version control systems record changes to a file or set of files over time so that you can recall and review specific changes later. They have traditionally been used to manage large source code projects for software development. However, in the last few years more nuanced uses have started to emerge. Researchers are using VCS for tracking datasets, writers are using them to track changes in manuscripts and more recently people are using them to distribute and maintain websites. 

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. Git adds several features previous VCS / SCM systems didn't have:   
1. Context Switching  
2. Role-based control  
3. Disposable experimentation  

These features along with Git's small size, speed, cross-platform availability and more recently web-based distribution platforms (Github, Bitbucket, etc.) have made it the standard in VCM. 

***
<a name="install"></a>
#### Installing Git on Ubuntu
In order to work with Git version control, we first need to install it. Git is maintained in most software repos for Linux, and is available for both Mac and Windows. 

In order to install git on Ubuntu Linux (the virtual machine for this course) we use the apt package management tool with the following command:

	sudo apt-get install git

Press **Enter**

#### Installing Git on Mac OS X

Download Git from [http://git-scm.com/download/mac](http://git-scm.com/download/mac). 

Or you can install it via GitHub for Mac install. Their GUI Git tool has an option to install command line tools as well. You can download that tool from the GitHub for Mac website, at [http://mac.github.com](http://mac.github.com).

#### Install Git on Windows

Another easy way to get Git installed is by installing GitHub for Windows. The installer includes a command line version of Git as well as the GUI. It also works well with Powershell, and sets up solid credential caching and sane CRLF settings. Things you really want. You can download this from the GitHub for Windows website, at [http://windows.github.com](http://windows.github.com).

If you like to live a bit more on the edge, you can try a vanilla version of pure Git. Just go to [http://git-scm.com/download/win](http://git-scm.com/download/win) and the download will start automatically. Note that this is a project called Git for Windows, which is separate from Git itself; for more information on it, go to [https://git-for-windows.github.io/](https://git-for-windows.github.io/). There is no functional advantage of this version over the Github developed version. It just removes the Github connection. 

***

<a name="configure"></a>
#### Configuring Git

Before we can start using git, we will need to configure it. This will allow git to track who makes changes to files. This allows attribution of changes for collaboration on projects, one of the many benefits of using git. To configure Git, we just need to provide our name, and email address. Open up a terminal prompt, or Git terminal in Windows. 

	git config --global user.name "Your Name Here"
	git config --global user.email you@youremail.com
	

The final setting we need to configure is your primary text editor of choice.
 
Changes to files in git repository are always documented. This lets collaborators, or sometimes you go back later and get a gentle reminder what your thoughts were at the time of any change made. Git can launch any text editor you prefer, (nano, emacs, Vi, etc.). We will configure it to work with nano, a small text editor that comes with most Linux distributions and MacOSX and will run in the terminal.

	git config --global core.editor nano

For Windows, there isn't to my knowledge and simple command prompt driven editor. With that being the case, we will configure Git to use the graphical Notepad editor that comes with Windows. 

	git config core.editor notepad

That's it. Git is now installed, and configured. We can start using it. 

***

<a name="track"></a>
#### Tracking Changes With Git

In order to work with Git, we need a project and some files in that project. For the sake of this course, we will make up a project directory to work in. For this example, we can just call our project directory "darwin".

	mkdir darwin
	cd darwin

Now that we have a project directory, we need to initialize it with Git. This only needs to be done when you first decide you want Git to track changes on a project. From inside the project directory use the following command: 

	git init

>Initialized empty Git repository in /darwin/.git/


That's it. Now Git will track all changes made to any files in this directory and any subdirectories below it. 

In order to help you remember what Git is tracking, you'll want to use the "status" command of Git. 
Checking on the status of your git project **frequently** can help you keep track of what's going on in your project. It can also help you avoid mistakes. Try it now. 

	git status

You should see output like the following: 

>On branch master

>Initial commit

>nothing to commit (create/copy files and use "git add" to track)


Ok, now lets create a project file. 

	nano darwin.txt

Now let's enter some text:

***Charles Darwin***

Then we can exit and save our file.

**Ctl-X**  
**Y**  
**Enter**  

If we check on the repository status again:

>	git status

>On branch master

>Initial commit

>Untracked files:
>  (use "git add <file>..." to include in what will be committed)

>	darwin.txt

>nothing added to commit but untracked files present (use "git add" to track)



You can see now that our file is present in the directory and Git sees it, but we aren't currently tracking the changes to this file. This is a good place to mention, Git will *almost* always tell you what to do next if you read the output of the status command. Lets go ahead and add the darwin.txt file to the Git tracker so that we can keep track of any future changes. 

	git add darwin.txt

Let's check out repository status again:

	git status

Now we can see that the file is added to git, and all future changes will be tracked. We can also remove the file from the staging area if we made a mistake. 

	git rm --cached darwin.txt

and check the status:

	git status

Now, we can see that the file has been removed from staging. 
Lets go ahead and add it again:

	git add darwin.txt

and check the status:

	git status

OK, so git should be tracking our file again. The next step is to commit those changes. A commit is a snapshot of our repository. In this case it's only 1 file (darwin.txt), but in a project a commit can include changes to any number of files or folders. It will always commit all changes tracked that are added using the "git add" command from above. So if you don't want to commit a change, don't add it until you're ready. Once a change is commited, we can always look back and see what the change was, who made it, and why. 

Lets commit our changes:

	git commit -m "Added Darwin's name"  
	
> [master (root-commit) 2739ad0] Added Darwin's name  
> 1 file changed, 1 insertion(+)  
> create mode 100644 darwin.txt  


The command above is pretty self explanatory. The -m option is one way we can specify a commit message. This message will always be connected to the commit, so no matter who is looking at the changes, they will be able to get an idea of what changes were made, and why they were made.

Now say we haven't touched this project for a number of... weeks. We are ready to dig back into it, but when we open the file, we see things we don't remember. We can remind ourselves of what changes were made, and why with the git log command. 

	git log  
	
> commit 2739ad0fe4f08bb62f41097f6ac791e3fe972471  
> Author: Lyndon Coghill <lcoghill@fieldmuseum.org>  
> Date:   Mon May 4 10:40:31 2015 -0500  
> Added Darwin's name

Here we see some basic information about our commit.  
1. **Commit SHA**: A unique commit identifier for each commit.  
2. **Author**: Who made the commit  
3. **Date**: When the commit was made  
4. And the **commit message** we added during our commit. 

As you are probably starting to see, the commit message can be critical. You want to use enough information to be informative, but not so much that it can't be read quickly in the log file.

***

<a name="remote"></a>

#### Using a remote Git Server

Now we remember what changes we have made and why. You've decided your work is at a point where you can't risk losing it, or you want to distribute it to collaborators or the world. That's where a service like [Github](www.github.com) or [Bitbucket](www.bitbucket.org) comes in. These are remote Git services that will save your Git repositories on a different server so you or others can always retreive them and see the commits and changes made over time. For personal use, this is a great way to backup your code / projects. For sharing, Github has become the defacto standard to share open-source projects as we will see shortly. Let's go ahead and add a remote server / project. First, let's take a few seconds and create a Github account if you don't have one already. Just go to www.github.com and sign up. It's free and easy.

Lets go to our Github accounts and create an empty repository.   

Step By Step:  
1. Sign into your Github account.  
2. Click on the green "New Repository" button on the right hand side of the page. 
 
![](static/new_repo.png?raw=true) 

You will be presented with a page that contains several options.  

![](static/github_project.png?raw=true) 


Let's go through each one.  
1. Repository Name: The project name. In our case let's just call it **darwin**.  
2. Description: A short, optional description of your project. We can leave this blank.  
3. Public / Private: On Github, all projects are public (open) as default. This means anyone can see everything in them. Most of the time this is OK, but if you want to keep a project private, or only share it with a few people, you'd want to choose the private option. Github charges a small monthly fee for private projects, but they are free on Bitbucket.  
4. Initialize this repository with a README: this can be helpful for others viewing your project to know what it is about. For our case, we can leave this blank for now.  

Finally, click the green **Create repository** button. 


Now that we have those repositories created, we can add a remote link, and push our files to the server. The remote link tells git, that any time you give the push or pull command, you want git to look at this server. 

	git remote add origin https://github.com/yourlogin/darwin.git

Now that we have told our local copy of git where the server is located, we want to copy our project and all commits to the server. We can do that with the following command:

	git push -u origin master

Enter your username and password and press **Enter**. One note, Git will not display any characters when typing your password. 

> Counting objects: 3, done.  
> Writing objects: 100% (3/3), 241 bytes | 0 bytes/s, done.  
> Total 3 (delta 0), reused 0 (delta 0)  
> To https://github.com/lcoghill/darwin.git  
>  * [new branch]      master -> master  
> Branch master set up to track remote branch master from origin.  

Let's go to Github and see if our project is there and make some changes to it. In reality, these changes could be from a different computer, or made by a collaborator and pushed to our remote server. In our case, we will make them online for simplicity. 

If everything worked, you should be able to see your file under the darwin project on Github.com, by visiting [https://github.com/username/darwin/](https://github.com/username/darwin/) and it should look something like the image below.

![](static/github_commit.png?raw=true) 

Now let's go ahead and edit our file online. 
Click the file name darwin.txt You should see a page showing you the contents of the file.
Click on the small pencil icon next to History above the contents window to edit the file.
You will be taken to a page where you can make changes to your file, save them and log a commit message like below. 

![](static/github_edit.png?raw=true) 

Let's go ahead and add a second line to our file:  
1. "On the Origin of Species" or something similar.   
2. Add a commit message  
3. Click **Commit Changes**  

We now have some changes on our remote copy of the repository, we want to copy those changes locally. We can do that with the git pull command. 

	git pull origin master  
	
> remote: Counting objects: 3, done.  
> remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0  
> Unpacking objects: 100% (3/3), done.  
> From https://github.com/lcoghill/darwin  
>  * branch            master     -> FETCH_HEAD  
>    2739ad0..0aecd7a  master     -> origin/master  
> Updating 2739ad0..0aecd7a  
> Fast-forward  
>  darwin.txt | 1 +  
>  1 file changed, 1 insertion(+)  


This should sync our local and rempote repositories, so that they contain the same files, commits, etc. 

What about correcting a mistake? Say for example you made some changes to a file in a project, and it turns out it breaks everything. 

Lets make a change to our darwin.txt file. 

	nano darwin.txt
Add the line:
***"Alfred Wallace was here!"***
and save the file.

We then decided that change was made in error and fortunately Git gives us a way to do that. We can reverse all changes since the last commit by using the checkout command. Lets try that now:

	git checkout -- darwin.txt

this command reverses all changes since the last commit. If we check darwin.txt now, we should see our addition removed.

	cat darwin.txt

***

<a name="branches"></a>

#### Git Branches
One final introductory topic I would like to cover is the idea of branches. Branches, as the name suggests, are different copies of the same Git repository where changes made to one copy don't affect the primary copy. You may have noticed we have been using the parameter "master" when we did pull or push commands. Master is the main branch of any repository. You can have other branches, work with them, push and pull them, and it will never change the master branch until you **merge** them. The graphic below, from the book [Pro Git](http://git-scm.com/book/en/v2), illustrates the idea of branching nicely:

![](static/advance-master.png?raw=true) 


Let's work through a very simple example. 

First lets add a branch called 'test'.

	git branch test

Now let's checkout that branch so that any changes we make are applied to the 'test' branch and not made to the master branch.
	
	git checkout test
>Switched to branch 'test'

Now, we can make some changes to our file. Let's open up the file and add the following line: 

"**Tortoises are more interesting than finches.**" 

Save the file. Then we need to add the file to git tracker, and make our commit.

	git add darwin.txt
	git commit darwin.txt -m 'Added obvious fact'  
	
> [test 4f73941] Added obvious fact  
> 1 file changed, 1 insertion(+)  

Now if we run git status we will see our changes were commited to this branch. 

	git status

>On branch test  
>nothing to commit, working clean directory  

So our critical change is saved on branch **test**, but what if we decided our experimental changes work and we want to move it to our master branch. That is easy to do with git merge. 

First, we need to switch back to the master branch.

	git checkout master  
	
> Switched to branch 'master'  
> Your branch is up-to-date with 'origin/master'.  


Taking a quick look at our file darwin.txt, you can see the new changes aren't there. 

	cat darwin.txt

That's a shame. We can fix it though. In order to incorporate them, we just need to merge our test branch with our master branch using the following command:

	git merge test  

> Updating 0aecd7a..4f73941  
> Fast-forward  
>  darwin.txt | 1 +  
>  1 file changed, 1 insertion(+)  

now if we look at our darwin.txt file, we will see the changes there.

	cat darwin.txt 

all that is left to do is clean up after ourselves. Delete the old branch, and push our changes to the remote server.

	git branch -d test  
	
> Deleted branch test (was 4f73941).

	git push origin master  

> Counting objects: 5, done.  
> Compressing objects: 100% (2/2), done.  
> Writing objects: 100% (3/3), 331 bytes | 0 bytes/s, done.  
> Total 3 (delta 0), reused 0 (delta 0)  
> To https://github.com/lcoghill/darwin.git  
>    0aecd7a..4f73941  master -> master  

***

On a side note, Github has some great features. Make sure to *follow* your favorite developers and *star* your favorite packages. That will provide you with notifications any time those repositories are updated. 

***
<a name="useful"></a>
#### Useful Resources

1. [Git](http://git-scm.com/) - Primary Git SCM website.
1. [Try Git - Code School](https://try.github.io/levels/1/challenges/1) - More interactive practice with Git.
1. [Free Git Pro Book](http://git-scm.com/book/en/v2) Great free in-depth book about Git. 
1. [Github.com](https://github.com/) - Free collaborative web-based portal for Git.
1. [Bitbucket.org](https://bitbucket.org/) - Free collaborative web-based protal for Git.

