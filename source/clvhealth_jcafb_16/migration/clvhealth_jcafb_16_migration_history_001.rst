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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-16]"

===============================================
Migração do Banco de Dados [CLVhealth-JCAFB-16]
===============================================

[tkl-odoo16-vm-18] Criar uma nova instância do *CLVhealth-JCAFB-16* (2024-10-30a)
---------------------------------------------------------------------------------

    #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. :red:`(Not Used)` Excluir a instância do *CLVhealth-JCAFB-16* existente:

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

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo16-vm-18** e executar o **create_db.py**:

        ::

            # ***** tkl-odoo16-vm-18 (session 2)
            #

            ssh tkl-odoo16-vm-18 -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 create_db.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_16"

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18 (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

[tkl-odoo16-vm-18] Instalação do(s) módulo(s) [ver lista] (2024-10-30a)
-----------------------------------------------------------------------

    #. Lista de Módulos:

        * contacts
        * base_address_extended

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. Usando a sessão ssh com o servidor **tkl-odoo16-vm-18** e executar o **/usr/bin/odoo**:

        ::

            /usr/bin/odoo -c /etc/odoo/odoo-man.conf -d clvhealth_jcafb_16 -i contacts,base_address_extended,l10n_br_base,l10n_br_zip --stop-after-init

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18 (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. Lista de Aplicativos instalados a partir da instalação de "**contacts**":

        * project
        * mass_mailing
        * hr
        * mail
        * contacts
        * survey

[tkl-odoo16-vm-18] Instalar o(s) módulo(s) [ver lista]
------------------------------------------------------

    #. [tkl-odoo16-vm-18] Editar o arquivo **/opt/odoo/clvsol_clvhealth_jcafb/project/install.py**, **adicionando/habilitando** o(s) Módulo(s):

        * l10n_br_base
        * l10n_br_zip

    #. [tkl-odoo16-vm-18] **Executar** a instalação do(s) Módulo(s) adicionado(s)/habilitado(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo16-vm-18** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo16-vm-18 (session 1)
                #

                ssh tkl-odoo16-vm-18 -l root

                /etc/init.d/odoo stop

                su odoo
                
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo16-vm-18** e executar o **install.py**:

            ::

                # ***** tkl-odoo16-vm-18 (session 2)
                #

                ssh tkl-odoo16-vm-18 -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_16"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

            ::

                # ***** tkl-odoo16-vm-18 (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-30b)
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
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2024-10-30b.sql

            gzip clvhealth_jcafb_16_2024-10-30b.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2024-10-30b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_16_2024-10-30b.sql
        * /opt/odoo/clvhealth_jcafb_16_2024-10-30b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz

.. index:: clvhealth_jcafb_16_2024-10-30b.sql
.. index:: clvhealth_jcafb_16_2024-10-30b.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2024-10-30b
.. index:: clvsol_filestore_clvhealth_jcafb_16_2024-10-30b

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-30b)
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
            # gzip -d clvhealth_jcafb_16_2024-10-30b.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2024-10-30b.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2024-10-30b.tar.gz

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
