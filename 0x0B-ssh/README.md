# SSH

In this project, I became familiar connecting to and working
with servers using the SSH protocol. I worked on a server
provided by ALX.

## Tasks :page_with_curl:

* **0. Use a private key**
  * [0-use_a_private_key](./0-use_a_private_key): Bash script that uses `ssh` to connect to my
Holberton-provided server.

* **1. Create an SSH key pair**
  * [1-create_ssh_key_pair](./1-create_ssh_key_pair): Bash script that creates an RSA key pair.

* **2. Client configuration file**
  * [2-ssh_config](./2-ssh_config): SSH configuration file configured to use the private key
`~/.ssh/holberton` and to refuse authentication using a password.

* **Generating an SSH Key Pair**
* ssh-keygen -t rsa

* **Generate an SSH Key Pair with a Larger Number of Bits**
* ssh-keygen -b 4096
* **To change or remove the passphrase, simply type:**
* ssh-keygen -p
* **To find out the fingerprint of an SSH key, type:**
* ssh-keygen -l

* **Copying your Public SSH Key to a Server with SSH-Copy-ID**
* ssh-copy-id username@remote_host
* ssh username@remote_host #to login after

* **Copying your Public SSH Key to a Server Without SSH-Copy-ID**
* cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
* ssh username@remote_host #to login after

* **Copying your Public SSH Key to a Server Manually**
* cat ~/.ssh/id_rsa.pub  #to access your public key
* mkdir -p ~/.ssh  ##create directory on the remote server if not exist
* echo public_key_string >> ~/.ssh/authorized_keys #create or append the public key

* **Connecting to a Remote Server**
* ssh username@remote_host

* **login to a server with a different port**
* ssh -p port_num username@remote_host

* **If you wish to be able to connect without a password to one server from within another server,**
* ssh -A username@remote_host



* ***Server-Side Configuration Options***
* **Disabling Password Authentication**
* sudo nano /etc/ssh/sshd_config  #connect to your remote server and open the /etc/ssh/sshd_config file
* PasswordAuthentication no #uncomment and set to no
* sudo service ssh restart  #then restart the ssh service

* **Changing the Port that the SSH Daemon Runs On**
* sudo nano /etc/ssh/sshd_config
* #Port 22
  Port 4444 # to change from default 22 to 4444
* sudo service sshd restart

* **Keeping Connections Alive to Avoid Timeout**
* nano ~/.ssh/config
* Host *  #should be at the top of the page
    ServerAliveInterval 120 #sends a packet to the server every 2 min to keep the server alive
*
