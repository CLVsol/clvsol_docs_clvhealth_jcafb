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
JCAFB-2026-15 (Preparação pré Jornada [5])
==========================================

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

[kl-odoo15-jcafb26-vm] Remover a Residência dos Pacientes
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `kl-odoo15-jcafb26-vm <https://kl-odoo15-jcafb26-vm>`_

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Residence is unavailable*: :bi:`Set` **marcado**
                * *Residence*: :bi:`Remove`
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Remover o Grupo dos Pacientes
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Responsible Empĺoyee*: :bi:`Remove`
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o *Patient State* dos Pacientes
-----------------------------------------------------------------

    #. Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Selected**" (**142**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Available**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Não Contemplado**" (**95**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Available**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Unselected Administrativamente**" (**38**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Available**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Não Quis Participar**" (**71**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Não Encontrado**" (**40**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Ausente**" (**22**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Patient Markers`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" » :bi:`Patient Markers` = "**Indisponível**" (**14**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unselected**" (**1**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**New**" (**1**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Unknown**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Executar a Atualização de todos os Pacientes (Rec)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Executar a Ação :bi:`Patient Related Patient (Rec) Update` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-08a)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-08a.sql

            gzip clvhealth_jcafb_2026_15_2025-07-08a.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-08a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-08a.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-08a.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-08a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-08a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-08a

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-08a)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-08a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-08a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-08a.tar.gz

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

[tkl-odoo15-jcafb26-vm] Remover o *Patient Tags* dos Pacientes
--------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**).

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Patient Tag*: :bi:`Set` **lista vazia**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Renovar o *Random ID* de todos os Pacientes
-------------------------------------------------------------------

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Random ID*: :bi:`Set` "**/**"

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2026-15*
----------------------------------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2026**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2026**

[tkl-odoo15-jcafb26-vm] Atualizar a Idade de Referência dos Pacientes
---------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Patient Reference Age Refresh*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Summaries**
------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Escluir manualmente todos os arquivos presentes no diretório "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/summary_files**" do Servidor.

    #. Escluir manualmente todos os :bi:`File System Files` do :bi:`File System Directory` "**Summary Files**":

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Files`

        #. Ativar o filtro **Agrupar por** » :bi:`Directory`

        #. Selecionar todas os :bi:`File System Files` referentes a "**Summary Files**" (**0**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Executar a Ação :bi:`Patient Mass Edit` para todos os :bi:`Patients`:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * **Health** » :bi:`Health` » :bi:`Patients`

        #. Selecionar todos os :bi:`Patients` (**905**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Summary*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. Executar a Ação :bi:`Employee Mass Edit` para todos os :bi:`Funcionários`:

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Funcionários` » :bi:`Funcionários`

        #. Selecionar todos os :bi:`Funcionários` (**387**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Summary*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb26-vm] Excluir todos os **Summaries**:

        #. Acessar a *view* **Summaries**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Summaries`

        #. Selecionar todos os :bi:`Summaries` (**416**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir os :bi:`Contact Information Patterns` sem :bi:`Matches`
---------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Excluir os :bi:`Contact Information Patterns` sem :bi:`Matches`:

        #. Acessar a *view* :bi:`Contact Information Patterns`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information`

        #. Selecionar os :bi:`Contact Information Patterns` com :bi:`Number of Matches` = **0** (**4**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir os :bi:`Street Patterns` sem :bi:`Matches`
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Excluir os :bi:`Street Patterns` sem :bi:`Matches`:

        #. Acessar a *view* :bi:`Street Patterns`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Street Patterns`

        #. Selecionar os :bi:`Street Patterns` com :bi:`Number of Matches` = **0** (**1**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o *Residence State* de todas as **Residências**
---------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Acessar a *view* **Residences**:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

    #. Selecionar todas as :bi:`Residences` (**366**)

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Residence State*: **Set** » **Unknown**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o *Register State* de todas as **Residências**
--------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *view* **Residences**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as :bi:`Residences` (**366**)

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Atualizar o *Register State* de todos os **Pacientes**
------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *view* **Patients**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os :bi:`Patients` (**905**)

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-09a)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-09a.sql

            gzip clvhealth_jcafb_2026_15_2025-07-09a.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-09a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-09a.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-09a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-09a.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-09a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-09a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09a

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-09a)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-09a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-09a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09a.tar.gz

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

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2666,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2666**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2666'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2631 clv.document,2666 clv.document NULL     164.178-60

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2666**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.lab_test.result(2033,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.lab_test.result,2033**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.lab_test.result' AND ref_id = 'clv.lab_test.result,2033'
                ORDER BY ref_id

            ::

                id   ref_id                   ref_model           ref_name ref_code
                2681 clv.lab_test.result,2033 clv.lab_test.result NULL     342.789-74

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.lab_test.result,2033**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2669,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2669**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2669'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2609 clv.document,2669 clv.document NULL     164.181-66

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2669**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2002,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2002**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2002'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2104 clv.document,2002 clv.document NULL     163.514-01

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2002**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2003,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2003**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2003'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2107 clv.document,2003 clv.document NULL     163.515-84

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2003**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2042,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2042**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2042'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2051 clv.document,2042 clv.document NULL     163.554-90

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2042**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Restaurar a integridade de "**Participations**"
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_.

    #. [tkl-odoo15-jcafb26-vm] Verificar a integridade de :bi:`Participations`:

        #. Acessar a *View* *Participations*:

            * Menu de acesso:
                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.document(2041,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb26-vm:12322 <https://tkl-odoo15-jcafb26-vm:12322>`_.

    #. [tkl-odoo15-jcafb26-vm:12322] Selecionar o registro de "**survey_user_input**" apontando para "**clv.document,2041**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "survey_user_input"
                WHERE ref_model = 'clv.document' AND ref_id = 'clv.document,2041'
                ORDER BY ref_id

            ::

                id   ref_id            ref_model    ref_name ref_code
                2050 clv.document,2041 clv.document NULL     163.553-00

    #. [tkl-odoo15-jcafb26-vm:12322] Editar o registro de "**survey_user_input**" apontando para "**clv.document,2041**":

        * Parâmetros utilizados:
            * **ref_id**: **NULL**
            * **ref_model**: **NULL**
            * **ref_code**: **NULL**

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-09b)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-09b.sql

            gzip clvhealth_jcafb_2026_15_2025-07-09b.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-09b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-09b.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-09b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-09b.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-09b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-09b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09b

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-09b)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-09b.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-09b.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz

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
