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

====================================
JCAFB-2021v-15 (Exportação de Dados)
====================================

Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2021v-15*
-----------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. :red:`(Não Executado)` Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2021v**

        #. Configurar o parâmetro :bi:`Person` » :bi:`Reference Date`: **31/01/2021**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2021**

Atualisar *Patient (Aux) Age Ranges* para todos os Pacientes (Aux) (método alternativo)
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Patient (Aux): Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient (Aux): Compute Age Reference**"

        #. Executar a Ação Agendada "**Patient (Aux): Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Patient (Aux): Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient (Aux): Update Age Range**"

        #. Executar a Ação Agendada "**Patient (Aux): Update Age Range**", clicando no botão **Rodar Manualmente**.

Atualisar *Patient Age Ranges* para todos os Pacientes (método alternativo)
---------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Patient: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Compute Age Reference**"

        #. Executar a Ação Agendada "**Patient: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Patient: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Update Age Range**"

        #. Executar a Ação Agendada "**Patient: Update Age Range**", clicando no botão **Rodar Manualmente**.

Atualisar *Person Age Ranges* para todas as Pessoas (método alternativo)
------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Person: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Compute Age Reference**"

        #. Executar a Ação Agendada "**Person: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Person: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Update Age Range**"

        #. Executar a Ação Agendada "**Person: Update Age Range**", clicando no botão **Rodar Manualmente**.

.. toctree::   :maxdepth: 2
