# <span style="font-family:Papyrus; font-size:2em;">sshort</span> - SSH shorcut

 **Description**: **ssh** sh**ort**cut to speed up the connection to remote machines using SSH in Linux. The script uses a encrypted file with a master password to store credentials of all sessions.

 **Dependencies**: openSSH, sshpass, whiptail (newt), gpg (GnuPG)


## Table of Contents
 - [Deployment](#deployment)
 - [Usage](#usage)
 - [Important notes](#important-notes)

## Deployment

### Install the script
1. Install Dependencies
2. git clone https://github.com/UnaiRuiz/sshort.git
3. Add exec permission to the script 
```
chmod +x sshort
```
### Add script to PATH:
1. create your own `bin` directory:
```
cd ~/
mkdir bin
```
2. Add your new dir to PATH:

  * Using ZSH:

Open .zshrc to modify it:
```
nano ~/.zshrc
```
Uncomment next line:
```
export PATH=$HOME/bin:/usr/local/bin:$PATH
```
Reload file:
```
source ~/.zshrc
```
  * Using Bash:

Open .bashrc to modify it:
```
nano ~/.bashrc
```
Add next line:
```
export PATH=~/bin:.:$PATH
```
Reload file:
```
source ~/.bashrc
```
3. Add sshort to `bin`:

* As a symbolic link (recommended for source control): 
```
cd ~/bin
ln -s </path/to/cloned/sshort> sshort
```
* Move the script:
```
mv </path/to/cloned/sshort> ~/bin/sshort
```
## Usage
### Create your own encrypted file
1. Create and open your own hosts file:
```
nano <decryptedfile>
```
2. Add one session per line following the next structure:
```
#id session category host port auth_method(password|key) username password ssh_key
1 examplesession test 10.10.10.10 22 password foo bar None
```
3. Encrypt the file using GnuPG using symmetric cipher:
```
gpg --batch --quiet --yes --passphrase <masterpassword> -c <decryptedfile>
rm <filename> 
```
### [Optional] Add encrypted file to the script
1. Open sshort:
```
nano sshort
```
2. Modify following lines:
```
# ======= Config Parameters ======
decryptedfile=</path/to/decryptedfile>
encryptedfile=</path/to/encryptedfile>
# ================================
```

## Important Notes:
- The name of a session must not contain the name of a category to which it does not belong.
- The name of a session must not contain the name of another.
- Preferably the name of a category should not contain the name of another.
- First line of the hosts file is ignored. Use it as a header.
