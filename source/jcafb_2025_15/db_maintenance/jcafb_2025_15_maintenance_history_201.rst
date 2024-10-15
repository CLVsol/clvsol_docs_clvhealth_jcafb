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

================================================
Manutenção do Banco de Dados - JCAFB-2025-15 [1]
================================================

[clvheatlh-jcafb-2024-aws-tst] Atualizar os fontes do projeto (2024-05-23a)
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

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-22b)
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
            gzip -d clvhealth_jcafb_2025_15_2024-05-22b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15
            # dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-22b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            # rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm-17] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm-17] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm-17** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            ssh tkl-odoo15-jcafb25-vm-17 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm-17] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-05-26a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-26a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm-17** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm-17] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm-17 <https://tkl-odoo15-jcafb25-vm-17>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
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
            gzip -d clvhealth_jcafb_2025_15_2024-05-26a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15
            # dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-26a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            # rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2024-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2024-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2024-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024-aws-tst <https://clvheatlh-jcafb-2024-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://44.215.174.44**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-05-26a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-26a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            ssh clvheatlh-jcafb-2025-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-05-26a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-26a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2025-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-pro <https://clvheatlh-jcafb-2025-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
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
            gzip -d clvhealth_jcafb_2025_15_2024-08-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15
            # dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            # rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

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

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-08-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            ssh clvheatlh-jcafb-2025-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-08-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-pro <https://clvheatlh-jcafb-2025-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm-17] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-12b)
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm-17] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm-17** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            ssh tkl-odoo15-jcafb25-vm-17 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm-17] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-08-12b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-12b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-12b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-12b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm-17** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm-17] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm-17 <https://tkl-odoo15-jcafb25-vm-17>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb25-vm-17**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm-17] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-06a)
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm-17] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm-17** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            ssh tkl-odoo15-jcafb25-vm-17 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm-17] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-09-06a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-06a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm-17** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm-17] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm-17 <https://tkl-odoo15-jcafb25-vm-17>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb25-vm-17**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm-17] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-24a)
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm-17] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm-17** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            ssh tkl-odoo15-jcafb25-vm-17 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm-17] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-09-24a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-24a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-24a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm-17** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm-17
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm-17] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm-17 <https://tkl-odoo15-jcafb25-vm-17>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb25-vm-17**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-09-28b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-28b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            ssh clvheatlh-jcafb-2025-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-09-28b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-28b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-pro <https://clvheatlh-jcafb-2025-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-13a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-10-13a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-13a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-13a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            ssh clvheatlh-jcafb-2025-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-10-13a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-13a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-pro <https://clvheatlh-jcafb-2025-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-13a)
-------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2024-10-13a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-13a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-13a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025n-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-15a)
---------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-15a.sql

            gzip clvhealth_jcafb_2025_15_2024-10-15a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-15a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-10-15a.sql
.. index:: clvhealth_jcafb_2025_15_2024-10-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-10-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-15a

[clvheatlh-jcafb-2025n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-15a)
-------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-10-15a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-15a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025n-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
