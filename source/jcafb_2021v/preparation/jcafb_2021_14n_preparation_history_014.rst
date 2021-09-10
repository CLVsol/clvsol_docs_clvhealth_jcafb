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

===========================================================================
Preparação do Banco de Dados - JCAFB-2021v-14n (Recadastramento de Campo 1)
===========================================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-04a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-04a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-04a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Substituir um Paciente do Projeto JCAFB-2021v (Recusa em Participar)
--------------------------------------------------------------------

    #. **Conectar-se**, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. **Identificar o Paciente e a Residência que serão substituidos:**

        #. Utilizar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Utilizar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

    #. **Selecionar um novo Paciente para o Projeto JCAFB-2021v:**

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar a classificação dos Pacientes pelo campo :bi:`Ramdon ID`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar o primeiro Paciente listado com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = "**Categoria do Paciente em substituição**" » :bi:`Patient State` = :bi:`Available`

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Selected**

                * *Patient Verification Execute*: **marcado**

                * *Responsible Empĺoyee*: **Set** » **Nome do Grupo responsável pela Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Verificar se a Categoria da Residência está corretamente informada. Caso um novo registro para a Residência tenha sido criado, a Categoria precisa ser manualmente indicada.

        #. Executar a Ação "**Patient Residence Update**":

            * Parâmetros utilizados:

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Residence Update* para executar a Ação.

    #. **Desselecionar o Paciente substituido do Projeto JCAFB-2021v:**

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar o Paciente a ser substituido (identificado anteriormente).

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Unselected**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Acessar a *Tab* *Documents*.

        #. Acessar a *View* *Documents* a partir da *Tab* *Documents*.

        #. Selecionar os Documentos apresentados com: :bi:`Phase` = "**JCAFB-20201v**".

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Refers to*: **Set** » **Registro da nova Criança selecionada**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Voltar ao Registro do Paciente desselecionado.

        #. Acessar a *Tab* *Lab Test Requests*.

        #. Acessar a *View* *Lab Test Requests* a partir da *Tab* *Lab Test Requests*.

        #. Selecionar as Requisições de Exames apresentadas com: :bi:`Phase` = "**JCAFB-20201v**".

        #. Executar a Ação ":bi:`Lab Test Request Mass Edit`":

            * Parâmetros utilizados:

                * *Refers to*: **Set** » **Registro da nova Criança selecionada**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Voltar ao Registro do Paciente desselecionado.

        #. Executar a Ação "**Patient Residence Update**":

            * Parâmetros utilizados:

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Residence Update* para executar a Ação.

    #. **Criar/Reprocessar os Sumários para todas as entidades envolvidas (Pacientes, Residências e Grupo Responsável) no processo de substitução da Criança.**

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:17.966`

    #. **Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Auxiliar)**:

        * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_030`"

Recadastrar um Paciente selecionado para o Projeto JCAFB-2021v (Mudança para Endereço Atendido)
-----------------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. **Conectar-se**, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. **Identificar o Paciente e a Residência que serão substituidos:**

        #. Utilizar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Utilizar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Utilizar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. **Desselecionar a antiga Residência do Paciente a ser recadastrado:**

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar a Residência a ser desselecionada.

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Unselected**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. **Executar o Recadastramento** (Mudança para um outro Endereço dentro da Comunidade atendida pela JCAFB21v) **do Paciente** Selecionado para o Projeto JCAFB-2021v, considerando as informações do novo Endereço apresentadas para o mesmo.

        #. Usar como referência: :doc:`/user_guide/reregistration/reregistration_workflow_020_010_050`", considerando:

            * Os :bi:`Register State` do Paciente e do do Paciente (Aux) **serão alterados** para :bi:`Revised`.

            * Os :bi:`Patient State` e :bi:`Patient (Aux) State` do Paciente **serão mantidos** como :bi:`Selected`.

    #. **Criar/Reprocessar os Sumários para todas as entidades envolvidas (Paciente, antiga Residência, nova Residência e Grupo Responsável) no processo de Recadastramento do Paciente.**

Recadastrar um Paciente selecionado para o Projeto JCAFB-2021v (Mudança para Endereço Desconhecido/Não Atendido)
----------------------------------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. **Conectar-se**, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. **Identificar o Paciente e a Residência que serão substituidos:**

        #. Utilizar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Utilizar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Utilizar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. **Desselecionar a antiga Residência do Paciente a ser recadastrado:**

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar a Residência a ser desselecionada.

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Unselected**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. **Executar o Recadastramento** (Mudança para um Endereço Desconhecido/Não Atendido) **do Paciente** Selecionado para o Projeto JCAFB-2021v.

        #. Usar como referência: :doc:`/user_guide/reregistration/reregistration_workflow_020_010_070`", considerando:

            * Os :bi:`Register State` do Paciente e do do Paciente (Aux) **serão alterados** para :bi:`Revised`.

            * Os :bi:`Patient State` e :bi:`Patient (Aux) State` do Paciente **serão marcados** como :bi:`Unavailable`.

    #. **Selecionar um novo Paciente para o Projeto JCAFB-2021v:**

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar a classificação dos Pacientes pelo campo :bi:`Ramdon ID`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar o primeiro Paciente listado com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = "**Categoria do Paciente em substituição**" » :bi:`Patient State` = :bi:`Available`

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Selected**

                * *Patient Verification Execute*: **marcado**

                * *Responsible Empĺoyee*: **Set** » **Nome do Grupo responsável pelo Paciente**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Executar a Ação "**Patient Residence Update**":

            * Parâmetros utilizados:

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Residence Update* para executar a Ação.

    #. **Desselecionar o Paciente do Projeto JCAFB-2021v (Finalização):**

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar o Paciente a ser substituido:

        #. Acessar a *Tab* *Documents*.

        #. Acessar a *View* *Documents* a partir da *Tab* *Documents*.

        #. Selecionar os Documentos apresentados com: :bi:`Phase` = "**JCAFB-20201v**".

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Refers to*: **Set** » **Registro do novo Paciente selecionado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Voltar ao Registro do Paciente desselecionado.

        #. Acessar a *Tab* *Lab Test Requests*.

        #. Acessar a *View* *Lab Test Requests* a partir da *Tab* *Lab Test Requests*.

        #. Selecionar as Requisições de Exames apresentadas com: :bi:`Phase` = "**JCAFB-20201v**".

        #. Executar a Ação ":bi:`Lab Test Request Mass Edit`":

            * Parâmetros utilizados:

                * *Refers to*: **Set** » **Registro do novo Paciente selecionado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. **Criar/Reprocessar os Sumários para todas as entidades envolvidas (Pacientes, Residências e Grupo Responsável) no processo de Recadastramento do Paciente.**

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:19.315`

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-10a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-10a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-09-10a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-10a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-09-10a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-09-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-09-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-10a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-10a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-10a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Atualizar o *Register State* dos Pacientes já recadastrados
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Residências já recadastrados
-------------------------------------------------------------

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes (Aux) já recadastrados
-----------------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::   :maxdepth: 2
