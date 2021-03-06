# Jenkins Best Practices

* https://en.wikipedia.org/wiki/Continuous_integration<- Read this!
* https://wiki.jenkins-ci.org/display/JENKINS/Jenkins+Best+Practices
* http://www.slideshare.net/andrewbayer/7-habits-of-highly-effective-jenkins-users
* Set up version control of job configurations
* Keep jobs simple! Don't put a ton of bash in each job. If a job needs to do something complex, put it in a script in GitHub and check it out as needed.
* Use templated builders to simplify common tasks
* Keep all scripts in version control - avoid running scripts that live on the Jenkins server filesystem
* Don't install unnecessary plugins - plugins are often written by third parties and can interact with each other in strange ways
* Use LDAP authentication if possible for traceability - avoid anonymous access
* If possible, set up user/group roles so that only the people who need access to the internals of Jenkins have access
* Backup artifacts
* Keep Jenkins up to date! Out of date installations tend to rot.
* Tie jobs into Sonar to track code quality
* Commit often! It's easier to collaborate on code when everyone is constantly integrating their changes.
* Job names in Jenkins should not use spaces - directories are created for each job, and some tools don't support directories with spaces 
* You can enforce this with the Restrict Project Naming global configuration using the pattern \S*
* Set up a Jenkins display where everyone can see when your jobs are failing

### Guy's Favorite Jenkins Plugins
* Doony: Not quite a plugin, but it's a set of easy-to-install UI improvements for Jenkins. http://doony.org/
* AnsiColor: Colorized console logs.
* Build Monitor Plugin: Pretty live job status monitor. 
* Build Trigger Badge Plugin: At a glance, see why each build was triggered - an upstream job, a manual trigger, an SCM trigger, etc.
* Console Tail Plugin: See the last n lines of the latest build on a job's main page. Find out why your build failed without digging through logs.
* Embeddable-build-status: Show your build status with a live icon you can embed in your GitHub readme.
* Jenkins disk-usage plugin: Easily keep track of your disk space usage on the Jenkins master.
* Jenkins Jabber notifier plugin: Notify chatrooms and users of build failures.
* Jenkins Workspace Cleanup Plugin: Delete your workspace before or after builds. Ensure a fresh build every time.
* Monitoring: Track Jenkins master and slave performance. This is crucial when your Jenkins installation starts acting funny and you want to know why.
* Naginator: Automatically re-run failed builds, in case they failed due to an environmental issue.
* ShiningPanda Plugin: Creates Python virtualenvs for you to work in.
* Template Project plugin: Use jobs as templates for other jobs. Lets you easily manage multiple jobs that share a similar configuration.
* Timestamper: Timestamp your console logs.
* SCM Sync Configuration Plugin: Sync your Jenkins configuration files (which are mostly XML) to GitHub. Version control everything.

### Jenkins Administration
* If you need to restart Jenkins, go to /safeRestart or /restart
* If this doesn't work, you'll need to SSH into Jenkins and run sudo service jenkins restart
* To update Jenkins, run sudo yum update jenkins
* If you install plugins, do it one at a time and restart Jenkins after each plugin, then go into a few configuration menus and run a few jobs to make sure nothing is broken. Installing Jenkins plugins is a bit risky and it's best avoided unless you have a really good reason to do it.
* We're using the latest LTS Jenkins version. https://wiki.jenkins-ci.org/display/JENKINS/LTS+Release+Line
* The Jenkins home directory is /var/lib/jenkins.
* Don't disable the Maven plugin. Jenkins won't start up. If you do disable it by accident, re-enable it with sudo rm /var/lib/jenkins/plugins/maven-plugin.jpi.disabled
* If you accidentally lock everyone out of Jenkins due to incorrect security settings, disable global security in /var/lib/jenkins/config.xml
