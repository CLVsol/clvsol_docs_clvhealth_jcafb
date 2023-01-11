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

==================================================
Criação do Servidor Local "tkl-odoo15-jcafb23n-vm"
==================================================

    This project will help you create a server to host the **Odoo 15 (CLVhealth-JCAFB)** solution, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

        * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

        * ISO file: "**turnkey-odoo-17.1-bullseye-amd64.iso**".

VM preparation (1)
------------------

    #. This Virtual Machilne was created from a copy of the VM :doc:`/setup/server_tkl-odoo15-jcafb23-vm`"

    #. Manually Changed arameters:

        - VM Name and VM Location: **tkl-odoo15-jcafb23n-vm** - **D:\\vm\\tkl-odoo15-jcafb23n-vm**.

    #. Credentials (passwords set using **Interactive System Initialization**):

        - Webmin, SSH: username **root**
        - PostgreSQL, Adminer: username **postgres**
        - Odoo Master Account: **admin**

    #. To access the **Confconsole**:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

            confconsole

    #. To execute the **Interactive System Initialization**:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

            turnkey-init

    #. `Set Master Password <https://tkl-odoo15-jcafb23n-vm/web/database/manager>`_

        #. Copy "**admin_passwd =**" from **/etc/odoo/odoo.conf**" file to "**/etc/odoo/odoo-man.conf**" file.

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

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo15-jcafb23n-vm -l root

            ::

                passwd odoo

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Upgrade the software:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. Reinitialize the VM.

VM preparation (2)
------------------

    #. Update host name, executing the following commands:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            HOSTNAME=tkl-odoo15-jcafb23n-vm
            echo "$HOSTNAME" > /etc/hostname
            sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
            # /etc/init.d/hostname.sh start

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_15"

            dropdb -i clvhealth_jcafb_2021v_15

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo15-jcafb23n-vm
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
