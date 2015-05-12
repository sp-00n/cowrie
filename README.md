# Cowrie

Cowrie is a medium interaction SSH honeypot designed to log brute force attacks and, most importantly, the entire shell interaction performed by the attacker.

Cowrie is directly based on [Kippo](http://github.com/desaster/kippo/) by desaster.
Kippo is inspired, but not based on [Kojoney](http://kojoney.sourceforge.net/).

## Features

Some interesting features:
* Fake filesystem with the ability to add/remove files. A full fake filesystem resembling a Debian 5.0 installation is included
* Possibility of adding fake file contents so the attacker can 'cat' files such as /etc/passwd. Only minimal file contents are included
* Session logs stored in an [UML Compatible](http://user-mode-linux.sourceforge.net/)  format for easy replay with original timings
* Cowrie saves files downloaded with wget/curl or uploaded with SFTP and scp for later inspection

Additional functionality over standard kippo:

* SFTP and SCP support for file upload
* Support for SSH exec commands
* Logging of direct-tcp connection attempts (ssh proxying)
* Logging in JSON format for easy processing in log management solutions
* Many, many additional commands

## Requirements

Software required:

* An operating system (tested on Debian, CentOS, FreeBSD and Windows 7)
* Python 2.5+
* Twisted 8.0+
* PyCrypto
* pyasn1
* Zope Interface

## How to run it?

Edit cowrie.cfg to your liking and start the honeypot by running:

`./start.sh`

start.sh is a simple shell script that runs Cowrie in the background using twistd. Detailed startup options can be given by running twistd manually. For example, to run Cowrie in foreground:

`twistd -y cowrie.tac -n`

By default Cowrie listens for ssh connections on port 2222. You can change this, but do not change it to 22 as it requires root privileges. Use port forwarding instead. (More info: [MakingKippoReachable](https://github.com/desaster/kippo/wiki/Making-Kippo-Reachable)).

Files of interest:

* dl/ - files downloaded with wget are stored here
* log/cowrie.log - log/debug output
* log/cowrie.json - transaction output in JSON format
* log/tty/ - session logs
* utils/playlog.py - utility to replay session logs
* utils/createfs.py - used to create fs.pickle
* data/fs.pickle - fake filesystem
* honeyfs/ - file contents for the fake filesystem - feel free to copy a real system here

## Is it secure?

Maybe. See [FAQ](https://github.com/desaster/kippo/wiki/FAQ)

## I have some questions!

Please visit https://github.com/micheloosterhof/cowrie/issues
