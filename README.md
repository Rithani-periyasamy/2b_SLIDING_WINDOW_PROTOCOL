# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

#Server output:

import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(1)

print("Waiting for connection...")

conn, addr = s.accept()

print("Connected to", addr)

while True: data = conn.recv(1024).decode()

if not data:

break

print("Frames received:", data)

ack = "ACK for " + data

conn.send(ack.encode())

conn.close()

#Server output:

Waiting for connection...

Connected to('127.0.0.1',59954)

Frames received: 1 2 3

Frames received: 4 5 6

Frames received: 7 8 

#Client program:

import socket

s = socket.socket()

s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))

w = int(input("Enter window size: "))

frames = list(range(1, n+1))

i = 0

while i < n: send_frames = frames[i:i+w] msg = " ".join(map(str, send_frames))

print("Sending frames:", msg)

s.send(msg.encode())

ack = s.recv(1024).decode()

print("Received:", ack)

i += w

s.close() 

#Client Output:

Enter number of frames: 8

Enter window size: 3

Sending frames: 1 2 3

Received: ACK for 1 2 3

Sending frames: 4 5 6

Received: ACK for 4 5 6

Sending frames: 7 8 

Received: ACK for 7 8

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
