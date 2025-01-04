---
title: "Playing Offense: AWS Edition"
datePublished: Sat Jan 04 2025 14:12:18 GMT+0000 (Coordinated Universal Time)
cuid: cm5i9jh2x00050amk0dpcfy97
slug: playing-offense-aws-edition
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735979547569/0da907e5-ac49-408a-a5a7-8ab5a839589b.png

---

## Access methods

Before we talk about the services, we need to talk about how authentication is done. One method is through AWS’s own GUI dashboard where you can either login as an IAM user or a root user (basically the dude with admin privileges). This does require stuff like **IAM user ID, email, passwords,** etc.

Whereas when we are dealing with the **AWS CLI** it is much simpler, we have an **Access key ID, Security token** for long-term access and an additional **session token** for short term access.

## IAM

![AWS Identity and Access Management | AWS Cheat Sheet](https://digitalcloud.training/wp-content/uploads/2022/02/iam-authentication-methods.png align="left")

Very similar to Linux, users are nothing but profiles made for individuals, more on that as we progress through this article. IAM stands for Identity and Access Management (which is obviously managing people and authorisation in simple terms). **Groups** on the other hand is a collective of users with defined persmissions. Most entities in IAM relate to grouping of entities and assigning sets of permissions. When it’s short-term, we use IAM roles to allocate perms to these users. When we need temporary roles, we use **Assumed Roles**. Now how do we define permissions? We got **policies**. It’s basically a JSON file that defines a blueprint of all the permissions you need to allocate to an entity what services and to what extent that entity can access things…

example policy for full access to an AWS S3 bucket…

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
        }
    ]
}
```

## Vulnerabilities

![Limit access to Amazon S3 buckets owned by specific AWS accounts | AWS  Storage Blog](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2020/11/27/Amazon-S3-Featured-Image.png align="left")

Vulnerabilities in AWS based sites often start with open S3 buckets (which are persistent data storages often for anybody to access). You can get a list open S3 buckets through various tools online.

Now, we need to search for how to get access to the buckets, it can be through SSRF where we can employ various tactics like os command injection, open redirects, etc. Usually the credentials are stored in the `http://169.254.169.254/latest/meta-data` path whose IP address comes from the reserved [IPv4 Link Local Address](https://en.wikipedia.org/wiki/Link-local_address) [space](https://en.wikipedia.org/wiki/Link-local_address) which can only be accessed from within that instance’s network.

### Enumeration through LLMs

Now, once we get the credentials it’s time to authenticate and then view all sorts of IAM users, roles, policies. I’m lazy so I like to form complex queries through LLMs like ChatGPT.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735999587824/09b2940a-c33a-48fd-b157-3c970981e327.png align="center")

It is possible to look for privilege escalation chances through the `pacu` tool. But since the enumerative functions of `pacu` take too long, sometimes it’s better to manually explore what’s out there through the AWS cli and some Google Dorking.

![Attacking AWS Cognito with Pacu (p2) - Rhino Security Labs](https://rhinosecuritylabs.com/wp-content/uploads/2023/10/image5-1000x645.png align="left")