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

=============================================
JCAFB-2025-15 (Preparação pré Jornada II [5])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Executar a Atualização dos Pacientes (Rec)
------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Update` para Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Verification State` = :bi:`Warning (L1)`" » :bi:`Verification State` = :bi:`"State" has changed` (160 Pacientes):

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Unselected`" » :bi:`Verification State` = :bi:`Warning (L1)`" » :bi:`Verification State` = :bi:`"State" has changed` (30 Pacientes):

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Waiting`" » :bi:`Verification State` = :bi:`Warning (L1)`" » :bi:`Verification State` = :bi:`"State" has changed` (234 Pacientes):

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Associar os Pacientes selecionados a uma Residência
---------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Associar os Pacientes selecionados a uma Residência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Residence`

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido` (160 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Residence` para executar a Ação.

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido` (160 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Residence` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Associar os Pacientes em espera a uma Residência
------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Associar os Pacientes em espera a uma Residência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Residence`

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Waiting`" » :bi:`Residence` = :bi:`Indefinido` (234 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Residence` para executar a Ação.

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Waiting`" » :bi:`Residence` = :bi:`Indefinido` (216 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Residence` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Patient Residence Update* para todas as Residências
--------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Residence Update`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State`

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Patient State` = ":bi:`Selected`" ou ":bi:`Waiting`" (394 Pacientes):

        #. Executar a Ação ":bi:`Patient Residence Update`":

            * Parâmetros utilizados:

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Residence Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09b.sql

            gzip clvhealth_jcafb_2025_15_2024-12-09b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-09b.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-09b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-09b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Criar os Documentos e os Resultados de Exames para as Crianças incluídas no Projeto JCAFB-2025
----------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Event Set Up [Patient]` para as Crianças incluídas no Projeto JCAFB-2025:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected` (72 Pacientes) ou :bi:`Waiting` (102 Pacientes)

        #. Executar a Ação ":bi:`Event Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Events*: **nenhum**

                * *Document Types*:

                    #. **QSC25**

                    #. **QSF25**

                * *Document Category*: **(Campo) Questionário**

                * *Lab Test Types*:

                    #. **ECP25**

                    #. **EEV25**

                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Event Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Documentos e os Resultados de Exames para os Idosos incluídos no Projeto JCAFB-2025
--------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Event Set Up [Patient]` para os Idosos incluídos no Projeto JCAFB-2025:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected` (88 Pacientes) ou :bi:`Waiting` (132 Pacientes)

        #. Executar a Ação ":bi:`Event Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Events*: **nenhum**

                * *Document Types*:

                    #. **QMD25**

                    #. **QSF25**

                    #. **QSI25**

                * *Document Category*: **(Campo) Questionário**

                * *Lab Test Types*:

                    #. **ECP25**

                    #. **EUR25**

                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Event Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Estabelecer as *Tags* para as Crianças incluídas no Projeto JCAFB-2025
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para as Crianças incluídas no Projeto JCAFB-2025:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected` (72 Pacientes) ou :bi:`Waiting` (102 Pacientes)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient Tag*: **Add**:

                    * **Questionário QSC25 Ausente**
                    
                    * **Questionário QSF25 Ausente**

                    * **Resultado de Exame ECP25 Ausente**

                    * **Resultado de Exame EEV25 Ausente**

                    * **Verificado com Alertas**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Estabelecer as *Tags* para os Idosos incluídos no Projeto JCAFB-2025
--------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Idosos incluídos no Projeto JCAFB-2025:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected` (88 Pacientes) ou :bi:`Waiting` (132 Pacientes)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient Tag*: **Add**:

                    * **Questionário QMD25 Ausente**
                    
                    * **Questionário QSF25 Ausente**

                    * **Questionário QSi25 Ausente**
                    
                    * **Resultado de Exame ECP25 Ausente**

                    * **Resultado de Exame EUR25 Ausente**

                    * **Verificado com Alertas**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09c)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09c.sql

            gzip clvhealth_jcafb_2025_15_2024-12-09c.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09c.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-09c.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-09c.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-09c
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09c

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09c)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09c.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09c.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Estabelecer as *Categories* para as Residências do Projeto JCAFB-2025
---------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Residence Mass Edit` para as Residências incluídas no Projeto JCAFB-2025:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`District`

        #. Selecionar todas as Residências com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Indefinido`" » :bi:`District` = :bi:`Baixada` (77 Residências)

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** **Zona Urbana**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Indefinido`" » :bi:`District` = :bi:`Centro` (130 Residências)

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** **Zona Urbana**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Indefinido`" » :bi:`District` = :bi:`Cohabs` (79 Residências)

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** **Zona Urbana**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Category` = ":bi:`Indefinido`" » :bi:`District` = :bi:`Vilo Oliveira` (73 Residências)

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** **Zona Urbana**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09d)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09d.sql

            gzip clvhealth_jcafb_2025_15_2024-12-09d.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09d.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09d.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-09d.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-09d.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-09d
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09d

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09d)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09d.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09d.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09d.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 01 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 01 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 01 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 01 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 01 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 02 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 02 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 02 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 02 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 02 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 03 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 03 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 03 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 03 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 03 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 04 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 04 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 04 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 04 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 04 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 05 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 05 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 05 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 05 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 05 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 06 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 06 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 06 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 06 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 06 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 07 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 07 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 07 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 07 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 07 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 08 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 08 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 08 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 08 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 08 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 09 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 09 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 09 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 09 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 09 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 10 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 10 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 10 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 10 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 10 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 11 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 11 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 11 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 11 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 11 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 12 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 12 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 12 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 12 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 12 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 13 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 13 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 13 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 13 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 13 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 14 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 14 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 14 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 14 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 14 (2025)**" (22 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Grupo 15 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Grupo 15 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 15 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 15 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Grupo 15 (2025)**" (12 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Coord 01 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Coord 01 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Coord 01 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Coord 01 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Coord 01 (2025)**" (40 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar os Sumários relativos ao Grupo de Campo "Coord 02 (2025)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Summary Set Up` para o Grupo de Campo "**Coord 02 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Coord 02 (2025)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Coord 02 (2025)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2025**" » :bi:`Responsible Empĺoyee` ="**Coord 02 (2025)**" (34 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09e)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09e.sql

            gzip clvhealth_jcafb_2025_15_2024-12-09e.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-09e.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09e.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-09e.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-09e.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-09e.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-09e
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09e

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09e)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09e.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09e.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
