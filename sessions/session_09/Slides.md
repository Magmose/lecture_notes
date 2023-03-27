

class: center, middle

## DevOps, Software Evolution and Software Maintenance

<img src="https://www.saa-authors.eu/picture/739/ftw_768/saa-mtcwmza4nzq5mq.jpg" width=40%/>

# Security


Mircea Lungu, Associate Professor,<br>
[IT University of Copenhagen, Denmark](https://www.itu.dk)<br>
`mlun@itu.dk`

---


<a href="https://www.inc.com/joe-galvin/60-percent-of-small-businesses-fold-within-6-months-of-a-cyber-attack-heres-how-to-protect-yourself.html">
<img src="./images/cyberattacks_close_businesses.png" alt="Drawing" style="align: left; width: 80%"/>
</a>



---

## Before we Start: State of the Projects

**Logging** 
  - Did you add logging to your MiniTwit?
  - What frameworks / libraries / tools did you use? 

--


**Logging in Practice**
  - Could you catch a bug in production with the help of the scenario that we provided you? 
  - What was the bug? Did the logging help?
  - Do you see access logs? 
  - Is anybody trying to hack your system?




---


### Site Reliability Engineer


"The SRE role of today **combines the skills of the developer responsible for writing applications and the skills that operations engineers use to deploy those applications**. 

The SRE moves an application from proof of concept, to quality control, and then to deployment – **automating that entire process** and giving it consistency.

--

By **continuing to run security experiments**, we can evaluate and improve such vulnerabilities proactively in the ecosystem before they become crisis situations." ([Through the looking glass: Security and the SRE](https://opensource.com/article/18/3/through-looking-glass-security-sre))

--

Question: Is it the same or not? 





---

## Compare the following quotes


- "I was upgraded from engineer to Site Reliability Engineer. It is one of the most important roles in our company". (My friend K)

- "We can implement a Facebook competitor for you" (My friend J and me)

##### Which one is more professional?
---



## Being A Professional = Building Dependable Systems

Webster's definition of **dependable**:

```
adj: capable of being trusted or depended on : RELIABLE

```

<!-- <img src="images/dependable.png" alt="Drawing" style="width: 200px;"/> -->

Sommerville defines **dependability** as: 
- **availability**  -- probability that a system is operational at a given time -- Uptime / (Uptime + Downtime), e.g. "5 nines"

- **reliability** -- probability of correct functioning  for some given time  -- MTBF = mean time between failures 

- **safety**  -- ability to operate w/o catastrophic failure

- **security** <-- *today's focus*!!!!




---




# Information Wants to be Free...



<img src="https://images-na.ssl-images-amazon.com/images/I/51FbpAQFVPL.jpg" alt="Drawing" style="width: 200px; float:right; margin: 10px;"/>


"Information wants to be free...

... Information also wants to be expensive.

... That tension will not go away

" 

 


Security = "preventing information from being freed :)"


<br/>
(A question from the book: "Can you map the flow of information in the world?" + [One possible attempt at answering it](https://mircealungu.com/post/13-09-01-visualizing-stack-overflow/) )






---

# Security

... the protection of computer systems and networks from the theft of or damage to their hardware, software, or  data, as well as from the disruption or misdirection of the services they provide. [1]


[1] https://commons.erau.edu/cgi/viewcontent.cgi?article=1476&context=jdfsl 


---

# State of the Security

- **The most common way to discover security failures?**
  - when a security incident happens 


- **Average time until people found out they were hacked?**
  - half a year! [1]
  - By this time, it is often too late, and damage has been done. 
  - *Story*: Russian vs. Brazilian hackers.


[1] 2017 Cost of Data Breach Study by IBM -  https://www.ibm.com/downloads/cas/ZYKLN2E3


---


## What to do? 
  
  
**As Devs coming to DevOps...** we must become good with
   - security
   - system administration
   - networking

--

**We need a proactive and systematic approach**
  1. understand threats
  1. assess risk
  1. test security
  1. detect breaches
  
---


# 1. Understanding Threats


### What is a threat? 

A threat is defined by a triplet:

1. Intent (we can guess)
2. Capability (we can't change)
3. Opportunity <-- (this is our focus!)


---

### Who attacks you? 

* Black Hat - bad guys in the western movies

* White hat - ethical hackers, working with orgs to strengthen security

* Grey Hat - not malicious, usually notify you that they hacked you

* Script Kiddies - they have time on their hands


What differentiates them: **intent** & **capability**...

---

## Migrating from GCE to DO: A Case Study

<img src="images/ufw_and_docker.png" width="90%" />

---

## The Next Day: Backup of ES is very small... 

### Looking in the DB Shows a Single Document:
<img src="images/give_us_btc.png" width="100%" />


---

## What went wrong ?

- docker circumvents the UFW firewall configuraition and opens the ports to the world! [a discussion](https://github.com/docker/for-linux/issues/690)
- undermines the point of the reverse proxy :)

---

# Learning from the "Intelligence Field"

1. Collect (**What are your assets**? What is worth protecting?)
1. Analyse the adversary and opportunities
1. Process (**What are the *risks*? Which should be addressed?**)
1. Disseminate (Implement mitigations)

---

# So How do *we* assess risk? 

### Risk Matrices

- **Severity**. e.g., Insignificant, Negligible, Marginal, Critical, Catastrophic
- **Likelihood** e.g., Certain, Likely, Possible, Unlikely, Rare
- **Risk** = f(Likelihood, Severity)

## 

<img src="images/matrix.png" alt="Drawing" style="height: 300px;"/>





---

# e.g. A More Detailed Matrix

<img src="images/risk-rating-matrix.png" style="width:500px; float: right"/>

---


## Open Web Application Security Project: OWASP


- Online Community
- Maintains lists of vulnerabilityes for web applications


- **OWASP Top 10** Include:
  1. Broken Access Control
  3. Injection (XSS, SQL, etc.)
  7. Identification and Authenticaion Failures
  9. Insufficient Logging & Monitoring (!!!)







---

### Detail: Insufficient Logging and Monitoring

Issue included in the Top 10 **based on an industry survey**

Strategy for determining if you have **sufficient monitoring**

- examine the logs following *penetration testing* (defined later)


- the testers’ actions should be recorded sufficiently to understand what damages they may have inflicted


Note: *applying this strategy is part of your assignment*

---


## Insufficient Logging and Monitoring: When...

- Auditable events are not logged
  - e.g. loginsfailed logins, and high-value transactions
- Warnings and errors generate no log messages
  - (or inadequate, or unclear)
- You're not looking at the logs!
- The application is unable to detect, escalate, or alert for active attacks in real time or near real time.

Source: [OWASP Top 10: Insufficient Logging and Monitoring](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A10-Insufficient_Logging%252526Monitoring)

Logging Cheatsheet from OWASP: https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html

---

## Testing Security: Penetration Testing

- a.k.a. pen-testing
- simulate attacks on your system
- helps understand what an attacker can do

> "blue teams always need **red teams** to test them against each other"

- requires you to know potential vulnerabilities




---


### Automating Pen Testing

- tools exist that can automate the process
- you provide a target IP and they scan it for vulnerabilities

- Kali Linux
  - security focused distro
  - contains a very large set of tools (https://tools.kali.org/tools-listing)
  - can be installed in meta-packages (https://www.kali.org/news/kali-linux-metapackages/)
    - top10
    - web
    - wireless
    - etc.

---

### Tool: Metasploit

- ruby-based framework for vulnerability scanning
- very popular
- large number of plugings


<img src="images/metasploit_modules.png" alt="Drawing" style="width: 300px;"/>


More: https://github.com/rapid7/metasploit-framework

A lot: https://books.google.dk/books?id=EOlODwAAQBAJ

---

### Tool: WMAP Plugin for Metasploit

- feature-rich web application vulnerability scanner 
- originally created from a tool named SQLMap
- integrated with Metasploit 
- see exercises for usage



[1] https://www.offensive-security.com/metasploit-unleashed/wmap-web-scanner/

---

### More Pen-Testing Tools

Inside Kali Linux
- [skipfish](https://www.systutorials.com/docs/linux/man/1-skipfish/)
- [nmap](https://nmap.org/book/man-port-scanning-basics.html)

Desktop Apps
- OWASP ZAP 
  - free, open-source penetration testing tool 
  - maintained under the umbrella of the OWASP 
  - [getting started](https://www.zaproxy.org/getting-started/), [docs](https://www.zaproxy.org/docs/api/#introduction)
- The tools in the [list of OWASP vulnerability scanning tools](https://owasp.org/www-community/Vulnerability_Scanning_Tools)

Online Services 
- Detectify (https://detectify.com/)
 - quite nice
 - requires an account
 - require you to prove that you own the website
- Mozilla Observatory (https://observatory.mozilla.org/)
- shodan.io


---

## Detection

Is hard.

Warning signs that you might have an intruder
 - abnormal network traffic (important to monitor!)
 - unusual resource usage (ditto)
 - you can't access your server
 - your server IP has been blacklisted
 
---


### Detection - Approach

- Develop baseline for normal
- Stop intruders from taking information out 
  - firewall
  - traffic filtering
  - white/black listing
- Auditing, system hardening, compliance testing, e.g. Lynis

 
---


### Tool for System Hardening: Lynis

- analyzes the system from within
- treats the system as white box as opposed to blackbox


``` 

sudo lynis audit system

... 

 [+] Boot and services
------------------------------------
  - Service Manager                                           [ systemd ]
  - Checking UEFI boot                                        [ DISABLED ]
  - Checking presence GRUB                                    [ OK ]
  - Checking presence GRUB2                                   [ FOUND ]
    - Checking for password protection                        [ NONE ]
  - Check running services (systemctl)                        [ DONE ]
        Result: found 27 running services
  - Check enabled services at boot (systemctl)                [ DONE ]
        Result: found 54 enabled services
  - Check startup files (permissions)                         [ OK ]

[+] Containers
------------------------------------
    - Docker
      - Docker daemon                                         [ RUNNING ]
        - Docker info output (warnings)                       [ 1 ]
      - Containers
        - Total containers                                    [ UNKNOWN ]
          - Running containers                                [ 4 ]
    - File permissions                                        [ OK ]

[+] Security frameworks
------------------------------------
  - Checking presence AppArmor                                [ FOUND ]
    - Checking AppArmor status                                [ ENABLED ]
  - Checking presence SELinux                                 [ NOT FOUND ]
  - Checking presence TOMOYO Linux                            [ NOT FOUND ]
  - Checking presence grsecurity                              [ NOT FOUND ]
  - Checking for implemented MAC framework                    [ OK ]

```
 
---


# Practical Steps to Improve Security in your Web Application





## 1. Evaluate Dependencies


- Keep dependencies up to date


- Scan dependencies for security breaches
  - source code and container images too
  - add security checks as part of your CI





**Principle**

  > "If its part of your app, it should be part of your security process"


##### Case Study
[Postmortem for Malicious eslint Packages Published on July 12th, 2018](https://eslint.org/blog/2018/07/postmortem-for-malicious-package-publishes)



---



<img src="images/hacker_license_plate.png" style="width:400px" />
[source](https://hackaday.com/2014/04/04/sql-injection-fools-speed-traps-and-clears-your-record/)




--

## 2. Never Trust User Input

- Validate the input before using it
  - in the webpages
  - in the API
- Use parameterized DB queries (or whatever framework help you can)

> Principle: "All input is bad until proven otherwise"


---


## 3. Protect your Servers

- Keep software on servers up to date


- e.g. [`apt-get install unattended-upgrades`](https://wiki.debian.org/UnattendedUpgrades)



---



## 4. Protect Secrets

- Don’t commit credentials and other secrets (like keys and certs) into a VCS repository


- Use 2FA for secret repositories


- Consider using dedicated tools and vaults for secrets


##### Case Study
[The Uber Breach](https://www.bloomberg.com/news/articles/2017-11-21/uber-concealed-cyberattack-that-exposed-57-million-people-s-data) - started accessing a private GitHub repo, where keys were found for an AWS account, etc.

---


## 5. Go Hack Yourself

- Create a red team to pen test


- Stress the app infrastructure

*Note: part of the assignment*

---

## 6. Protect your CI/CD tools 

- CI pipeline is part of your infrastructure


##### Case Study

Multiple US government agencies [hacked due to misconfiguration of their TeamCity CI tool](https://cd.foundation/blog/2021/01/07/could-ci-cd-tool-teamcity-really-have-been-exploited-to-hack-the-us/_)

---

## 7. Automatic Backups

- This is critical

- Test your full recovery process


**Principle**

> Data is probably your most precious asset; don't lose it

> A backup is not useful unless you can use it to actually perform the backup



---


## 8. Log Everything 

- Your key to being able to detect attacks 
- See previous lecture for details


---

# References:

- [Five Easy Steps to Keep on Your Organization’s DevOps Security Checklist
](https://www.tripwire.com/state-of-security/devops/devops-security-checklist/)
- [What Is A Risk Assessment Matrix?](https://sectara.com/news/risk-assessment-matrix/)
- [ Guide To Conducting Cybersecurity Risk Assessment For Critical Information Infrastructure](https://www.csa.gov.sg/-/media/csa/documents/legislation_supplementary_references/guide_to_conducting_cybersecurity_risk_assessment_for_cii.pdf), Dec 2019
- The DevOps Security Checklist by Sqreen


Further Reading
- [Information Security Risk Analysis – A Matrix-based Approach ](https://www.albany.edu/~goel/publications/goelchen2005.pdf) -- an advanced approach to security risk analysis 
