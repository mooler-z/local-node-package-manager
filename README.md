# Local Network NPM Installer

In environments without internet access, this setup allows you to share and install NPM packages from one machine over a local network. This is especially useful when multiple users are working on a Node.js project and need access to the same dependencies without direct access to npm’s online registry.

## Overview

This project provides two scripts to make NPM packages available over a local network:
1. **npm_server.py**: Hosts the `node_modules` directory, allowing other devices on the network to access it.
2. **client.py**: Downloads packages from the host machine and installs them on the client machine.

> The setup heavily relies on recursion for fetching dependencies, making it efficient for mirroring complex package structures.

## Setup Instructions

### 1. Setting up the Host Machine

On the machine with the `node_modules` directory:
1. Ensure `http-server` is installed to serve files over HTTP:
   ```bash
   npm install -g http-server
   ```
2. Start the HTTP server in the directory containing `node_modules`:
   ```bash
   http-server ./node_modules
   ```
   This will serve `node_modules` over HTTP, making it accessible to other machines on the local network.

3. Run the `npm_server.py` script to set up the environment:
   ```bash
   python3 npm_server.py
   ```
   
4. Note the IP address of this machine for clients to connect to.

### 2. Setting up the Client Machine

On any client machine needing access to the packages:
1. Run the `client.py` script, providing the host IP address when prompted:
   ```bash
   python3 client.py
   ```
2. The script will automatically fetch and install packages from the host machine’s `node_modules` folder.

### Notes
- Make sure both machines are on the same network.
- `client.py` script handles dependencies recursively, ensuring a complete installation even for complex projects.

## How It Works

1. **Host Machine**: Shares the `node_modules` directory over HTTP, making packages available on the network.
2. **Client Machine**: Connects to the host, downloads required packages recursively, and installs them locally.

This setup provides a quick, easy way to manage NPM dependencies in an offline or restricted environment.