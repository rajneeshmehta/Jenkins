# GitHub -> Jenkins -> Docker (Httpd WebServer)

This project create a flow which can be understood by this fig.

<img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/Task1-Workflow.png" alt="alt text" width="400" height="300">

## Step 1:
First we download the code from github repository, whenever Developer push the code to SCM
<img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/1.1.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/1.2.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/1.3.jpg" alt="alt text" width="700" height="500">

Then this code copy the code to relevent Folder.
```bash
if sudo ls -l /root/ | grep dev
then 
sudo cp -rvf * /root/dev/
else
sudo mkdir /root/dev/
sudo cp -rvf * /root/dev/
fi
```

## Step 2:
Now we setup Testing Environment for Q&A team.

<img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/2.1.jpg" alt="alt text" width="700"height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/2.2.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/2.3.jpg" alt="alt text" width="700" height="500">

This code run Httpd server in Docker container.

```bash
if [ "$(getenforce)" = "Enforcing" ]
then
sudo setenforce 0
fi

if [ "$(systemctl is-active docker)" = "inactive" ]
then
sudo systemctl enable docker
sudo systemctl start docker
fi

if sudo docker ps -a | grep devlopment-server
then
:
else
sudo docker run -dit --name devlopment-server -p 8082:80 -v "/root/dev/":/usr/local/apache2/htdocs/ httpd
fi
```

## Step 3:
After Q&A team approve the changes Jenkins will merge the Dev branch into Production Branch ( here Master Branch ) 


<img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/3.1.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/3.2.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/3.3.jpg" alt="alt text" width="700" height="500"><img src="https://github.com/rajneeshmehta/Jenkins-git-docker-webserver/blob/master/Images/Markdwon/3.4.jpg" alt="alt text" width="700" height="500">

