# Docker MSSQL Database
- This is a Dockerized MSSQL Database with sample data. 
- This project loads everything using a Vagrantfile which installs all the pre-requisites.
- Use at your own discretion.

# Optional Installs
These applications are fully optional to be installed on your development machine.
These are only required in order to host the MSSQL database and Docker engine used in this demo.
- Vagrant v2.2.5 from [Vagrant's website](https://www.vagrantup.com/)
- Virtualbox v6.0.12 from [Oracle Virtualbox Older Builds](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0)

# Running this Demo with Vagrant
- Ensure that Vagrant and VirtualBox are already installed on your development machine.
- Once confirmed, open VSCode and navigate to the root of the Project Folder ```%Local_Directory%\docker-mssqldb\```.
- Launch the terminal then type ```vagrant up``` or ```vagrant up --provision```. This command will bring up the guest VM and call the provision shell scripts to setup the database and the project.

# Running this Demo without Vagrant
To run this demo without installing the above applications, these are required to be on the developer machine.
- MSSQL Server. Developer version will do.
- Run the database create script found in ```%Local_Directory%\docker-mssqldb\db_scripts\db_init.sql``` against your Dev SQL Server.

# Verify if the database server is running
- Open your MSSQL Management Studio then try to connect to localhost,1466 using SA username and the password specified in the Vagrantfile. 

# Current State:
- Runs Ubuntu Xenial in Virtualbox provisioned via Vagrant.
- Installs Docker inside the guest VM. Then pulls and builds the MSSQL database.
- Sets up the sample databases and tables. The database will be exposed to the host machine on port 1466.

# Important Information!
Vagrant conflicts with Hyper-V
----
If you have Docker installed on your Development machine, you'll need to disable Hyper-V for Vagrant to work. 

In some cases, you may still encounter VT-x error even when you've already enable Virtualization in your BIOS. To deal with this, run the code below on an Administrator command prompt. Then reboot your computer. Note: This setting may be reset by Group Policies.

```
bcdedit /set hypervisorlaunchtype off
```

Vagrant SSH: Permission denied (publickey)
----
Running ```vagrant ssh -- -vv``` will show you that this error pertains to Windows SSH thinking the Vagrant private is not secured or "too open".

To work around this, locate the private_key file generated when you run ```vagrant up```, then only grant your current Windows user account and remove any inherited permissions by going to the files ```Properties > Security > Advanced Security Settings (using the Edit button)```.
