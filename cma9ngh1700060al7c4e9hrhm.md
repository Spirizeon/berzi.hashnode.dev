---
title: "Setting up Wazuh: XDR for InfraSec"
datePublished: Sun May 04 2025 12:50:28 GMT+0000 (Coordinated Universal Time)
cuid: cma9ngh1700060al7c4e9hrhm
slug: setting-up-wazuh-xdr-for-infrasec

---

Let's dive deeper into mastering SIEM setups with WAZUH! It is a SIEM+XDR (extended detection response) tool. The best part about why we are focusing on it now instead of Splunk from Day 4 is that it is open-source and easier to setup. Ofcourse we will be using docker to install it.
Installing the wazuh-manager

wazuh-manager is the daemon that will run on our machine which will monitor everything happening in the servers, to keep things clean, we will download and run a docker container for it. Read some docs if you still get stuck.

Install the wazuh-docker repo with all the docker-compose files inside

git clone github.com/wazuh/wazuh-docker.git -b v4.7.0

cd into the repo, we will start a single-node instance since we are only setting up the dash on our own computer. Read more about the difference between single and multi-node instances here

to build the docker container, we now run the command

docker-compose -f generate-indexer-certs.yml run --rm generator

this will build the wazuh-certs-generator:0.0.1 image.

In order to start the docker network, (the cluster of interconnected docker containers), we will run:

docker-compose up -d

After waiting an approx. of 5 mins (even if it says it's done), we can go to localhost on our browser to access the dashboard. The credentials by default are admin and SecretPassword but you can change them.

r/Wazuh - Help with Wazuh Dashboard

You may come across such a window, but instead of 1, we will have 0 active agents shown here, they are the nodes we are monitoring.
Setting up the nodes

We can use docker to setup nodes but that would require having systemd installed. So we will use VMs (virtual machines). For that we will use the virtualisation software called vmware workstation (you can use vmware fusion if you run a mac). Let's create a VM of this distro called Slax, based off debian.
Installing the dependencies

apt-get update && apt-get install wget lsb-release

Now we will go back to our dashboard and click Deploy new agent In there, since we are setting up a debian linux node, we will do the following settings...

let us give the node the nickname 'local'. for demonstration purposes, we will set 127.0.0.1 but please set it with your monitoring machine's own IP.

Copy and paste the commands into your VM node.

There might be an issue with your machine not being able to detect the manager's IP, thanks to this blog, this can easily be fixed.

Now, all we have to do is click close and go back to our home page.

From here, we can monitor our nodes clearly.

