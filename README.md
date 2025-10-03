# Integrate Jenkins Server with Gitea

## Install Gitea Plugin in Jenkins GUI

1. Navigate to Manage Jenkins > Plugins > Available plugins 
2. Search "Gitea"
3. Download

## Generate Gitea token for Jenkins

1. Login to Gitea and click the profile picture > settings
2. Select applications tab
3. Name the token "jenkins-token-1"
4. Check read and write box for each API route in list (unless you know what you're doing)
5. Click save
6. Copy token output and save it somewhere safe


## Add Gitea credentials to Jenkins

1. Login to Jenkins and navigate to manage Jenkins > credentials
2. Click "global" under stored scopes and then "add credentials" in the upper right corner
3. select "Gitea Personal Access Token" under "kind"
4. Paste the key we got from Gitea into the Token box
5. give it a descriptive ID: "gitea-credentials-1"
6. Create the Token.

## Configure the Gitea Plugin in Jenkins

1. Navigate to Manage Jenkins > System
2. Scroll down until you find the Gitea Servers section and click Add Gitea Server.
3. Server URL: Enter the URL or IP address of your Gitea instance (you must include http:// or https:// depending on your gitea server setup).
4. Check the manage hooks box, and then provide the corresponding token from the dropdown.
6. Click Save.

## Configure Gitea Webhook

1. Navigate to Profile Icon > Settings > Webhooks
2. Input this in Target URL box: [YOUR JENKINS IP OR URL DON'T FORGET TRANSFER PROTOCOL (HTTP:// or HTTPS://)]/gitea-webhook/post
#### IMPORTANT: If your jenkins IP address is private, you must specify in your Gitea app.ini file or Docker YAML to allow the host. See my repository on Installing Gitea for help with the YAML.
3. Save Webhook

## Create Gitea Test Repository

1. Click the plus sign in the top right corner and then 'New Repository'
2. Name it 'test'

## Configure Jenkins Test Pipeline Item

1. Navigate to Jenkins Home Dashboard
2. Click 'New Item'
3. Give it a name 'test'
4. Select multibranch pipeline and click OK
5. Under Branch Sources, select gitea from dropdown menu. provide the credentials, your gitea name, and then select the test repository (make sure name and credentials are valid)
6. Click Save and you should see a successful scan.



## You're now ready to automate with Jenkins and Gitea!
