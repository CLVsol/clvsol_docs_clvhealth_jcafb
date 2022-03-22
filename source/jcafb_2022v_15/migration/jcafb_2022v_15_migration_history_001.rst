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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2022v-15]"

=====================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2022v-15]
=====================================================

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo15-jcafb22-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

:borange:`(**)` Atualizar os fontes do projeto
----------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb22-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo15-jcafb22-vm
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

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_verification
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_export
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_process
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Criar uma nova instância do *CLVhealth-JCAFB-2022v-15*
------------------------------------------------------

    #. [tkl-odoo15-jcafb22-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb22-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            ssh tkl-odoo15-jcafb22-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb22-vm] Excluir a instância do *CLVhealth-JCAFB-2022v-15* existente:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2022v_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2022v_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb22-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb22-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb22-vm (session 2)
            #

            ssh tkl-odoo15-jcafb22-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2022v_15"

        * **Execution time: 0:05:44.773**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb22-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb22-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2022v-15* (2022-03-22a)
--------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb22-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb22-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            ssh tkl-odoo15-jcafb22-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb22-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2022v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2022v_15_2022-03-22a.sql

            gzip clvhealth_jcafb_2022v_15_2022-03-22a.sql
            pg_dump clvhealth_jcafb_2022v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2022v_15_2022-03-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz clvhealth_jcafb_2022v_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb22-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2022v_15_2022-03-22a.sql
        * /opt/odoo/clvhealth_jcafb_2022v_15_2022-03-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz

.. index:: clvhealth_jcafb_2022v_15_2022-03-22a.sql
.. index:: clvhealth_jcafb_2022v_15_2022-03-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2022v_15_2022-03-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2022v_15_2022-03-22a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2022v-15* (2022-03-22a)
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb22-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb22-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            ssh tkl-odoo15-jcafb22-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb22-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2022v_15_2022-03-22a.sql.gz

            dropdb -i clvhealth_jcafb_2022v_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2022v_15
            psql -f clvhealth_jcafb_2022v_15_2022-03-22a.sql -d clvhealth_jcafb_2022v_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2022v_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2022v_15_2022-03-22a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb22-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb22-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb22-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb22-vm <https://tkl-odoo15-jcafb22-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb22-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
