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

## Program
```
import socket
import subprocess

# Create socket
s = socket.socket()

# Bind IP and Port
s.bind(('localhost', 8000))

# Listen for client
s.listen(1)

print("Server listening on port 8000...")

# Accept connection
c, addr = s.accept()

print("Connected:", addr)

while True:

    # Receive command
    command = c.recv(1024).decode().strip()

    # Exit condition
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:

        # Execute command
        completed = subprocess.run(
            command,
            capture_output=True,
            text=True,
            shell=True
        )

        # Combine output and error
        output = completed.stdout + completed.stderr

        # If no output
        if not output:
            output = "Command executed successfully."

    except Exception as e:

        output = f"Command failed: {e}"

    # Send result to client
    c.sendall(output.encode())

# Close connection
c.close()
s.close()
```
```
import socket

# Create socket
s = socket.socket()

try:

    # Connect to server
    s.connect(('localhost', 8000))

    print("Connected to server.")
    print("Type commands or 'exit' to quit.\n")

    while True:

        # Get command
        cmd = input("Enter command: ").strip()

        if not cmd:
            continue

        # Send command
        s.send(cmd.encode())

        # Exit
        if cmd.lower() == 'exit':
            print("Closing connection...")
            break

        # Receive result
        data = b""

        while True:

            part = s.recv(4096)

            data += part

            if len(part) < 4096:
                break

        # Display output
        print("\n----- RESULT -----")
        print(data.decode())
        print("------------------\n")

except ConnectionRefusedError:

    print("Server is not running!")

finally:

    s.close()
```


## Output
<img width="1918" height="1067" alt="Screenshot 2026-05-20 104122" src="https://github.com/user-attachments/assets/4f1c38b1-4900-4a7a-8ecf-48db80465602" />

<img width="1918" height="1073" alt="Screenshot 2026-05-20 104140" src="https://github.com/user-attachments/assets/62c757ff-016f-4317-bc05-761ab97c2e43" />

## Result
Thus Execution of Network commands Performed 
