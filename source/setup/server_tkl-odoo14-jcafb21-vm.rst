.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Servidor Local tkl-odoo14-jcafb21-vm

=================================================
Criação do Servidor Local "tkl-odoo14-jcafb21-vm"
=================================================

This project will help you create a server to host the **CLVhealth-JCAFB**, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstation infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-16.0-buster-amd64.iso**".


    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-16.0-buster-amd64.iso**".

VM preparation
--------------

    #. Create a new Virtual Machine using the following parameters:

        - Choose the "**Custom (advanced)**" configuration type
        - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
        - Choose the gest operating system: **I will install the operating system later**
        - Select the Guest Operatin System: **Linux** (Version: **Debian 10.x 64-bit**)
        - Set a VM Name and a VM Location of your preference (**tkl-odoo14-jcafb21-vm** - **D:\\vm\\tkl-odoo14-jcafb21-vm**).
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

            ssh tkl-odoo14-jcafb21-vm -l root

            confconsole

    #. To execute the **Interactive System Initialization**:

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

            turnkey-init

    #. Upgrade the software:

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:110:118::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:110:118::/var/lib/odoo:/bin/bash

    #. :red:`(Not Used)` Set the **Odoo Master Account** password:

        #. Edit the file "**/etc/odoo/odoo.conf**" (as odoo):

            ::

                admin_passwd = $pbkdf2-sha512$25000$...

            ::

                ;admin_passwd = admin

        #. Stop and start the Odoo server, using the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                /etc/init.d/odoo stop

                /etc/init.d/odoo start

        #. Please set a master password to secure it:

            * `How to Recover/Change Master Password in Odoo <https://www.youtube.com/watch?v=SJlM6jUslxk>`_

    #. Update host name, executing the following commands:

        ::

            HOSTNAME=tkl-odoo14-jcafb21-vm
            echo "$HOSTNAME" > /etc/hostname
            sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
            # /etc/init.d/hostname.sh start

    #. Change the timezone, executing the following command and picking out the time zone from a list:

        ::

            dpkg-reconfigure tzdata

        * Geographic area: **America**
        * Time Zone: **Sao Paulo**

    #. :red:`(Not Used)` Set the time and date manually, executing the following command:

        ::

            date -set="STRING"

        * STRING: **19 JUL 2018 15:06:00**

    #. Enable **Connecting through SSH tunnel**:

        * `Solving SSH “channel 3: open failed: administratively prohibited” error when tunnelling <https://blog.mypapit.net/2012/06/solving-ssh-channel-3-open-failed-administratively-prohibited-error-when-tunnelling.html>`_ 
        * `Secure TCP/IP Connections with SSH Tunnels <https://www.postgresql.org/docs/9.1/static/ssh-tunnels.html>`_ 
        * `Using an SSH Tunnel <http://confluence.dbvis.com/display/UG91/Using+an+SSH+Tunnel>`_ 

        #. Edit the file "**/etc/ssh/sshd_config**" (as root):

            ::

                AllowTcpForwarding no

            ::

                AllowTcpForwarding yes

        #. To stop and start the sshd service, use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@tkl-odoo14-jcafb21-vm

            ::

                ssh -L 33335:localhost:5432 root@tkl-odoo14-jcafb21-vm

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo14-jcafb21-vm

            ::

                ssh -L 33335:127.0.0.1:5432 root@tkl-odoo14-jcafb21-vm

Development
-----------

    #. Notes on the installation:

        #. Installation: **/usr/lib/python3/dist-packages/odoo**

        #. Configuration File: **/etc/odoo/odoo.conf**

        #. Init file: **/etc/init.d/odoo**

        #. DAEMON: **/usr/bin/odoo**

        #. LOGFILE: **/var/log/odoo/odoo-server.log**

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Copy file "**/etc/odoo/odoo.conf**" into "**/etc/odoo/odoo-man.conf**". Edit the file "**/etc/odoo/odoo-man.conf**" (as root):

        ::

            logfile = /var/log/odoo/odoo-server.log

        ::

            # logfile = /var/log/odoo/odoo-server.log
            logfile = False

    #. Setup the file "**/etc/odoo/odoo-man.conf**" (Group: odoo[118] Owner: odoo[112]) permissions, using the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf


    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Install **basic dependencies** needed by Odoo, using the following commands (as root):

        * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

            ::

                2020-06-10 00:03:29,810 2675 WARNING ? odoo.addons.base.models.res_currency: The num2words python library is not installed, amount-to-text features won't be fully available. 

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            pip3 install num2words

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            mkdir /opt/odoo

            chown -R odoo:odoo /opt/odoo

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            cd /opt/odoo
            su odoo

            git config --global user.email "carlos.vercelino@clvsol.com"
            git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

            git config --global alias.lg "log --oneline --all --graph --decorate"

            git config --list

            exit

    #. To install erppeek (for python 3.5), use the following commands (as root):

        ::

            pip3 install erppeek

    #. To install xlrd 1.2.0, execute the following commands (as root):

        ::

            pip3 install xlrd==1.2.0

    #. To install xlrd 1.1.0, execute the following commands (as root):

        ::

            pip3 install xlrd
            pip3 install xlwt
            pip3 install xlutils

        ::

            root@tkl-odoo14-jcafb21-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlrd
            Requirement already satisfied: xlrd in /usr/lib/python3/dist-packages (1.1.0)
            root@tkl-odoo14-jcafb21-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlwt
            Collecting xlwt
              Downloading https://files.pythonhosted.org/packages/44/48/def306413b25c3d01753603b1a222a011b8621aed27cd7f89cbc27e6b0f4/xlwt-1.3.0-py2.py3-none-any.whl (99kB
                100% |████████████████████████████████| 102kB 1.3MB/s 
            odoo 12.0.post20200609 requires pyldap, which is not installed.
            odoo 12.0.post20200609 requires qrcode, which is not installed.
            odoo 12.0.post20200609 requires vobject, which is not installed.
            Installing collected packages: xlwt
            Successfully installed xlwt-1.3.0
            root@tkl-odoo14-jcafb21-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlutils
            Collecting xlutils
              Downloading https://files.pythonhosted.org/packages/c7/55/e22ac73dbb316cabb5db28bef6c87044a95914f713a6e81b593f8a0d2f79/xlutils-2.0.0-py2.py3-none-any.whl (55kB)
                100% |████████████████████████████████| 61kB 1.0MB/s 
            Requirement already satisfied: xlrd>=0.7.2 in /usr/lib/python3/dist-packages (from xlutils) (1.1.0)
            Requirement already satisfied: xlwt>=0.7.4 in /usr/local/lib/python3.7/dist-packages (from xlutils) (1.3.0)
            Installing collected packages: xlutils
            Successfully installed xlutils-2.0.0

        **To Verify**:

            * :red:`odoo 12.0.post20200609 requires pyldap, which is not installed.`
            * :red:`odoo 12.0.post20200609 requires qrcode, which is not installed.`
            * :red:`odoo 12.0.post20200609 requires vobject, which is not installed.`

    #. To install xlrd 1.2.0, execute the following commands (as root):

        ::

            pip3 install xlrd==1.2.0

    #. :red:`(Not Used)` To install odoolib (for python 3.5), use the following commands (as root):

        ::

            pip3 install odoo-client-lib

    #. Install **basic dependencies** needed by Brazilian Localization, using the following commands (as root):

        #. To install "`node-less <https://github.com/odoo/odoo/issues/16463>`_", use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                apt-get install node-less

        #. To install "`suds-py3 <https://stackoverflow.com/questions/46043345/how-use-suds-client-library-in-python-3-6-2>`_", use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                pip3 install suds-py3

        #. To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                pip3 install erpbrasil.base

        #. To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

            ::

                ssh tkl-odoo14-jcafb21-vm -l root

            ::

                pip3 install pycep-correios

    #. To install yaml, use the following commands (as root):

        ::

            pip3 install pyyaml

Replace the Odoo installation (Odoo 14.0)
-----------------------------------------

    #. Delete the 'Turnkeylinux Example ' database, using the following procedure:

        #. Open a web browser and type in the Odoo URL, in my case: http://tkl-odoo14-jcafb21-vm.

        #. Click on 'Manage Databases'.

        #. Clik on 'Delete' (Delete the 'Turnkeylinux Example ' database).

    #. To replace the Odoo installation (Odoo 14.0), use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # wget -O - https://nightly.odoo.com/odoo.key | apt-key --keyring /usr/share/keyrings/odoo.gpg add -
            echo "deb [signed-by=/usr/share/keyrings/odoo.gpg] http://nightly.odoo.com/14.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list

            apt-get update

            apt-get install odoo

            # apt-get remove odoo

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Configure Odoo Server timeouts

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

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

                workers = 2

            ::

                # workers = 2
                workers = 5

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = base,web

            ::

                # server_wide_modules = base,web
                server_wide_modules = None

    #. Configure "osv_memory_age_limit"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[14.0] DeprecationWarning: The osv-memory-age-limit <https://github.com/odoo/odoo/issues/60681>`_

            ::

                osv_memory_age_l3imit = 1.0

            ::

                # osv_memory_age_limit = 1.0
                osv_memory_age_limit = False

    #. To install Jinja2-2.11.2, execute the following commands (as root):

        * Issue:

            ::

                2021-01-14 13:29:55,275 8698 WARNING clvhealth_jcafb_2021v_14 py.warnings: /usr/lib/python3/dist-packages/jinja2/sandbox.py:82: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated, and in 3.8 it will stop working
                from collections import MutableSet, MutableMapping, MutableSequence
 
        ::

            pip3 install -U Jinja2

        ::

            root@tkl-odoo14-jcafb21-vm ~# pip3 install -U Jinja2
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

            ssh tkl-odoo14-jcafb21-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 12.0
            git clone https://github.com/CLVsol/clvsol_odoo_client --branch 13.0
            git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_l10n_brazil --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_history --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_history_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_verification --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_verification_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_summary --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_summary_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_export --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_export_jcafb --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_report --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_report_jcafb --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_process --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_process_jcafb --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync_jcafb --branch 13.0to14.0
            git clone https://github.com/OCA/partner-contact oca_partner-contact --branch 13.0

    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons

        ::

            # addons_path = /usr/lib/python3/dist-packages/odoo/addons
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_odoo_addons,/opt/odoo/clvsol_odoo_addons_l10n_br,/opt/odoo/clvsol_odoo_addons_l10n_br_jcafb,/opt/odoo/clvsol_odoo_addons_jcafb,/opt/odoo/clvsol_l10n_brazil,/opt/odoo/clvsol_odoo_addons_history,/opt/odoo/clvsol_odoo_addons_history_jcafb,/opt/odoo/clvsol_odoo_addons_verification,/opt/odoo/clvsol_odoo_addons_verification_jcafb,/opt/odoo/clvsol_odoo_addons_summary,/opt/odoo/clvsol_odoo_addons_summary_jcafb,/opt/odoo/clvsol_odoo_addons_export,/opt/odoo/clvsol_odoo_addons_export_jcafb,/opt/odoo/clvsol_odoo_addons_report,/opt/odoo/clvsol_odoo_addons_report_jcafb,/opt/odoo/clvsol_odoo_addons_process,/opt/odoo/clvsol_odoo_addons_process_jcafb,/opt/odoo/clvsol_odoo_addons_sync,/opt/odoo/clvsol_odoo_addons_sync_jcafb

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo14-jcafb21-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb"

            dropdb -i clvhealth_jcafb

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l odoo

        ::

            /etc/init.d/odoo stop

        ::

            # ***** clvheatlh-jcafb-2020-aws-pro
            #

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

Repositories
------------

    #. `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

          Name of the Turnkey Linux Server.

    #. `clvsol_odoo_client (13.0) <https://github.com/CLVsol/clvsol_odoo_client>`_

          CLVsol Odoo Client.

    #. `clvsol_clvhealth_jcafb (14.0) <https://github.com/CLVsol/clvsol_clvhealth_jcafb/tree/14.0>`_

          Implemantation of CLVhealth-JCAFB-2021, the CLVsol Health Management solution for JCAFB.

    #. `clvsol_l10n_brazil (14.0) <https://github.com/CLVsol/clvsol_l10n_brazil/tree/14.0>`_

          Core da localização Brasileira do Odoo (used by CLVsol solutions)
          Este projeto contêm os módulos básicos da localização brasileira do Odoo, para uso exclusivo pelas soluções da CLVsol.
          Os módulos desse projeto deverão ser substituídos pelos módulos equivalentes do repositório `OCA/l10n-brazil (13.0) <https://github.com/OCA/l10n-brazil/tree/13.0>`_, quando disponíveis para a versão do Odoo utilizada.

    #. `OCA/l10n-brazil (12.0) <https://github.com/OCA/l10n-brazil/tree/12.0>`_

          Este projeto contêm os principais módulos da localização brasileira do Odoo.

    #. `clvsol_odoo_addons (14.0) <https://github.com/CLVsol/clvsol_odoo_addons/tree/14.0>`_

          CLVsol Odoo Addons.

    #. `clvsol_odoo_addons_jcafb (14.0) <https://github.com/CLVsol/clvsol_odoo_addons_jcafb/tree/14.0>`_

          CLVsol Odoo Addons - JCAFB customizations.

    #. `clvsol_odoo_addons_history (14.0) <https://github.com/CLVsol/clvsol_odoo_addons_history/tree/14.0>`_

          CLVsol Odoo Addons - History

    #. `clvsol_odoo_addons_history_jcafb (14.0) <https://github.com/CLVsol/clvsol_odoo_addons_history_jcafb/tree/14.0>`_

          CLVsol Odoo Addons - History - JCAFB customizations

    #. `clvsol_odoo_addons_l10n_br (14.0) <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br/tree/14.0>`_

          CLVsol Odoo Addons - Brazilian Localization.

    #. `clvsol_odoo_addons_l10n_br_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Brazilian Localization - JCAFB customizations

    #. `clvsol_odoo_addons_verification (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_verification/tree/13.0>`_

          CLVsol Odoo Addons - Verification

    #. `clvsol_odoo_addons_verification_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_verification_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Verification - JCAFB customizations

    #. `clvsol_odoo_addons_summary (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_summary/tree/13.0>`_

          CLVsol Odoo Addons - Summary

    #. `clvsol_odoo_addons_summary_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_summary_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Summary - JCAFB customizations

    #. `clvsol_odoo_addons_export (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_export/tree/13.0>`_

          CLVsol Odoo Addons - Export

    #. `clvsol_odoo_addons_export_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_export_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Export - JCAFB customizations

    #. `clvsol_odoo_addons_report (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_report/tree/13.0>`_

          CLVsol Odoo Addons - Report

    #. `clvsol_odoo_addons_report_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_report_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Report - JCAFB customizations

    #. `clvsol_odoo_addons_process (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_process/tree/13.0>`_

          CLVsol Odoo Addons - Process

    #. `clvsol_odoo_addons_process_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_process_jcafb/tree/13.0>`_

          CLVsol Odoo Addons - Process - JCAFB customizations

    #. `clvsol_odoo_addons_sync (14.0) <https://github.com/CLVsol/clvsol_odoo_addons_sync/tree/14.0>`_

          CLVsol Odoo Addons - Sync

    #. `clvsol_odoo_addons_sync_jcafb (13.0to14.0) <https://github.com/CLVsol/clvsol_odoo_addons_sync_jcafb/tree/13.0to14.0>`_

          CLVsol Odoo Addons - Sync - JCAFB customizations

References
----------

    #. Installing Odoo (12)

     * `Odoo Nightly builds <https://nightly.odoo.com/>`_ 
     * `Installing Odoo (12) <https://www.odoo.com/documentation/13.0/setup/install.html>`_ 
     * `How to install Odoo 14 on Debian 9 <https://www.rosehosting.com/blog/how-to-install-odoo-12-on-debian-9/>`_ 
     * `How to deploy Odoo 14 on Ubuntu 18.04 <https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/>`_ 
