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

### 2. 