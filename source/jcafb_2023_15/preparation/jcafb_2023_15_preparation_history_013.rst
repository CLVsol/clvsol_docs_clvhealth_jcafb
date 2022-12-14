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

========================================
JCAFB-2023-15 (Preparação pré Jornada 1)
========================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-07a)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-07a.sql.gz

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

Definir a composição do Grupos da JCAFB-2023
--------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Definir a composição do Grupos da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-08a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-08a.sql

            gzip clvhealth_jcafb_2023_15_2022-12-08a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-08a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-08a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-08a.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-08a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-08a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-08a)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-08a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-08a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08a.tar.gz

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

Executar a seleçlão dos Pacientes para a JCAFB-2023
---------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Executar a seleçlão dos Pacientes para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-08b)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-08b.sql

            gzip clvhealth_jcafb_2023_15_2022-12-08b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-08b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-08b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-08b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-08b.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-08b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-08b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-08b)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-08b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-08b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-08b.tar.gz

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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_base

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_base

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_export

        * clv_export_jcafb

    #. [tkl-odoo15-jcafb23-vm] **Executar** a instalação do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-10a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-10a.sql

            gzip clvhealth_jcafb_2023_15_2022-12-10a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-10a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-10a.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-10a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-10a)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-10a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-10a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-10a.tar.gz

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

Configurar as permissões do usuário de referência da JCAFB-2023
---------------------------------------------------------------

    #. Configurar as permissões do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Configurações` » :bi:`Usuários e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Configurar as permissões:

            * User Type

                * Tipos de usuário: **Utilizador Interno**

            * Marketing

                * Inquéritos: **Administrador**

            * *Human Resources*
            
                * Funcionários: **Administrador**

            * *Administration*
            
                * Administração:

            * *Other*:

                * *Employee*: :bi:`Manager (Employee)`
                * *Event*: :bi:`Manager (Event)`
                * *Export*: :bi:`Manager (Export)`
                * *External Sync*:
                * *File System*: :bi:`Manager (File System)`
                * *Global Tag*: :bi:`Manager (Global Tag)`
                * *Patient (Aux)*: :bi:`Manager (Patient (Aux))`
                * *Patient*: :bi:`Manager (Patient)`
                * *Phase*: :bi:`User (Phase)`
                * *Pool*: :bi:`Manager (Pool)`
                * *Processing*:
                * *Residence*: :bi:`Manager (Residence)`
                * *Set*: :bi:`Manager (Set)`
                * *Survey*:  :bi:`Manager (Survey)`
                * *Verification*: :bi:`Manager (Verification)`

            * *Base*:

                * :bi:`Log User (Base)`,
                * :bi:`Manager (Base)` ​
                * :bi:`Register User (Base)`,
                * :bi:`Super User (Base)`,
                * :bi:`User (Base)`,

            * *Document*:

                * :bi:`Manager (Document)`,
                * :bi:`User (Document)` ​

            * *Lab Test*:

                * :bi:`Manager (Lab Test)`,
                * :bi:`User (Lab Test)` ​

            * *Technical*:

                * **Acesso a endereços privados**
                * **Acesso para exportar recurso**
                * **Mail Template Editor**

            * *Extra Rights*:

                * **Criação de Contato**

Atualizar as permissões dos Coordenadores da JCAFB-2023
-------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação *Employee User Groups Update* para os Coordenadores da JCAFB-2023:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Funcionários**:

            * Menu de acesso:

                * **Funcionários** » **Funcionários** » **Funcionários**

        #. Selecionar os **Coordenadores** da JCAFB-2023

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-11a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-11a.sql

            gzip clvhealth_jcafb_2023_15_2022-12-11a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-11a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-11a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-11a.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-11a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-11a)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-11a.sql.gz

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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_lab_test
        * clv_patient_jcafb
        * clv_patient_aux_jcafb

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

                # python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_jcafb

                # python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-13a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-13a.sql

            gzip clvhealth_jcafb_2023_15_2022-12-13a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-13a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-13a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-13a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-13a.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-13a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-13a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-13a)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-13a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-13a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13a.tar.gz

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

Criar os *Patient Code Pools* para as Campanhas da JCAFB-2023
-------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Patient Code Pools* para as Campanhas da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Patient Code Pool`

        * *Patient Code Pools* criados:
            
            * **(Campanha) Patient Code Pool 01**

                * *Name*: **(Campanha) Patient Code Pool 01**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

            * **(Campanha) Patient Code Pool 02**

                * *Name*: **(Campanha) Patient Code Pool 02**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

            * **(Campanha) Patient Code Pool 03**

                * *Name*: **(Campanha) Patient Code Pool 03**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

            * **(Campanha) Patient Code Pool 04**

                * *Name*: **(Campanha) Patient Code Pool 04**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

            * **(Campanha) Patient Code Pool 05**

                * *Name*: **(Campanha) Patient Code Pool 05**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

            * **(Campanha) Patient Code Pool 06**

                * *Name*: **(Campanha) Patient Code Pool 06**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **100**

Criar os *Document Code Pools* para as Campanhas da JCAFB-2023
--------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Document Code Pools* para as Campanhas da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        * *Document Code Pools* criados:
            
            * **(Campanha) Document Code Pool 01**

                * *Name*: **(Campanha) Document Code Pool 01**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

            * **(Campanha) Document Code Pool 02**

                * *Name*: **(Campanha) Document Code Pool 02**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

            * **(Campanha) Document Code Pool 03**

                * *Name*: **(Campanha) Document Code Pool 03**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

            * **(Campanha) Document Code Pool 04**

                * *Name*: **(Campanha) Document Code Pool 04**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

            * **(Campanha) Document Code Pool 05**

                * *Name*: **(Campanha) Document Code Pool 05**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

            * **(Campanha) Document Code Pool 06**

                * *Name*: **(Campanha) Document Code Pool 06**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **200**

Criar os *Lab Test Result Code Pools* para as Campanhas da JCAFB-2023
---------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Lab Test Result Code Pools* para as Campanhas da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 01**

                * *Name*: **(Campanha) Lab Test Result Code Pool 01**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 02**

                * *Name*: **(Campanha) Lab Test Result Code Pool 02**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 03**

                * *Name*: **(Campanha) Lab Test Result Code Pool 03**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 04**

                * *Name*: **(Campanha) Lab Test Result Code Pool 04**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 05**

                * *Name*: **(Campanha) Lab Test Result Code Pool 05**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

        * *Lab Test Result Code Pools* criados:
            
            * **(Campanha) Lab Test Result Code Pool 06**

                * *Name*: **(Campanha) Lab Test Result Code Pool 06**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **100**

Criar os *Patient Code Pools* para as atividades de Campo da JCAFB-2023
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Patient Code Pools* para as atividades de Campo da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Patient Code Pool`

        * *Patient Code Pools* criados:
            
            * **(Campo) Patient Code Pool 01**

                * *Name*: **(Campo) Patient Code Pool 01**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **50**

            * **(Campo) Patient Code Pool 02**

                * *Name*: **(Campo) Patient Code Pool 02**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **50**

            * **(Campo) Patient Code Pool 03**

                * *Name*: **(Campo) Patient Code Pool 03**
                * *Code Sequence*: **clv.person.code**
                * *Number of Items*: **50**

Criar os *Document Code Pools* para os Grupos de Campo da JCAFB-2023
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Document Code Pools* para os Grupos de Campo da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        * *Document Code Pools* criados:
            
            * **(Campo) Document Code Pool Grupo 01 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 01 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 02 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 02 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 03 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 03 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 04 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 04 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 05 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 05 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 06 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 06 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 07 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 07 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 08 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 08 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 09 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 09 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 10 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 10 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 11 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 11 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

            * **(Campo) Document Code Pool Grupo 12 (2023)**

                * *Name*: **(Campo) Document Code Pool Grupo 12 (2023)**
                * *Code Sequence*: **clv.document.code**
                * *Number of Items*: **48**

Criar os *Lab Test Result Code Pools* para os Grupos de Campo da JCAFB-2023
---------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Lab Test Result Code Pools* para os Grupos de Campo da **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Request Code Pool`

        * *Lab Test Request Code Pools* criados:
            
            * **(Campo) Lab Test Result Code Pool Grupo 01 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 01 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 02 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 02 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 03 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 03 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 04 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 04 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 05 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 05 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 06 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 06 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 07 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 07 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 08 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 08 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 09 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 09 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 10 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 10 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 11 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 11 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

            * **(Campo) Lab Test Result Code Pool Grupo 12 (2023)**

                * *Name*: **(Campanha) Lab Test Result Code Pool Grupo 12 (2023)**
                * *Code Sequence*: **clv.lab_test.result.code**
                * *Number of Items*: **24**

Atualizar as Sequências
-----------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Acessar a *View* *Sequências*:

        * Menu de acesso:

            * **Configurações** » :bi:`Técnico` » :bi:`Sequências e Identificadores` » :bi:`Sequências`

    #. Atualizar as Sequências:

        #. **clv.export.code**:

            * Prefixo: **82**
            * Tamanho da Seqüência: **4**
            * Próximo Número: **1001**

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-13b)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-13b.sql

            gzip clvhealth_jcafb_2023_15_2022-12-13b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-13b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-13b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-13b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-13b.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-13b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-13b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-13b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-13b)
-----------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2023_15_2022-12-13b.sql.gz

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
