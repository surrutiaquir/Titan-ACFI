## Automatic Login

Logging into our local machine first and then Titan from there can get annoying after a little while with all the typing. In order to simplify the process somewhat, you can setup an automatic logins. To do this, open a terminal on your local machine and cd into your  **~/.ssh**  folder. Here, you can create a public/private rsa key pair by typing

```console
$ cd ~/.ssh
$ ssh-keygen -t rsa
```


It will then give you the prompt:  _Enter file in which to save the key_. We recommend choosing a convenient filename here, such as  **id_rsa_umass**. You’ll then be prompted for a passphrase. Just press enter without writing anything (no passphrase is assigned). This isn’t needed as long as you’re careful with your own local machine and it also allows you to call ssh from within a shell script. If this was successful, you should see something resembling the following:

```console
Seba-Macbook:.ssh surrutiaquir$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/surrutiaquir/.ssh/id_rsa): id_rsa_umass
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_rsa_umass.
Your public key has been saved in id_rsa_umass.pub.
The key fingerprint is:
SHA256:6MVM6lZmNfAiHQ0hYKW18DI+aPfnG/9qs5Asc2UfZKc surrutiaquir@Seba-Macbook
The key's randomart image is:
+---[RSA 3072]----+
|  +o+ =+ |
| . = + +.  |
|  + + + + o .  |
| o o B o + o |
|  o + o S o E  |
| . . = * + . . |
|  B B .  |
| . * +o  |
|  oo+=.  |
+----[SHA256]-----+
```

This process will create two files,  **id_rsa_umass**  and  **id_rsa_umass.pub**. While still in the  **~/.ssh**  folder, open the **config** file with your favorite text editor (if no **config** file exists yet, just create it: `touch config`) and write the following lines at the end of it

```console
Host titan-acfi
        User titan
        Hostname 128.119.50.175
        IdentityFile ~/.ssh/id_rsa_umass
        ServerAliveInterval 100
```

and save and close it. You now need to copy the public key to the remote host. To do this, type

```console
$ cat ~/.ssh/id_rsa_umass.pub | ssh titan@128.119.50.175 'cat >> .ssh/authorized_keys'
```

using the password when prompted. We can now further simplify the step into Titan by adding the following lines to the  **config**  file in the  **~/.ssh**  folder

```console
Host username
        User username
        Hostname titan.physics.umass.edu
```

with  **username**  replaced with your chosen Titan username.

If you now start a new terminal on your local machine, you should be able to simply type

```console
$ ssh titan-acfi
```

to get into our local machine without a password from your computer. Once there, you should be to type

```console
$ ssh username
```

to log into Titan, after you insert your Titan password when prompted.

**Note:**  _it’s possible to repeat the procedure to log into Titan without a password as well. However, in the interest of security, We’d recommend against this._


> Written with [StackEdit](https://stackedit.io/).
