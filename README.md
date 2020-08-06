# Instructions for macOS

## If you're pairing with me:

1. Send me your public ssh key.
2. Run `ssh pair-with-me@0.tcp.ngrok.io -p {port-number-i-give-you}`

## If you want to do this yourself:

Get your software:
- brew install tmux
- brew install wemux
- brew cask install ngrok

Create user account for pair:
- apple -> System Preferences -> Users and Groups -> (unlock) -> +.
- Create a standard account with username e.g. `pair-with-me`, you won't give out the
  password.

You may need to restart at this point.

Enable remote login for pair account:
- apple -> System Preferences -> Sharing -> (tick) Remote Login
- Enable it for 'only these users' and list your pair account

Add some files to pair's home dir:
- sudo mkdir /Users/pair-with-me/.ssh
- sudo touch /Users/pair-with-me/.ssh/authorized_keys
- sudo chmod 600 /Users/pair-with-me/.ssh/authorized_keys
- sudo chmod 700 /Users/pair-with-me/.ssh/authorized_keys
- sudo chown busbud-pair /Users/pair-with-me/.ssh
- sudo chown busbud-pair /Users/pair-with-me/.ssh/authorized_keys
- sudo touch /Users/pair-with-me/.zshrc

Add the public keys of any pairs to authorized_keys
Add `wemux mirror|pair|rogue; exit` to the .zshrc.

Disable access via anything except public key:
- sudo vim /etc/ssh/sshd_config

Ensure following settings are correct:
```
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
```

Expose your local ssh agent:
- ngrok tcp 22

Your pairs can connect with this command:
- ssh pair-with-me@0.tcp.ngrok.io -p {port-number-from-ngrok}


Main reference: http://martinbrochhaus.com/pair.html
