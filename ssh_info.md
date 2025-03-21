# SSH

## Table of content

- [1. Basic principles](#1-basic-principles)
- [2. Setting up your Keys](#2-setting-up-your-keys)
- [3. Useful Links](#3-useful-links)


## 1.Basic principles

**SSH** (Secure Shell Protocol) allows for secure access and communication to a computer over an unsecure network, like the Internet. You can imagine it like a encrypted channel, which protects from evesdropping or third parties.
It has a broad range of applications, like
1. Data transfer and tunneling traffic
2. Remote administration of servers
3. Access to remote files
4. Safe creation of Backups




SSH uses the idea of **asymmetric cryptography** and a **keypair**. 
The **keypair** consists of two keys, the **public key** and the **private key**. The public key can be viewed by everybody and for the usecase with Github, is on your Github profile, where everybody can see it. The private key, however, must be held secretive.

![work_ssh_image](https://cdn.prod.website-files.com/5ff66329429d880392f6cba2/6798c653a6f92c868e7ea53b_61c1b963247368113bbeef17_Secure%2520Shell%2520work.png)

### Authentification Process
when initiating a SSH connection there are always two parties, the server (for example GitHub) and the client (your local machine)

- Step 1: The server checks if the client has the public key
- Step 2: The server sends a encrypted message to the client, which can be solved with the private key
- Step 3: The server checks verifies the client's response with the public key
- Step 4: If everything checked, a SSH-Session will be started




## 2.Setting up your Keys


### Creating the keypair
First you need to set up a pair of keys. You can do this with the 'keygen' command.

`ssh-keygen -t ed25519 -C "your_email@example.com"`

- The ed25519-algorithm used in SSH key generation is used for asymmetric encryption and authentication in secure communications. Alternatively a rsa algorithm exists

Usually the computer asks you where to store your keys and if you want to enter an additional passphrase. You can enter a passphrase if you like, but it's not necessary. It is an extra layer of security.

This step creates two files:

- **id_ed25519 (private key – keep it secret!)**

- **id_ed25519.pub (public key)**

You can now copy the public key to your Github profile
Simply go to `Settings > SSH and GPG Keys > New SSH key`

### Adding Keypair to the SSH-Agent
First we need to start the SSH-Agent.
`eval "$(ssh-agent -s)"` 

To add your key, simply type `ssh-add ~/.ssh/id_ed25519`.
**Note: You have to add your private key to the SSH-Agent**

### Testing if everything worked
You can check with the command `ssh -T git@github.com`, if everything worked.
If your keys were successfully added, a welcome message will appear on the command line

### Using the keys
You can set SSH now as the default for certain repositories by typing
`git remote set-url origin git@github.com:username/repository.git`.
**Note that you need git@github.com and not the https:// address**

Now you should be able to push and pull from Github with SSH.


## 3.Useful Links
- https://www.youtube.com/watch?v=P0Fk-K2eZF8
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://www.techtarget.com/searchsecurity/definition/Secure-Shell
- https://www.youtube.com/watch?v=GSIDS_lvRv4


