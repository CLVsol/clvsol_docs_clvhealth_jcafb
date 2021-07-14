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

Executar o Cadastramento/Recadastramento (Preparação das Entidades do Cadastro Auxiliar)
----------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento:

        * Workbook: "**JCAFB02021v - clv.patient - Recadastramento (pré Jornada).xlsx**"

        * Planilha: "**Recadastramento (pré Jornada) 1**"

    #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_020`"

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

            #. Executar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.882`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - Patient (2)**"

            #. Executar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.234`

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:08.210`

Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Auxiliar)
------------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_030`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_010`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_010_005`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_010_006`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_010_010`"

        #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_005`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_010`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_020`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_030`"

            .. #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_050`"

            .. #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_060`"

            .. #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_020_070`"

        .. #. :doc:`/user_guide/reregistration/reregistration_workflow_030_020_030`"

:red:`(Não Executado)` Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Principal)
------------------------------------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_040`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/user_guide/reregistration/reregistration_workflow_040_030`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_040_030_020_110`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_040_030_020_120`"

            #. :doc:`/user_guide/reregistration/reregistration_workflow_040_030_020_130`"

Atualizar o *Register State* dos Pacientes já recadastrados
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes (Aux) já recadastrados
-----------------------------------------------------------------

    #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::   :maxdepth: 2
