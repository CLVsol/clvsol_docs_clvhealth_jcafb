.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: blue
.. role:: bmaroon
.. role:: borange
.. role:: bi

=================================================
Criação do Servidor Local "tkl-odoo16-jcafb26-vm"
=================================================

    :bmaroon:`(** Este Servidor foi criado a partir de uma cópia do Servidor "tkl-odoo16-vm-18" **)`

    This project will help you create a server to host the **Odoo 16**, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

        * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

        * ISO file: "**turnkey-odoo-18.0-bookworm-amd64.iso**".

VM preparation (1)
------------------

    #. Create a new Virtual Machine using the following parameters:

        - Choose the "**Custom (advanced)**" configuration type
        - Choose de "Virtual Machine Hardware Compatibility": **Workstation 14.x**
        - Choose the gest operating system: **I will install the operating system later**
        - Select the Guest Operatin System: **Linux** (Version: **Debian 10.x 64-bit**)
        - Set a VM Name and a VM Location of your preference (**tkl-odoo16-jcafb26-vm** - **E:\\vm\\tkl-odoo16-jcafb26-vm**).
        - Processor Configuration:

            - Number of processors: **4**
            - Number of cores per processor: **2**

        - Memory for the Virtual Machine: **2048 MB**
        - Choose "**Use bridged networking**" for the Network Type. This way you will give the operating system, direct acces to an external Ethernet network (otherwise you can use **network address translation (NAT)**)
        - Leave the default parameters for the next three windows:

            - Select I/O Controller Types
            - Select a Disk Type
            - Select a Disk

        - Specify Disk Capacity:

            - Maximum disk size: **32.0 GB**
            - Select: **Split virtual disk into multiple files**

        - Set the Disk File of your choice: **sda\\sda.vmdk**
        - Finish the Virtual Machine creation.

    #. Credentials (passwords set at first boot):

        - Webmin, SSH: username **root**
        - PostgreSQL, Adminer: username **postgres**
        - Odoo Master Account: **admin**

    #. To access the **Confconsole**:

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

            confconsole

    #. To execute the **Interactive System Initialization**:

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

            turnkey-init

Shrinking VM Disk Images
------------------------

    #. **Preparation of the VM**

        #. On the main vm toolbar after opening the VM and BEFORE powering it on choose VM -> Power -> Power On to Firmware. That works for the NEXT ONE boot::

            Configure the Boot so that 'CD-ROM Drive' is the first option.
            Save and Exit.

    #. **First Step - Backup**

        Make a backup.  The steps below can really destroy images; follow them AT YOUR OWN RISK.

    #. **Wiping Free Space**

        Even after you delete the files, the hard drive image still has the contents of the old file on it.  This is why programs like photorec can work.  We need to wipe the data clean off the drive by writing NULL (hex 0x00) bytes to all of the free areas on the drive.  This still doesn't make the image any smaller.  More on this later ...
        
        Wiping Linux From CD
        The easiest way to wipe extfs filesystems (ext2, ext3, ext4) is with zerofree.  It's the faster choice.  You can download the iso image of Parted Magic and configure your VM to mount that as a virtual CD-ROM.  Boot from it, then open a terminal by clicking on the black monitor icon at the bottom.  From there, it is a few simple commands

            ::

                # Wipe a hard drive partition.  Let's say that /dev/sda1 is for /boot and /dev/sda2 is /root
                zerofree -v /dev/sda1

    #. **VMWare Workstation - Windows Host**

        Open up VMWare Workstation and edit the virtual machine.  Select the hard disk, then there's a button on the right that says Utilities.  Under that drop-down menu is an option, "Compact".  Presto-chango, you are done.

:bmaroon:`Backup:` :blue:`tkl-odoo16-jcafb26-vm_2024-10-24a.rar`

Development (1)
---------------

    #. Notes on the installation:

        #. Installation: **/usr/lib/python3/dist-packages/odoo**

        #. Configuration File: **/etc/odoo/odoo.conf**

        #. Init file: **/etc/init.d/odoo**

        #. DAEMON: **/usr/bin/odoo**

        #. LOGFILE: **/var/log/odoo/odoo-server.log**

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo16-jcafb26-vm -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            mkdir /opt/odoo

            chown -R odoo:odoo /opt/odoo

    #. Edit the file "**/etc/odoo/odoo.conf**" (as root):

        ::

            db_host = localhost
            db_maxconn = 64
            db_name = TurnkeylinuxExample

        ::

            # db_host = localhost
            db_host = False
            db_maxconn = 64
            # db_name = TurnkeylinuxExample
            db_name =

    #. Copy file "**/etc/odoo/odoo.conf**" into "**/etc/odoo/odoo-man.conf**". Edit the file "**/etc/odoo/odoo-man.conf**" (as root):

        ::

            logfile = 

        ::

            # logfile = 
            logfile = False

    #. Setup the file "**/etc/odoo/odoo-man.conf**" (Group: odoo Owner: odoo) permissions, using the following commands (as root):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Delete the 'Turnkeylinux Example' database, using the following procedure:

        #. Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

            ::

                ssh tkl-odoo16-jcafb26-vm -l root

                /etc/init.d/odoo stop

                su odoo

        #. [tkl-odoo16-jcafb26-vm] Excluir a instância do *Turnkeylinux Example* existente:

            ::

                cd /opt/odoo
                dropdb -i TurnkeylinuxExample

                cd /var/lib/odoo/.local/share/Odoo/filestore
                rm -rf TurnkeylinuxExample

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo manual:

            ::

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Upgrade the software:

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. Reinitialize the VM.

:bmaroon:`Backup:` :blue:`tkl-odoo16-jcafb26-vm_2024-10-24b.rar`

VM preparation (2)
------------------

    #. Update host name, executing the following commands:

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            HOSTNAME=tkl-odoo16-jcafb26-vm
            echo "$HOSTNAME" > /etc/hostname
            sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
            # /etc/init.d/hostname.sh start

    #. Change the timezone, executing the following command and picking out the time zone from a list:

        ::

            dpkg-reconfigure tzdata

        * Geographic area: **America**
        * Time Zone: **Sao Paulo**

    #. Enable **Connecting through SSH tunnel**:

        * `Solving SSH “channel 3: open failed: administratively prohibited” error when tunnelling <https://blog.mypapit.net/2012/06/solving-ssh-channel-3-open-failed-administratively-prohibited-error-when-tunnelling.html>`_ 
        * `Secure TCP/IP Connections with SSH Tunnels <https://www.postgresql.org/docs/9.1/static/ssh-tunnels.html>`_ 
        * `Using an SSH Tunnel <http://confluence.dbvis.com/display/UG91/Using+an+SSH+Tunnel>`_ 

        #. Edit the file "**/etc/ssh/sshd_config**" (as root):

            ::

                #AllowTcpForwarding yes

            ::

                #AllowTcpForwarding yes
                AllowTcpForwarding yes

        #. To stop and start the sshd service, use the following commands (as root):

            ::

                ssh tkl-odoo16-jcafb26-vm -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@tkl-odoo16-jcafb26-vm

            ::

                ssh -L 33335:localhost:5432 root@tkl-odoo16-jcafb26-vm

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo16-jcafb26-vm

            ::

                ssh -L 33335:127.0.0.1:5432 root@tkl-odoo16-jcafb26-vm

Development (2)
---------------

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            cd /opt/odoo
            su odoo

            git config --global user.email "carlos.vercelino@gmail.com"
            git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

            git config --global alias.lg "log --oneline --all --graph --decorate"

            git config --list

            exit

    #. Configure Odoo Server timeouts

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as root):

            * `Command-line interface: odoo-bin <https://www.odoo.com/documentation/12.0/reference/cmdline.html>`_
            * `Difference between CPU time and wall time <https://service.futurequest.net/index.php?/Knowledgebase/Article/View/407/0/difference-between-cpu-time-and-wall-time>`_

            ::

                limit_time_cpu = 60
                limit_time_real = 120

            ::

                # limit_time_cpu = 60
                limit_time_cpu = 36000
                # limit_time_real = 120
                limit_time_real = 72000

    #. Configure Odoo Server workers

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `Sample odoo.conf file  <https://gist.github.com/Guidoom/d5db0a76ce669b139271a528a8a2a27f>`_
            * `How to Speed up Odoo <https://www.rosehosting.com/blog/how-to-speed-up-odoo/>`_
            * `What is a “worker” in Odoo? <https://stackoverflow.com/questions/35918633/what-is-a-worker-in-odoo>`_

            ::

                workers = 0

            ::

                # workers = 0
                workers = 5

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = base,web

            ::

                # server_wide_modules = base,web
                server_wide_modules = None

:bmaroon:`Backup:` :blue:`tkl-odoo16-jcafb26-vm_2024-10-24c.rar`

Development (3)
---------------

    #. To install pip3 (for python 3.5), use the following commands (as root):

        ::

            apt-get install python3-pip

            apt-get install python3-pip
            Reading package lists... Done
            Building dependency tree... Done
            Reading state information... Done
            The following additional packages will be installed:
              python3-distutils python3-lib2to3 python3-setuptools python3-wheel
            Suggested packages:
              python-setuptools-doc
            Recommended packages:
              build-essential python3-dev
            The following NEW packages will be installed:
              python3-distutils python3-lib2to3 python3-pip python3-setuptools python3-wheel
            0 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.
            Need to get 2084 kB of archives.
            After this operation, 10.6 MB of additional disk space will be used.
            Do you want to continue? [Y/n] 
            Get:1 http://deb.debian.org/debian bookworm/main amd64 python3-lib2to3 all 3.11.2-3 [76.3 kB]
            Get:2 http://deb.debian.org/debian bookworm/main amd64 python3-distutils all 3.11.2-3 [131 kB]
            Get:3 http://deb.debian.org/debian bookworm/main amd64 python3-setuptools all 66.1.1-1 [521 kB]
            Get:4 http://deb.debian.org/debian bookworm/main amd64 python3-wheel all 0.38.4-2 [30.8 kB]
            Get:5 http://deb.debian.org/debian bookworm/main amd64 python3-pip all 23.0.1+dfsg-1 [1325 kB]
            Fetched 2084 kB in 1s (4019 kB/s)     
            debconf: delaying package configuration, since apt-utils is not installed
            Selecting previously unselected package python3-lib2to3.
            (Reading database ... 89630 files and directories currently installed.)
            Preparing to unpack .../python3-lib2to3_3.11.2-3_all.deb ...
            Unpacking python3-lib2to3 (3.11.2-3) ...
            Selecting previously unselected package python3-distutils.
            Preparing to unpack .../python3-distutils_3.11.2-3_all.deb ...
            Unpacking python3-distutils (3.11.2-3) ...
            Selecting previously unselected package python3-setuptools.
            Preparing to unpack .../python3-setuptools_66.1.1-1_all.deb ...
            Unpacking python3-setuptools (66.1.1-1) ...
            Selecting previously unselected package python3-wheel.
            Preparing to unpack .../python3-wheel_0.38.4-2_all.deb ...
            Unpacking python3-wheel (0.38.4-2) ...
            Selecting previously unselected package python3-pip.
            Preparing to unpack .../python3-pip_23.0.1+dfsg-1_all.deb ...
            Unpacking python3-pip (23.0.1+dfsg-1) ...
            Setting up python3-lib2to3 (3.11.2-3) ...
            Setting up python3-distutils (3.11.2-3) ...
            Setting up python3-setuptools (66.1.1-1) ...
            Setting up python3-wheel (0.38.4-2) ...
            Setting up python3-pip (23.0.1+dfsg-1) ...
            Processing triggers for man-db (2.11.2-2) ...
            Enumerating objects: 1891, done.
            Counting objects: 100% (1891/1891), done.
            Delta compression using up to 8 threads
            Compressing objects: 100% (1205/1205), done.
            Writing objects: 100% (1891/1891), done.
            Total 1891 (delta 80), reused 1855 (delta 66), pack-reused 0

    #. :red:`(Failed - Not Used)` To install erppeek (for python 3.5), use the following commands (as root):

        ::

            pip3 install erppeek

        ::

            pip3 install erppeek
            error: externally-managed-environment

            × This environment is externally managed
            ╰─> To install Python packages system-wide, try apt install
                python3-xyz, where xyz is the package you are trying to
                install.
                
                If you wish to install a non-Debian-packaged Python package,
                create a virtual environment using python3 -m venv path/to/venv.
                Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
                sure you have python3-full installed.
                
                If you wish to install a non-Debian packaged Python application,
                it may be easiest to use pipx install xyz, which will manage a
                virtual environment for you. Make sure you have pipx installed.
                
                See /usr/share/doc/python3.11/README.venv for more information.

            note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
            hint: See PEP 668 for the detailed specification.

    #. To install erppeek (for python 3.5, Debian 12), use the following commands (as root):

        ::

            pip3 install erppeek --break-system-packages

        ::

            pip3 install erppeek --break-system-packages                           
            Collecting erppeek
              Downloading ERPpeek-1.7.1-py2.py3-none-any.whl (22 kB)
            Installing collected packages: erppeek
            Successfully installed erppeek-1.7.1
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install pandas, use the following commands (as root):

        ::

            pip3 install pandas --break-system-packages

        ::

            pip3 install pandas --break-system-packages
            Collecting pandas
              Downloading pandas-2.2.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (13.1 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 13.1/13.1 MB 38.4 MB/s eta 0:00:00
            Collecting numpy>=1.23.2
              Downloading numpy-2.1.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.3 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.3/16.3 MB 41.5 MB/s eta 0:00:00
            Requirement already satisfied: python-dateutil>=2.8.2 in /usr/lib/python3/dist-packages (from pandas) (2.8.2)
            Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3/dist-packages (from pandas) (2022.7.1)
            Collecting tzdata>=2022.7
              Downloading tzdata-2024.2-py2.py3-none-any.whl (346 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 346.6/346.6 kB 46.7 MB/s eta 0:00:00
            Installing collected packages: tzdata, numpy, pandas
            Successfully installed numpy-2.1.3 pandas-2.2.3 tzdata-2024.2
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. :red:`(Failed - Not Used)` To install xlutils, execute the following commands (as root):

        ::

            pip3 install xlutils

        ::

            pip3 install xlutils
            error: externally-managed-environment

            × This environment is externally managed
            ╰─> To install Python packages system-wide, try apt install
                python3-xyz, where xyz is the package you are trying to
                install.
                
                If you wish to install a non-Debian-packaged Python package,
                create a virtual environment using python3 -m venv path/to/venv.
                Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
                sure you have python3-full installed.
                
                If you wish to install a non-Debian packaged Python application,
                it may be easiest to use pipx install xyz, which will manage a
                virtual environment for you. Make sure you have pipx installed.
                
                See /usr/share/doc/python3.11/README.venv for more information.

            note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
            hint: See PEP 668 for the detailed specification.

    #. To install xlutils, execute the following commands (as root):

        ::

            pip3 install xlutils --break-system-packages

        ::

            pip3 install xlutils --break-system-packages
            Collecting xlutils
              Downloading xlutils-2.0.0-py2.py3-none-any.whl (55 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 55.1/55.1 kB 2.0 MB/s eta 0:00:00
            Requirement already satisfied: xlrd>=0.7.2 in /usr/lib/python3/dist-packages (from xlutils) (1.2.0)
            Requirement already satisfied: xlwt>=0.7.4 in /usr/lib/python3/dist-packages (from xlutils) (1.3.0)
            Installing collected packages: xlutils
            Successfully installed xlutils-2.0.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh tkl-odoo17-vm-18 -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/erppeek --branch master
            # git clone https://github.com/OCA/l10n-brazil --branch 16.0
            git clone https://github.com/CLVsol/OCA_l10n-brazil --branch 16.0
            # git clone https://github.com/CLVsol/clvsol_odoo_client --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_client --branch 16.0
            # git clone https://github.com/CLVsol/clvsol_l10n_brazil --branch 14.0
            git clone https://github.com/CLVsol/clvsol_l10n_brazil --branch 16.0
            # git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 16.0
            # git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 16.0

    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo17-vm-18 -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as root):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons

        ::

            # addons_path = /usr/lib/python3/dist-packages/odoo/addons
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_l10n_brazil,/opt/odoo/clvsol_odoo_addons
            
    #. To install erpbrasil.base, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-18 -l root

        ::

            pip3 install erpbrasil.base --break-system-packages

            pip3 install erpbrasil.base --break-system-packages
            Collecting erpbrasil.base
              Downloading erpbrasil.base-2.3.1-py2.py3-none-any.whl (21 kB)
            Installing collected packages: erpbrasil.base
            Successfully installed erpbrasil.base-2.3.1
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install phonenumbers, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-18 -l root

        ::

            pip3 install phonenumbers --break-system-packages

            pip3 install phonenumbers --break-system-packages
            Collecting phonenumbers
              Downloading phonenumbers-8.13.48-py2.py3-none-any.whl (2.6 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.6/2.6 MB 18.2 MB/s eta 0:00:00
            Installing collected packages: phonenumbers
            Successfully installed phonenumbers-8.13.48
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install email-validator, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-18 -l root

        ::

            pip3 install email-validator --break-system-packages

            pip3 install email-validator --break-system-packages
            Collecting email-validator
              Downloading email_validator-2.2.0-py3-none-any.whl (33 kB)
            Collecting dnspython>=2.0.0
              Downloading dnspython-2.7.0-py3-none-any.whl (313 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 313.6/313.6 kB 7.2 MB/s eta 0:00:00
            Requirement already satisfied: idna>=2.0.0 in /usr/lib/python3/dist-packages (from email-validator) (3.3)
            Installing collected packages: dnspython, email-validator
            Successfully installed dnspython-2.7.0 email-validator-2.2.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install brazilcep, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-18 -l root

        ::

            pip3 install brazilcep --break-system-packages

            pip3 install brazilcep --break-system-packages
            Collecting brazilcep
              Downloading brazilcep-6.5.0-py3-none-any.whl (9.6 kB)
            Requirement already satisfied: zeep>=4.2.1 in /usr/lib/python3/dist-packages (from brazilcep) (4.2.1)
            Collecting requests>=2.28.2
              Downloading requests-2.32.3-py3-none-any.whl (64 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 64.9/64.9 kB 1.7 MB/s eta 0:00:00
            Requirement already satisfied: charset-normalizer<4,>=2 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.0.1)
            Requirement already satisfied: idna<4,>=2.5 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.3)
            Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (1.26.12)
            Requirement already satisfied: certifi>=2017.4.17 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (2022.9.24)
            Installing collected packages: requests, brazilcep
              Attempting uninstall: requests
                Found existing installation: requests 2.28.1
                Not uninstalling requests at /usr/lib/python3/dist-packages, outside environment /usr
                Can't uninstall 'requests'. No files were found to uninstall.
            Successfully installed brazilcep-6.5.0 requests-2.32.3
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

:bmaroon:`Backup:` :blue:`tkl-odoo16-jcafb26-vm_2024-10-30a.rar`

Development (4)
---------------

    #. :red:`(Failed - Not Used)` To install yaml, use the following commands (as root):

        ::

            pip3 install pyyaml

        ::

            pip3 install pyyaml
            error: externally-managed-environment

            × This environment is externally managed
            ╰─> To install Python packages system-wide, try apt install
                python3-xyz, where xyz is the package you are trying to
                install.
                
                If you wish to install a non-Debian-packaged Python package,
                create a virtual environment using python3 -m venv path/to/venv.
                Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
                sure you have python3-full installed.
                
                If you wish to install a non-Debian packaged Python application,
                it may be easiest to use pipx install xyz, which will manage a
                virtual environment for you. Make sure you have pipx installed.
                
                See /usr/share/doc/python3.11/README.venv for more information.

            note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
            hint: See PEP 668 for the detailed specification.

    #. :red:`(Failed - Not Used)` To install yaml, use the following commands (as root):

        ::

            pip3 install pyyaml --break-system-packages

        ::

            pip3 install pyyaml --break-system-packages
            WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7feeb5d26950>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/pyyaml/
            WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7feeb4610450>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/pyyaml/
            WARNING: Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7feeb4610950>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/pyyaml/
            WARNING: Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7feeb4611310>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/pyyaml/
            WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7feeb4611d50>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/pyyaml/
            ERROR: Could not find a version that satisfies the requirement pyyaml (from versions: none)
            ERROR: No matching distribution found for pyyaml

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo16-jcafb26-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025_16"

            dropdb -i clvhealth_jcafb_2025_16

Development (5)
---------------

    #. :red:`(Not Used)` Configure "osv_memory_age_limit"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[14.0] DeprecationWarning: The osv-memory-age-limit <https://github.com/odoo/odoo/issues/60681>`_

            ::

                osv_memory_age_limit = 1.0

            ::

                # osv_memory_age_limit = 1.0
                osv_memory_age_limit = False

    #. :red:`(Not Used)` To install Jinja2-2.11.2, execute the following commands (as root):

        * Issue:

            ::

                2021-01-14 13:29:55,275 8698 WARNING mfmng_2021v_14 py.warnings: /usr/lib/python3/dist-packages/jinja2/sandbox.py:82: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated, and in 3.8 it will stop working
                from collections import MutableSet, MutableMapping, MutableSequence
 
        ::

            pip3 install -U Jinja2

        ::

            root@tkl-odoo16-jcafb26-vm ~# pip3 install -U Jinja2
            Collecting Jinja2
              Downloading https://files.pythonhosted.org/packages/30/9e/f663a2aa66a09d838042ae1a2c5659828bb9b41ea3a6efa20a20fd92b121/Jinja2-2.11.2-py2.py3-none-any.whl (125kB)
                100% |████████████████████████████████| 133kB 1.2MB/s 
            Requirement already satisfied, skipping upgrade: MarkupSafe>=0.23 in /usr/lib/python3/dist-packages (from Jinja2) (1.1.0)
            Installing collected packages: Jinja2
              Found existing installation: Jinja2 2.10
                Not uninstalling jinja2 at /usr/lib/python3/dist-packages, outside environment /usr
                Can't uninstall 'Jinja2'. No files were found to uninstall.
            Successfully installed Jinja2-2.11.2

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh tkl-odoo16-jcafb26-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_client --branch 13.0
            git clone https://github.com/MostlyOpen/clvsol_clvhealth_jcafb --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_log --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_summary --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_process --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_process_jcafb --branch 15.0
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_sync --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_log_jcafb --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_summary_jcafb --branch 15.0
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0
            git clone https://github.com/MostlyOpen/clvsol_l10n_brazil --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_l10n_br --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_sync_jcafb --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_export --branch 15.0_dev
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_export_jcafb --branch 15.0_dev

    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as root):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons

        ::

            # addons_path = /usr/lib/python3/dist-packages/odoo/addons
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_odoo_addons,/opt/odoo/clvsol_odoo_addons_log,/opt/odoo/clvsol_odoo_addons_verification,/opt/odoo/clvsol_odoo_addons_process,/opt/odoo/clvsol_odoo_addons_process_jcafb,/opt/odoo/clvsol_odoo_addons_sync,/opt/odoo/clvsol_odoo_addons_jcafb,/opt/odoo/clvsol_odoo_addons_log_jcafb,/opt/odoo/clvsol_odoo_addons_verification_jcafb,/opt/odoo/clvsol_l10n_brazil,/opt/odoo/clvsol_odoo_addons_l10n_br,/opt/odoo/clvsol_odoo_addons_sync_jcafb,/opt/odoo/clvsol_odoo_addons_export,/opt/odoo/clvsol_odoo_addons_export_jcafb,/opt/odoo/clvsol_odoo_addons_summary,/opt/odoo/clvsol_odoo_addons_summary_jcafb
            
:bmaroon:`(Not Implemented)` Upgrade the odoo software
------------------------------------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo16-jcafb26-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            su odoo

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

References
----------

    #. Installing Odoo (15)

     * `Odoo Nightly builds <https://nightly.odoo.com/>`_ 
     * `Installing Odoo (15) <https://www.odoo.com/documentation/15.0/setup/install.html>`_ 
