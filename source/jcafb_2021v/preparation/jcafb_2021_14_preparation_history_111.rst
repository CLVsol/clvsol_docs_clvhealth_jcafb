.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

======================================================================================================
:red:`(Não Executado)` Preparação do Banco de Dados - JCAFB-2021v-14 (Recadastramento (pré Jornada) 1)
======================================================================================================

Executar a Criação do Cadastro Auxiliar (Criação do Cadastro Auxiliar)
----------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento:

        * Workbook: "**JCAFB02021v - clv.person - Recadastramento (pré Jornada).xlsx**"

        * Planilha: "**Recadastramento (pré Jornada) 1**"

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration/reregistration_workflow_020`"

    **Método Alternativo**:

    #. [mint19] Copiar manualmente o arquivo "**JCAFB02021v - clv.person - Recadastramento (pré Jornada).xls**":

        * de: **/home/mint20/Downloads**

        * para: **sftp://odoo@tkl-odoo14-jcafb21-vm/opt/odoo/clvsol_filestore/clvhealth_jcafb** 

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente o *Processing Schedule* **Reregistration Import XLS (1)**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar o *Processing Schedule* "**Reregistration Import XLS (1)**"

        #. Executar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

:red:`(Não Executado)` Executar o *Verification Batch* “Current Phase - Default Batch”
--------------------------------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:15.537`

Executar o *Verification Batch* “Current Phase - Default Batch” (método alternativo)
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Current Phase - Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:00:18.144`

Adicionar novos *Street Patterns*
---------------------------------

    #. Adicionar os novos *Street Patterns* listados a seguir, utilizando o procedimento :doc:`/procedures/reregistration/reregistration_procedure_030_010_025`:

        * *Address (Aux)* "Rua Nova Fernão [Centro]".

        * *Address (Aux)* "Rua Nova Olinda [Centro)]".

Executar o *Verification Batch* “Current Phase - Default Batch” (método alternativo)
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Current Phase - Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:00:17.416`

Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Auxiliar)
------------------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration/reregistration_workflow_030`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_010`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_010_010`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_010_020`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020_010`" e/ou :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020_020`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_010`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_010_010`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_010_020`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_010_030`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_020`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_020_010`" e/ou :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_020_020`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_020_040`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_030`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_030_010`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020`"

            #. Processar o Recadastramento de todas as Pessoas indicadas por: :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020_040`"

Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Principal)
-------------------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration/reregistration_workflow_040`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_040_020`"

            #. Processar o Recadastramento de todas as Pessoas indicadas por: :doc:`/reference_guide/reregistration/reregistration_workflow_040_020_010`"

        #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_030`"

            #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_030_020`"

Executar o *Verification Batch* “Current Phase - Default Batch” (método alternativo)
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Current Phase - Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:00:32.131`

Atualizar o *State* de Endereços afetados pelo Recadastramento
--------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit` para Endereços afetados pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Please, verify "Address State".`"

        #. Executar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** » **Unavailable**

                * *Address Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Default Batch” (método alternativo)
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:28:36.667`

Atualizar a Fase de Famílias afetadas pelo Recadastramento
----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Mass Edit` para Famílias afetadas pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Address "Phase" mismatch.`"

        #. Executar a Ação ":bi:`Family Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *Phase*: **Set** » **JCAFB-2021v**

                * *Family Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *State* de Famílias afetadas pelo Recadastramento
-------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Mass Edit` para afetadas pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Address "State" mismatch.`"

        #. Executar a Ação ":bi:`Family Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **Set** » **Available**

                * *Phase*: **Set** » **JCAFB-2021v**

                * *Family Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:40.519`

Atualizar o *State* de Endereços afetados pelo Recadastramento
--------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit` para Endereços afetados pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Please, verify "Address State".`"

        #. Executar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** » **Unavailable**

                * *Address Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Default Batch”
-----------------------------------------------

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:29:39.260`

Atualizar o *State* de Endereços (Aux) afetados pelo Recadastramento
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address (Aux) Reload` para Endereços (Aux) afetados pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"State" has changed.`

        #. Executar a Ação ":bi:`Address (Aux) Reload`":

            * Parâmetros utilizados:

                * *Address (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

Atualizar o *Register State* dos Endereços já recadastrados
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Address Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Address Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Famílias já recadastradas
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Family Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Family Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Pessoas já recadastradas
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Person Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Person Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Endereços (Aux) já recadastrados
-----------------------------------------------------------------

    #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Address (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Pessoas (Aux) já recadastradas
---------------------------------------------------------------

    #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:36.025`

.. toctree::   :maxdepth: 2
