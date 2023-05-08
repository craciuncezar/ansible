# Ansible

## TLDR;

Having to setup a new laptop is definitely not my favorite thing to do, so I took some time to automate the process by using [ansible](https://www.ansible.com/). This is the place were I keep all my configs and tasks to setup a new machine (macOS). If you special one, for whatever reason want to learn how I configure my terminal/shell or my programs this is the place to be.

> This repo is obviously subject to change, so I might change apps or settings.

The command to do the magic is the following one:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/cezarcraciun/.zprofile && eval "$(/opt/homebrew/bin/brew shellenv)" && brew install ansible && sudo ansible-pull -U https://github.com/craciuncezar1996/ansible.git
```

> **Note:** I'm using [brew](https://brew.sh/) as a package manager and the ansible-pull command, this will pull the latest version of the playbook from the repository, there is no need to clone the repo, I only need to run the command.

Running the whole setup is not needed all the time, so I can also target specific tasks by using tags that match the filename inside the tasks folder. For example, if I want to setup my terminal, I can run the following command:

```sh
ansible-playbook local.yml --tags "terminal"
```

## Goals

- [x] Installs Homebrew Package Manager
- [x] Installs Ansible and start pulling the latest version of the playbook
- [x] Setup the terminal
- [x] Install node yarn and n
- [x] Setup my macOS system preferences
- [x] Setup git
- [x] Install dev and personal programs
- [ ] Pray to the Lord that everything goes well

## Testing

Buying a new computer to test this setup or reinstalling a fresh OS whenever I make a change is not feasible, who would've thought about that... so I use docker with a linux image to test my stuff on a new fresh container.

```bash
docker build . -t new-computer
docker run --rm -it -v $(pwd):/usr/local/bin new-computer bash
```

Once in the container, I can run the following command to run ansible and test the setup:

```bash
ansible-playbook local.yml
```
