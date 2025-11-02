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

.. toctree::   :maxdepth: 2
