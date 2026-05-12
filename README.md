# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.


## PROGRAM - ARP
CLIENT.PY
```

import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address = {
    "169.254.94.36": "2A:2E:89:67:C8:7C"
}
while True:
    ip=c.recv(1024).decode()
    try:
       c.send(address[ip].encode())
    except KeyError:
       c.send("Not Found".encode())

SERVER.PY

import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
## OUPUT - ARP
<img width="879" height="237" alt="image" src="https://github.com/user-attachments/assets/1190cdd6-cb12-41c3-a779-a9c8f0fabeb7" />
```
## PROGRAM - RARP
CLIENT.PY
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for connection...")
c, addr = s.accept()
print("Connected to", addr)
address = {
    "2A:2E:89:67:C8:7C": "169.254.94.36"
}
while True:
    mac = c.recv(1024).decode()
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())
```
SERVER.PY

```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    mac = input("Enter MAC Address : ")
    s.send(mac.encode())
    print("IP Address :", s.recv(1024).decode())
```
## OUPUT -RARP
<img width="871" height="239" alt="image" src="https://github.com/user-attachments/assets/f642837b-fe91-4ee5-bd69-b7d7356b95b5" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
