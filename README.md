# What is SSH ? 

SSh stands for Secure Socket Shell and It's a protocol that allow two devices to communicate in a secure way. 
It uses 3 techniques to achieve that:

* Symmetrical Encryption
* Asymmetrical Encryption
* Hashing

Symmetrical encryption uses one secret Key :key: for encryption and decryption by both parts. 
The problem is that anyone who has the key can access to the message or to the communication. 

To solve that, this protocol uses what they call Key Exchange algorithm. Basically, that key :key: is never transfered instead the 
two computers share public pieces of data (a public key) and then manipulate it (with a private key) to independently calculate the Secret key :key:. That secret key is
specific to each SSH session and is generated prior to authentication, that process actually uses Asymmetrical
encryption.

In order to verify the authenticity of the message, in other words to check that It hasn´t been altered, the protocol uses another form of cryptography called Hashing.


# How to connect SSH key with our device 

1) Open Git bash 
2) All our keys (private and public) are saved inside a .ssh folder in our user root folder, to check what keys we saved already

```bash
ls -al ~/.ssh 
```
3) To generate the keys
```bash
  ssh-keygen -t rsa -b 4096 -C "your email" 
```
**-t** is the cryptographic algorithm. 

**-b** is the byte size of key

**-C** is comment 

4) Start SSH agent (I read that we could think of it as a wallet to save our keys)

```bash
  eval "$(ssh-agent -s)"
```
5) Add private key to the Agent
```bash
  ssh-add ~/.ssh/id_rsa
```
6) Copy the public key. We can do it using the following command or straight forward opening the file.
```bash
  Clip < ­~/.ssh/id_rsa_pub 
```
7) In our github, go to settings -> SSH and GPG keys 
![Step 1](https://github.com/gomezlucas/Ssh-github/blob/main/images/1.png)
![Step 2](https://github.com/gomezlucas/Ssh-github/blob/main/images/2.png)

8) Click on **New SSH Key button**
![Step 3](https://github.com/gomezlucas/Ssh-github/blob/main/images/3.png)

9) Complete the Title field and paste the public key copied in the 6th step. Add new Key.
![Step 4](https://github.com/gomezlucas/Ssh-github/blob/main/images/4.png)

10) In Git bash, test the connection 
```bash
   ssh -T git@github.com
```
If it shows a message saying *The user has been authenticated*, the process was succesful. Now we can clone a Repo from any terminal in our computer

# Extra info

```bash
  ~/ is shorthand for the current user's home folder.
  ~  = Alt + 126 
  @  = Alt + 64 
```

# Resources: 
- https://stackoverflow.com/questions/52113738/starting-ssh-agent-on-windows-10-fails-unable-to-start-ssh-agent-service-erro
- https://www.techtarget.com/searchsecurity/definition/Secure-Shell
- https://7sabores.com/blog/usar-multiples-llaves-ssh-git
- https://askubuntu.com/questions/85149/what-does-mean
- https://github.com/antonykidis/Setup-ssh-for-github

 
## :rotating_light:	Never share your private key! 


