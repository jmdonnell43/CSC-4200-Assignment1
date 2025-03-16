# CSC-4200-Assignment1
This Python 3 project uses TCP sockets to implement a simple client-server model with SSL/TLS and AES-256 message encryption.


## Features

A TCP server that can handle several client connections
Handling client requests in multiple threads
Two-layer protection:
The connection is encrypted using SSL/TLS.
Encrypting individual messages using AES-256-CBC
Secure message recording; server acknowledgement messages
Appropriate error management for encryption and connection problems


## Requirements

- OpenSSL (for certificate generation) - Python 3.6 or later
AES encryption using the PyCryptodome library

## Project Structure

```
├── server.py          # Server implementation
├── client.py          # Client implementation
├── Makefile           # Build and run commands
├── README.md          # This file
└── design_explanation.md  # Design documentation
```

## Installation

1. Clone the repository:
   ```
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Build the project:
   ```
   make build
   ```

This will install the necessary dependencies (PyCryptodome) and create a virtual environment.

## Encryption Details

Two encryption layers are used in this implementation:

1. **SSL/TLS Encryption** - Protects the actual TCP connection
2. **AES-256-CBC Encryption** - Encrypts every single message

The steps involved in AES encryption are as follows: - Creates a random Initialization Vector (IV) for every message - Pads the message to the proper block size - Encrypts the message using AES-256 in CBC mode - Combines the IV with the ciphertext and encodes to base64 for transmission

Your communication is more securely protected with this dual-layer method.

## Usage

### Running the Server and Client Together

To run both the server and client:

```
make run
```

This will start the server in the background and launch the client.

### Running the Server Only

```
make run-server
```

### Running the Client Only

```
make run-client
```

### Command Line Arguments

Both the server and client accept the following command line arguments:

- `--host`: Server hostname or IP address (default: 127.0.0.1)
- `--port`: Server port (default: 8443)

Example:
```
python3 server.py --host 0.0.0.0 --port 9000
python3 client.py --host example.com --port 9000
```

### Client Usage

After starting the client, you can send messages to the server:

1. Type your message and press Enter
2. Your message will be encrypted with AES-256 before transmission
3. The server will decrypt your message, process it, and send an encrypted response
4. The client will decrypt and display the server's response
5. Type 'exit' to quit the client

## Cleanup

To remove compiled files, logs, and the virtual environment:

```
make clean
```

## Security Notes

- The encryption key is hardcoded for simplicity. In a real-world application, this should be securely stored and distributed.
- Certificate verification is disabled in the client. In production, proper certificate validation should be implemented.
- The server generates self-signed certificates for SSL/TLS encryption.
