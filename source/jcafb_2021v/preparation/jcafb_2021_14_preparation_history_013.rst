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

Criar os Documentos para as Crianças selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSC21**

                    #. **QSF21**

                    #. **TCR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para os Idosos selecionados para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QMD21**

                    #. **QSF21**

                    #. **QSI21**

                    #. **TID21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar as Requisições de Exames para as Crianças selecionadas para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Test Request Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EEV21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Criar as Requisições de Exames para os Idosos selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Test Request Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EUR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:19.032`

Criar os Sumários para os Grupos de Campo do Projeto JCAFB-2021v
----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Employee Summary Set Up` para os Grupos de Campo do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar todos os Funcionários com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

Criar os Sumários para as Residências selecionados para o Projeto JCAFB-2021v
-----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Residence Summary Set Up` para as Residências selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Residence State`

        #. Selecionar todos as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Residence State` = ":bi:`Selected`"

        #. Executar a Ação ":bi:`Residence Summary Set Up`":

            #. Utilize o botão :bi:`Residence Summary Set Up` para executar a Ação.

Criar os Sumários para os Pacientes selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State`

        #. Selecionar todos as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Patient State` = ":bi:`Selected`"

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

.. toctree::   :maxdepth: 2
