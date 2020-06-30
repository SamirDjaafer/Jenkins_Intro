# How to use Jenkins

## Initiating a new pipeline

1. Go on the Jenkins home page, for eng57 this is the link filipe made for us | http://18.130.21.164:8080/
2. Click `New Item` at the top left to make a new pipeline 
3. Click on `freestyle project` and name your pipeline

## Configuring the pipeline
### General

1. `Discard old builds` - tick this box
2. `Max no of builds` - we will set this to 3 for now.
3. `Github project` - tick this box
4. `project url` - this is your github link for this repo. e.g. `https://github.com/SamirDjaafer/multi_vm_vagrant`

### Office 365 connector

1. Adding a webhook to recieve notifications on teams. Go to teams chat where you want the notification. Click connectors, jenkins, copy and paste the URL into the Pipeline configuration where it says URL. Give it a name e.g. jenkins-samir-eng57
2. `Restrict where this project can be run` - This is the environment where we want to run. We have a testing environment called `sparta-ubuntu-node`

### Source code management

1. We need to select `git` ofcourse!
2. In `repo url` you need to put the link you would use to clone the repo. This will have `.git` on the end
3. For `credentials`, ensure you have made a new SSH key. Follow github documentation for help on this
4. so we will create a new key on our local machine. For this example we will call it `jenkins-key-samir`
5. Then `add credentials`, the kind will be `SSH Username with private key`. Copy your key from the file in `.ssh` which corresponds to the key name. There will be a private key and a `.pub` key. Make sure you put in the private key. The `.pub` key is for github.
6. Put in your username and password and click add
7. for `branch specifier`, choose the branches where you are monitoring (listening for incoming commits/pushes).

### We also need to add this to github - our webhook and the .pub key !

1. On github go to your repo and go to settings
2. Click webhooks and then `add webhook`
3. The payload URL is your jenkins IP so in my case it is `http://18.130.21.164:8080/` followed by `github-webhook` 
4. Add the .pub SSH key to our Github list of SSH keys

! Now our webhook has been configured correctly! !

### Build triggers

1. `GitHub hook trigger for GITScm polling` - Tick this box! thats it for this section!

### Build Environment

1. `Provide Node & npm bin/ folder to PATH` - Tick this box
2. `Sparta-Node-JS` should be there for node installation. This is our testing environment

### Build 

1. Execute the shell commands you want to run from inside your virtual machine on the testing environment.

### Post-build actions

1. Git Publisher
2. Push Only If Build Succeeds - (Tick box)
3. Merge Results - (Tick box)
4. Add Branch
5. Branch to push - (write master)
6. Target remote name - (write origin)






