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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-24a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-11-24a.sql

            gzip clvhealth_jcafb_2024_15_2023-11-24a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-11-24a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-11-24a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-11-24a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-11-24a.sql
.. index:: clvhealth_jcafb_2024_15_2023-11-24a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-11-24a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-24a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-11-24a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-11-24a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-11-24a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-11-24a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-01a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-01a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-01a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-01a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-01a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-01a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-01a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-01a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-01a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01a

[clvheatlh-jcafb-2024-aws-pro] Atualizar os fontes do projeto (2023-12-01b)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-01b)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-01b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-01b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz

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

[clvheatlh-jcafb-2024-aws-tst] Atualizar os fontes do projeto (2023-12-01)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-01b)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-01b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-01b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-05a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-05a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-05a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-05a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-05a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-05a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-05a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-05a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-05a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-05a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-05a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-05a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-05a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-05a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-05a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-05a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-05a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-06a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-06a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-06a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-06a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-06a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-06a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-06a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-06a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-06a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-06a

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-07a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-07a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-07a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-07a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-07a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-07a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-07a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-07a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-07a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-08a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-08a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-08a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-08a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-08a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-08a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-08a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-08a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-08a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-08a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-08a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-08a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-08a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-09a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-09a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-09a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-09a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-09a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-09a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-09a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-09a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-09a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-09a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-09a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-09a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-09a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz

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

[clvheatlh-jcafb-2024-aws-tst] Atualizar os fontes do projeto (2023-12-10a)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-10a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-10a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-10a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

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

[clvheatlh-jcafb-2024-aws-pro] Atualizar os fontes do projeto (2023-12-10a)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-10a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-10a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-10a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-11a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-11a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-11a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-11a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-11a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-11a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-11a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-11a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-11a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-12a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-12a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-12a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-12a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-12a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-12a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-12a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-12a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-12a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-12a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-12a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-12a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz

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

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14b)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-14b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-14b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14b)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-14b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-14b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

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

            * "**https://52.201.81.145**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-16a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-16a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-16a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-16a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-16a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-16a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz

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

            * "**https://52.201.81.145**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-17a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-17a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-17a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-17a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-17a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-17a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz

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

            * "**https://52.201.81.145**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Atualizar os fontes do projeto (2023-12-22a)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_summary_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-22a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-22a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-22a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz

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

[clvheatlh-jcafb-2024-aws-pro] Atualizar os fontes do projeto (2023-12-22a)
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

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull
            cd /opt/odoo
            rm -r  /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git clone https://github.com/MostlyOpen/clvsol_odoo_addons_summary_jcafb --branch 15.0

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-22a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-22a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-22a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz

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

            * "**https://52.201.81.145**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-27a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-27a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-27a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz

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

[clvheatlh-jcafb-2024-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-27a)
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
            gzip -d clvhealth_jcafb_2024_15_2023-12-27a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-27a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz

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

            * "**https://52.201.81.145**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Reinicializar o *PostgreSQL* (2024-01-08a)
-------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2024-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            ssh clvheatlh-jcafb-2024-aws-tst -l root

            /etc/init.d/odoo stop

            /etc/init.d/postgresql start

            # /etc/init.d/postgresql restart

            su odoo

    #. [clvheatlh-jcafb-2024-aws-tst] Executar os comandos de reinicializaçãpo do PostgreSQL:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            /etc/init.d/postgresql stop

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-17a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-17a.sql

            gzip clvhealth_jcafb_2024_15_2024-01-17a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-17a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-17a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-17a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-17a.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-17a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-17a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-17a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-17a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-17a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-17a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-17a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-19a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-19a.sql

            gzip clvhealth_jcafb_2024_15_2024-01-19a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-19a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-19a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-19a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-19a.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-19a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-19a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-19a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-19a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-19a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-19a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-19a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-21a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-21a.sql

            gzip clvhealth_jcafb_2024_15_2024-01-21a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-21a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-21a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-21a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-21a.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-21a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-21a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-21a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-21a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-21a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-21a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-21a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-24a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-24a.sql

            gzip clvhealth_jcafb_2024_15_2024-01-24a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-24a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-24a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-24a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-24a.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-24a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-24a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-24a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-24a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-24a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-24a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-24a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-29a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-29a.sql

            gzip clvhealth_jcafb_2024_15_2024-01-29a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-29a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-29a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-29a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-29a.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-29a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-29a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-29a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-29a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-29a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29a.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-29b)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-29b.sql

            gzip clvhealth_jcafb_2024_15_2024-01-29b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-01-29b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-29b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-01-29b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-01-29b.sql
.. index:: clvhealth_jcafb_2024_15_2024-01-29b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-01-29b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29b

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-29b)
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
            gzip -d clvhealth_jcafb_2024_15_2024-01-29b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-01-29b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-01-29b.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-02-07a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-02-07a.sql

            gzip clvhealth_jcafb_2024_15_2024-02-07a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-02-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-02-07a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-02-07a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-02-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-02-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-02-07a.sql
.. index:: clvhealth_jcafb_2024_15_2024-02-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-02-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07a

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-02-07b)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-02-07b.sql

            gzip clvhealth_jcafb_2024_15_2024-02-07b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-02-07b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-02-07b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-02-07b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-02-07b.sql
.. index:: clvhealth_jcafb_2024_15_2024-02-07b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-02-07b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07b

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-02-07b)
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
            gzip -d clvhealth_jcafb_2024_15_2024-02-07b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-02-07b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-02-07b.tar.gz

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

[clvheatlh-jcafb-2024n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-04-03a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-04-03a.sql

            gzip clvhealth_jcafb_2024_15_2024-04-03a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-04-03a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-04-03a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-04-03a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-04-03a.sql
.. index:: clvhealth_jcafb_2024_15_2024-04-03a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-04-03a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-04-03a

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-04-03a)
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
            gzip -d clvhealth_jcafb_2024_15_2024-04-03a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-04-03a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-04-03a.tar.gz

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
