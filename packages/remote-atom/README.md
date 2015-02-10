# remote-atom

Remote Atom is a package for Atom which implement the Textmate's 'rmate'
feature for Atom. It transfers files to be edited from remote server using SSH
port forward and transfers the files back when they are saved.

# Installation
Remote Atom can be easily installed using the Atom package manager. On the
remote server, we need to install [rmate](https://github.com/aurora/rmate). It
is the same executable for TextMate and Sublime Text. You don't have to
install it if your Textmate/Sublime Text alternatives are working. If not, it
can be install by running this script (assume that you have the permission),

```bash
curl -o /usr/local/bin/rmate https://raw.githubusercontent.com/aurora/rmate/master/rmate
sudo chmod +x /usr/local/bin/rmate
```

You can also rename the command to `ratom`

```
mv /usr/local/bin/rmate /usr/local/bin/ratom
```

# Usage

Open your Atom application, go to the menu `Packages -> Remote Atom`,
and click `Start Server`. Your can also launch the server via command palette.
The server can also be configured to be launched at startup in the preference.

Then, open an ssh connection to the remote server with remote port forwarded.
It can be done by

```bash
ssh -R 52698:localhost:52698 user@example.com
```

After running the server, you can just open the file on the remote system by

```
rmate test.txt
```

If everything has been setup correctly, your should be able to see the opening file in Atom.

### SSH config
It could be tedious to type `-R 52698:localhost:52698` everytime you ssh. To make your
life easier, add the following to `~/.ssh/config`,

```
Host example.com
    RemoteForward 52698 localhost:52698
    User user
```

From now on, you only have to do `ssh example.com`.

### Known issues
Since each window of Atom is a separate instance, the tcp server can only be running
on one window. Therefore, file will only be opened in the window with the server running.
If that window is closed, the server can be restarted by clicking
`Packages -> Remote Atom -> Start Server`.


# TODO
- writing tests