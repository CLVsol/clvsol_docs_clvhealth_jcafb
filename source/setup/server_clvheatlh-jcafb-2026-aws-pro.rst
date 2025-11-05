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

.. index:: Criação do Servidor de Testes na AWS clvheatlh-jcafb-2026-aws-pro

===================================================================
Criação do Servidor de Testes na AWS "clvheatlh-jcafb-2026-aws-pro"
===================================================================

    This project will help you create a server to host the **Odoo 16 (CLVhealth-JCAFB)**, based on an `Odoo <https://www.odoo.com/>`_  appliance, in the AWS infrastructure.

Server preparation (1)
----------------------

    #. Create, via TrunKey Hub, a new Key Pair:

        * Region: **Virginia (East USA)**
        * Label: **clvheatlh-jcafb-2026-aws-pro**
        * Private Key File: **clvheatlh-jcafb-2026-aws-pro.pem**

    #. Create, via TrunKey Hub, the Amazon EC2 instance clvheatlh-jcafb-2026-aws-pro-aws:

        * Launch to Amazon EC2: **18.0**

        * Basics:

            * **Odoo**
            * TurnKey Appliance: **Odoo**
            * Hostname: **clvheatlh-jcafb-2026-aws-pro**

        * Instance:

            * Region: **Virginia (East USA)**
            * Size: **T2.Medium ($0.052/hour)** (RAM: 4 GB CPU: 2 vCPU NET: Low to Mod)

        * Root account:

            * Root password: "*******" :red:`(It is not working for version 18.0)`
            * SSH key-pair: **clvheatlh-jcafb-2026-aws-pro**

        * Application settings:

            * PostgreSQL postgres password: "*******"
            * Odoo admin password: "*******"

        * Advanced configuration:

            * Root file system size (GB): **30**
            * Availability Zone: **Automatic**
            * Install Security Updates: **Enabled**
            * Configure Security Alerts: **Enabled**
            * Auto-associate Elastic IP: **None**

        * Security Group: **turnkey-odoo-6939** (Inbound)::

            Port (Service)   Source
            -------------------------------------
            N/A(PING)        0.0.0.0/0
            22(SSH)          0.0.0.0/0
            80(HTTP)         0.0.0.0/0
            443(HTTPS)       0.0.0.0/0
            12321(Webmin)    0.0.0.0/0  (enabled)
            12322(Adminer)   0.0.0.0/0  (enabled)

    #. Create, via AWS Console, a new Elastic IP:

        * Region: **Virginia (East USA)**
        * Label: **clvheatlh-jcafb-2026-aws-pro**
        * IP address: **100.29.168.114**

    #. Prepare the **private key** "**clvheatlh-jcafb-2026-aws-pro.pem**" for use:

        #. Make a copy of the file "**clvheatlh-jcafb-2026-aws-pro.pem**":

            ::

                cp /home/mint20/Downloads/clvheatlh-jcafb-2026-aws-pro.pem /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-pro.pem

                chmod 600 /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-pro.pem

    #. Setup the "**Root password**":

        #. Log into the server using ssh using the privater key (as root):

            ::

                ssh -i /home/mint20/.ssh/clvheatlh-jcafb-2026-aws-pro.pem clvheatlh-jcafb-2026-aws-pro -l root

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

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-pro -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

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

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Delete the 'Turnkeylinux Example ' database, using the following procedure:

        #. Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

            ::

                ssh clvheatlh-jcafb-2026-aws-pro -l root

                /etc/init.d/odoo stop

                su odoo

        #. [clvheatlh-jcafb-2026-aws-pro] Excluir a instância do *CLVhealth-JCAFB-2022v-15* existente:

            ::

                cd /opt/odoo
                dropdb -i TurnkeylinuxExample

                cd /var/lib/odoo/.local/share/Odoo/filestore
                rm -rf TurnkeylinuxExample

        #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo manual:

            ::

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Upgrade the software:

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

Server preparation (2)
----------------------

    #. Update host name, executing the following commands:

        ::

            HOSTNAME=clvheatlh-jcafb-2026-aws-pro
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

                ssh clvheatlh-jcafb-2026-aws-pro -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establisTrunKeyh a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@clvheatlh-jcafb-2026-aws-pro

            ::

                ssh -L 33335:localhost:5432 root@clvheatlh-jcafb-2026-aws-pro

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@clvheatlh-jcafb-2026-aws-pro

            ::

                ssh -L 33335:127.0.0.1:5432 root@clvheatlh-jcafb-2026-aws-pro

Development (2)
---------------

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

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

    #. To install yaml, use the following commands (as root):

        ::

            pip3 install pyyaml --break-system-packages

        ::

            pip3 install pyyaml --break-system-packages
            Collecting pyyaml
              Downloading pyyaml-6.0.3-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (806 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 806.6/806.6 kB 23.0 MB/s eta 0:00:00
            Installing collected packages: pyyaml
            Successfully installed pyyaml-6.0.3
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
                workers = 3

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `Sample odoo.conf file  <https://gist.github.com/Guidoom/d5db0a76ce669b139271a528a8a2a27f>`_
            * `How to Speed up Odoo <https://www.rosehosting.com/blog/how-to-speed-up-odoo/>`_
            * `What is a “worker” in Odoo? <https://stackoverflow.com/questions/35918633/what-is-a-worker-in-odoo>`_
            * `System configuration <https://www.odoo.com/documentation/16.0/administration/install/deploy.html>`_

            ::

                max_cron_threads = 2

            ::

                # max_cron_threads = 2
                # max_cron_threads = 1
                max_cron_threads = 2

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = base,web

            ::

                # server_wide_modules = base,web
                server_wide_modules = None

    #. To install pandas, use the following commands (as root):

        ::

            pip3 install pandas --break-system-packages

        ::

            pip3 install pandas --break-system-packages
            Collecting pandas
              Downloading pandas-2.3.3-cp311-cp311-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (12.8 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.8/12.8 MB 87.6 MB/s eta 0:00:00
            Collecting numpy>=1.23.2
              Downloading numpy-2.3.4-cp311-cp311-manylinux_2_27_x86_64.manylinux_2_28_x86_64.whl (16.9 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.9/16.9 MB 74.3 MB/s eta 0:00:00
            Requirement already satisfied: python-dateutil>=2.8.2 in /usr/lib/python3/dist-packages (from pandas) (2.8.2)
            Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3/dist-packages (from pandas) (2022.7.1)
            Collecting tzdata>=2022.7
              Downloading tzdata-2025.2-py2.py3-none-any.whl (347 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 347.8/347.8 kB 40.5 MB/s eta 0:00:00
            Installing collected packages: tzdata, numpy, pandas
            Successfully installed numpy-2.3.4 pandas-2.3.3 tzdata-2025.2
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l odoo

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

            ssh clvheatlh-jcafb-2026-aws-pro -l root

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

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            pip3 install erpbrasil.base --break-system-packages
            
            pip3 install erpbrasil.base --break-system-packages
            Collecting erpbrasil.base
              Downloading erpbrasil_base-2.4.1-py3-none-any.whl (21 kB)
            Requirement already satisfied: wheel in /usr/lib/python3/dist-packages (from erpbrasil.base) (0.38.4)
            Installing collected packages: erpbrasil.base
            Successfully installed erpbrasil.base-2.4.1
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install phonenumbers, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            pip3 install phonenumbers --break-system-packages

            pip3 install phonenumbers --break-system-packages
            Collecting phonenumbers
              Downloading phonenumbers-9.0.17-py2.py3-none-any.whl (2.6 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.6/2.6 MB 40.1 MB/s eta 0:00:00
            Installing collected packages: phonenumbers
            Successfully installed phonenumbers-9.0.17
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install email-validator, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            pip3 install email-validator --break-system-packages

            pip3 install email-validator --break-system-packages
            Collecting email-validator
              Downloading email_validator-2.3.0-py3-none-any.whl (35 kB)
            Collecting dnspython>=2.0.0
              Downloading dnspython-2.8.0-py3-none-any.whl (331 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 331.1/331.1 kB 15.9 MB/s eta 0:00:00
            Requirement already satisfied: idna>=2.0.0 in /usr/lib/python3/dist-packages (from email-validator) (3.3)
            Installing collected packages: dnspython, email-validator
            Successfully installed dnspython-2.8.0 email-validator-2.3.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install brazilcep, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            pip3 install brazilcep --break-system-packages

            pip3 install brazilcep --break-system-packages
            Collecting brazilcep
              Downloading brazilcep-7.0.1-py3-none-any.whl (15 kB)
            Collecting requests>=2.28.2
              Downloading requests-2.32.5-py3-none-any.whl (64 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 64.7/64.7 kB 3.4 MB/s eta 0:00:00
            Collecting aiohttp>=3.8.1
              Downloading aiohttp-3.13.2-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (1.7 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 49.4 MB/s eta 0:00:00
            Collecting aiohappyeyeballs>=2.5.0
              Downloading aiohappyeyeballs-2.6.1-py3-none-any.whl (15 kB)
            Collecting aiosignal>=1.4.0
              Downloading aiosignal-1.4.0-py3-none-any.whl (7.5 kB)
            Requirement already satisfied: attrs>=17.3.0 in /usr/lib/python3/dist-packages (from aiohttp>=3.8.1->brazilcep) (22.2.0)
            Collecting frozenlist>=1.1.1
              Downloading frozenlist-1.8.0-cp311-cp311-manylinux1_x86_64.manylinux_2_28_x86_64.manylinux_2_5_x86_64.whl (231 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 231.1/231.1 kB 31.9 MB/s eta 0:00:00
            Collecting multidict<7.0,>=4.5
              Downloading multidict-6.7.0-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (246 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 246.7/246.7 kB 37.7 MB/s eta 0:00:00
            Collecting propcache>=0.2.0
              Downloading propcache-0.4.1-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (210 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 210.0/210.0 kB 24.6 MB/s eta 0:00:00
            Collecting yarl<2.0,>=1.17.0
              Downloading yarl-1.22.0-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (365 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 365.8/365.8 kB 45.1 MB/s eta 0:00:00
            Requirement already satisfied: charset_normalizer<4,>=2 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.0.1)
            Requirement already satisfied: idna<4,>=2.5 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.3)
            Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (1.26.12)
            Requirement already satisfied: certifi>=2017.4.17 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (2022.9.24)
            Requirement already satisfied: typing-extensions>=4.2 in /usr/lib/python3/dist-packages (from aiosignal>=1.4.0->aiohttp>=3.8.1->brazilcep) (4.4.0)
            Installing collected packages: requests, propcache, multidict, frozenlist, aiohappyeyeballs, yarl, aiosignal, aiohttp, brazilcep
              Attempting uninstall: requests
                Found existing installation: requests 2.28.1
                Not uninstalling requests at /usr/lib/python3/dist-packages, outside environment /usr
                Can't uninstall 'requests'. No files were found to uninstall.
            Successfully installed aiohappyeyeballs-2.6.1 aiohttp-3.13.2 aiosignal-1.4.0 brazilcep-7.0.1 frozenlist-1.8.0 multidict-6.7.0 propcache-0.4.1 requests-2.32.5 yarl-1.22.0
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb"

            dropdb -i clvhealth_jcafb

Replace the Odoo installation (Odoo 16.0)
-----------------------------------------

    #. Remover o banco de dados *CLVhealth-JCAFB-2026-16*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            cd /opt/odoo

            dropdb -i clvhealth_jcafb_2026_16

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16

    #. To replace the Odoo installation (Odoo 16.0), use the following commands (as root) "`Install Odoo 15 on Debian 10 / Debian 11 <https://computingforgeeks.com/how-to-install-odoo-on-debian-linux/>`_":

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

        ::

            apt install gnupg2

            wget https://nightly.odoo.com/odoo.key

            cat odoo.key | gpg --dearmor | tee /etc/apt/trusted.gpg.d/odoo.gpg  >/dev/null

            echo "deb http://nightly.odoo.com/16.0/nightly/deb/ ./" | tee /etc/apt/sources.list.d/odoo.list

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
            Recommended packages:
              python3-ldap
            The following packages will be REMOVED:
              odoo-16
            The following NEW packages will be installed:
              odoo
            0 upgraded, 1 newly installed, 1 to remove and 1 not upgraded.
            Need to get 208 MB of archives.
            After this operation, 194 MB of additional disk space will be used.
            Do you want to continue? [Y/n] Y
            Get:1 http://nightly.odoo.com/16.0/nightly/deb ./ odoo 16.0.20251104 [208 MB]
            Fetched 208 MB in 25s (8284 kB/s)                                                                                                                                    
            debconf: delaying package configuration, since apt-utils is not installed
            (Reading database ... 86497 files and directories currently installed.)
            Removing odoo-16 (16.0.0+dfsg.2-2~bpo12+1) ...
            Selecting previously unselected package odoo.
            (Reading database ... 45913 files and directories currently installed.)
            Preparing to unpack .../odoo_16.0.20251104_all.deb ...
            Unpacking odoo (16.0.20251104) ...
            Setting up odoo (16.0.20251104) ...

        ::

            # apt-get remove odoo

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-pro -l root

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

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Remote access to the server (2)
-------------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025_16"

            dropdb -i clvhealth_jcafb_2025_16

