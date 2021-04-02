.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

====================================================================
:red:`(Não Executado)` Preparação do Banco de Dados - JCAFB-2021v-14
====================================================================

:red:`(Já Executado)` Atualizar o *Person Category* de todas as Pessoas
-----------------------------------------------------------------------

    Critérios utilizados:

        * **Criança**: todas as Pessoas na faixa etária "3-10 anos".

        * **Idoso**: todas as Pessoas na faixa etária "60+ anos".

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Age Ranges` » :bi:`Categories`

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**0-2 anos**" » :bi:`Category` = "**Criança**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**3-10 anos**" » :bi:`Category` = "**indefinido**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**11-17 anos**" » :bi:`Category` = "**Gestante**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Gestante**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**18-59 anos**" » :bi:`Category` = "**Gestante**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Gestante**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**18-59 anos**" » :bi:`Category` = "**Idoso**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**60+ anos**" » :bi:`Category` = "**indefinido**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**indefinido**" » :bi:`Category` = "**Idoso**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Person State` » :bi:`Categories`

        #. Selecionar todas as Pessoas com: :bi:`Person State` = "**Unavailable**" » :bi:`Category` = "**Criança**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Criança**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Person State` = "**Unavailable**" » :bi:`Category` = "**Idoso**"

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Remove** » **Idoso**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar as Crianças para o Projeto JCAFB-2021v
-------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Available`

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** » **Selected**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar os Idosos para o Projeto JCAFB-2021v
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para os Idosos selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Available`

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** » **Selected**

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

            * :bi:`Execution time: 0:00:38.521`

Selecionar as Pessoas (Aux) para o Projeto JCAFB-2021v
------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person (Aux) Reload` para as Pessoas (Aux) selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"State" has changed.`

        #. Executar a Ação ":bi:`Person (Aux) Reload`":

            * Parâmetros utilizados:

                * *Update Contact Information Data*: **desmarcado**

                * *Update Address Data*: **desmarcado**

                * *Update Family Data*: **desmarcado**

                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:37.874`

Selecionar os Endereços para o Projeto JCAFB-2021v
--------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit` para os Endereços selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L0)`" » :bi:`Verification Outcome Informations` = :bi:`Please, verify "Address State".`

        #. Executar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *Address State*: **Set** » **Selected**

                * *Address Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:35.880`

Selecionar os Endereços (Aux) para o Projeto JCAFB-2021v
--------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address (Aux) Reload` para os Endereços (Aux) selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"State" has changed.`

        #. Executar a Ação ":bi:`Address (Aux) Reload`":

            * Parâmetros utilizados:

                * *Address (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:34.927`

Selecionar as Famílias para o Projeto JCAFB-2021v
-------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para as Famílias selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L0)`" » :bi:`Verification Outcome Informations` = :bi:`Address "State" mismatch.`

        #. Executar a Ação ":bi:`Family Mass Edit`":

            * Parâmetros utilizados:

                * *Family State*: **Set** » **Selected**

                * *Family Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:38.492`

Criar Famílias para o Projeto JCAFB-2021v
-----------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person (Aux) Associate to Family` para Pessoas selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person (Aux) State` » :bi:`Family`

        #. Selecionar todas as Pessoas (Aux) com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person (Aux) State` = ":bi:`Selected`" » :bi:`Family` = :bi:`Indefinido`

        #. Executar a Ação ":bi:`Person (Aux) Associate to Family`":

            * Parâmetros utilizados:

                * *Create new Family*: **marcado**

                * *Associate all Persons from Reference Address*: **marcado**

                * *Family Verification Execute*: **marcado**

                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Family` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:35.788`

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = :bi:`"Family" should not be set.`

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Family is unavailable*: **Set** » **desmarcado**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:35.154`

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person (Aux) Reload`:

        #. Acessar a *View* *Persons (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Error (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"Family" should not be set.`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"Family" has changed.`

        #. Executar a Ação ":bi:`Person (Aux) Reload`":

            * Parâmetros utilizados:

                * *Update Contact Information Data*: **desmarcado**

                * *Update Address Data*: **desmarcado**

                * *Update Family Data*: **marcado**

                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:29:04.115`

.. toctree::   :maxdepth: 2
