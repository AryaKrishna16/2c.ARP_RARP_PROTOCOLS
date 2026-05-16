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
P
## PROGRAM - ARP
 ## Client 
 ```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Client Waiting for Connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    print("Requested IP Address:", ip)
    try:
        mac = address[ip]
        c.send(mac.encode())
        print("MAC Address Sent:", mac)
    except KeyError:

        c.send("Not Found".encode())

```

## Server
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
print("Connected to ARP Client")
while True:
    ip = input("Enter Logical IP Address : ")
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address :", mac)
```
## OUPUT - ARP
<img width="1639" height="923" alt="Screenshot 2026-05-16 135608" src="https://github.com/user-attachments/assets/ff457a70-6b7e-45e3-bd68-068424e1967a" />

## PROGRAM - RARP
## Client
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("RARP Client Waiting for Connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    mac = c.recv(1024).decode()
    if not mac:
        break
    print("Requested MAC Address:", mac)
    try:
        ip = address[mac]
        c.send(ip.encode())
        print("IP Address Sent:", ip)
    except KeyError:
        c.send("Not Found".encode())
```

## Server 
```
import socket

s = socket.socket()

s.connect(('localhost', 9000))

print("Connected to RARP Client")

while True:

    mac = input("Enter MAC Address : ")

    s.send(mac.encode())

    ip = s.recv(1024).decode()

    print("Logical IP Address :", ip)
```
## OUPUT -RARP
<img width="1627" height="923" alt="Screenshot 2026-05-16 141421" src="https://github.com/user-attachments/assets/1ad89ae9-9e62-4627-8f08-17a27a116b1c" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
