.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

===============================================================================
Preparação do Banco de Dados - JCAFB-2021v-14 (Recadastramento (pré Jornada) 1)
===============================================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-22a)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-22a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-22a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-22a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

:red:`(Não Executado)` Associar os Pacientes a uma Residência
-------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Patient Associate to Residence* para os Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes.

        #. Exercutar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Selecionar todos os Pacientes.

        #. Exercutar a Ação ":bi:`Patient Verification Execute`":

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

Executar a Criação do Cadastro Auxiliar (Criação do Cadastro Auxiliar)
----------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento:

        * Workbook: "**JCAFB02021v - clv.patient - Recadastramento (pré Jornada).xlsx**"

        * Planilha: "**Recadastramento (pré Jornada) 1**"

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_020`"

    **Método Alternativo Executado**:

        #. [mint19] Copiar manualmente, se necessário, o arquivo "**JCAFB02021v - clv.patient - Recadastramento (pré Jornada).xls**":

            * de: **/home/mint20/Downloads**

            * para: **sftp://odoo@tkl-odoo14-jcafb21-vm/opt/odoo/clvsol_filestore/clvhealth_jcafb** 

        #. [tkl-odoo14-jcafb21-vm] Executar manualmente os *Processing Schedule* **Reregistration Import XLS - Patient (1)** e **Reregistration Import XLS - Patient (2)**:

            #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

            #. Acessar a *View* :bi:`Processing Schedules`:

                * Menu de acesso:

                    * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - Patient (1)**"

            #. Exercutar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.810`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - Patient (2)**"

            #. Exercutar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.257`

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:06.927`

Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Auxiliar)
------------------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_010`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_010_005`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_010_006`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_010_010`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_010_030`"

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_010`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_020`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_030`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_050`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_060`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_070`"

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_030`"

:red:`(Não Executado)` Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Principal)
------------------------------------------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_110`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_120`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_130`"

Atualizar o *Patient Category* de todos os Pacientes
----------------------------------------------------

    Critérios utilizados:

        * **Criança**: todos os Pacientes na faixa etária "3-10 anos".

        * **Idoso**: todos os Pacientes na faixa etária "60+ anos".

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Categories`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Patient State` = "**Unavailable**" » :bi:`Category` = "**Criança**"

        #. Exercutar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Unavailable**" » :bi:`Category` = "**Idoso**"

        #. Exercutar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Categories` » :bi:`Age Ranges`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Patient State` = "**Unavailable**" » :bi:`Category` = "**Indefinido**" :bi:`Age Range` = "**3-10 anos**"

        #. Exercutar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Patient State` = "**Unavailable**" » :bi:`Category` = "**Indefinido**" :bi:`Age Range` = "**60+ anos**"

        #. Exercutar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes já recadastrados
-----------------------------------------------------------

    #. Exercutar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes (Aux) já recadastrados
-----------------------------------------------------------------

    #. Exercutar a Ação ":bi:`Patient (Aux) Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-22b)
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-22b.sql

            gzip clvhealth_jcafb_2021v_14_2021-03-22b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-22b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-22b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-22b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-03-22b.sql
.. index:: clvhealth_jcafb_2021v_14_2021-03-22b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-03-22b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-22b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-22b)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-22b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-22b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-22b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
