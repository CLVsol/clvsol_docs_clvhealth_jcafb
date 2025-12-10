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
Manutenção do Banco de Dados - JCAFB-2026-16 [1]
================================================

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-05-04b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-05-04b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16
            # dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-05-04b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-07-10a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-07-10b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-07-10b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-07-10b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-07-10b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-07-10b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-07-13b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-07-13b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-07-13b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-07-13b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-07-13b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-07-13b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-11-02a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-01b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-11-01b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-01b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-01b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-11-01b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-01b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-pro <https://clvheatlh-jcafb-2026-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.29.168.114**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-20a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-20a.sql

            gzip clvhealth_jcafb_2026_16_2025-11-20a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-20a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-20a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-20a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-11-20a.sql
.. index:: clvhealth_jcafb_2026_16_2025-11-20a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-11-20a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-20a

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29a.sql

            gzip clvhealth_jcafb_2026_16_2025-11-29a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-11-29a.sql
.. index:: clvhealth_jcafb_2026_16_2025-11-29a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-11-29a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29a

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-11-29a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-29a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29b)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29b.sql

            gzip clvhealth_jcafb_2026_16_2025-11-29b.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29b.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-11-29b.sql
.. index:: clvhealth_jcafb_2026_16_2025-11-29b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-11-29b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29b

[clvheatlh-jcafb-2026-aws-pro] Atualizar os fontes do projeto (2025-11-29b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29c)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29c.sql

            gzip clvhealth_jcafb_2026_16_2025-11-29c.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-11-29c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29c.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-11-29c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-11-29c.sql
.. index:: clvhealth_jcafb_2026_16_2025-11-29c.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-11-29c
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29c

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-11-29c)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-11-29c.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-29c.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-02a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-02a.sql

            gzip clvhealth_jcafb_2026_16_2025-12-02a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-02a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-02a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-02a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-02a.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-02a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-02a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02a

[clvheatlh-jcafb-2026-aws-pro] Atualizar os fontes do projeto (2025-12-02b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-02b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-02b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-02b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-pro <https://clvheatlh-jcafb-2026-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.29.168.114**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-12-02b)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-02b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-02b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-02b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-03a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-03a.sql

            gzip clvhealth_jcafb_2026_16_2025-12-03a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-03a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-03a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-03a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-03a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-03a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-03a.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-03a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-03a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03a

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-03b)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-03b.sql

            gzip clvhealth_jcafb_2026_16_2025-12-03b.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-03b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-03b.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-03b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-03b.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-03b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-03b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03b

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-03b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-03b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-03b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-03b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-06a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-06a.sql

            gzip clvhealth_jcafb_2026_16_2025-12-06a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-06a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-06a.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-06a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-06a

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-06a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-06a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-06a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-07a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-07a.sql

            gzip clvhealth_jcafb_2026_16_2025-12-07a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-07a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-07a.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-07a

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-07a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-07a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2026-aws-tst] Atualizar os fontes do projeto (2025-12-09a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-pro] Atualizar os fontes do projeto (2025-12-09a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2026-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-09a)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09a.sql

            gzip clvhealth_jcafb_2026_16_2025-12-09a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-09a.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-09a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-09a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09a

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-09b)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09b.sql

            gzip clvhealth_jcafb_2026_16_2025-12-09b.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09b.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09b.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09b.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-09b.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-09b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-09b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09b

[clvheatlh-jcafb-2026-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-09c)
--------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            ssh clvheatlh-jcafb-2026-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09c.sql

            gzip clvhealth_jcafb_2026_16_2025-12-09c.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-09c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09c.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-09c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-09c.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-09c.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-09c
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09c

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-09c)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2026_16_2025-12-09c.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-09c.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
