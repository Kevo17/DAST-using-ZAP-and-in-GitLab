<h1>DAST using ZAP and in GitLab</h1>


<h2>Description</h2>
This lab focuses on leveraging OWASP ZAP (Zed Attack Proxy), a robust Dynamic Application Security Testing (DAST) tool, within the GitLab platform. ZAP helps identify security vulnerabilities in web applications by actively scanning for common web application vulnerabilities, performing attack simulations, and providing detailed reports.

During this hands-on lab, participants will gain practical experience in integrating ZAP into the GitLab pipeline to enhance the security of their web applications. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>ZAP</b>
- <b>JSON</b>
- <b>GitLab</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Linux</b> 

<h2>Program walk-through:</h2>

First, we need to pull ZAP’s stable docker image: <br/>
```
docker pull owasp/zap2docker-stable:2.10.0
 ```
<br/>
<p align="center">
<img src="https://i.imgur.com/SfCRDmu.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s see the usage of ZAP Docker for Baseline Scan: <br/>
```
docker run --rm owasp/zap2docker-stable:2.10.0 zap-baseline.py --help
 ```
<br/>
<p align="center">
<img src="https://i.imgur.com/Ikd44oM.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run zap-baseline.py with basic options: <br/>
```
docker run --rm owasp/zap2docker-stable:2.10.0 zap-baseline.py -t https://prod-rcgsg0ei.lab.practical-devsecops.training
 ```
<br/>
<p align="center">
<img src="https://i.imgur.com/mtknTQL.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run the scan in GitLab in the YAML configuration file: <br/>
```
- docker pull owasp/zap2docker-stable:2.10.0
```
```
- docker run --user $(id -u):$(id -g) -w /zap -v $(pwd):/zap/wrk:rw --rm owasp/zap2docker-stable:2.10.0 zap-baseline.py -t <YOUR HOST URL> -J zap-output.json
 ```
<br/>
<p align="center">
<img src="https://i.imgur.com/b38bGJu.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Here is the result of this job: <br/>
<p align="center">
<img src="https://i.imgur.com/3ot3ebE.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
