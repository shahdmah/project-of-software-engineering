from socket import *

try:
    server_socket = socket(AF_INET, SOCK_STREAM)  # Create a socket object
    host = "127.0.0.1"  # Server IP address
    port = 7002  # Server port
    server_socket.bind((host, port))  # Bind the socket to the address
    server_socket.listen(5)  # Listen for incoming connections (max 5 clients)
    print("Server listening on port", port)

    while True:
        client_socket, client_address = server_socket.accept()  # Accept a new connection
        print("Connection from:", client_address)
        
        while True:
            message = client_socket.recv(2048).decode('utf-8')  # Receive message from client
            if not message:
                break
            print("Client:", message)
            
            # Echo back the received message
            response = input("Server: ")  # Take input from the server
            client_socket.send(response.encode('utf-8'))  # Send the response to the client
        
        client_socket.close()  # Close the client connection
except KeyboardInterrupt:
    print("Server terminated")
finally:
    server_socket.close()  # Close the server socket
