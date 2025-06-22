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

.. index:: Criação do Servidor de Testes na AWS clvheatlh-jcafb-2026-aws-tst

===================================================================
Criação do Servidor de Testes na AWS "clvheatlh-jcafb-2026-aws-tst"
===================================================================

    This project will help you create a server to host the **Odoo 16 (CLVhealth-JCAFB)**, based on an `Odoo <https://www.odoo.com/>`_  appliance, in the AWS infrastructure.

Server preparation (1)
----------------------

    #. Create, via TrunKey Hub, a new Key Pair:

        * Region: **Virginia (East USA)**
        * Label: **clvheatlh-jcafb-2026-aws-tst**
        * Private Key File: **clvheatlh-jcafb-2026-aws-tst.pem**

    #. Create, via AWS Console, a new Elastic IP:

        * Region: **Virginia (East USA)**
        * Label: **clvheatlh-jcafb-2026-aws-tst**
        * IP address: **xxx**

    #. Create, via TrunKey Hub, the Amazon EC2 instance clvheatlh-jcafb-2026-aws-tst-aws:

        * Launch to Amazon EC2: **18.0**

        * Basics:

            * **Odoo**
            * TurnKey Appliance: **Odoo**
            * Hostname: **clvheatlh-jcafb-2026-aws-tst**

        * Instance:

            * Region: **Virginia (East USA)**
            * Size: **T2.Micro ($0.013/hour)**

        * Root account:

            * Root password: "*******" :red:`(It is not working for version 18.0)`
            * SSH key-pair: **clvheatlh-jcafb-2026-aws-tst**

        * Application settings:

            * PostgreSQL postgres password: "*******"
            * Odoo admin password: "*******"

        * Advanced configuration:

            * Root file system size (GB): **30**
            * Availability Zone: **Automatic**
            * Install Security Updates: **Enabled**
            * Configure Security Alerts: **Enabled**
            * Auto-associate Elastic IP: **None**


:red:`Oops! An error occured`

Sorry about this, the error has been logged and we will look into it.

If you repeatedly receive this error, please drop us a line and we will help you work around the issue until its fixed.

support@turnkeylinux.org

        * Security Group: **turnkey-odoo-4a73** (Inbound)::

            Port (Service)   Source
            -------------------------------------
            N/A(PING)        0.0.0.0/0
            22(SSH)          0.0.0.0/0
            80(HTTP)         0.0.0.0/0
            443(HTTPS)       0.0.0.0/0
            12321(Webmin)    0.0.0.0/0  (enabled)
            12322(Adminer)   0.0.0.0/0  (enabled)

    #. Prepare the **private key** "**clvheatlh-jcafb-2026-aws-tst.pem**" for use:

        #. Make a copy of the file "**clvheatlh-jcafb-2026-aws-tst.pem**":

            ::

                cp /home/mint20/Downloads/clvheatlh-jcafb-2026-aws-tst.pem /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-tst.pem

                chmod 600 /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-tst.pem

    #. Setup the "**Root password**":

        #. Log into the server using ssh using the privater key (as root):

            ::

                ssh -i /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-tst.pem clvheatlh-jcafb-2026-aws-tst -l root

        #. Update **root** password:

            ::

                passwd root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Delete the 'Turnkeylinux Example ' database, using the following procedure:

        #. Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

                /etc/init.d/odoo stop

                su odoo

        #. [clvheatlh-jcafb-2026-aws-tst] Excluir a instância do *CLVhealth-JCAFB-2022v-15* existente:

            ::

                cd /opt/odoo
                dropdb -i TurnkeylinuxExample

                cd /var/lib/odoo/.local/share/Odoo/filestore
                rm -rf TurnkeylinuxExample

        #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo manual:

            ::

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Upgrade the software:

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

Server preparation (2)
----------------------

    #. Update host name, executing the following commands:

        ::

            HOSTNAME=clvheatlh-jcafb-2026-aws-tst
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

        #. To restart the SSH service, use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establisTrunKeyh a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@clvheatlh-jcafb-2026-aws-tst

            ::

                ssh -L 33335:localhost:5432 root@clvheatlh-jcafb-2026-aws-tst

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@clvheatlh-jcafb-2026-aws-tst

            ::

                ssh -L 33335:127.0.0.1:5432 root@clvheatlh-jcafb-2026-aws-tst

Development (2)
---------------

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            cd /opt/odoo
            su odoo

            git config --global user.email "carlos.vercelino@clvsol.com"
            git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

            git config --global alias.lg "log --oneline --all --graph --decorate"

            git config --list

            exit

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
            0 upgraded, 5 newly installed, 0 to remove and 1 not upgraded.
            Need to get 2084 kB of archives.
            After this operation, 10.6 MB of additional disk space will be used.
            Do you want to continue? [Y/n] 
            Get:1 http://deb.debian.org/debian bookworm/main amd64 python3-lib2to3 all 3.11.2-3 [76.3 kB]
            Get:2 http://deb.debian.org/debian bookworm/main amd64 python3-distutils all 3.11.2-3 [131 kB]
            Get:3 http://deb.debian.org/debian bookworm/main amd64 python3-setuptools all 66.1.1-1 [521 kB]
            Get:4 http://deb.debian.org/debian bookworm/main amd64 python3-wheel all 0.38.4-2 [30.8 kB]
            Get:5 http://deb.debian.org/debian bookworm/main amd64 python3-pip all 23.0.1+dfsg-1 [1325 kB]
            Fetched 2084 kB in 0s (45.7 MB/s) 
            debconf: delaying package configuration, since apt-utils is not installed
            Selecting previously unselected package python3-lib2to3.
            (Reading database ... 90350 files and directories currently installed.)
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

Development (3)
---------------

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
            * `System configuration <https://www.odoo.com/documentation/16.0/administration/install/deploy.html>`_

            ::

                workers = 0

            ::

                # workers = 0
                # workers = 3
                workers = 2

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `Sample odoo.conf file  <https://gist.github.com/Guidoom/d5db0a76ce669b139271a528a8a2a27f>`_
            * `How to Speed up Odoo <https://www.rosehosting.com/blog/how-to-speed-up-odoo/>`_
            * `What is a “worker” in Odoo? <https://stackoverflow.com/questions/35918633/what-is-a-worker-in-odoo>`_
            * `System configuration <https://www.odoo.com/documentation/16.0/administration/install/deploy.html>`_

            ::

                max_cron_threads = 2

            ::

                # max_cron_threads = 2
                max_cron_threads = 1

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = base,web

            ::

                # server_wide_modules = base,web
                server_wide_modules = None

Replace the Odoo installation (Odoo 15.0)
-----------------------------------------

    #. To replace the Odoo installation (Odoo 15.0), use the following commands (as root) "`Install Odoo 15 on Debian 10 / Debian 11 <https://computingforgeeks.com/how-to-install-odoo-on-debian-linux/>`_":

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

        ::

            apt install gnupg2

            wget https://nightly.odoo.com/odoo.key

            cat odoo.key | gpg --dearmor | tee /etc/apt/trusted.gpg.d/odoo.gpg  >/dev/null

            echo "deb http://nightly.odoo.com/15.0/nightly/deb/ ./" | tee /etc/apt/sources.list.d/odoo.list

            apt-get update

            apt-get install odoo

        ::

            apt-get install odoo
            Reading package lists... Done
            Building dependency tree... Done
            Reading state information... Done
            The following packages were automatically installed and are no longer required:
              fonts-glyphicons-halflings fonts-ocr-b libjs-jquery-form
            Use 'apt autoremove' to remove them.
            The following additional packages will be installed:
              python3-mock python3-pbr
            Suggested packages:
              python-mock-doc
            Recommended packages:
              python3-ldap
            The following packages will be REMOVED:
              odoo-16
            The following NEW packages will be installed:
              odoo python3-mock python3-pbr
            0 upgraded, 3 newly installed, 1 to remove and 1 not upgraded.
            Need to get 198 MB of archives.
            After this operation, 3087 kB disk space will be freed.
            Do you want to continue? [Y/n] Y
            Get:1 http://deb.debian.org/debian bookworm/main amd64 python3-pbr all 5.10.0-2 [61.4 kB]
            Get:2 http://deb.debian.org/debian bookworm/main amd64 python3-mock all 4.0.3-4 [64.0 kB]
            Get:3 http://nightly.odoo.com/15.0/nightly/deb ./ odoo 15.0.20240714 [198 MB]      
            Fetched 198 MB in 11s (17.9 MB/s)                                                                                                                                     
            debconf: delaying package configuration, since apt-utils is not installed
            (Reading database ... 91415 files and directories currently installed.)
            Removing odoo-16 (16.0.0+dfsg.2-3~bpo12+1) ...
            Selecting previously unselected package python3-pbr.
            (Reading database ... 50831 files and directories currently installed.)
            Preparing to unpack .../python3-pbr_5.10.0-2_all.deb ...
            Unpacking python3-pbr (5.10.0-2) ...
            Selecting previously unselected package python3-mock.
            Preparing to unpack .../python3-mock_4.0.3-4_all.deb ...
            Unpacking python3-mock (4.0.3-4) ...
            Selecting previously unselected package odoo.
            Preparing to unpack .../odoo_15.0.20240714_all.deb ...
            Unpacking odoo (15.0.20240714) ...
            Setting up python3-pbr (5.10.0-2) ...
            Setting up python3-mock (4.0.3-4) ...
            Setting up odoo (15.0.20240714) ...

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

        ::

            # apt-get remove odoo

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo15-jcafb24-vm -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. Set the **postgres** user password (PostgreSQL Database Server) using Webmin.

    #. Set "**/etc/init.d/odoo**" file Permitions:

        * Allow executing file as program: **marked**.

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. :red:`(Not Used)` Install **basic dependencies** needed by Brazilian Localization, using the following commands (as root):

        #. To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                pip3 install erpbrasil.base

        #. To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                # pip3 install pycep-correios
                # Não utilizar versões > 5.1.0
                #   'pycep-correios' is now 'brazilcep' 
                #   (This package has been renamed. Use pip install brazilcep instead.)
                #   https://pypi.org/project/pycep-correios/
                #   (New package: https://pypi.org/project/brazilcep/)
                pip3 install pycep-correios==5.1.0

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l odoo

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            pip3 install erpbrasil.base --break-system-packages
            Collecting erpbrasil.base
              Downloading erpbrasil.base-2.3.0-py2.py3-none-any.whl (13 kB)
            Installing collected packages: erpbrasil.base
            Successfully installed erpbrasil.base-2.3.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. :red:`(Failed - Not Used)` To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb"

            dropdb -i clvhealth_jcafb

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l odoo

        ::

            /etc/init.d/odoo stop

        ::

            # ***** clvheatlh-jcafb-2020-aws-pro
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

:red:`Não Executado`
--------------------

    #. :red:`(Not Used)` To install odoolib (for python 3.5), use the following commands (as root):

        ::

            pip3 install odoo-client-lib

    #. Install **basic dependencies** needed by Brazilian Localization, using the following commands (as root):

        #. To install "`node-less <https://github.com/odoo/odoo/issues/16463>`_", use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                apt-get install node-less

        #. To install "`suds-py3 <https://stackoverflow.com/questions/46043345/how-use-suds-client-library-in-python-3-6-2>`_", use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                pip3 install suds-py3
