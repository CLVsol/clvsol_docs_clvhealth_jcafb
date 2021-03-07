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

Associar as Pessoas selecionadas aos Grupos da JCAFB-2021v
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *Persons*:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Community` » :bi:`Persons`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person State` » :bi:`Responsible Employee` » :bi:`Address Name` » :bi:`Categories`

    #. Selecionar as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`:

        * Distribuir os Idosos e Crianças selecionados pelos Grupos da JCAFB-2021v de forma que o números de Idosos e Crianças sejam equanimemente distribuido entre os Grupos.

Associar os Endereços selecionados aos Grupos da JCAFB-2021v
------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Address State` » :bi:`Responsible Employee`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Address State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`indefinido`

        #. Exercutar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *Get Responsible Empĺoyee*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Associar as Familias selecionadas aos Grupos da JCAFB-2021v
-----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Family State` » :bi:`Responsible Employee`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Family State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`indefinido`

        #. Exercutar a Ação ":bi:`Family Mass Edit`":

            * Parâmetros utilizados:

                * *Get Responsible Empĺoyee*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:41.249`

Associar as Pessoas disponíveis aos Grupos da JCAFB-2021v
---------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person State` » :bi:`Verification State` » :bi:`Outcome Informations` » :bi:`Responsible Employee`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Available`" » :bi:`Verification State` = ":bi:`Warning (L0)`" » :bi:`Outcome Informations` = :bi:`Address "Responsible Empĺoyee" mismatch.` » :bi:`Responsible Employee` = :bi:`Indefinido`

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Person Verification Execute*: **marcado**

                * *Get Responsible Empĺoyee*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:41.155`

.. toctree::   :maxdepth: 2
