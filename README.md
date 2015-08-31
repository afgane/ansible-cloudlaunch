This is an Ansbile playbook for installing [Galaxy Cloud Launch][1] application
for a production server setup.

Usage instructions
------------------
Before starting, you will need access to the machine where you want to install
Cloud Launch. Currently, the installation has been tailored for Ubuntu 14.04.
Note that this playbook requires `sudo` access and will create a new system user.

To use this playbook, clone this repository:

    git clone https://github.com/afgane/ansible-cloudlaunch.git

Then, supply the required variables. Edit file `cl.yml` and provide values for
the two passwords under the `vars` section. Also, edit `inventory/hosts` and
provide the IP address and access details (i.e., user name and SSH key) for the
machine where you want to install Cloud Launch.

Run the playbook with the following command:

    ansible-playbook -i inventory/hosts cl.yml

Once the installation process has completed, connect to the target machine and
create an Admin user by executing the following set of commands:

    cd /srv/cloudlaunch
    source .cl/bin/activate
    python cloudlaunch/biocloudcentral/manage.py createsuperuser

You can now log in as an admin at `<server IP>/admin` using the created account.


Once the Cloud Launch application is running, you can check on its status with
`supervisorctl status cloudlaunch` or restart it with
`supervisorctl restart cloudlaunch`.

[1]: https://github.com/galaxyproject/cloudlaunch
