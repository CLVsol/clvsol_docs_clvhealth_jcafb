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
Manutenção do Banco de Dados - JCAFB-2023-15
============================================

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-11-20a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

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

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-11-21c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-21c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Não Executado)` [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvheatlh-jcafb-2023-aws-tst**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-05a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

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

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-05c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-05c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-05c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-07a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

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

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-07a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-07a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-11a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-11a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-11a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-11a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-13b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-13b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-13b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-13b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-15a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-15a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-15a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-15a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-19a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-19a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-19a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-19a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-19a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-19a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-20b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-20b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-20b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-20b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-20b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-20b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-20c)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-20c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-20c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-20c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-20c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-20c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-27b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-27b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-27b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-27b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-27b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-27b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2022-12-28a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-28a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2022-12-28a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-28a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-28a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-28a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2023-01-03a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-03a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-03a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-03a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-03a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-03a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-03a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-04a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-04a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-04a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-04a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-04a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-04a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-04a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-04a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-04a)
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-04a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-04a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Atualizar os fontes do projeto (2023-01-05a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-04a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-04a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-04a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-05a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-05a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-05a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-05a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-05a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-05a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-05a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-05a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05a

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-05a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-05a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2023-01-05a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-05a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-05a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05b)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-05b.sql

            gzip clvhealth_jcafb_2023_15_2023-01-05b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-05b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-05b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-05b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-05b.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-05b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-05b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-05b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-05b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-05b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-05b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05b)
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-05b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-05b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-05b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-13a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-13a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-13a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-13a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-13a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-13a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-13a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-13a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-13a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a

[clvheatlh-jcafb-2023-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-13a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-13a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-13a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-pro <https://clvheatlh-jcafb-2023-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://44.210.61.227**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-13a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-13a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-13a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-13a)
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-13a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-13a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Atualizar os fontes do projeto (2023-01-14a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-14a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-14a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-14a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-14a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-14a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-14a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-14a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-14a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-14a

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2023-01-14a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-14a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-14a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-14a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-14a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-14a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-14a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-14a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-15a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-15a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-15a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-15a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-15a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-15a

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-15a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-15a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-15a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-15a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-15a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-15a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-17a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-17a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-17a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-17a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-17a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-17a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-17a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-17a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-17a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17a

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-17a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-17a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-17a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-17b)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-17b.sql

            gzip clvhealth_jcafb_2023_15_2023-01-17b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-17b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-17b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-17b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-17b.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-17b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-17b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17b

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-17b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-17b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-17b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-17b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-17b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-17b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-17b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-18a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-18a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-18a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-18a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-18a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-18a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-18a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-18a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-18a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-18a

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-18a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-18a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-18a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-18a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-18a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-18a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-18a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2023-aws-pro] Atualizar os fontes do projeto (2023-01-19a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

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

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

[clvheatlh-jcafb-2023-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-19a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            ssh clvheatlh-jcafb-2023-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-19a.sql

            gzip clvhealth_jcafb_2023_15_2023-01-19a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-01-19a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-19a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-01-19a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-01-19a.sql
.. index:: clvhealth_jcafb_2023_15_2023-01-19a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-01-19a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-19a

[clvheatlh-jcafb-2023-aws-tst] Atualizar os fontes do projeto (2023-01-19a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2023-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

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

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

[clvheatlh-jcafb-2023-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-19a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2023-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2023-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            ssh clvheatlh-jcafb-2023-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2023-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2023_15_2023-01-19a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-19a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2023-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2023-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2023-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2023-aws-tst <https://clvheatlh-jcafb-2023-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://15.229.54.255**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb23-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-19a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-19a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-19a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-19a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
