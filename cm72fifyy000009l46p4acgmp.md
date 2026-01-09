---
title: "eJPT-CTF-1: Assessment Methodologies: Information Gathering CTF 1"
datePublished: Wed Feb 12 2025 21:34:33 GMT+0000 (Coordinated Universal Time)
cuid: cm72fifyy000009l46p4acgmp
slug: ejpt-ctf-1-assessment-methodologies-information-gathering-ctf-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1767961420248/c0f53216-934b-410a-8d24-08a45c93b713.jpeg

---

This lab focuses on information gathering and reconnaissance techniques to analyze a target website. Participants will explore various aspects of the website to uncover potential vulnerabilities, sensitive files, and misconfigurations. By leveraging investigative skills, they will learn how to identify critical information that could assist in further penetration testing or exploitation.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">the machine is within a private network, so you can’t use online enumeration tools like sublist3r, or theHarvester. I’ve used the following tools hence: gobuster, nmap and curl</div>
</div>

# Lab Environment

A website is accessible at [**http://target.ine.local**](http://target.ine.local). Perform reconnaissance and capture the following flags.

* **Flag 1:** This tells search engines what to and what not to avoid.
    
* **Flag 2:** What website is running on the target, and what is its version?
    
* **Flag 3:** Directory browsing might reveal where files are stored.
    
* **Flag 4:** An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.
    
* **Flag 5:** Certain files may reveal something interesting when mirrored.
    

# Tools

* Firefox
    
* Curl
    
* HTTrack
    

---

### Note

In this lab, the flag will follow the format: FLAG1{MD5Hash} OR FL@G1{MD5Hash}. For example, FLAG1{0f4d0db3668dd58cabb9eb409657eaa8}. You need to submit only the MD5 hash string, excluding the braces. For instance: 0f4d0db3668dd58cabb9eb409657eaa8.

This tells search engines what to and what not to avoid.  
visit: `target.ine.local/robots.txt`

What website is running on the target, and what is its version?

`nmap -sC target.ine.local`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739395436796/c6b31990-80f0-4e72-9a6c-773f0b54a605.png align="center")

Directory browsing might reveal where files are stored.

The stack is wordpress and Apache, so google potential directories in wordpress that can have listing enabled, here’s a list:

* [`http://target-site.com/wp-content/uploads/`](http://target-site.com/wp-content/uploads/)
    
* [`http://target-site.com/wp-includes/`](http://target-site.com/wp-includes/)
    
* [`http://target-site.com/wp-content/plugins/`](http://target-site.com/wp-content/plugins/)
    
* [`http://target-site.com/wp-content/themes/`](http://target-site.com/wp-content/themes/)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739395543552/6d793f95-0bb0-44e3-ab6f-708bdd21b101.png align="center")

An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739395603312/7d923759-60bd-4d3a-83c9-693a88ee0676.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739395653800/cd2a818e-6e09-4d62-8ef5-05e7e3e09bfe.png align="center")

Certain files may reveal something interesting when mirrored.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739395845093/6e28d294-47a4-42c5-b9a6-da54fb1479a4.png align="center")