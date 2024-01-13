---
title: "ZySec: Day #7"
datePublished: Thu Dec 21 2023 16:05:06 GMT+0000 (Coordinated Universal Time)
cuid: clqfe8ubj000008js9jaf1u5s
slug: zysec-day-7
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703173580030/d1511c2f-a95f-42d8-8dbc-74a817ad1d65.png

---

On this day, we will talk about the various OWASP security principles, and how they connect up with NIST's CSF and RMF.We will also have an extra on GitSecOps (Git Security Operations) for celebrating the completion of first week since this series' launch.

#### What is OWASP

Acronym for "Open Worldwide Application Security Project", it's an online community that produces freely available articles, methodologies, documentation, tools, and technologies in the field of web application security.

#### OWASP security principles

Principles suggested by OWASP for building and maintaining secure web applications.

* Defense in depth: Have multiple layers of security for protecting an asset, best example being multi-factor authentication through OTPs (one-time passwords) during logins that require not just a user and password but also the OTP.
    
* Minimize attack surface: An attack surface is the collection of all possible security risks a threat actor can possess to an organization's particular system. OWASP suggests minimising that (through security frameworks like NIST CSF).
    
* Separation of duties: Critical actions shall be divided into various roles and if there is a hierarchy, there should be various forms of authorization before the next action can be taken.
    
* Principle of Least privilege: Users must have the **least** amount of access required to perform their tasks. This helps in reducing potential expansion of attack surface.
    
* Fixing security issues correctly: Follow a risk-management framework like NIST RMF or the one adopted by the organization.
    
* Secure defaulting: An optimal security posture for all users is the default security posture.
    
* Fail-safe: There should be a secure defaulting step performed to keep things secured when something fails. For example, when a server containing high-risk (non-volatile) assets gets unauthorised access, it automatically turns off to protect them.
    
* Part-trust policy: Never trust 3rd parties fully even if they are affiliated with the organization, they may have different security policies which may interfere/clash with the concerned ones.
    
* Open-Design: Keep the source code open, but keep the secrets and auth keys confidential. Apart from that, keep the architecture and policies open. Confidentiality of source code is not a key factor but it is other factors like these. It will help the wider public add comments and ideas for bettering the system.
    

### Week 1 Extra: GitSecOps fundamentals

When we are pushing code to Github, we need to make sure that the code is robust, functional and well-tested for vulnerabilities. Here are some strategies that can help in that:

* Signing commits: After we set up our SSH keys, we can also set up GPG keys with appropriate encryption (like RSA 4096) to make clear in the git history that the commit came from an authorised device. GPG authentication adds an extra level of security over SSH key-based auth (+ passwords if the keys require).
    
* Creating CI/CD pipelines for auto-testing code: Github actions are free for personal repositories [(also read this please)](https://docs.github.com/en/actions/quickstart). Through that, we can basically build blueprints that will upload our code onto github's cloud machine, test it, and **only push it into the repo if all specified checks are passed** (Github's cloud containers use Arch Linux by the way so keep that in mind while writing terminal commands)
    
* Enabling dependabot and codeQL: Dependabot and codeQL will constantly check your repositories for potential vulnerabilities and create pull requests for them which you can look at and close yourself or get someone else to solve them for you. You can find the option here:
    
    ```bash
    https://github.com/<user>/<repo>/settings/security_analysis
    ```
    
    That's all, Thanks for sticking along till week 1!
    
    ### Some extra reads:
    
* [https://github.com/OWASP/DevGuide/blob/master/02-Design/01-Principles%20of%20Security%20Engineering.md](https://github.com/OWASP/DevGuide/blob/master/02-Design/01-Principles%20of%20Security%20Engineering.md)