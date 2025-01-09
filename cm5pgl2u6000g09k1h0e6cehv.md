---
title: "Vinyls & Offensive Google Cloud"
datePublished: Thu Jan 09 2025 15:03:53 GMT+0000 (Coordinated Universal Time)
cuid: cm5pgl2u6000g09k1h0e6cehv
slug: vinyls-offensive-google-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736430969889/33fe1d02-e462-4de4-9379-2d644883d40e.png

---

So couple of days ago, I was introduced to this cool community known as “Security BSides”, here’s more…

## What’s BSides?

**ACCORDING TO WIKIPEDIA: Security BSides** (commonly referred to as BSides) is a series of loosely affiliated information security conferences. It was co-founded by Mike Dahn, Jack Daniel, and Chris Nickerson in 2009. Due to an overwhelming number of presentation submissions to [Black Hat](https://en.wikipedia.org/wiki/Black_Hat_Briefings) USA in 2009, the rejected presentations were presented to a smaller group of individuals. The event was named after the ["B-side" of a vinyl record](https://en.wikipedia.org/wiki/A-side_and_B-side).

Over time the conference format matured and was released to enable individuals to start their own BSides conferences. The Las Vegas BSides conference is also considered part of Hacker Summer Camp given its schedule and proximity to other security conferences during that time.

Of the three standard conference event styles, structured, [unconference](https://en.wikipedia.org/wiki/Unconference), and hybrid. BSides falls into the unconference, or anti-conference, event style and is completely attendee driven. Attendees appear at a predetermined time, discuss ideas, and collaboratively agree upon what the schedule will look like for that day. Talks that get the most attention and conversation get added to the schedule.

## Why Cyber-Security communities are cool

Firstly, you encounter tons of like-minded people, people with interests so rare that it’d be hard to spot them in even developer communities (which is kinda surprising). Plus these communities are tight-knit and appreciate collaborative growth, since everybody are somewhat technically sound. We can establish proper communication channels for conferences, workshops and even career help. Also the seminars are cool as hell. Because in CyberSecurity, when it comes to something cool, it means something that only very few people try or something nobody has tried before.

## Red-Teaming GCP

### Authentication Mechanisms

Just like AWS, we can access our Google Cloud Platform account graphically through either the GCP Portal, which would need a gmail account and password. When it comes to CLI based access, we again have long term and short term access. Short term access requires an access token while long term access works with a credentials file stored in the `~/.config/gcloud` folder inside the credentials.db file.

Btw, GCP is kinda different from AWS in terms of resource hierarchy, here’s the chart i stole from their website.  

![Mapping your organization with the Google Cloud Platform resource hierarchy  | Google Cloud Blog](https://storage.googleapis.com/gweb-cloudblog-publish/images/cloud-hierarchy-1omgk.max-700x700.PNG align="left")

IAM related policies, groups and roles are kind of the same. Also, for each service, we have a special robot account known as a **service account**, enumerations on them can be done the same way like we do in AWS, through the GCloud CLI.

### Extracting Meta-Data

It can be done through SSRF and RCE, here’s the curl command for example:

`curl -H "Metadata-Flavor: Google"` [`http://169.254.169.254/computeMetadata/v1/instance/service-accounts`](http://169.254.169.254/computeMetadata/v1/instance/service-accounts/233003792018-comp)`/<service_account_name>/token`

This one gives you access to the JSON file for credentials we talked about earlier.

### Investigating GCloud Storages

Once you have access to one of the accounts, you can check the storages under it. Through `gcloud storage ls`, and through `gcloud storage cat` you can inspect file contents (kinda like bash) .

Also, you can do authenticated enumeration through gcp\_enum script found on GitHub and OFCOURSE, there are 100s of automated enumeration and privilege escalation tools on GitHub (but try the ones by RhinoSecurityLabs)

## NEW: CodeForces Grind

Okay, so today’s question is: **A. Say Hello With C++!**

I know, pretty basic. But gotta start somewhere y’know! Anyways, here’s the solution:

```cpp
#include <iostream>
using namespace std;


int main(){
	string name;
	cin >> name;
	cout << "Hello, " << name;
	return 0;

}
```