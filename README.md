Remote PC Cotrol
Overview

We will implement two different programs that will run on separate terminals:

    serverprog.py (Server Program)
    clientprog.py (Client Program)

Socket Programming Functions

Here are some of the key socket programming functions used in this project:
Function	Description
socket.socket()	Creates a socket.
socket.bind()	Binds hostname and port to the socket.
socket.listen()	Starts the TCP listener.
socket.accept()	Accepts client connection and waits for a connection.
socket.connect()	Initiates the TCP connection.
s.recv()	Receives a TCP message.
s.send()	Sends a TCP message.
socket.gethostname()	Returns the hostname of the machine.
Importing Required Modules

We will import the following modules to facilitate our program:

python

import time
import socket
import sys
import os

    time: Works with time functions.
    socket: Establishes connections between two nodes on the network.
    sys: Provides information about the Python interpreter.
    os: Interacts with the operating system.

Server Program (serverprog.py)
Code

python

import time
import socket
import sys
import os

# Initialize socket
soc = socket.socket()

# Get hostname
host = socket.gethostname()

# Set port
port = 8080

# Bind the socket to host and port
soc.bind(('', port))

print("Waiting for connections...")

# Listen for connections
soc.listen()

# Accepting incoming connections
conn, addr = soc.accept()

print(addr, "is connected to server")

# Take command as input
command = input(str("Enter Command: "))
conn.send(command.encode())

print("Command has been sent successfully.")

# Receive confirmation
data = conn.recv(1024)

if data:
    print("Command received and executed successfully.")

Explanation

    Socket Creation: The server creates a socket and binds it to a specified hostname and port.
    Listening: The server listens for incoming connections and waits for a client to connect.
    Command Input: The server takes a command input from the user and sends it to the connected client.
    Confirmation: The server waits for confirmation from the client that the command has been received.

Client Program (clientprog.py)
Code

python

import time
import socket
import sys
import os

# Initialize socket
soc = socket.socket()

# Set host
host = "127.0.0.1"
port = 8080

# Connect to the server
soc.connect((host, port))
print("Connected to Server.")

# Receive command from server program
command = soc.recv(1024)
command = command.decode()

# Match the command and execute it on client system
if command == "open":
    print("Command is:", command)
    soc.send("Command received".encode())

    # Execute the specified file
    os.system('test.bat')

Explanation

    Socket Creation: The client creates a socket and connects to the server using the specified hostname and port.
    Command Reception: The client waits to receive a command from the server.
    Command Execution: If the received command matches "open", the client executes the specified batch file.

Conclusion

By following this tutorial, you will be able to control a PC remotely using Python and socket programming. Make sure to run the serverprog.py first to allow the client to connect successfully. Happy coding!
