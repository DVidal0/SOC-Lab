<h1>Home SOC</h1>

<h2>Description</h2>
The project consists on a basic home SOC lab made with a VM from Azure. We will get the attacks by deactivating all security measures and making the VM fully open to the internet.
<br/>

<h2>Objectives</h2>
- <b>Become familiar with the Azure enviroment and Microsoft Sentinel</b>

<h2>Environments Used </h2>
- <b>Microsoft Azure</b>

<h2>Walkthrough:</h2>
Create a VM inside a Resource Group in Azure and disable the firewall and all protections. In this case it's a VM with Windows 10 installed.
Once open to the internet, we start recieving login attempts. <br/>
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=101Aez5iamat2LY7zHLlMVdSAJcHOBwng" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Create a Log Analytics Workspace, a Sentinel instance and a Data Collection Rule that gathers the logs stored by the VM. <br/>
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=105kwr84AxpSuc0ND9_fZZjM1_on8mY3d" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

In the Log Analytics Workspace que can use KQL to query the logs from the VM. In this case, we are interested in the failed login attempts (Id 4625). <br/>
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=1062Cp-JrDCIMcpzC4TGGgVYPVJ0s4Ii_" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Add a watchlist in Sentinel. This is a csv file with the IP ranges and the corresponding location, like the one that Microsoft offers in their website <a href="https://www.microsoft.com/en-us/download/details.aspx?id=53601">Microsoft IP Range GeoLocation</a>. In a future version i'll try to make it live.<br/>
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=10eqloGSZ-UksEdOSayb9umkss_P2Hazn" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Now we can query the failed login attempts and correlate the IP adresses with the watchlist using 'ipv4_lookup'.
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=10jdfuRqu7rvZv5OsD8kylg11zfFuJTaq" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Now we create a map using a workbook from Sentinel. This is the map of incoming attacks after 24 hours.
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=110qgKi6kjb9tj5reEIxf5XDOeHDLoEB5" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Using Sentinel analytics we can create an alert rule that creates an alert when the number of failed login attempts is greater than a number.
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=10oCwOXgJeYMDt_JAkGdbNNW_n2LVbZJT" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>

Each alert creates an incident that can be assigned for revision.
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=10tnrPCFROkHpUi3Y7pgDhIIFaKoMXiBo" height="80%" width="80%" alt="SOC Lab Steps"/>
<br/>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
