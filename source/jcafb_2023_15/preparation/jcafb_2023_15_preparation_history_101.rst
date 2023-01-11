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

=============================
JCAFB-2023-15 (Atualização 1)
=============================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-05b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        .. * clv_lab_test

        .. * clv_lab_test_jcafb

        * clv_lab_test_pool_jcafb

        .. * clv_lab_test_log_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

.. toctree::   :maxdepth: 2
