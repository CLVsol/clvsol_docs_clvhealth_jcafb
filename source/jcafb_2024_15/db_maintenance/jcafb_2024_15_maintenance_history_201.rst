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
Manutenção do Banco de Dados - JCAFB-2024-15
============================================

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-07-26a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-07-26a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-07-26a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-07-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-07-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-07-26a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            ssh clvheatlh-jcafb-2024-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-07-26a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-07-26a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-07-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-07-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-pro <https://clvheatlh-jcafb-2024-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-pro] Atualizar os fontes do projeto (2023-08-22c)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2024-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-08-22c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            ssh clvheatlh-jcafb-2024-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-08-22c.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-08-22c.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-pro <https://clvheatlh-jcafb-2024-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Atualizar os fontes do projeto (2023-08-22c)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2024-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-08-22c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-08-22c.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-08-22c.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-09-20a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-09-20a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-09-20a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-09-20a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            ssh clvheatlh-jcafb-2024-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-09-20a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-09-20a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-pro <https://clvheatlh-jcafb-2024-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-10-31a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-10-31a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-10-31a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-10-31a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-10-31a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-10-31a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            ssh clvheatlh-jcafb-2024-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-10-31a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-10-31a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-10-31a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-10-31a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-pro <https://clvheatlh-jcafb-2024-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-02a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-11-02a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-11-02a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-02a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            ssh clvheatlh-jcafb-2024-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-11-02a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-11-02a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-pro <https://clvheatlh-jcafb-2024-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-02a)
-------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #

            ssh clvheatlh-jcafb-2024n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-11-02a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-11-02a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024n-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.218.44.85**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-22a)
---------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #

            ssh clvheatlh-jcafb-2024n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-11-22a.sql

            gzip clvhealth_jcafb_2024_15_2023-11-22a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-11-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-11-22a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-11-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-11-22a.sql
.. index:: clvhealth_jcafb_2024_15_2023-11-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-11-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-22a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-22a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2024_15_2023-11-22a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-11-22a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-22a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
