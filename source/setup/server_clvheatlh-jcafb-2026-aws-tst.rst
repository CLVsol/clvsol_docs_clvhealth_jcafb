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

        * Security Group: **turnkey-odoo-2aba** (Inbound)::

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
        * Label: **clvheatlh-jcafb-2026-aws-tst**
        * IP address: **xxx**

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
              Downloading PyYAML-6.0.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (762 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 763.0/763.0 kB 17.6 MB/s eta 0:00:00
            Installing collected packages: pyyaml
            Successfully installed pyyaml-6.0.2
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
                # workers = 2
                workers = 0

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
              Downloading pandas-2.3.0-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.4 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.4/12.4 MB 70.2 MB/s eta 0:00:00
            Collecting numpy>=1.23.2
              Downloading numpy-2.3.1-cp311-cp311-manylinux_2_28_x86_64.whl (16.9 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.9/16.9 MB 61.0 MB/s eta 0:00:00
            Requirement already satisfied: python-dateutil>=2.8.2 in /usr/lib/python3/dist-packages (from pandas) (2.8.2)
            Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3/dist-packages (from pandas) (2022.7.1)
            Collecting tzdata>=2022.7
              Downloading tzdata-2025.2-py2.py3-none-any.whl (347 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 347.8/347.8 kB 47.4 MB/s eta 0:00:00
            Installing collected packages: tzdata, numpy, pandas
            Successfully installed numpy-2.3.1 pandas-2.3.0 tzdata-2025.2
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l odoo

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
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_l10n_brazil,/opt/odoo/clvsol_odoo_addons
            
    #. To install erpbrasil.base, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            pip3 install erpbrasil.base --break-system-packages

            pip3 install erpbrasil.base --break-system-packages
            Collecting erpbrasil.base
              Downloading erpbrasil.base-2.3.2-py2.py3-none-any.whl (21 kB)
            Installing collected packages: erpbrasil.base
            Successfully installed erpbrasil.base-2.3.2
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install phonenumbers, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            pip3 install phonenumbers --break-system-packages

            pip3 install phonenumbers --break-system-packages
            Collecting phonenumbers
              Downloading phonenumbers-9.0.8-py2.py3-none-any.whl (2.6 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.6/2.6 MB 36.1 MB/s eta 0:00:00
            Installing collected packages: phonenumbers
            Successfully installed phonenumbers-9.0.8
            WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

    #. To install email-validator, use the following commands (as root):

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            pip3 install brazilcep --break-system-packages

            pip3 install brazilcep --break-system-packages
            Collecting brazilcep
              Downloading brazilcep-7.0.0-py3-none-any.whl (15 kB)
            Collecting requests>=2.28.2
              Downloading requests-2.32.4-py3-none-any.whl (64 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 64.8/64.8 kB 3.4 MB/s eta 0:00:00
            Collecting aiohttp>=3.8.1
              Downloading aiohttp-3.12.13-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 47.4 MB/s eta 0:00:00
            Collecting aiohappyeyeballs>=2.5.0
              Downloading aiohappyeyeballs-2.6.1-py3-none-any.whl (15 kB)
            Collecting aiosignal>=1.1.2
              Downloading aiosignal-1.3.2-py2.py3-none-any.whl (7.6 kB)
            Requirement already satisfied: attrs>=17.3.0 in /usr/lib/python3/dist-packages (from aiohttp>=3.8.1->brazilcep) (22.2.0)
            Collecting frozenlist>=1.1.1
              Downloading frozenlist-1.7.0-cp311-cp311-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (235 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 235.3/235.3 kB 38.4 MB/s eta 0:00:00
            Collecting multidict<7.0,>=4.5
              Downloading multidict-6.6.3-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (246 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 246.6/246.6 kB 41.6 MB/s eta 0:00:00
            Collecting propcache>=0.2.0
              Downloading propcache-0.3.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (213 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 213.5/213.5 kB 32.8 MB/s eta 0:00:00
            Collecting yarl<2.0,>=1.17.0
              Downloading yarl-1.20.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (348 kB)
                 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 349.0/349.0 kB 46.7 MB/s eta 0:00:00
            Requirement already satisfied: charset_normalizer<4,>=2 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.0.1)
            Requirement already satisfied: idna<4,>=2.5 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (3.3)
            Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (1.26.12)
            Requirement already satisfied: certifi>=2017.4.17 in /usr/lib/python3/dist-packages (from requests>=2.28.2->brazilcep) (2022.9.24)
            Installing collected packages: requests, propcache, multidict, frozenlist, aiohappyeyeballs, yarl, aiosignal, aiohttp, brazilcep
              Attempting uninstall: requests
                Found existing installation: requests 2.28.1
                Not uninstalling requests at /usr/lib/python3/dist-packages, outside environment /usr
                Can't uninstall 'requests'. No files were found to uninstall.
            Successfully installed aiohappyeyeballs-2.6.1 aiohttp-3.12.13 aiosignal-1.3.2 brazilcep-7.0.0 frozenlist-1.7.0 multidict-6.6.3 propcache-0.3.2 requests-2.32.4 yarl-1.20.1
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

Replace the Odoo installation (Odoo 16.0)
-----------------------------------------

    #. :red:`(Not Used)` Remover o banco de dados *CLVhealth-JCAFB-2026-16*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            cd /opt/odoo

            dropdb -i clvhealth_jcafb_2026_16

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16

    #. To replace the Odoo installation (Odoo 16.0), use the following commands (as root) "`Install Odoo 15 on Debian 10 / Debian 11 <https://computingforgeeks.com/how-to-install-odoo-on-debian-linux/>`_":

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

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
              fonts-glyphicons-halflings fonts-ocr-b libjs-jquery-form linux-image-6.1.0-37-amd64 linux-image-6.1.0-38-amd64
            Use 'apt autoremove' to remove them.
            Recommended packages:
              python3-ldap
            The following packages will be REMOVED:
              odoo-16
            The following NEW packages will be installed:
              odoo
            0 upgraded, 1 newly installed, 1 to remove and 61 not upgraded.
            Need to get 208 MB of archives.
            After this operation, 194 MB of additional disk space will be used.
            Do you want to continue? [Y/n] Y
            Get:1 http://nightly.odoo.com/16.0/nightly/deb ./ odoo 16.0.20251120 [208 MB]
            Fetched 208 MB in 12s (17.3 MB/s)                                                                                                                                                            
            debconf: delaying package configuration, since apt-utils is not installed
            (Reading database ... 106213 files and directories currently installed.)
            Removing odoo-16 (16.0.0+dfsg.2-2~bpo12+1) ...
            userdel: user odoo is currently used by process 713777
            deluser: `/usr/sbin/userdel odoo' returned error code 8. Exiting.
            groupdel: cannot remove the primary group of user 'odoo'
            delgroup: `/sbin/groupdel odoo' returned error code 8. Exiting.
            Selecting previously unselected package odoo.
            (Reading database ... 65629 files and directories currently installed.)
            Preparing to unpack .../odoo_16.0.20251120_all.deb ...
            Unpacking odoo (16.0.20251120) ...
            Setting up odoo (16.0.20251120) ...

        ::

            # apt-get remove odoo

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh clvheatlh-jcafb-2026-aws-tst -l root

            ::

                passwd odoo


        #. :red:`(Not Used)` Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:105:114::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:105:114::/var/lib/odoo:/bin/bash

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

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Remote access to the server (2)
-------------------------------

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
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025_16"

            dropdb -i clvhealth_jcafb_2025_16

