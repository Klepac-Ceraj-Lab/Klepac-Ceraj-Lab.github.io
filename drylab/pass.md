@def title="Pass Password Manager"

# Setting up `pass` password manager

If you're not using a password manager,
you really should be.
And if you need a password manager for the command line,
[`pass`][^pass] is the way to go.
But it takes some setup.

## Install

The lab servers should already have `pass` installed
and available for all users.
pass` can be installed with most linux package managers
(eg `sudo apt install pass`) or on a Mac with [`Homebrew`][^brew] (`brew install pass`).

## Set up GPG keys

`Pass` will encrypt your passwords using "GNU privacy guard" (`GPG`).
This is a [key-pair based encryption][^keypair] scheme,
so the first thing you need to do is create your key pairs.
There's a handy guide on [github][^githubgpg], but I'll walk through it here.

From the command line, run `gpg --full-generate-key` and follow the prompts.
You can use the default options for just about everything,

1. Use `RSA` encryption
2. Use 3072 bits (up to 4096 is fine)
3. OK for the key to not expire, but more secure to set expiration (eg 1y)
4. Enter your name and wellesley email address (note is not required)
5. Enter a _strong password that you will remember_
   (this key will give access to all your other passwords, so make sure it's secure and don't share it)

Expanding on point 5 - this is in principle the last password you'll ever need to remember,
It needs to be **really** secure, but also easy to remember.
You can follow [this example](https://preshing.com/20110811/xkcd-password-generator/),
(that site also has a generator, but you can also make your own).

Here's an example of the command line output:

```sh
❯ gpg --full-generate-key
gpg (GnuPG) 2.2.20; Copyright (C) 2020 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: keybox '/home/kevin/.gnupg/pubring.kbx' created
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072)
Requested keysize is 3072 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Kevin Bonham
Email address: kbonham@wellesley.edu
Comment: pass key
You selected this USER-ID:
    "Kevin Bonham (pass key) <kbonham@wellesley.edu>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
```

## Initialize password store

Now that you have a GPG key pair, you can use it to encrypt your `pass` password store.
First, double check where the GPG keys are, probably in `~/.gnupg/`:

```sh
❯ gpg --list-secret-keys
/home/kevin/.gnupg/pubring.kbx
------------------------------
sec   rsa3072 2021-09-21 [SC]
      66CA3CDE333F5DC2F8D93D375402F446ABFD7FDB
uid           [ultimate] Kevin Bonham (pass key) <kbonham@wellesley.edu>
ssb   rsa3072 2021-09-21 [E]
```

What we need is that long hexedecimal number,
which we'll give to `pass init`:

```sh
❯ pass init 66CA3CDE333F5DC2F8D93D375402F446ABFD7FDB
mkdir: created directory '/home/kevin/.password-store/'
Password store initialized for 66CA3CDE333F5DC2F8D93D375402F446ABFD7FDB
```

That's it! Now you're ready to start storing passwords.

## Using `pass`

There are many examples of usage on the [`pass`][^pass] website,
but the primary uses (for me) are:

1. Storing secure passwords
2. Creating secure passwords
3. Retrieving secure passwords.

### Storing passwords

If you already have passwords that you want to store, it's pretty easy:

```sh
❯ pass insert test
Enter password for test:
Retype password for test:

❯ pass ls
Password Store
└── test
```

Here, `test` is the name of the password.
But we can make them much more informative / organized.
For example, let's say I want to store some passwords for Wellesley,
and some for personal use.

```sh
❯ pass insert wellesley/gmail
mkdir: created directory '/home/kevin/.password-store/wellesley'
Enter password for wellesley/gmail:
Retype password for wellesley/gmail:

❯ pass insert personal/gmail
mkdir: created directory '/home/kevin/.password-store/personal'
Enter password for personal/gmail:
Retype password for personal/gmail:

❯ pass insert personal/facebook
Enter password for personal/facebook:
Retype password for personal/facebook:

❯ pass ls
Password Store
├── personal
│   ├── facebook
│   └── gmail
├── test
└── wellesley
    └── gmail
```

### Generating Passwords

Using short, easy-to remember passwords, or using the same password repeatedly,
is insecure, and happily isn't necessary when you have a password manager.
`pass` will make randomly generated secure passwords for you, then store them.

```sh
❯ pass generate wellesley/other-test 20
The generated password for wellesley/other-test is:
n2~]pirsO+miQH4#Jkn?

❯ pass ls wellesley
wellesley
├── gmail
└── other-test
```

Here, the `20` at the end is the length of the password.
You can use `-n` (or `--no-symbols`) to use only letters and numbers,
and use `-c` to put the password on your clipboard instead of printing it to the screen.

### Retrieving Passwords

To get a password, simply do `pass <name of password>`.
If you forget what you've named a password,
just do `pass ls` (or even just `pass`),
optionally including a subfolder.

```
❯ pass
Password Store
├── personal
│   ├── facebook
│   └── gmail
├── test
└── wellesley
    ├── gmail
    └── other-test

❯ pass personal
personal
├── facebook
└── gmail

❯ pass personal/facebook
youshouldntusefacebook
```

Note, when I entered the last command,
a dialogue popped up that asked me to enter my **GPG key** password.
This won't happen every time,
but about once per hour or so by default (it is possible to change it).

You can also put the password directly onto your clipboard if you use `-c`.

## Conclusions

That's it! You can now use `pass` for all your password needs.
You can also use `git` to keep a version-controlled record of your passwords
and sync them (in encrypted form) to other devices,
use it on your phone etc.

You can also securely store notes and other information,
and pipe passwords to other command line tools.
Enjoy!

## References

[^pass]: https://passwordstore.org
[^brew]: https://brew.sh
[^keypair]: It's not super important to understand this, but GPG is widely used and very secure. You can read more about the methodology here: https://en.wikipedia.org/wiki/Public-key_cryptography
[^githubgpg]: https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key