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

==========================================
JCAFB-2024-15 (Preparação pré Jornada [7])
==========================================

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-14b.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-16a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-16a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-16a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-16a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-16a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-16a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-16a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-16a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-16a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-16a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-16a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-16a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-17a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-17a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-17a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-17a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-17a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-17a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-17a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-17a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-17a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-17a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-17a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-17a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-17a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-21a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-21a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-21a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-21a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-21a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-21a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-21a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-21a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-21a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-21a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-21a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-21a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Atualizar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Lista de Módulos:

        * clv_patient_summary_jcafb
        * clv_employee_summary_jcafb

    #. [tkl-odoo15-jcafb24-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb24-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                ssh tkl-odoo15-jcafb24-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb24-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 2)
                #

                ssh tkl-odoo15-jcafb24-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2024_15" -m clv_patient_summary_jcafb clv_employee_summary_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-21b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-21b.sql

            gzip clvhealth_jcafb_2024_15_2023-12-21b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-21b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-21b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-21b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-21b.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-21b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-21b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21b

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-21b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-21b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-21b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-21b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

Criar os Sumários relativos ao Grupo de Campo "Grupo 01 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 01 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 01 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 01 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 01 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 02 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 02 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 02 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 02 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 02 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 03 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 03 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 03 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 03 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 03 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 04 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 04 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 04 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 04 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 04 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 05 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 05 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 05 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 05 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 05 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 06 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 06 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 06 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 06 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 06 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 07 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 07 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 07 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 07 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 07 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 08 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 08 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 08 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 08 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 08 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 09 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 09 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 09 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 09 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 09 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 10 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 10 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 10 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 10 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 10 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 11 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 11 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 11 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 11 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 11 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 12 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 12 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 12 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 12 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 12 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 13 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 13 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 13 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 13 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 13 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 14 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 14 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 14 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 14 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 14 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 15 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 15 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 15 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 15 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 15 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Idosos - Ribeirao da Varzea (2024)"
----------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Idosos - Ribeirao da Varzea (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Idosos - Ribeirao da Varzea (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Idosos - Ribeirao da Varzea (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Idosos - Ribeirao da Varzea (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-22a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-22a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-22a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-22a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-22a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-22a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-22a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-22a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-22a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-27a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-27a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-27a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-27a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-27a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-27a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-27a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-27a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-27a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-27a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-27a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-27a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-12-27a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-17a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2024-01-17a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-19a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2024-01-19a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2024-01-21a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2024-01-21a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
