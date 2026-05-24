# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server.py
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)

print(f"Server listening on {host}:{port}...")

# Wait for client to connect
c, addr = s.accept()
print(f"Connected to client: {addr}")

# Specify the file you want to send to the client
filename = 'sample.txt.txt' 

try:
    # Open the file in binary read mode ('rb')
    with open(filename, 'rb') as f:
        print(f"Sending {filename}...")
        
        while True:
            # Read chunks of 1024 bytes
            data = f.read(1024)
            if not data:
                break  # File reading is complete
            c.send(data)
            
    print("File sent successfully.")
except FileNotFoundError:
    print(f"Error: The file '{filename}' was not found. Please create it first.")

# Clean up connections
c.close()
s.close()
print("Connection closed.")

```
client.py
```
import socket

s = socket.socket()
host = socket.gethostname() 
port = 60000 

s.connect((host, port))
s.send("Hello server!".encode())

# Open the file in binary write mode ('wb')
with open('received_file', 'wb') as f:
    while True:
        print('Receiving data...')
        data = s.recv(1024)
        
        if not data:
            break # Break the loop if no more data is arriving
            
        print(f"Data chunk received: {len(data)} bytes")
        f.write(data)
        break

print('Successfully received the file.')
s.close()
print('Connection closed.')

```
## OUPUT
<img width="650" height="125" alt="image" src="https://github.com/user-attachments/assets/841640f0-262a-460a-83e7-3db0f3186151" />

<img width="660" height="111" alt="image" src="https://github.com/user-attachments/assets/11a12db5-3f22-45cc-aeb1-8f0bb92d5e72" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
