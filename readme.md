# ECDSA Node

This project demonstrates a basic application of Public Key Cryptography using Elliptic Curve Digital Signatures (ECDSA). It consists of a client-server architecture where the server facilitates transfers between different addresses. Note that this is a centralized system with a single server handling all transfers.

## Table of Contents

- [Warning](#warning)
- [Project Structure](#project-structure)
- [Technical Overview](#technical-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Demo](#demo)
- [Contributing](#contributing)
- [License](#license)

## Warning

This project is a simple exercise and includes known security vulnerabilities, such as:

- The client requests your public key.
- The server stores account public keys.
- Transactions lack a nonce, allowing intercepted transaction signatures to be reused until the wallet is drained.

## Project Structure

The project is divided into two main parts:

- **Client**: A React application using Vite.
- **Server**: A Node.js server using Express.

## Technical Overview

### Cryptography

- **Elliptic Curve Digital Signature Algorithm (ECDSA)**: This project uses ECDSA for signing transactions. ECDSA is a cryptographic algorithm used by many cryptocurrencies to ensure that funds can only be spent by their rightful owners. It involves generating a pair of keys: a private key for signing transactions and a public key for verifying them.

- **Key Generation**: The `generate.js` script in the server's `scripts` folder is used to generate new Private Key - Public Key/Address pairs. These keys are crucial for signing and verifying transactions. The script uses elliptic curve cryptography libraries to create secure keys.

### Client-Server Interaction

- **Client**: The client is built using React and Vite, providing a user interface for interacting with the server. It allows users to initiate transactions by signing them with their private keys. The client sends the signed transaction to the server for processing.

- **Server**: The server is built using Node.js and Express. It handles transaction requests, verifies signatures using the public keys, and updates balances accordingly. The server maintains a simple in-memory database of balances and public keys.

### Transaction Flow

1. **Key Pair Generation**: Users generate a key pair using the `generate.js` script. The public key is shared with the server, while the private key is kept secret. This ensures that only the owner of the private key can sign transactions.

2. **Transaction Creation**: The client creates a transaction, which includes the sender's address, receiver's address, and the amount to be transferred. The transaction is then signed with the user's private key to ensure authenticity.

3. **Signature Verification**: The server receives the signed transaction and verifies the signature using the sender's public key. This step ensures that the transaction was indeed authorized by the owner of the funds.

4. **Balance Update**: If the signature is valid, the server updates the balances of the sender and receiver. The sender's balance is decreased by the transaction amount, and the receiver's balance is increased by the same amount.

## Installation

### Client

1. Navigate to the `/client` directory.
2. Run `npm install` to install all dependencies.
3. Run `npm run dev` to start the application.
4. Access the app at [http://127.0.0.1:5173/](http://127.0.0.1:5173/).

### Server

1. Navigate to the `/server` directory.
2. Run `npm install` to install all dependencies.
3. Run `npx node index` to start the server.
4. The server will connect to the default port 3042.

## Usage

### Generating Key Pairs

The server includes a `scripts` subfolder with a `generate.js` file. Run this script to create new Private Key - Public Key/Address pairs. These pairs, along with their currency amounts, must be manually added to the `balances` and `privateKeys` objects in `index.js`.

### Running the Application

1. Start the server as described in the installation section.
2. Start the client application.
3. Use the client interface to perform transactions between addresses.

## Demo

![Demo](./client/public/demo.gif)

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add some feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Open a pull request.

## License

This project is licensed under the ISC License. See the [LICENSE](LICENSE) file for details.