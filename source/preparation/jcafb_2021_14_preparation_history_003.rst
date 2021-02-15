.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

=============================================
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

Associar as Pessoas selecionadas aos Grupos da JCAFB-2021v
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *Persons*:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Community` » :bi:`Persons`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person State` » :bi:`Responsible Employee` » :bi:`Categories`

    #. Selecionar as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`» :bi:`Category` = :bi:`Criança`:

        * Distribuir as Crianças selecionados pelos Grupos da JCAFB-2021v de forma que o número de Crianças seja equanimemente distribuido entre os Grupos.

    #. Selecionar as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`» :bi:`Category` = :bi:`Idoso`:

        * Distribuir os Idosos selecionados pelos Grupos da JCAFB-2021v de forma que o número de Idosos seja equanimemente distribuido entre os Grupos.

Criar os Documentos para as Crianças selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Person]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Person]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSC21**

                    #. **TCR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para os Idosos selecionados para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Person]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Person]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QMD21**

                    #. **QSI21**

                    #. **TID21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para as Famílias selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Family]` para as Famílias selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Family State`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Family State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Family]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSF21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar as Requisições de Exames para as Crianças selecionadas para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Person]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Lab Test Request Set Up [Person]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EEV21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Criar as Requisições de Exames para os Idosos selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Person]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Lab Test Request Set Up [Person]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EUR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

.. toctree::   :maxdepth: 2
