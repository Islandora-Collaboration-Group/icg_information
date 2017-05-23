# Documentation: Help with Ansible

## Table of Contents

* Glossary
* Important: Recommended Order of Installation
* Install Ansible on PC (requires Windows 10 Ubuntu bash) or Mac
* Ansible Components
* Ansible Commands
* Ansible Host_vars
* More Great Help Documentation

## [* Glossary](https://www.virtualbox.org/wiki/Documentation)

* **Ansible** - Ansible is a free-software platform seamlessly unites workflow orchestration with configuration management, provisioning, and application deployment in one easy-to-use and deploy platform. It combines multi-node software deployment, ad hoc task execution, and configuration management. It manages nodes over SSH or over PowerShell. Modules work over JSON and standard output and can be written in any programming language. The system uses YAML to express reusable descriptions of systems.

* * *


## Important: Recommended Order of Installation

1. Install git

2. Install virtualbox

3. Install vagrant

4. Install ansible

* * *


## Install Ansible on PC (requires [Windows 10 Ubuntu bash](http://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)) or Mac

Download: [http://docs.ansible.com/ansible/intro_installation.html](http://docs.ansible.com/ansible/intro_installation.html) 

**Stay updated by installing the newest release**

* * *


## Ansible Components

* Plays - Ansible steps or actions 

    * Roles (they organize the tasks)

    * Tasks (the steps or actions defined for a specific package or series of commands)

    * Files (files to be copied from the host (laptop) to the guest (Vagrant box, remote server etc.)

    * Templates (files that can have defined variables thus "templated")

    * Defaults (group and host_vars for Playbooks) used to be known as vars (local to role)

    * Handlers (timed actions or dependent on other roles finishing prior to execution)

* Playbooks - Contain the commands that configure the targets. (written in YML)

* Inventory - List of managed hosts (servers, VMs). Can be formed in to groups

* ansible.cfg - How Ansible itself is configured

* Modules -Ansible ships with a number of modules that can be executed directly on remote hosts or through Playbooks

* * *


## Ansible Commands

* Ad-hoc commands - An ad-hoc command is to do something really quick, but don’t want to save for later. Often used with tags

    * ansible-playbook -i inventory playbook.yml --tags"mysql” (run a specific role)

    * ansible webservers -m git -a "repo=git://foo.example.org/repo.git dest=/srv/myapp version=HEAD" (deploy code)

    * ansible webservers -m ping (ping all web servers)

    * ansible webservers -m service -a "name=httpd state=started" (Ensure a service is stopped)

* Playbooks ansible-playbook -i inventory playbook.yml

    * Playbooks can declare configurations but they can also orchestrate steps of any manual ordered process, even as different steps must bounce back and forth between sets of machines in particular orders. They can launch tasks synchronously or asynchronously..

* * *


## Ansible Host_vars

Since the documentation is not very specific on this topic here is the order of precedence for vars in the current version of Ansible:

1. Vars set on the command line -e foo=set_on_cmd_line

2. Vars set in the vars_files: block in the play

3. Vars set in the vars: block in the play

4. Vars set in host_vars/

5. Vars set in group_vars/

Role default vars roles/.../defaults/main.yml

You should think of host_vars and group_vars more like defaults rather than overrides for defaults. If you have the same var set in you vars_files: block like you do in your example it will take precedence.

* * *


## More Great Help Documentation

1. [Ansible Getting Started](https://www.ansible.com/get-started)

2. [Ansible Docs](https://docs.ansible.com/)

3. [Ansible Intro to Playbooks](http://docs.ansible.com/ansible/playbooks_intro.html)

4. [Ansible Galaxy (For Ansible Scripts)](https://galaxy.ansible.com/)

5. [Ansible Best Practices](http://docs.ansible.com/ansible/playbooks_best_practices.html)

6. [Intro to Ansible](http://docs.ansible.com/ansible/intro.html)

