Inspired from [kleiram/vagrant-symfony](https://github.com/kleiram/vagrant-symfony.git) repository.

# Vagrant environment for PHP and Symfony2

This project provides a virtual environment for PHP Symfony2 development using
[Vagrant](https://www.vagrantup.com).

## What's in the box?

When you start Vagrant, this environment will provide the following tools
that can be useful when developing for PHP Symfony2:

- Git (with aliases and script which improves terminal [see project here](https://github.com/NansPellicari/git-config))
- vim
- cURL
- Wget
- MySQL
  * Username: `root`
  * Password: empty
- SQLite
- mongodb
- nginx
- PHP
- PHP-FPM
- APC
- PEAR
- XDebug
- RabbitMQ
- Memcached
- ruby & gem
- nodejs
- frontend tools (grunt, grunt-cli, bower, sass)
- capistrano
- symfony (aliases and [console completion](https://github.com/jaytaph/SFConsole) )

Additionally, it will create a MySQL database called `symfony` that a Symfony2
application can connect to without any configuration.

## Usage and requirements

### Ansible

[Ansible](http://ansible.com) is used to provision the virtual machine, so you
must have that installed. Follow the
[installation instructions](http://docs.ansible.com/intro_installation.html#installation).

### blockinfile Ansible role

It is required for git ([doc](https://galaxy.ansible.com/list#/roles/1475)).

```
$ ansible-galaxy install yaegashi.blockinfile
```

### Usage

Installation is as easy as cloning a GitHub project:

```
$ cd your-project
$ git clone https://github.com:NansPellicari/vagrant-ansible-debian8-php.git vagrant
```

Or, if you're using Git already in your project, you can use it as a submodule:

```
$ cd your-project
$ git submodule add https://github.com:NansPellicari/vagrant-ansible-debian8-php.git vagrant
```

After the project is added, you can start the environment like this:

```
$ cd vagrant
$ vagrant up
```

Starting the VM might take some time, since it will download the entire box
and additional applications/library. When the VM is done setting up, point
your browser towards [http://10.10.15.150](http://10.10.15.150) and there you
have it.

#### Note

If you're using Windows, you have to modify the `Vagrantfile` a little bit to
make it all work (since Windows doesn't support NFS). Replace the following
lines in the Vagrantfile:

```ruby
config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", :nfs => true
config.vm.synced_folder "..", "/var/www", id: "application",  :nfs => true
```

with:

```ruby
config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root"
config.vm.synced_folder "..", "/var/www", id: "application"
```

## License

```
Copyright (c) 2015, Nans Pellicari <nans.pellicari@gmail.com>
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

The views and conclusions contained in the software and documentation are those
of the authors and should not be interpreted as representing official policies,
either expressed or implied, of the FreeBSD Project.
```
