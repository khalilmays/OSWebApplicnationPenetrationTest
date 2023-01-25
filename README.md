<h1>OS and Web Application Penetration Test</h1>

<h2>Description</h2>
For this project, I played the role of a penetration tester for a fictional organization named Rekall Corporation. My job was to was to find vulnerabilities that were present in Rekall's web application, linux, and windows server using offensive security skills that I learned. This project required me to capture flags and input them into a website to prove that I actually found the vulnerabilities. Throughout the project I utilized the different phases of penetration test engagements like reconnaissance, planning, exploitation, post-exploitation. During the project, I documented every vulnerability and provided mitigation reccomendations in the penetration report that you can find below.

<br />


<h2>Technologies Used</h2>

- <b>Kali Linux</b>
- <b>Metasploit</b>
- <b>Meterpreter</b>
- <b>Nessus</b>
- <b>OSINT Tools</b>
- <b>SSH</b>
- <b>FTP</b>
- <b>Google (dorking)</b>
- <b>Mimikatz (Kiwi)</b>
- <b>John The Ripper</b>
- <b>Burp Suite</b>
- <b>Priviledge Escalation</b>
- <b>Docker</b>

<h2>Walk-Through Creating Webapp:</h2>

<p align="center">
Select "App Services" in the Azure search field: <br/>
<img src="https://i.imgur.com/k7h6mdZ.png" height="80%" width="80%" alt="App Services"/>
<br />
<br />
Select "Create" to create your app:  <br/>
<img src="https://i.imgur.com/PCaXvLb.png" height="80%" width="80%" alt="Create app"/>
<br />
<br />
Selected these options for the "Basics" tab: <br/>
<img src="https://i.imgur.com/EszCcBi.png" height="80%" width="80%" alt="Basics"/>
<br />
<br />
Selcted these options for the App Service Plan:  <br/>
<img src="https://i.imgur.com/WJK5EeZ.png" height="80%" width="80%" alt="App service plan"/>
<br />
<br />
Leave the default options for every other tab and select the "Review + Create" tab. Then you will select the create button at the bottom of your screen to create your web app.
<br />
<br />
Once you have created your app you can either select "Go to Resource" or you can go to the app by clicking "App Services" in the Azure search bar. Then would select your app from this page:  <br/>
<img src="https://i.imgur.com/BzsA80B.png" height="80%" width="80%" alt="select app"/>
<br />
<br />
After selecting your app, a menu of options appears on the left. You will choose the "Custom domains" option:  <br/>
<img src="https://i.imgur.com/MHx7ZTp.png" height="30%" width="30%" alt="custom domains"/>
<br />
<br />
A new page will open, and you will be able to see a unique IP address that your app was assigned:  <br/>
<img src="https://i.imgur.com/B4hKa5S.png" height="80%" width="80%" alt="IP address"/>
<br />
<br />
Your domain is now accessible on the internet and it begins with the name you chose ".azurewebsites.net"
<br />
<br />
This is the docker container that I deployed to my web app using Azure Cloud Shell:  <br/>
<img src="https://i.imgur.com/C0QSchr.png" height="80%" width="80%" alt="Docker Container"/>
<br />
<br />
To get into Azure CLoud Shell, you click the shell logo located inthe tool bar:  <br/>
<img src="https://i.imgur.com/0sHCBtm.png" height="80%" width="80%" alt="Azure Cloud Shell"/>
<br />
<br />
I configured the web app with the container mentioned above by running the following command:  <br/>
az webapp config container set --name (name of your webapp) --resource-group (name of your resource group) --docker-custom-image-name cyberxsecurity/project1-apachewebserver --enable-app-service-storage-t  <br/>
<br />
<br />
After pressing enter you should see this output: <br />
<img src="https://i.imgur.com/syypJCY.png" height="80%" width="80%" alt="Output"/>
<br />
<br />
To verify that the container has been added correctly, make sure to run the fdollowing command to show the container for your webapp: <br />
az webapp config container show --name (name of your webapp) --resource-group (name of your resourece group) <br />
<br />
<br />
Next, visit the domain that you chose to see if your container was successfully deployed. The webpage should like like this: <br />
<img src="https://i.imgur.com/uT6TQzD.png" height="80%" width="80%" alt="12"/> <br />
<br />
<br />
To customize your webpage you have to access the HTML pages of your webapp. To do so return to your webapp and select "SSH" then select "Go": <br />
<img src="https://i.imgur.com/cceC0GI.png" height="80%" width="80%" alt="11"/> <br />
<br />
<br />
Once you're in the container, you need to change directories to the location of the HTML files: <br />
<img src="https://i.imgur.com/xJPkGSo.png" height="80%" width="80%" alt="10"/> <br />
<br />
<br />
Once you're in the container, you need to change directories to the location of the HTML files: <br />
<img src="https://i.imgur.com/xJPkGSo.png" height="80%" width="80%" alt="9"/> <br />
<br />
<br />
To customize your webpage as you want, run the following command: <br/>
index.html <br/>
<br/>
<br/>
<h2>Walk-Through Self-Signed Certificate:</h2>

Azure gives you a trusted certificate for your domain, but to analyze the difference I created a self-signed certificate.
<br/>
<br/>
First you will need to acccess Azure key vaults, do so by searching in key vault at the top of the page: <br/>
<img src="https://i.imgur.com/SzrM9K6.png" height="80%" width="80%" alt="7"/> <br />
<br />
<br />
Select "+ Create" from the key vault page to make your key vault: <br/>
<img src="https://i.imgur.com/r4Fv21x.png" height="80%" width="80%" alt="7"/> <br />
<br />
<br />
On the "create key vault" tab you need to make sure you select your subscirption and resource groups, key vault name , region, pricing, and for this project I left the other options (Access Policy, Networking, and Tags) as default. Then, select "Review + Create" to create your key vault: <br/>
<img src="https://i.imgur.com/OIhfkbN.png" height="40%" width="40%" alt="6"/> <br />
<br />
<br />
Next create a self-signed certificate using OpenSSL. Go back and select the "SSH" button again: <br/>
<img src="https://i.imgur.com/PabIV2k.png" height="80%" width="80%" alt="5"/> <br />
<br />
<br />
From the command line, enter the follwing command: <br/>
openssl req -x509 -sha256 -nodes- -days 365 -newkey rsa:2048 -keyout (privatekeyname.key) -out (certificatename.crt) -addtext "extendedKeyUsage=serverAuth" <br/>
The command should look similar to this: <br/>
<img src="https://i.imgur.com/8lT5HvZ.png" height="80%" width="80%" alt="4"/> <br />
<br />
<br />
The options chose do the following: <br/>
- <b>-x509: Indicates for OpenSSL to create an SSL certificate.</b>
- <b>-sha256: Uses the sha256 hasing alogrithm.</b>
- <b>-days 365: States the certificate will be valid for one year.</b>
- <b>-newkey rsa:2048: Uses a 2048-bit RSA key.</b>
- <b>-keyout project1-key.key: The outputted name of the private key.</b>
- <b>-out project-cert.crt: The outputted name of the certificate. </b>
- <b>-addtext "extendedKeyUsage=serverAuth": Indicates how a public key can be used.</b>
<br/>
<br/> 
After pressing enter, you will need to answer the following questions: <br/>
<img src="https://i.imgur.com/N46x2NA.png" height="80%" width="80%" alt="1"/> <br />
<br/>
<br/>
Next, view the newly create key (.key) and certificate (.crt) by using the "ls" command: <br/>
<img src="https://i.imgur.com/KdXLSn8.png" height="80%" width="80%" alt="2"/> <br />
<br />
<br />
Next create a PFX format certificate because that's how Azure requires theirs. Run the following command: <br />
openssl pkcs12 -export -out (new_certificatename.pfx) -inkey project1-key.key -in project1-cert.crt <br/>
<img src="https://i.imgur.com/ZFVePql.png" height="80%" width="80%" alt="3"/> <br />
<br/>
<br/>
The options chose do the following: <br/>

- <b>pkcs12: Indicates for OpenSSL to create a PFX certificate.</b>
- <b>-export -out project1-cert.fpfx: States what to name the PFX file.</b>
- <b>-inkey projec1-key.key: This is the current private key that you are importing.</b>
- <b>-in project1-cert.crt: This is the current certificate that you are importing.</b>
</b>
</b>
Next a prompt will appear asking for a password to encrypt your PFX key. Put in a password nad make sure not to forget it. <br/>
</b>
</b>
You can view your new PFX certificate by running the "ls" command:
<img src="https://i.imgur.com/j50ubyA.png" height="80%" width="80%" alt="13"/> <br />
<br />
<br />
Download the PFX certificate using the follwoing steps: <br/>

- <b>(1) Click the "Upload/Download" icon in the toolbar of the cloud shell.</b>
- <b>(2) Select "Download".</b>
- <b>(3) Enter the name of your PFX certificate in the "Download a file" window.</b>
- <b>(4) Click "Download."</b>
<br/>
<img src="https://i.imgur.com/POUEIel.png" height="80%" width="80%" alt="14"/> <br />
<br/>
<br/>
Next, import the certificate to Azure. Return to the Azure portal and select "Key Vaults", then select the key vault you created in the previous part. Then from the key vault, select the "Certificates" and then "+ Generate/Import,": <br/>
<img src="https://i.imgur.com/iO26098.png" height="80%" width="80%" alt="15"/> <br />
<br/>
<br/>
On the "Create a certificate" page,select the following: <br/>


- <b>Method of Certificate: Import</b>
- <b>Certificate Name: project1PFX-cert</b>
- <b>Upload Certificate File: Select your PFX certificate (check the downloads folder)</b>
- <b>Password: Enter the password that you encrypted your certificate with</b>
<img src="https://i.imgur.com/gKzvN7s.png" height="80%" width="80%" alt="16"/> <br />
<br/>
<br/>
Select the "Create" icon to upload the certificate. <br/>
<img src="https://i.imgur.com/2VtSDLQ.png" height="80%" width="80%" alt="17"/> <br />
<br/>
<br/>
Now go to the webpage and your browser should notify you that your connection the website is not secure due to the certificate being self-signed. <br/>
<img src="https://i.imgur.com/u9wKRlr.png" height="80%" width="80%" alt="18"/> <br />
<img src="https://i.imgur.com/QfNdxYv.png" height="80%" width="80%" alt="19"/> <br />
<br/>
<br/>
<h2>Walk-Through Security:</h2>

First create an Azure Front Door instance. Do so by navigating to the app you created, then select the "Networking" option followed by "Azure Front Door": <br/>
<img src="https://i.imgur.com/0qs9DHT.png" height="80%" width="80%" alt="20"/> <br />
<br/>
<br/>
Next select the "create new" option under "Front Door Instance." Name your Front Door, then leave all of the settings default and click the "add" button. <br/>
<img src="https://i.imgur.com/bWzGF8C.png" height="80%" width="80%" alt="21"/> <br />
<br/>
<br/>
You will return to the Azure Front Door page and then click "OK": <br/>
<img src="https://i.imgur.com/BGvXaDt.png" height="80%" width="80%" alt="22"/> <br />
<br/>
<br/>
To verify that your Front Door is working, select "Networking" again and then Azure Front Door. You should see the following prompt:
<img src="https://i.imgur.com/KwnXE9z.png" height="80%" width="80%" alt="23"/> <br />
<br/>
<br/>
Next, set up the Web Application Firewall (WAF). To do that search "webapp" or "firewall" in the Azure search bar, the WAF that was created previously should be shown:<br/>
<img src="https://i.imgur.com/wesmQ8d.png" height="80%" width="80%" alt="24"/> <br />
<br/>
<br/>
There will be options on the left side of the screen, select the one that says "Managed Rules": <br/>
<img src="https://i.imgur.com/QmHyRE5.png" height="80%" width="80%" alt="25"/> <br />


























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
