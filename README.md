# Instructions for macOS

## If you're pairing with me:

1. Send me your public ssh key.
2. Run the command I give you, something like this: `ssh pair-with-me@{number}.tcp.ngrok.io -p {number}`.

## If you want to do this yourself:

Get your software:
```
brew install tmux
brew cask install ngrok

git clone git://github.com/zolrath/wemux.git /usr/local/share/wemux
ln -s /usr/local/share/wemux/wemux /usr/local/bin/wemux
cp /usr/local/share/wemux/wemux.conf.example /usr/local/etc/wemux.conf
```

To configure wemux, open `/usr/local/etc/wemux.conf` and add the line `host_list=(your_username)`

Create user account for pair:
- apple -> System Preferences -> Users and Groups -> (unlock) -> +.
- Create a standard (non-admin) account with username e.g. `pair-with-me`, you won't give out the
  password.

You may need to restart at this point.

Enable remote login for pair account:
- apple -> System Preferences -> Sharing -> (tick) Remote Login
- Enable it for 'only these users' and list your pair account

Add some files to pair's home dir:
```
sudo mkdir /Users/pair-with-me/.ssh
sudo touch /Users/pair-with-me/.ssh/authorized_keys
sudo chmod 700 /Users/pair-with-me/.ssh
sudo chmod 600 /Users/pair-with-me/.ssh/authorized_keys
sudo chown pair-with-me /Users/pair-with-me/.ssh
sudo chown pair-with-me /Users/pair-with-me/.ssh/authorized_keys
sudo touch /Users/pair-with-me/.zshrc
```

Add the public keys of any pairs to authorized_keys:

```
echo '~ssh-public-key~' | sudo tee -a /Users/pair-with-me/.ssh/authorized_keys > /dev/null
```

Add `wemux mirror|pair|rogue; exit` to the .zshrc:

```
echo 'wemux pair; exit' | sudo tee -a /Users/pair-with-me/.zshrc > /dev/null
```

Disable access via anything except public key:
```
sudo vim /etc/ssh/sshd_config
```

Ensure following settings are correct:
```
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
```

Expose your local ssh agent:
```
ngrok tcp 22
```

Your pairs can connect with this command:
```
ssh pair-with-me@{number-from-ngrok}.tcp.ngrok.io -p {port-number-from-ngrok}
```

If you want a quick way of outputting the command for your pairs, consider a script like this one: https://github.com/AlexChalk/dotfiles/blob/20a001d4b1c487cc1a6614d11ea8495ae59dd13b/bin/ngrok_ssh.


Main reference: http://martinbrochhaus.com/pair.html
