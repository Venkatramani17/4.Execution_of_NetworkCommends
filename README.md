# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>
## PROGRAM

server.py
```
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()
```
client.py
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()
```



## Output
tracert:
<img width="1054" height="702" alt="image" src="https://github.com/user-attachments/assets/786e23fa-9ec2-47e0-b8ba-662a39eccdfc" />

ping:
<img width="1182" height="525" alt="image" src="https://github.com/user-attachments/assets/52a49ac4-4e48-461f-bd1b-254ead9f8b7f" />


nslookup:
<img width="952" height="462" alt="image" src="https://github.com/user-attachments/assets/56eb53a4-8e5f-43a8-8301-f20330efb427" />

netstat:
<img width="927" height="728" alt="image" src="https://github.com/user-attachments/assets/2d1da0ea-c349-4314-82d2-f46fa4f2e6b0" />


ipconfig:

<img width="902" height="764" alt="image" src="https://github.com/user-attachments/assets/fcc68807-ef8b-4987-b788-0c5c46a79fdf" />


getmac:

<img width="945" height="306" alt="image" src="https://github.com/user-attachments/assets/f53eeb3c-9d83-4fc5-9478-a124a668de8c" />

arp:

<img width="916" height="739" alt="image" src="https://github.com/user-attachments/assets/29dd9559-e1a8-45f8-9d89-d72502d5b14f" />



## Result
Thus Execution of Network commands Performed 
