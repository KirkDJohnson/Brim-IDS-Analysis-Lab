<h1>Nessus Vulnerability Scanner Lab </h1>


<h2>Description</h2>
Text
<br />


<h2>Utilities Used</h2>

- <b>Brim</b> 
- <b>Wireshark</b>
- <b>VirusTotal</b>


<h2>Environments Used </h2>

- <b>Ubuntu Linux VM </b> 

<h2>Lab Overview:</h2>

<p align="center">
Scenerio for the lab.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/130925aa-64bb-433d-80a7-7b8429502c70"  alt="Brim Analysis"/>
<br />
<br />
With the tools provided in the lavb I choose to first use Brim as it has the most enriched data compared to Wireshark and Network Miner.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/c6423690-ae47-4427-85d4-bf330ed451d2"  alt="Brim Analysis"/>
<br />
<br />
Seeing that are Suricata IDS logs, I filtered to see what alerts where generated. The alert " Misc activity, A network Trojan was detected, Potential Corporate..." I first investigated.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/94a1a5b4-985e-4e25-a268-d5152db72b02"  alt="Brim Analysis"/>
<br />
<br />
Filtering for the source IP that triggered the alert, it shows three alerts, sparked from downloading an "non-executable" from the internet which is often used for mawlare to disguise a malicious file.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/f3ac73e8-f61b-41a0-8bcb-01f420c13036"  alt="Brim Analysis"/>
<br />
<br />
Doubling clicking on the first alert provides further details that revealed the alert signature was generated from MSXMLHTTP which is a component used for making HTTP requests which which I will note for later.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/74791c30-5572-4b1d-afe3-c710546ae826"  alt="Brim Analysis"/>
<br />
<br />
However, the third alert is generted with the signature "ET POLICY PE EXE or DLL Windows file download HTTP", which indicates a different file extension than the previous alert <br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/8443dc8e-e2b9-418a-a9af-b62860916fa8"  alt="Brim Analysis"/>
<br />
<br />
Text<br/>
<img src=""  alt="Brim Analysis"/>
<br />
<br />
Text<br/>
<img src=""  alt="Brim Analysis"/>
<br />
<br />
Text<br/>
<img src=""  alt="Brim Analysis"/>
<br />
<br />
Text<br/>
<img src=""  alt="Brim Analysis"/>
<br />
<br />
  
<h2>Thoughts</h2>
Text

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
