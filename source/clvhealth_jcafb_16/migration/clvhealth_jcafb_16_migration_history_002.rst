.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .bgreen {font-weight: bold; color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bblue {font-weight: bold; color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: bgreen
.. role:: blue
.. role:: bblue
.. role:: bmaroon
.. role:: borange
.. role:: bi

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-16]" (2)

===================================================
Migração do Banco de Dados [CLVhealth-JCAFB-16] (2)
===================================================

[tkl-odoo16-vm-18] Preparação do conrteúdo do arquivo "host.csv" (2024-11-12a)
------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Editar manualmente um registro (*row*) do arquivo "/opt/odoo/clvsol_clvhealth_jcafb/project/host.csv", informando as credenciais:

        * name: "**tkl-odoo16-vm-18**"
        * server: "**https://192.168.25.212**"
        * dbname: "**clvhealth_jcafb_16**"
        * user: "**admin**"
        * user_pw: "*******"
        * user_apikey: "**vazio**"
        * data_user_pw: "*******"
        * data_user_apikey: "**vazio**"
        * master_pw: "*******"
        * notes: "**vazio**"
 

[tkl-odoo16-vm-18] Criar uma nova instância do *CLVhealth-JCAFB-16* (2024-11-13a)
---------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Excluir a instância do *CLVhealth-JCAFB-16* existente:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_16

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo manual:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo16-vm-18** e executar o **install.py**:

        ::

            # ***** tkl-odoo16-vm-18 (session 2)
            #

            ssh tkl-odoo16-vm-18 -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py

        * **Execution time: 0:01:45.255**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18 (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-13a)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2024-11-13a.sql

            gzip clvhealth_jcafb_16_2024-11-13a.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2024-11-13a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2024-11-13a.sql
        * /opt/odoo/clvhealth_jcafb_16_2024-11-13a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz

.. index:: clvhealth_jcafb_16_2024-11-13a.sql
.. index:: clvhealth_jcafb_16_2024-11-13a.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2024-11-13a
.. index:: clvsol_filestore_clvhealth_jcafb_16_2024-11-13a

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-13a)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2024-11-13a.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2024-11-13a.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-11-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
