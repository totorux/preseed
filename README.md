# Ubuntu/Debian Minimal CD Preseeding

The scripts in this repo automate the process of embedding preseed files into
a initrd.gz of a ubuntu/debian [mini.iso][ubuntu-minimalcd], along with the ability
to add things like your ssh public key so that login is automatic as well.

The `remaster` script does the majority of the work, with directories in 
files/preseeds supplying a set of configuration files and helper scripts.
For example, `netinstall` is configured to automatically download the 
`network-console` component, it will embed your ssh public key so that you 
can log in, and it will generate the ssh host keys on your computer rather
than at run time so that you know what the fingerprints should be.
`netinstall-watchdog` is the same, except it adds a small C program that
will reboot the computer after a timeout is up.

They are very temperamental and experimental. Play with the results in 
virtual machines first, and note the "WITHOUT ANY WARRANTY" bit.

## Legal

<pre>
Copyright (C) 2010  Daniel Richman

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

For a full copy of the GNU General Public License, 
see &lt;http://www.gnu.org/licenses/&gt;.
</pre>

## Usage

The remaster script is the only one you should run directly. If required, it 
downloads a mini.iso from [ubuntu.com][ubuntu-minimalcd], loop-mounts it and 
unpacks it. It will require sudo access to do this.

Edit files/settings/*, then:

<pre>
Usage ./remaster <preseed> <Linux distrib> <Distrib version> <Arch> <Update>
Where <preseed> is one of the items in files/preseeds/, <Linux distrib> is one of the items: debian or ubuntu, <Distrib version> is one of the items: stable, saucy ...(depend of the debian/ubuntu version you want to use), <Arch> is one of the items: i386 amd64, <Update> is needed if you want to download the new version of the mini.iso put: update
You can add custom preseed by making a new folder in files/preseeds/ and puttiong you own preseed called 'preseed.cfg' without network configuration who is in files/settings/network.cfg
If no iso files is found in files/download/ (with a name like: mini-ubuntu-saucy-amd64.iso) it will be downloaded, else the script will use the founded file.
</pre>

I apologise for the lack of documentation.

## Dependencies

 - wget
 - bash
 - cpio
 - mkisofs
 - fakeroot
 - ssh-keygen

[ubuntu-minimalcd]: https://help.ubuntu.com/community/Installation/MinimalCD
[source]: http://github.com/danielrichman/preseed
