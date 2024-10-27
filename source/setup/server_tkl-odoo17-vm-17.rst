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

============================================
Criação do Servidor Local "tkl-odoo17-vm-17"
============================================

    This project will help you create a server to host the **Odoo 17**, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

        * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

        * ISO file: "**turnkey-odoo-18.0-bookworm-amd64.iso**".

VM preparation (1)
------------------

    #. Create a new Virtual Machine using the following parameters:

        - Choose the "**Custom (advanced)**" configuration type
        - Choose de "Virtual Machine Hardware Compatibility": **Workstation 14.x**
        - Choose the gest operating system: **I will install the operating system later**
        - Select the Guest Operatin System: **Linux** (Version: **Debian 10.x 64-bit**)
        - Set a VM Name and a VM Location of your preference (**tkl-odoo17-vm-17** - **E:\\vm\\tkl-odoo17-vm-17**).
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

            ssh tkl-odoo17-vm-17 -l root

            confconsole

    #. To execute the **Interactive System Initialization**:

        ::

            ssh tkl-odoo17-vm-17 -l root

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

:bmaroon:`Backup:` :blue:`tkl-odoo14-vm-17_2024-10-24a.rar`

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

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo17-vm-17 -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

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

            ssh tkl-odoo17-vm-17 -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Delete the 'Turnkeylinux Example' database, using the following procedure:

        #. Estabelecer uma sessão ssh com o servidor **tkl-odoo17-vm-17** e paralizar o *Odoo*:

            ::

                ssh tkl-odoo17-vm-17 -l root

                /etc/init.d/odoo stop

                su odoo

        #. [tkl-odoo17-vm-17] Excluir a instância do *Turnkeylinux Example* existente:

            ::

                cd /opt/odoo
                dropdb -i TurnkeylinuxExample

                cd /var/lib/odoo/.local/share/Odoo/filestore
                rm -rf TurnkeylinuxExample

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo17-vm-17** ao modo manual:

            ::

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Upgrade the software:

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. Reinitialize the VM.

:bmaroon:`Backup:` :blue:`tkl-odoo14-vm-17_2024-10-24b.rar`

VM preparation (2)
------------------

    #. Update host name, executing the following commands:

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            HOSTNAME=tkl-odoo17-vm-17
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

                ssh tkl-odoo17-vm-17 -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@tkl-odoo17-vm-17

            ::

                ssh -L 33335:localhost:5432 root@tkl-odoo17-vm-17

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo17-vm-17

            ::

                ssh -L 33335:127.0.0.1:5432 root@tkl-odoo17-vm-17

Development (2)
---------------

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

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

:bmaroon:`Backup:` :blue:`tkl-odoo17-vm-17_2024-10-25a.rar`

Replace the Odoo installation (Odoo 17.0)
-----------------------------------------

    #. To replace the Odoo installation (Odoo 17.0), use the following commands (as root) "`Install Odoo 15 on Debian 10 / Debian 11 <https://computingforgeeks.com/how-to-install-odoo-on-debian-linux/>`_":

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

        ::

            apt install gnupg2

            wget https://nightly.odoo.com/odoo.key

            cat odoo.key | gpg --dearmor | tee /etc/apt/trusted.gpg.d/odoo.gpg  >/dev/null

            echo "deb http://nightly.odoo.com/17.0/nightly/deb/ ./" | tee /etc/apt/sources.list.d/odoo.list

            apt-get update

            apt-get install odoo

        :bmaroon:`Alerta! (installed odoo package post-installation script subprocess returned error exit status 1)`

        ::

            apt-get install odoo
            Reading package lists... Done
            Building dependency tree... Done
            Reading state information... Done
            The following packages were automatically installed and are no longer required:
              fonts-glyphicons-halflings iso-codes libavahi-client3 libavahi-common-data libavahi-common3 libcups2 libdbus-1-3 libdouble-conversion3 libdrm-amdgpu1 libdrm-common libdrm-intel1
              libdrm-nouveau2 libdrm-radeon1 libdrm2 libdw1 libegl-mesa0 libegl1 libevdev2 libgbm1 libgl1 libgl1-mesa-dri libglapi-mesa libglvnd0 libglx-mesa0 libglx0 libgstreamer-plugins-base1.0-0
              libgstreamer1.0-0 libgudev-1.0-0 libhyphen0 libinput-bin libinput10 libjs-jquery-ui libmd4c0 libmtdev1 liborc-0.4-0 libpciaccess0 libpcre2-16-0 libqt5core5a libqt5dbus5 libqt5gui5
              libqt5network5 libqt5positioning5 libqt5printsupport5 libqt5qml5 libqt5qmlmodels5 libqt5quick5 libqt5sensors5 libqt5svg5 libqt5webchannel5 libqt5webkit5 libqt5widgets5 libsensors-config
              libsensors5 libunwind8 libvulkan1 libwacom-common libwacom2 libwayland-client0 libwayland-server0 libwoff1 libx11-xcb1 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-icccm4 libxcb-image0
              libxcb-keysyms1 libxcb-present0 libxcb-randr0 libxcb-render-util0 libxcb-shape0 libxcb-sync1 libxcb-util1 libxcb-xfixes0 libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxdamage1
              libxfixes3 libxkbcommon-x11-0 libxkbcommon0 libxshmfence1 libxxf86vm1 python3-feedparser python3-html2text python3-mako python3-mock python3-pbr python3-suds wkhtmltopdf xkb-data
            Use 'apt autoremove' to remove them.
            The following additional packages will be installed:
              fonts-urw-base35 gsfonts python3-cffi-backend python3-cryptography python3-geoip2 python3-maxminddb python3-openssl python3-renderpm python3-rjsmin
            Suggested packages:
              fonts-freefont-otf | fonts-freefont-ttf fonts-texgyre python-cryptography-doc python3-cryptography-vectors python-maxmindb-doc python-openssl-doc python3-openssl-dbg python3-renderpm-dbg
            Recommended packages:
              python3-ldap
            The following packages will be REMOVED:
              odoo-14
            The following NEW packages will be installed:
              fonts-urw-base35 gsfonts odoo python3-cffi-backend python3-cryptography python3-geoip2 python3-maxminddb python3-openssl python3-renderpm python3-rjsmin
            0 upgraded, 10 newly installed, 1 to remove and 0 not upgraded.
            Need to get 221 MB of archives.
            After this operation, 429 MB of additional disk space will be used.
            Do you want to continue? [Y/n] Y
            Get:1 http://deb.debian.org/debian bullseye/main amd64 python3-cffi-backend amd64 1.14.5-1 [85.8 kB]
            Get:2 http://security.debian.org bullseye-security/main amd64 python3-cryptography amd64 3.3.2-1+deb11u1 [222 kB]
            Get:3 http://deb.debian.org/debian bullseye/main amd64 python3-maxminddb amd64 2.0.3-1 [27.0 kB]                                      
            Get:4 http://deb.debian.org/debian bullseye/main amd64 python3-geoip2 all 2.9.0+dfsg1-2 [23.1 kB]                  
            Get:5 http://deb.debian.org/debian bullseye/main amd64 python3-openssl all 20.0.1-1 [53.7 kB]                      
            Get:6 http://security.debian.org bullseye-security/main amd64 python3-renderpm amd64 3.5.59-2+deb11u1 [80.1 kB]  
            Get:7 http://deb.debian.org/debian bullseye/main amd64 python3-rjsmin amd64 1.1.0+dfsg1-3+b4 [17.1 kB]                              
            Get:8 http://deb.debian.org/debian bullseye/main amd64 gsfonts all 1:8.11+urwcyr1.0.7~pre44-4.5 [3125 kB]
            Get:9 http://deb.debian.org/debian bullseye/main amd64 fonts-urw-base35 all 20200910-1 [6367 kB]
            Get:10 http://nightly.odoo.com/17.0/nightly/deb ./ odoo 17.0.20241027 [211 MB]              
            Fetched 221 MB in 18s (12.1 MB/s)                                                                                                                                                            
            perl: warning: Setting locale failed.
            perl: warning: Please check that your locale settings:
                LANGUAGE = "en_US.UTF-8",
                LC_ALL = (unset),
                LC_MONETARY = "pt_BR.UTF-8",
                LC_CTYPE = "C",
                LC_COLLATE = "C",
                LC_ADDRESS = "pt_BR.UTF-8",
                LC_TELEPHONE = "pt_BR.UTF-8",
                LC_NAME = "pt_BR.UTF-8",
                LC_MEASUREMENT = "pt_BR.UTF-8",
                LC_IDENTIFICATION = "pt_BR.UTF-8",
                LC_NUMERIC = "pt_BR.UTF-8",
                LC_PAPER = "pt_BR.UTF-8",
                LANG = "en_US.UTF-8"
                are supported and installed on your system.
            perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
            perl: warning: Setting locale failed.
            perl: warning: Please check that your locale settings:
                LANGUAGE = "en_US.UTF-8",
                LC_ALL = (unset),
                LC_CTYPE = "C",
                LC_MONETARY = "pt_BR.UTF-8",
                LC_COLLATE = "C",
                LC_ADDRESS = "pt_BR.UTF-8",
                LC_TELEPHONE = "pt_BR.UTF-8",
                LC_NAME = "pt_BR.UTF-8",
                LC_MEASUREMENT = "pt_BR.UTF-8",
                LC_IDENTIFICATION = "pt_BR.UTF-8",
                LC_NUMERIC = "pt_BR.UTF-8",
                LC_PAPER = "pt_BR.UTF-8",
                LANG = "en_US.UTF-8"
                are supported and installed on your system.
            perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
            [master b85935a] saving uncommitted changes in /etc prior to apt run
             3 files changed, 3 insertions(+)
             create mode 100644 apt/sources.list.d/odoo.list
             create mode 100644 apt/trusted.gpg.d/odoo.gpg
            debconf: delaying package configuration, since apt-utils is not installed
            (Reading database ... 78112 files and directories currently installed.)
            Removing odoo-14 (14.0.0+dfsg.2-7+deb11u2) ...
            Selecting previously unselected package python3-cffi-backend:amd64.
            (Reading database ... 49386 files and directories currently installed.)
            Preparing to unpack .../0-python3-cffi-backend_1.14.5-1_amd64.deb ...
            Unpacking python3-cffi-backend:amd64 (1.14.5-1) ...
            Selecting previously unselected package python3-cryptography.
            Preparing to unpack .../1-python3-cryptography_3.3.2-1+deb11u1_amd64.deb ...
            Unpacking python3-cryptography (3.3.2-1+deb11u1) ...
            Selecting previously unselected package python3-maxminddb.
            Preparing to unpack .../2-python3-maxminddb_2.0.3-1_amd64.deb ...
            Unpacking python3-maxminddb (2.0.3-1) ...
            Selecting previously unselected package python3-geoip2.
            Preparing to unpack .../3-python3-geoip2_2.9.0+dfsg1-2_all.deb ...
            Unpacking python3-geoip2 (2.9.0+dfsg1-2) ...
            Selecting previously unselected package python3-openssl.
            Preparing to unpack .../4-python3-openssl_20.0.1-1_all.deb ...
            Unpacking python3-openssl (20.0.1-1) ...
            Selecting previously unselected package python3-rjsmin.
            Preparing to unpack .../5-python3-rjsmin_1.1.0+dfsg1-3+b4_amd64.deb ...
            Unpacking python3-rjsmin (1.1.0+dfsg1-3+b4) ...
            Selecting previously unselected package gsfonts.
            Preparing to unpack .../6-gsfonts_1%3a8.11+urwcyr1.0.7~pre44-4.5_all.deb ...
            Unpacking gsfonts (1:8.11+urwcyr1.0.7~pre44-4.5) ...
            Selecting previously unselected package fonts-urw-base35.
            Preparing to unpack .../7-fonts-urw-base35_20200910-1_all.deb ...
            Unpacking fonts-urw-base35 (20200910-1) ...
            Selecting previously unselected package python3-renderpm:amd64.
            Preparing to unpack .../8-python3-renderpm_3.5.59-2+deb11u1_amd64.deb ...
            Unpacking python3-renderpm:amd64 (3.5.59-2+deb11u1) ...
            Selecting previously unselected package odoo.
            Preparing to unpack .../9-odoo_17.0.20241027_all.deb ...
            Unpacking odoo (17.0.20241027) ...
            Setting up python3-rjsmin (1.1.0+dfsg1-3+b4) ...
            Setting up fonts-urw-base35 (20200910-1) ...
            Setting up gsfonts (1:8.11+urwcyr1.0.7~pre44-4.5) ...
            Setting up python3-maxminddb (2.0.3-1) ...
            Setting up python3-cffi-backend:amd64 (1.14.5-1) ...
            Setting up python3-geoip2 (2.9.0+dfsg1-2) ...
            Setting up python3-renderpm:amd64 (3.5.59-2+deb11u1) ...
            Setting up python3-cryptography (3.3.2-1+deb11u1) ...
            Setting up python3-openssl (20.0.1-1) ...
            Setting up odoo (17.0.20241027) ...

            Configuration file '/etc/odoo/odoo.conf'
             ==> Modified (by you or by a script) since installation.
             ==> Package distributor has shipped an updated version.
               What would you like to do about it ?  Your options are:
                Y or I  : install the package maintainer's version
                N or O  : keep your currently-installed version
                  D     : show the differences between the versions
                  Z     : start a shell to examine the situation
             The default action is to keep your current version.
            *** odoo.conf (Y/I/N/O/D/Z) [default=N] ? N
              File "/usr/lib/python3/dist-packages/odoo/addons/account/models/chart_template.py", line 315
                match element:
                      ^
            SyntaxError: invalid syntax

              File "/usr/lib/python3/dist-packages/odoo/addons/base/models/ir_ui_view.py", line 2712
                match self.ids:  # `self.ids` will silently filter out new records (`NewId`s)
                      ^
            SyntaxError: invalid syntax

              File "/usr/lib/python3/dist-packages/odoo/addons/base_automation/models/ir_actions_server.py", line 44
                match action.state:
                      ^
            SyntaxError: invalid syntax

              File "/usr/lib/python3/dist-packages/odoo/addons/mail/tools/jwt.py", line 58
                match algorithm:
                      ^
            SyntaxError: invalid syntax

            dpkg: error processing package odoo (--configure):
             installed odoo package post-installation script subprocess returned error exit status 1
            Processing triggers for fontconfig (2.13.1-4.2) ...
            Errors were encountered while processing:
             odoo
            perl: warning: Setting locale failed.
            perl: warning: Please check that your locale settings:
                LANGUAGE = "en_US.UTF-8",
                LC_ALL = (unset),
                LC_MONETARY = "pt_BR.UTF-8",
                LC_CTYPE = "C",
                LC_COLLATE = "C",
                LC_ADDRESS = "pt_BR.UTF-8",
                LC_TELEPHONE = "pt_BR.UTF-8",
                LC_NAME = "pt_BR.UTF-8",
                LC_MEASUREMENT = "pt_BR.UTF-8",
                LC_IDENTIFICATION = "pt_BR.UTF-8",
                LC_NUMERIC = "pt_BR.UTF-8",
                LC_PAPER = "pt_BR.UTF-8",
                LANG = "en_US.UTF-8"
                are supported and installed on your system.
            perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
            perl: warning: Setting locale failed.
            perl: warning: Please check that your locale settings:
                LANGUAGE = "en_US.UTF-8",
                LC_ALL = (unset),
                LC_CTYPE = "C",
                LC_MONETARY = "pt_BR.UTF-8",
                LC_COLLATE = "C",
                LC_ADDRESS = "pt_BR.UTF-8",
                LC_TELEPHONE = "pt_BR.UTF-8",
                LC_NAME = "pt_BR.UTF-8",
                LC_MEASUREMENT = "pt_BR.UTF-8",
                LC_IDENTIFICATION = "pt_BR.UTF-8",
                LC_NUMERIC = "pt_BR.UTF-8",
                LC_PAPER = "pt_BR.UTF-8",
                LANG = "en_US.UTF-8"
                are supported and installed on your system.
            perl: warning: Falling back to a fallback locale ("en_US.UTF-8").
            [master 25d3f4e] committing changes in /etc made by "apt-get install odoo"
             24 files changed, 108 insertions(+), 8 deletions(-)
             create mode 120000 fonts/conf.d/61-urw-bookman.conf
             create mode 120000 fonts/conf.d/61-urw-c059.conf
             create mode 120000 fonts/conf.d/61-urw-d050000l.conf
             create mode 120000 fonts/conf.d/61-urw-fallback-backwards.conf
             create mode 120000 fonts/conf.d/61-urw-fallback-generics.conf
             create mode 120000 fonts/conf.d/61-urw-gothic.conf
             create mode 120000 fonts/conf.d/61-urw-nimbus-mono-ps.conf
             create mode 120000 fonts/conf.d/61-urw-nimbus-roman.conf
             create mode 120000 fonts/conf.d/61-urw-nimbus-sans.conf
             create mode 120000 fonts/conf.d/61-urw-p052.conf
             create mode 120000 fonts/conf.d/61-urw-standard-symbols-ps.conf
             create mode 120000 fonts/conf.d/61-urw-z003.conf
             create mode 100644 ghostscript/fontmap.d/10gsfonts.conf
             create mode 100644 logrotate.d/odoo
             create mode 120000 systemd/system/odoo.service
            Enumerating objects: 1965, done.
            Counting objects: 100% (1965/1965), done.
            Delta compression using up to 8 threads
            Compressing objects: 100% (1221/1221), done.
            Writing objects: 100% (1965/1965), done.
            Total 1965 (delta 134), reused 1915 (delta 118), pack-reused 0
            E: Sub-process /usr/bin/dpkg returned an error code (1)

        ::

            # apt-get remove odoo

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo17-vm-17 -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. Set "**/etc/init.d/odoo**" file Permitions:

        * Allow executing file as program: **marked**.

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        :bmaroon:`Alerta! (Outdated python version detected, Odoo requires Python >= 3.10 to run.)`

        ::

            root@tkl-odoo17-vm-17 ~# su odoo
            ntp@tkl-odoo17-vm-17:/root$ cd /opt/odoo
            ntp@tkl-odoo17-vm-17:/opt/odoo$ /usr/bin/odoo -c /etc/odoo/odoo-man.conf
            Traceback (most recent call last):
              File "/usr/bin/odoo", line 5, in <module>
                import odoo
              File "/usr/lib/python3/dist-packages/odoo/__init__.py", line 21, in <module>
                assert sys.version_info > MIN_PY_VERSION, f"Outdated python version detected, Odoo requires Python >= {'.'.join(map(str, MIN_PY_VERSION))} to run."
            AssertionError: Outdated python version detected, Odoo requires Python >= 3.10 to run.
            ntp@tkl-odoo17-vm-17:/opt/odoo$

            python3 --version
            Python 3.9.2

:bmaroon:`Backup:` :blue:`tkl-odoo17-vm-17_2024-10-25b.rar`

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. :bmaroon:`(Not Implemented)` To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo17-vm-17 -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025_16"

            dropdb -i clvhealth_jcafb_2025_16

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

    #. To install yaml, use the following commands (as root):

        ::

            pip3 install pyyaml --break-system-packages

        ::

            pip3 install pyyaml --break-system-packages
            Collecting pyyaml
              Downloading PyYAML-6.0.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (757 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 757.7/757.7 kB 4.5 MB/s eta 0:00:00
            Installing collected packages: pyyaml
            Successfully installed pyyaml-6.0.1
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

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

            root@tkl-odoo17-vm-17 ~# pip3 install -U Jinja2
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

            ssh tkl-odoo17-vm-17 -l odoo

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

            ssh tkl-odoo17-vm-17 -l root

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
            
    #. :red:`(Failed - Not Used)` To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            pip3 install erpbrasil.base
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

    #. To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            pip3 install erpbrasil.base --break-system-packages
            Collecting erpbrasil.base
              Downloading erpbrasil.base-2.3.0-py2.py3-none-any.whl (13 kB)
            Installing collected packages: erpbrasil.base
            Successfully installed erpbrasil.base-2.3.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. :red:`(Failed - Not Used)` To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            # pip3 install pycep-correios
            # Não utilizar versões > 5.1.0
            #   'pycep-correios' is now 'brazilcep' 
            #   (This package has been renamed. Use pip install brazilcep instead.)
            #   https://pypi.org/project/pycep-correios/
            #   (New package: https://pypi.org/project/brazilcep/)
            pip3 install pycep-correios==5.1.0
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

    #. To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            # pip3 install pycep-correios --break-system-packages
            # Não utilizar versões > 5.1.0
            #   'pycep-correios' is now 'brazilcep' 
            #   (This package has been renamed. Use pip install brazilcep instead.)
            #   https://pypi.org/project/pycep-correios/
            #   (New package: https://pypi.org/project/brazilcep/)
            pip3 install pycep-correios==5.1.0 --break-system-packages
            Collecting pycep-correios==5.1.0
              Downloading pycep_correios-5.1.0-py2.py3-none-any.whl (7.1 kB)
            Requirement already satisfied: requests>=2.7.0 in /usr/lib/python3/dist-packages (from pycep-correios==5.1.0) (2.28.1)
            Requirement already satisfied: zeep>=2.0.0 in /usr/lib/python3/dist-packages (from pycep-correios==5.1.0) (4.2.1)
            Installing collected packages: pycep-correios
            Successfully installed pycep-correios-5.1.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

:bmaroon:`(Not Implemented)` Upgrade the odoo software
------------------------------------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo17-vm-17 -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo17-vm-17 -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo17-vm-17
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
