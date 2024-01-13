---
title: "ZySec: Day #4"
datePublished: Mon Dec 18 2023 15:21:53 GMT+0000 (Coordinated Universal Time)
cuid: clqb2dptz000208jwdwc3e9lx
slug: zysec-day-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702912895378/90e4ee77-0743-4ad6-8068-c1e5b30ce784.png

---

Welcome back! In this day, we will discuss how to setup a SIEM (System Information and Event Management) tool discussed before and explore how it works.

For this blog, we will use the enterprise version of a SIEM called "Splunk" which is very popular in the industry for log-monitoring. To skip the hassle, we will be using a dockerised version of it.

#### Setting up Docker

We will assume the user to be using a debian machine, if you are on windows, please refer to the docs for installing [docker-desktop](https://docs.docker.com/desktop/install/windows-install/)

```bash
$ curl -sSL https://get.docker.com/ | sh
$ systemctl start docker
```

#### Downloading the images

Image files are binaries that will build our container. A container is an isolated operating system environment in layman's terms. We will install the standalone version of Splunk-Docker, with help from the [docs](https://splunk.github.io/docker-splunk/SETUP.html#deploy).

```bash
$ docker pull splunk/splunk:latest
```

After downloading the image, we will run the container, connecting its internal host's port with our host machine's port, let's take 8000 as suggested. You can take anything else like 5000 or 12000.

```bash
$ docker run -p 8000:8000 -e "SPLUNK_PASSWORD=<password>" \
             -e "SPLUNK_START_ARGS=--accept-license" \
             -it splunk/splunk:latest
```

After heading to https://localhost:8000, you will come across the Splunk dashboard, in here you have to enter the user as 'admin' and password as the one you defined in the `docker run` command.

#### Trying out logs

In order to view the logs of a particular host, we will go to the 'Search' option on the left and search `host=` and then select our host from whatever is suggested by Splunk. The one suggested will be our docker container. We will be displayed a collection of logs recorded by our docker container when setting up Splunk.

Here, we can select any particular log and add its details to the search query to filter out results.

#### Setting up a dashboard

We can copy our search string, headover to the `dashboards` tab and create a new custom grid one through dashboard studio. Then add a new data source to our table with the `SPL query` as our search string. There we go! We made our first dashboard. Such practices can be used by security professionals to build dashboards that can be used for analysis and presentation to higher executives in an organization for vulnerability analysis.