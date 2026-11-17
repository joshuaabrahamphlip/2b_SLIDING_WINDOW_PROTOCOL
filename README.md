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
# SERVER

            import socket
            
            # Create socket
            s = socket.socket()
            
            # Bind host and port
            s.bind(('localhost', 8000))
            
            # Listen for connection
            s.listen(1)
            
            print("Waiting for connection...")
            
            # Accept connection
            conn, addr = s.accept()
            
            print("Connected to", addr)
            
            while True:
                # Receive data from client
                data = conn.recv(1024).decode()
            
                if not data:
                    break
            
                print("Frames received:", data)
            
                # Send acknowledgement
                ack = "ACK for " + data
                conn.send(ack.encode())
            
            # Close connection
            conn.close()
            s.close()


# CLIENT 

            import socket
            
            # Create socket
            s = socket.socket()
            
            # Connect to server
            s.connect(('localhost', 8000))
            
            # Get number of frames and window size
            n = int(input("Enter number of frames: "))
            w = int(input("Enter window size: "))
            
            frames = list(range(1, n + 1))
            
            i = 0
            
            while i < n:
                # Select frames within the window
                send_frames = frames[i:i + w]
            
                msg = " ".join(map(str, send_frames))
            
                print("Sending frames:", msg)
            
                # Send frames to server
                s.send(msg.encode())
            
                # Receive acknowledgement
                ack = s.recv(1024).decode()
            
                print("Received:", ack)
            
                i += w
            
            # Close socket
            s.close()


## OUPUT
<img width="1117" height="386" alt="Screenshot 2026-11-17 at 3 59 32 PM" src="https://github.com/user-attachments/assets/fdd83821-3093-4f41-9da7-c8a0130fffc2" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
