---
title: "Setting up SSH keys"
date: 2021-05-16
draft: false
tags: ["SSH", "github", "unix"]
---

## Brief explanation about SSH

Here is what [Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell) has to say
about SSH:

> "Secure Shell (SSH) is a cryptographic network protocol for operating network
  services securely over an unsecured network. Typical applications include remote
  command-line login and remote command execution, but any network service can be
  secured with SSH."

In simple terms, Secure Shell or SSH is a network protocol that allows users to
control and modify remote servers over the internet

## Setting up SSH keys

Since SSH is encrypted, we are required to use a password or set up key pairs
in order to use it. Although using passwords can seem convinient at first, they
are no where as secure as key pairs when it comes to security. It is highly
recommended that you use key pairs to login to your SSH server or in this case
your remote repository server.

I'm assuming you are on a unix machine like all sane developers.

- First, check if you already have an existing ssh key pair:

    ```sh
    ls -l ~/.ssh/
    ```

    If a message appears in the console containing the text “No such file or
    directory”, then you do not yet have an SSH key, and you will need to create
    one. If no message has appeared in the console output, you already have a
    key and can skip this section.

- Generate an ssh key pair if you don't have one already, and follow with the rest of the process:

    ```sh
    ssh-keygen -C <email address>
    ```

    The `C` flag is just to add a comment (in this case your email address or
    hostname for that matter) so that you get to add a comment to help you
    remember the key. Although you can add anything as a comment, it is
    generally a convention to add either your your email address or hostname as
    your comment.

    You may additionally get prompted for a location to save your generated
    keypair.  Default is fine. So just press `Enter`.

    It will also ask for a password. Enter one if you wish, but it’s not
    required.

## Adding them to your remote repository of choice

Go to your remote repository of choice, and add the SSH keypair. For instance, I
will be showing how to add one on GitHub.

### On GitHub

Login to your github account and go to `settings` in the top right corner. Next
on the left hand side, click `SSH and GPG keys`. Then, click the green button in
the top right corner that says `New SSH Key`. Name your key something that is
descriptive enough for you to remember where it came from. Leave this window
open while you do the next steps.

Now you need to copy your public SSH key. To do this, we’re going to use a
command called cat to read the file to the console. (Note that the .pub file
extension is important in this case.)

```sh
cat ~/.ssh/id_*.pub
```

Highlight and copy the output, which starts with `ssh-` and ends with your
saved comment from earlier, which in this case should be your email address.

Now, go back to GitHub in your browser window and paste the key you copied into
the key field. Then, click `Add SSH key`. You’re done! You’ve successfully added
your SSH key!

## Testing your ssh keys

When you test your connection, you'll need to authenticate this action using
your password, which is the SSH key passphrase you created earlier. For more
information on working with SSH key passphrases, see "[Working with SSH key
passphrases](https://docs.github.com/en/articles/working-with-ssh-key-passphrases)".

- Enter the following on a terminal:

    ```sh
        ssh -T git@github.com
        # attempts to ssh onto github
    ```

    You may see a warning like this:

    ```custom
        > The authenticity of host 'github.com (IP ADDRESS)' can't be established.
        > RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
        > Are you sure you want to continue connecting (yes/no)?
    ```

- Verify the fingerprint in the message you see matches [GitHub's RSA public key
  fingerprint](https://docs.github.com/en/github/authenticating-to-github/githubs-ssh-key-fingerprints).
  If it does, then type `yes`:

    ```custom
        > Hi username! You've successfully authenticated, but GitHub does not
        > provide shell access.
    ```

    You might see this error message:

    ```custom
        ...
        Agent admitted failure to sign using the key.
        debug1: No more authentication methods to try.
        Permission denied (publickey).
    ```

    This is a known problem with certain Linux distributions. For more
    information, see "[Error: Agent admitted failure to
    sign](https://docs.github.com/en/articles/error-agent-admitted-failure-to-sign)".

- Verify that the resulting message contains your username. If you receive a
"permission denied" message, see "[Error: Permission denied
(publickey)](https://docs.github.com/en/articles/error-permission-denied-publickey)".

## Conclusion

So there you have it. You just generated an `SSH key pair` and added it to a
remote repository (like GitHub in this case) of your choice. Now every time you
push or pull code to your remote repository make sure you are doing so over the
`SSH` protocol and not the `HTTPS` protocol.
