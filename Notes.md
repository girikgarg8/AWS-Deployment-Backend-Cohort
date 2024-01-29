AWS is Amazon Web Services, which is a cloud service provided by Amazon. Cloud, in the context of computer science, refers to remote machines or remote servers that are available to us for use.

The services which we explored in the cohort:

1. EC2: Elastic Cloud Compute: Virtual servers on the cloud

Some key terms:

Key: This contains certificates (in the form of .pem file) which are needed in order to SSH into the instance.

Security group: A set of firewall rules that control the traffic for the resource. We specify the ports and the protocols which with which our instance can interact.

Change the permission of the awskey by using `chmod 700 awskey.pem`

SSH into the instance by using `ssh -v -i ubuntu@IP` 

[AWS console](/AWS_console.png)
[Terminal](/Terminal.png)

In the new instance, the first thing which we should ideally do is to run `sudo apt-get update`

After that, I looked up the documentation online to install NVM on the AWS instance.

I cloned the Flights API Gateway repository from "singhsanket143/API_Gateway.git". This is not the Flights API Gateway microsevice, it's a simple express server to test AWS's functionality.

Once cloned, we install the dependencies using `npm install` and then run the app by using `node index.js`

[Application running on EC2 instance](/Application_running_on_EC2_instance.png)

Try to send a HTTP request to the instance by sending request to 'IP:3005/home' through the browser.

The problem with this approach is that if I kill the node process, then the API on 'IP:3005/home' will also not work. Opening multiple terminals to SSH is not a recommended approach.

Hence,we set up a daemon process (background process) by using the 'pm2' package.

In order to start the daemon process, use `npx pm2 start index.js`. In order to stop the daemon process, use `npx pm2 stop index.js`

PM2 is a powerful package and can handle load balancing to some extent, by itself.

[Terminal on terminating the instance](/Terminal_on_terminating_the_instance.png)