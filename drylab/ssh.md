@def title="Setting up SSH"

# Setting up SSH access

SSH (**S**ecure **SH**ell) is a protocol for sending
information securely over the internet.
For our purposes, it enables us to send files
and even commands for interacting with software
on remote computers.
This way, you can have a terminal open on your laptop
that has all the power of the lab servers.

This page will help you set up _authentication_
with a lab server.
We don't want just anyone to log in,
so we are using a method of authentication
using "key pair encryption."
Don't worry - you don't need to know what that means
in order to use it effectively.


## Users

If you need to access [lab servers](/drylab/computers) remotely,
you'll need to:

1. Have a user account set up on the server that you need access to.
2. Create an ssh key pair on your local computer (eg your laptop)
3. Have an administrator (eg Kevin) add your public key as an authorized key for your user
4. Set up your computer to use that key when attempting to connect to the lab server

Let's get started!

### 1. User account set up

For this, you'll need a server administrator (eg Kevin or Shelley)
to set up a user account for you on the remote server.

[Open an issue](https://github.com/Klepac-Ceraj-Lab/klepac-ceraj-lab.github.io/issues/new?assignees=kescobo&labels=admin&template=new-user.md&title=%5BNEW+USER%5D+your-name-here)
with the "new user" template.

Add your name to the issue title, eg `[NEW USER] Jane Doe`

Fill out the information requested:

- **Name**: Your name, eg "Jane Doe"
- **Wellesley email**: the user associated with your @wellesley.edu email, eg "jdoe123"
- **Requested username**: Typically your first name, or first initial and last name, all lowercase. Eg "jane"
- **Server(s) you need access to**: Put an `x` between the brackets (and remove the space) for the server(s)
  you need access to. For example, if you need access to `ada` and `rosalind`, it should look like this:

```
- [x] `ada`
- [ ] `hopper`
- [x] `rosalind`
```

- **Public Key** (see below)

### 2. Create SSH key pair

On your local laptop, create a directory in your home folder 
(if it doesn't already exist) called `.ssh/`,
and then change it to be your working directory.

```sh
$ mkdir ~/.ssh/
$ cd ~/.ssh
```

Now, run the `ssh-keygen` command to make a new key pair
for each server you need access to.
If you just run `ssh-keygen` with no arguments,
it will prompt you for a file location and a password.
Or you can enter them as arguments,
the `-f` argument to specify location, and `-N` to specify password.

```sh
$ ssh-keygen -f ada-key -N "Z4utPR9ij#4Go&"
Generating public/private rsa key pair.
Your identification has been saved in foo-key
Your public key has been saved in foo-key.pub
The key fingerprint is:
SHA256:iPHKUK1CnlyabTv9ceVE8H71NStHcNU5BRgIBntDsF4 kevin@gazelle
The key's randomart image is:
+---[RSA 3072]----+
|      oo+....+.oB|
|     . =  .o. oo.|
|  . + + E   o  o+|
| + B * + . o  ..=|
|  O = + S   +..o.|
|   = +     + .o  |
|    = . . . .    |
|     . . o       |
|        .        |
+----[SHA256]-----+
```

If you look in your directory, you should now see 2 files,
one with the file name you specified    
(I recommend `<servername>-key`, eg `ada-key` or `hopper-key`)
and one with the same name and the `.pub` extension.
The first is your *private* key, and the other is your *public* key.

**Do not share your private key**

Add the contents of your public key in the github issue you started above.
You can see the contents of the public key using `cat`:
eg:

```sh
$ cat ada-key.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDCCS+GHc79dd561BwJ4UHyQqDhNKTy4gvgjQB2WF4v0X4kePuTLbB5yDdbmb2Xo20bqqgjVY8k6Sgx/VT89XiBS3acoPqPYEgakRYysx4T2ARg+rVdnSH7J9YFywbYPvU9k/KTrBCwt1s1q1KM3YfmHpOuFyvydfZoT09J4wd6JXcXe9bfHJmbPK6dpoPCZhC7VgbIzP6ulQTj6d5UUpjwpodwRUXAOPMfb3AzmVXzvcJBtoROMtoCV5977Sh3l6X7gbvg61A8TJrptMV1XJzYmLKk7RMy9Md/KfkB7uNCihq6NVYqR8r47fgws70QxyStCod33JC5RXMq8fSi9fmMxPZqn804vgmKqb+lIWoaiRhYK/qcfkjTFzH/XWHnAGLhy63G6T1eDDp2Vn6zuhhPoViCQaQ0Ep84+pYkixjbDqs6WpMSucY8xrSBTSrZ9E/mKd2hwovjYQPxQg3R6J+Tg6Q+oKhkCGzQSa9YgeqxlHIqMcmEdUZwZclhvikRUhM= kevin@gazelle
```

**WARNING**: If you see a much longer output that begins with `-----BEGIN OPENSSH PRIVATE KEY-----`, *Do Not* share that - it's your private key. Keep it private!

If you need access to multiple servers,
repeat the process above to generate a new key
for each server you need access to.

### 3. Adding your public key as an authorized user

Once you have added the information above to a New User Request issue,
Kevin or Shelley will create a user account on the lab server(s),
and add your public keys to the list of authorized keys.

### 4. Set up your SSH configuration

Now it's time to set up a configuration file
so that when you use `ssh` commands, your system will know what to do.

The basic setup is:

```
Host <name>
    HostName <url or ip address>
    User <username>
    IdentityFile <path to private key>
```

- `<name>`: This can be whatever you like - this is the name you will use to connect
- `<url or ip address>`: address for the system you're connecting to.
  Info for lab systems [can be found here](/drylab/computers).
- `<username>`: user name from step 1
- `<path to private key>`: eg `~/.ssh/ada-key`

You can have separate entries for each system
that you need to connect to.
For example, this is just part of Kevin's `~/.ssh/config`:

```plaintext
Host ada
    HostName 149.130.201.24
    User kevin
    IdentityFile /home/kevin/.ssh/ada-key
Host hopper
    HostName vkclab-hopper.wellesley.edu
    User kevin
    IdentityFile /home/kevin/.ssh/hopper-key
Host github.com
    User git
    IdentityFile /home/kevin/.ssh/github-key
Host gitlab.com
    User git
    IdentityFile /home/kevin/.ssh/gitlab-key
Host rosalind
    HostName 149.130.162.151
    User kevin
    IdentityFile /home/kevin/.ssh/rosalind-key
```

Once complete, you should be able to do eg `ssh ada`
to connect.