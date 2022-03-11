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

====================================
JCAFB-2021v-15 (Exportação de Dados)
====================================

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-10a)
--------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-10a.sql

            gzip clvhealth_jcafb_2021v_15_2022-03-10a.sql
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz clvhealth_jcafb_2021v_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-10a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz

.. index:: clvhealth_jcafb_2021v_15_2022-03-10a.sql
.. index:: clvhealth_jcafb_2021v_15_2022-03-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_15_2022-03-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-10a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-10a)
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_15_2022-03-10a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_15
            psql -f clvhealth_jcafb_2021v_15_2022-03-10a.sql -d clvhealth_jcafb_2021v_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb21-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
