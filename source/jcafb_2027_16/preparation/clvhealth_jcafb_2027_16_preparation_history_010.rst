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

.. index:: JCAFB-2027-16 (Preparação pré Jornada [1])

==========================================
JCAFB-2027-16 (Preparação pré Jornada [1])
==========================================

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2026-04-20a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2026-04-20a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2026-04-20a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2026-04-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2026-04-20a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb27-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-05-03a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-05-03a.sql

            gzip clvhealth_jcafb_2027_16_2026-05-03a.sql
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-05-03a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz clvhealth_jcafb_2027_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2027_16_2026-05-03a.sql
        * /opt/odoo/clvhealth_jcafb_2027_16_2026-05-03a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

.. index:: clvhealth_jcafb_2027_16_2026-05-03a.sql
.. index:: clvhealth_jcafb_2027_16_2026-05-03a.sql.gz
.. index:: filestore_clvhealth_jcafb_2027_16_2026-05-03a
.. index:: clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a

[tkl-odoo16-jcafb27-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-05-03a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2027_16_2026-05-03a.sql.gz

            dropdb -i clvhealth_jcafb_2027_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2027_16
            psql -f clvhealth_jcafb_2027_16_2026-05-03a.sql -d clvhealth_jcafb_2027_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2027_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb27-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.223**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
