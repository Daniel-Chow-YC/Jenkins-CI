# What is Jenkins
- Jenkins is an automation server
- Jenkins is used for continuous integration
-  Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build.

# Accessing Jenkins
- To create a Jenkins create a vagrant file and provisions script as shown in this project
- To see Jenkins, simply bring up a web browser and go to URL http://myServer:8080 where myServer is the name of the system running Jenkins.
- To find the password `` cat /var/lib/jenkins/secrets/initialAdminPassword ``

# How to create CI pipline
- go to new item
- select freestyle project and name it
- On the configure page:
  - Select Github project and add URL
  - Under source code management add the repo url
    - You will need to add a private key.
    - Use ssh-keygen to generate a public/private key
    - Add these keys to the repo and then add the private key where needed
  - Under build triggers select GitHub hook trigger for GITScm polling
  - Under build environment select Provide Node & npm bin/ folder to PATH (this option will become later after installing nodejs and adding new nodejs installations)
  - Under build execute shell command:
   ````
    cd app
    npm install
    npm run test
   ````


- On Jenkins go to the Manage Jenkins tab then go to Manage Plugins
- Then install nodejs
- After installing the plugin, go to the global jenkins configuration panel (Global Tool Configuration) and add new NodeJS installations:
  - https://wiki.jenkins.io/display/JENKINS/NodeJS+Plugin

- On the Github repo go to settings and add a webhook
  - Webhook should look like: <host_name/host_ip>/github-webhook/
- Go into the VM and install ngrok: https://www.npmjs.com/package/ngrok
````
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs -y
sudo npm install --unsafe-perm -g ngrok
ngrok http 8080
````
- Replace the localhost:8080 with the new forwarded ip (.ngrok.io) in the webhooks on Github
- the webhook on github should now look like something like this: http://86a1cd90.ngrok.io/github-webhook/
- Note: running the command: ``ngrok http 8080`` will change the new forwarded .ngrok.io ip
- Note: must keep this command active for it to work
- NOTE: This method is very hacky. DO NOT DO THIS in a work environment.
