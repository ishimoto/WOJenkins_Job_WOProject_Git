WOJenkins\_Job\_WOProject\_Git
================================

**1.** Change directories into JENKINS\_HOME/jobs

>$ cd /Users/Shared/Jenkins/Home/jobs/

**2.** Clone job configuration from github.com repository

>$ sudo git clone https://github.com/ishimoto/WOJenkins_Job_WOProject_Git.git NAME\_OF\_MY\_WO\_PROJECT

**3.** Set correct ownership and permissions - If you used the Mac OSX Jenkins installer, the user and group that it will be using are both "jenkins"
 
>$ sudo chown -R jenkins:jenkins NAME\_OF\_MY\_WO\_PROJECT

**4.** Open Jenkins and tell it to reload the configuration files so it will see the new job

>Jenkins -> Manage Jenkins -> Reload Configuration from Disk

**5.** Open the new Job

>You should see a new job called NAME\_OF\_MY\_WO\_PROJECT

**6** Add a deploy key to your github Account

github -> Application Git Repository -> Repository Settings -> Deploy keys

--

**BUT** there is a problem

>Accessing multiple private GitHub repositories without a dedicated build user


This is because you can only use an SSH key once as a deploy key. The idea is to create an SSH key pair for every private GitHub repository. 

**6.1** creating a second ssh key
> ssh-keygen -t rsa -f ~/.ssh/id_rsa.REPONAME

The prompt will ask for a password, however, setting a password in this case is not recommended. When the keys are accessed, there is no user logged onto the build machine to type the password. After creating the key pair the public key can be found in ~/.ssh/id_rsa.REPONAME.pub. This is the key that acts as the deploy key for a repo on GitHub.

**6.2** creating a config file, so ssh knows which certificate has to be used

~/.ssh/config

>Host github-NAME\_OF\_MY\_WO\_PROJECT<br />
>HostName github.com<br />
>User ishimoto<br />
>IdentityFile /Users/Shared/Jenkins/.ssh/id\_rsa.NAME\_OF\_MY\_WO\_PROJECT<br />

**6.3** set the 'PROJECT\_GIT\_REPOSITORY' from

git@github.com:ishimoto/NAME\_OF\_MY\_WO\_PROJECT.git to git@github-NAME\_OF\_MY\_WO\_PROJECT:ishimoto/NAME\_OF\_MY\_WO\_PROJECT.git

--

**7.** Build

**注意：** https://issues.jenkins-ci.org/browse/JENKINS-16523
