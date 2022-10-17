# jenkins-mvn

### Installing

[https://www.jenkins.io/doc/book/installing/macos/](https://www.jenkins.io/doc/book/installing/macos/)
[https://www.jenkins.io/download/lts/macos/](https://www.jenkins.io/download/lts/macos/)

**Do:**
* Install the latest LTS version: brew install jenkins-lts
* Install a specific LTS version: brew install jenkins-lts@YOUR_VERSION
* Start the Jenkins service: brew services start jenkins-lts
* Restart the Jenkins service: brew services restart jenkins-lts
* Update the Jenkins version: brew upgrade jenkins-lts

http://localhost:8080

Copy pass:
/Users/emiligarriga/.jenkins/secrets/initialAdminPassword

Install default plugins

Set Form


### Status

ps -e | grep jenkins



### Actions

shutdown jenkins
restart jenkins

brew services stop jenkins-lts
brew services restart jenkins-lts


### Start

brew services restart jenkins-lts
http://localhost:8080


### jenkins CLI

http://localhost:8080/manage/cli/

Download
http://localhost:8080//jnlpJars/jenkins-cli.jar

From folder jar RUN:
java -jar jenkins-cli.jar -s [ngrok.io URL] -webSocket help

### Install Plugins

http://localhost:8080/manage/updateCenter/

Maven Integration
Authentication Tokens API
Role-based Authorization Strategy





### Start Jenkins when PC starts

https://github.com/fastlane/brewed-jenkins

Download:
https://github.com/fastlane/jenkins-app/releases/download/1.0/Jenkins.zip



### Webhook and Poll SCM

https://www.youtube.com/watch?v=MTm3cb7qiEo&list=WL&index=2&t=1469s

https://www.blazemeter.com/blog/how-to-integrate-your-github-repository-to-your-jenkins-project

Github
Repo Setting -> Webhooks



Jenkins
http://localhost:8080/job/webhooks/configure

Select Git




Insert credentials


Branch

Select the correct branch


GitHub hook trigger for GITScm polling




** For the localhost we must mask the URL
https://ngrok.com/download


Install

brew install ngrok/ngrok/ngrok

Mask URL

cd /usr/local/bin && ./ngrok http 8080
change  
http://localhost:8080
to
https://0fa2-79-159-184-99.eu.ngrok.io

### Maven integration

[https://mkyong.com/java/how-to-set-java_home-environment-variable-on-mac-os-x/](https://mkyong.com/java/how-to-set-java_home-environment-variable-on-mac-os-x/)

[https://www.ktexperts.com/maven-project-set-up-global-tool-configuration/](https://www.ktexperts.com/maven-project-set-up-global-tool-configuration/)

### Install maven

* brew install maven

* mvn -version

### install Java

[https://www.java.com/en/download/help/mac_install.html](https://www.java.com/en/download/help/mac_install.html)

### Inizialate

validate if has init:

```
echo $JAVA_HOME   
echo $MAVEN_HOME
```

## Search path

### See version

> /usr/libexec/java_home -V

> /usr/libexec/java_home

* $JAVA_HOME (.bash_)
  * nano ~/.zshenv
  * export JAVA_HOME=$(/usr/libexec/java_home)
  * export JAVA_HOME=$(/usr/libexec/java_home -v1.8.0_342)
  * source ~/.zshenv
  * echo $JAVA_HOME


* $JAVA_HOME (.zsh)
  * nano ~/.bash_profile
  * export JAVA_HOME=$(/usr/libexec/java_home)
  * export JAVA_HOME=$(/usr/libexec/java_home -v1.8.0_342)
  * source ~/.bash_profile
  * echo $JAVA_HOME


> mvn -version
> 
> [https://mkyong.com/maven/install-maven-on-mac-osx/])https://mkyong.com/maven/install-maven-on-mac-osx/

* $MAVEN_HOME (.bash_)
  * nano ~/.zshenv
  * export MAVEN_HOME=/usr/local/Cellar/maven/3.8.6/libexec
  * source ~/.zshenv
  * echo $MAVEN_HOME


* $MAVEN_HOME (.zsh)
  * nano ~/.bash_profile
  * export MAVEN_HOME=/usr/local/Cellar/maven/3.8.6/libexec
  * export PATH=$PATH:$MAVEN_HOME/bin
  * source ~/.bash_profile
  * echo $MAVEN_HOME


## Jenkins Global Tools

[https://www.metahat.net/2019/05/cannot-run-program-mvn-in-directory.html](https://www.metahat.net/2019/05/cannot-run-program-mvn-in-directory.html)

### Set JDK
* JDK 18
* $JAVA_HOME -> /Users/emiligarriga/Library/Java/JavaVirtualMachines/openjdk-18.0.2.1/Contents/Home

### Set Maven
 
[http://www.javawenti.com/?post=13285](http://www.javawenti.com/?post=13285)
 
* Maven 3.8.6
*  Install auto

### Config General

[http://localhost:8080/job/maven/configure](http://localhost:8080/job/maven/configure)

## Git

* Repo
* Creedentials
* Branch

## Build

* Goles
  * Any Maven option
  * Add ‘-X’ to the end to see more log

 >   Important
  >  * /Users/emiligarriga/.jenkins/workspace/[project]
   > * Has a pom.xml


The operation it is only done in /Users/emiligarriga/.jenkins/workspace/project-name[]


## Creating Email Notifications

[https://pradeep-sg406.medium.com/how-to-configure-email-notification-in-jenkins-227b58d3c017#:~:text=Go%20to%20the%20Jenkins%20home,'Use%20SMTP%20Authentication'%20option.](https://pradeep-sg406.medium.com/how-to-configure-email-notification-in-jenkins-227b58d3c017#:~:text=Go%20to%20the%20Jenkins%20home,'Use%20SMTP%20Authentication'%20option.)

[http://localhost:8080/manage/configure](http://localhost:8080/manage/configure)

[http://localhost:8080/job/webhooks/configure](http://localhost:8080/job/webhooks/configure)

## Pipelines

[https://www.jenkins.io/doc/book/pipeline/getting-started/](https://www.jenkins.io/doc/book/pipeline/getting-started/)

### Create a Pipeline jenkins project

#### Create script pipeline

[http://localhost:8080/job/pipelineJob/configure](http://localhost:8080/job/pipelineJob/configure)

* Descrive
  * Agent
  * MVN Tools (http://localhost:8080/manage/configureTools/)
    * JAVA_HOME (JDK 18 ‘/Users/emiligarriga/Library/Java/JavaVirtualMachines/openjdk-18.0.2.1/Contents/Home’)
    * MAVEN_HOME (Maven 3.8.6 ‘/usr/local/Cellar/maven/3.8.6/libexec’)

```
{
    pipeline {
        agent any
        tools {
            maven 'Maven 3.8.6'
            jdk 'JDK 18'
        }
        stages {
            stage('Git Clone') {
                steps {
                    git 'https://github.com/porsilasmoscasweb/jenkins-mvn.git'
                }
            }
            stage('Maven clean'){
                steps {
                    sh "mvn clean"
                }
            }
        }
    }
}
```

#### Syntax for github project

[http://localhost:8080/job/pipelineJob/pipeline-syntax/](http://localhost:8080/job/pipelineJob/pipeline-syntax/)

From jenkins file on GIT

## Deploy to server

DevOps: auto deployment (git -- jenkins -- remote server)

