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

.. toctree::   :maxdepth: 2
