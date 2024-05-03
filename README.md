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
When filtering for just the malicious IP, more packets are shown, one of which is an HTTP "GET" request packet to a suspicious domain, "awh93dhkylps5ulnq-be[.]com/czwih/fxla[.]php?l=gap1.cab"<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/1782c32e-84c5-4181-8ef2-697408c7c1ac"  alt="Brim Analysis"/>
<br />
<br />
Searching for suspicious domain from the GET request on VirusTotal shows that it is indeed malicious tied to phishing/malware. <br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/73a0f0a4-fad0-4b55-998c-91c6780fa0d0"  alt="Brim Analysis"/>
<br />
<br />
Switching over to Wireshark, I went to export -> HTTP and searched for the domain used in the GET request and saved/downloaded the file.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/0c703c3f-2332-4af2-8ff4-5615d3ff503e"  alt="Brim Analysis"/>
<br />
<br />
Once the file was exported to the VM, I used the terminal with the command sha256sum on the file to get the file hash for further analysis.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/7f0c0e5b-0d39-447c-807e-f2a1236502ef"  alt="Brim Analysis"/>
<br />
<br />
With the hash of the file I uploaded it to VirusTotal and discovered the gap1[.]cab was acuatlly draw.dll a trojan known as "Valak".<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/5d212ae3-107b-4437-85a5-0cbe338d617b"  alt="Brim Analysis"/>
<br />
<br />
After confirming the host had connection with a malicious domian I filtered for other domains the host reached out to that may also have been malicious through Brim and Wireshark.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/8ab61b2f-a212-447e-90f5-759d73cb3c22"  alt="Brim Analysis"/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/261dfb14-53cd-4571-b3a8-d3dce4b79cdd"  alt="Brim Analysis"/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/ad897491-9b4b-435c-bdef-b6404237a222"  alt="Brim Analysis"/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/dacd749a-7c38-4b42-a5d9-13bccdb8bb98"  alt="Brim Analysis"/>
<br />
<br />
I conducted further research on the two domains I found in Wireshark and Brim and found <br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/34ad4044-de5d-435e-9415-38935f1588e5"  alt="Brim Analysis"/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/f518206a-e225-428c-b34d-870f3578b885"  alt="Brim Analysis"/>
<br />
<br />
Lastly for this investigation, when I first examined the Suricata logs in Brim there were two alerts for "Not Suspicoius Traffic" from different IPs than the primarly attacker, but considering the host is compromised with a Trojan it is worth investigating all traffic for further Indicators of Attack<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/94a1a5b4-985e-4e25-a268-d5152db72b02"  alt="Brim Analysis"/>
<br />
<br />
The first IP I examined was 64[.]225[.]65[.]166, when uploaded to VirusTotal it has a 0/90 community score, however when it is a DigitalOcean domain meaning it is hosted int he cloud very cheap ans wasily created/deleted. More importantly, in the Relations tab, it hass Passive DNS replication and Communicating files with clearly malicious entities signifying this IP to be malicious and part of the attack.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/ea751eee-ef67-4e55-9dd3-b1dc3f929e88"  alt="Brim Analysis"/>
<br />
<br />
The second IP had a bit more evidence, VirusTotal did have a labled as malicious, however, filtering for the IP on brim shows a DNS query to 2partscow[.]top. Searching for that domain in VirusTotal also shows that is malicous with relations to futher malicious domains and files.<br/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/17d65d4a-9f9c-44f7-82c6-1d7d3ef185f7"  alt="Brim Analysis"/>
<img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/f21aec3b-6f32-48f4-a1b2-8c6b6ed5bf16"  alt="Brim Analysis"/>
  <img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/d3c9ae2e-84aa-4b4f-b21e-c750f28a4823"  alt="Brim Analysis"/>
  <img src="https://github.com/KirkDJohnson/Malicious-Download-Analysis-with-Brim-Lab/assets/164972007/7be7b89c-5de4-47cc-8f14-a4b5afc36fc3"  alt="Brim Analysis"/>
<br />
<h2>Thoughts</h2>
The lab/CTF was fairly straight forward 

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
