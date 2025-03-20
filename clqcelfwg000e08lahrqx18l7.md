---
title: "Setting up Wazuh: XDR for Infra monitoring"
datePublished: Wed Mar 19 2025 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clqcelfwg000e08lahrqx18l7
slug: wazuh-infrasec
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742476678889/ef7ba252-ee88-4563-9d5a-9c0a9923a898.png

---

On this day, we will dive deeper into mastering SIEM setups with WAZUH! It is a SIEM+XDR (extended detection response) tool. The best part about why we are focusing on it now instead of Splunk from Day 4 is that it is open-source and easier to setup. Ofcourse we will be using docker to install it.

#### Installing the wazuh-manager

wazuh-manager is the daemon that will run on our machine which will monitor everything happening in the servers, to keep things clean, we will download and run a docker container for it. [Read some docs if you still get stuck.](https://documentation.wazuh.com/current/deployment-options/docker/wazuh-container.html)

Install the wazuh-docker repo with all the docker-compose files inside

```bash
git clone https://github.com/wazuh/wazuh-docker.git -b v4.7.0
```

`cd` into the repo, we will start a `single-node` instance since we are only setting up the dash on our own computer. Read more about the difference between single and multi-node instances [here](https://medium.com/anton-on-security/living-with-multiple-siems-c7fea37c5020)

to build the `docker` container, we now run the command

```bash
docker-compose -f generate-indexer-certs.yml run --rm generator
```

this will build the `wazuh-certs-generator:0.0.1` image.

In order to start the docker network, (the cluster of interconnected docker containers), we will run:

```bash
docker-compose up -d
```

After waiting an approx. of 5 mins (even if it says it's done), we can go to `localhost` on our browser to access the dashboard. The credentials by default are `admin` and `SecretPassword` but you can change them.

![r/Wazuh - Help with Wazuh Dashboard](https://imgs.search.brave.com/vIM2mudty3kS5MFvEhb-VxOgqO7F37RfJ0h4ASOLyzk/rs:fit:860:0:0/g:ce/aHR0cHM6Ly9wcmV2/aWV3LnJlZGQuaXQv/aGVscC13aXRoLXdh/enVoLWRhc2hib2Fy/ZC12MC0wemk1eDhk/dnVsOGExLnBuZz93/aWR0aD04NzQmZm9y/bWF0PXBuZyZhdXRv/PXdlYnAmcz1kYzYw/YzA1NDZlMThlMTQy/ZmM3YjA1ZThiZGJm/MDU4NzkwMDIwODNk align="left")

You may come across such a window, but instead of 1, we will have 0 active agents shown here, they are the nodes we are monitoring.

#### Setting up the nodes

We can use docker to setup nodes but that would require having `systemd` installed. So we will use VMs (virtual machines). For that we will use the virtualisation software called `vmware workstation` (you can use `vmware fusion` if you run a mac). Let's create a VM of this distro called Slax, based off debian.

##### Installing the dependencies

```bash
apt-get update && apt-get install wget lsb-release 
```

Now we will go back to our dashboard and click `Deploy new agent` In there, since we are setting up a debian linux node, we will do the following settings...

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702992459194/4e5e6864-553d-41db-9c7d-14dfc66f5668.png align="center")

let us give the node the nickname 'local'. for demonstration purposes, we will set `127.0.0.1` but please set it with your monitoring machine's own IP.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702992557918/94817f86-fcbb-4888-ab85-06c56737e335.png align="center")

Copy and paste the commands into your VM node.

There might be an issue with your machine not being able to detect the manager's IP, thanks to [this blog](https://medium.com/@codingInformer/solution-for-wazuh-agentd-error-invalid-server-address-found-manager-ip-23bce7a99535), this can easily be fixed.

Now, all we have to do is click close and go back to our home page.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702993616581/b20f28b2-7868-4508-9c28-ec0bf73b6441.png align="center")

From here, we can monitor our nodes clearly.