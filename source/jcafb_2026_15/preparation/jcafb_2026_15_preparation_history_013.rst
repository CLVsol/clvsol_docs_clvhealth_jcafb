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
JCAFB-2026-15 (Preparação pré Jornada [4])
==========================================

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-07a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-07a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb26-vm] Excluir os  *Patient Markers* utilizdos no cadastramento de Pacientes da JCAFB-2025
-----------------------------------------------------------------------------------------------------------

    * MC1_Criancas
    * MC1_Idosos
    * MC2_Criancas
    * MC2_Idosos
    * MC3_Criancas
    * MC3_Idosos
    * MC4_Criancas
    * MC4_Idosos
    * MC5_Criancas
    * MC5_Idosos
    * MC6_Criancas
    * MC6_Idosos
    * MC7_Criancas
    * MC7_Idosos

[tkl-odoo15-jcafb26-vm] Atualizar a *Phase* dos Pacientes ainda não marcados como "JCAFB-2025"
----------------------------------------------------------------------------------------------

    * (59 Pacientes)

[tkl-odoo15-jcafb26-vm] Consolidar as informações dos registros de Pacientes
----------------------------------------------------------------------------

    * (905 Pacientes)

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07b.sql

            gzip clvhealth_jcafb_2026_15_2025-07-07b.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07b.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-07b.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-07b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-07b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07b

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-07b.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-07b.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb26-vm] Atualizar o *Patient History* de todos os Pacientes
---------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Executar a Ação :bi:`Patient History Update` para todos os Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **07/07/2025**
                * *Sign in date*: **02/01/2025**

            #. Utilize o botão :bi:`Patient History Update` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07c)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07c.sql

            gzip clvhealth_jcafb_2026_15_2025-07-07c.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07c.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-07c.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-07c.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-07c
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07c

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07c)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-07c.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-07c.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb26-vm] Atualizar o *Residence History* de todas as Residências
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Executar a Ação :bi:`Residence History Update` para todas as Residências:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as Residências (**366**)

        #. Executar a Ação ":bi:`Residence History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **07/07/2025**
                * *Sign in date*: **02/01/2025**

            #. Utilize o botão :bi:`Residence History Update` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir a *Phase* de todos os Pacientes da JCAFB-2025
-----------------------------------------------------------------------------

    * (905 Pacientes)

[tkl-odoo15-jcafb26-vm] Consolidar as informações dos registros de Pacientes
----------------------------------------------------------------------------

    * (905 Pacientes)

[tkl-odoo15-jcafb26-vm] Excluir a *Phase* de todas as Residências da JCAFB-2025
-------------------------------------------------------------------------------

    * (366 Residências)

[tkl-odoo15-jcafb26-vm] Consolidar as informações dos registros de Residências
------------------------------------------------------------------------------

    * (366 Residências)

[tkl-odoo15-jcafb26-vm] Atualizar o *Patient History* de todos os Pacientes
---------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Executar a Ação :bi:`Patient History Update` para todos os Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **07/07/2025**
                * *Sign in date*: **07/07/2025**

            #. Utilize o botão :bi:`Patient History Update` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o *Residence History* de todas as Residências
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Executar a Ação :bi:`Residence History Update` para todas as Residências:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as Residências (**366**)

        #. Executar a Ação ":bi:`Residence History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **07/07/2025**
                * *Sign in date*: **07/07/2025**

            #. Utilize o botão :bi:`Residence History Update` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07d)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07d.sql

            gzip clvhealth_jcafb_2026_15_2025-07-07d.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07d.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07d.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-07d.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-07d.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-07d
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07d

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07d)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-07d.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-07d.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07d.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
