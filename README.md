# SHELL

🔐 SSH (Secure Shell)
🎯 Objectives

    Learn SSH basics and functionality

    Understand key authentication

    Use SSH for remote commands and file transfers

🔧 What is SSH?

    Protocol for secure remote terminal access and file transfer

    Also supports SSH tunnels and SFTP

    Default port: 22

    SSH servers usually preinstalled on Linux

🔐 Symmetric vs. Asymmetric Encryption

Symmetric:

    One key encrypts/decrypts (shared secret)

    SSH uses a new session key per connection (e.g. AES, Blowfish)

Asymmetric:

    Public key encrypts, private key decrypts

    Used only during session setup

    Ex: Diffie-Hellman, Elliptic Curve

🧩 SSH Connection Steps

    TCP handshake

    Server offers encryption/auth keys

    Client verifies public key (via known_hosts)

    Asymmetric encryption establishes session

    Switches to symmetric encryption for speed

🖥️ OpenSSH Server

    Default on Debian

    Config file: /etc/ssh/sshd_config

    Service name: sshd

Tips:

    Disable root login remotely

    Disable weak ciphers

    Force SFTP shell if needed

🗂️ SSH Key Storage

    ~/.ssh/known_hosts: stores verified public keys

    Changing a key? Remove the old line to reconnect

    Always verify new keys securely

💻 Opening a Remote Shell

ssh [user@]host [command]

Examples:

ssh php.scweb.ca
ssh root@php.scweb.ca
ssh -C root@php.scweb.ca       # Enable compression
ssh -p 50022 server.com        # Custom port

📁 File Transfers (SCP & SFTP)

SCP:

scp file user@host:/path/     # Copy to remote
scp user@host:/file /local/   # Copy from remote

SFTP:

sftp user@host
Commands: put, get, ls, lls, cd, lcd, mkdir, lmkdir, exit

⚙️ Scripting SSH/SFTP

By default, SSH requires manual password entry, making scripting tricky.

Options:

    ❌ sshpass (not secure)

    ✅ SSH Key Authentication (recommended)

🔑 sshpass (Not Recommended)

sshpass -p"password" ssh user@host
sshpass -f"pass.txt" sftp user@host

Used when SSH keys are not an option. Avoid if possible.
🔑 SSH Key Authentication

    Public keys go in: ~/.ssh/authorized_keys

    Use ssh-copy-id to send your key to a server

    Avoid passphrases for automation (but use them for security)

Key Generation:

ssh-keygen                     # Default prompts
ssh-keygen -t rsa -b 4096 -C "your@email.com"

Send Key to Server:

ssh-copy-id user@host

🗃️ Multiple SSH Keys

Configure in ~/.ssh/config:

Host server1
  Hostname server1.com
  IdentityFile ~/.ssh/id_rsa
  User root

🔄 SSH Tunnels

Local Proxy via SOCKS:

ssh -D 2001 root@server.com    # Proxy on localhost:2001

Forward Remote RDP:

ssh -L 54000:10.13.37.2:3389 root@server.com

Reverse Tunnel:

ssh -R 54000:172.16.2.4:3389 root@server.com
