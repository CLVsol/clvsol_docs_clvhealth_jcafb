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

Criar os Grupos para a JCAFB-2021v
----------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar os Departamentos para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Departamentos`

        * Departamentos Criados:
            
            * **Grupo 01 (2021v)**

                * Nome do Departamento: "**Grupo 01 (2021v)**"

            * **Grupo 02 (2021v)**

                * Nome do Departamento: "**Grupo 02 (2021v)**"

            * **Grupo 03 (2021v)**

                * Nome do Departamento: "**Grupo 03 (2021v)**"

            * **Grupo 04 (2021v)**

                * Nome do Departamento: "**Grupo 04 (2021v)**"

    #. Criar os Funcionários para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        * Funcionários Criados:
            
            * **Grupo 01 (2021v)**

                * Nome do Funcionário: "**Grupo 01 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 01 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 02 (2021v)**

                * Nome do Funcionário: "**Grupo 02 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 02 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 03 (2021v)**

                * Nome do Funcionário: "**Grupo 03 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 03 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 04 (2021v)**

                * Nome do Funcionário: "**Grupo 04 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 04 (2021v)**
                * Cargo: **Grupo de Campo**

    #. Associar os Funcionários aos Departamentos:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        * Beatriz Rossi Bonin (Coordenador Geral): **Grupo 01 (2021v)**
        * Sofia Schalka (Coordenador Geral): **Grupo 01 (2021v)**

        * Beatriz Cerdá Mendes de Araujo (Coordenador de Campo): **Grupo 02 (2021v)**
        * Sarah de Araújo Sprenge (Coordenador de Campo): **Grupo 02 (2021v)**

        * Felipe Barboza Galhard (Coordenador de Campanha): **Grupo 03 (2021v)**
        * Guilherme Souza Macário (Coordenador de Campanha): **Grupo 03 (2021v)**

        * Luís Carlos Fogaça dos Santos (Coordenador de Análises): **Grupo 04 (2021v)**
        * Suelen Martins da Costa (Coordenador de Análises): **Grupo 04 (2021v)**
        * Rodrigo Gonçalves Queijo (Coordenador de Comunicação): **Grupo 04 (2021v)**

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
