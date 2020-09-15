Ansible Workshop
================

<!-- vscode-markdown-toc -->
* [Prerequisites](#Prerequisites)
	* [Build Virtual Machines](#BuildVirtualMachines)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Prerequisites'></a>Prerequisites

* Git, VirtualBox and Vagrant must be installed on a local machine before the workshop
  * Git
    * Download - https://git-scm.com/downloads
    * Install - https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
  * VirtualBox
    * Download - https://www.virtualbox.org/wiki/Downloads
    * Install - https://www.virtualbox.org/manual/UserManual.html#installation
  * Vagrant
    * Download - https://www.vagrantup.com/downloads.html
    * Install - https://www.vagrantup.com/docs/installation

  ### <a name='BuildVirtualMachines'></a>Build Virtual Machines

Launch MacOS/Linux Terminal or GitBash on Windows machine.

Go to home folder

```bash
cd $HOME
```

Clone git repository (replace MyUsername by real github username)

```bash
git clone https://MyUsername@github.com/svergun/ansible-workshop.git
```

Go to the workshop folder

```bash
cd ansible-workshop/
```

Build virtual machines

```bash
vagrant up
```

Check virtual machines status

```bash
~/ansible-workshop$ vagrant status
Current machine states:
 
control                   running (virtualbox)
node1                     running (virtualbox)
node2                     running (virtualbox)
```

Stop virtual machines

```bash
vagrant halt
```
