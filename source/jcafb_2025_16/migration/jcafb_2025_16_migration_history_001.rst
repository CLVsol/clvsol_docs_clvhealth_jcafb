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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2025-16]"

====================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2025-16]
====================================================

Desabilitar a instalação de todos os módulos
--------------------------------------------

    #. [tkl-odoo16-jcafb25-vm] Desabilitar a instalação de todos os módulos

Criar uma nova instância do *CLVhealth-JCAFB-2025-16*
------------------------------------------------------

    #. [tkl-odoo16-jcafb25-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo16-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb25-vm
            #

            ssh tkl-odoo16-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb25-vm] Excluir a instância do *CLVhealth-JCAFB-2025-16* existente:

        ::

            # ***** tkl-odoo16-jcafb25-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2025_16

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_16

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb25-vm** ao modo manual:

        ::

            # ***** tkl-odoo16-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo16-jcafb25-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo16-jcafb25-vm (session 2)
            #

            ssh tkl-odoo16-jcafb25-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025_16"

        * **Execution time: 0:00:27.503**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb25-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

.. toctree::   :maxdepth: 2
