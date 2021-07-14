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

=============================================
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

:borange:`(**)` Atualizar o(s) módulo(s) [clv_lab_test, clv_lab_test_jcafb]
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_lab_test
        * clv_lab_test_jcafb

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Atualizar o(s) módulo(s) [clv_survey]
-----------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_survey

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_survey
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Types* do Projeto JCAFB-2021v
--------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para os :bi:`Lab Test Types` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os :bi:`Lab Test Types` com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

Executar a Ação *Lab Test Request Receive* para recebimento de uma amostra para Exame
-------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Receive` para um :bi:`Lab Test Request` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Pesquisar pelo **Código** do :bi:`Lab Test Request` desejado.

        #. Executar a Ação ":bi:`Lab Test Request Receive`" para o registro encontrado:

            * Parâmetros utilizados:

                * Aceitar todos os parâmetros apresentados

            #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

Trascrição das Respostas de uma Folha de Resultados via Resultado de Exame associado
------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *Lab Test Results*:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Lab Test Type` ou qualquer outro para facilitar a procura pelo Resultado de Exame desejado.

    #. Selecionar e abrir o Resultado de Exame desejado.

    #. Executar a Ação ":bi:`Lab Test Result Set Survey User Input`":

        #. Utilize o botão :bi:`Set Survey User Input` para executar a Ação.

    #. Acessar o *link* apresentado no campo ":bi:`Survey URL`".

    #. Iniciar a Pesquisa.

Executar a Ação *Lab Test Result Criteria Refresh* para Resultados de Exames do Projeto JCAFB-2021v
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Result Criteria Refresh` para os :bi:`Lab Test Results` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Lab Test Results` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Lab Test Result Criteria Refresh`":

            #. Utilize o botão :bi:`Criteria Refresh` para executar a Ação.

:red:`(Não Utilizado)` Trascrição dos Resultados de um Exame via URL genérica
-----------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21-vm] usando uma das URLs:

        * [EAA21] JCAFB 2021 - Laboratório - Análise de Água: `http://tkl-odoo14-jcafb21-vm/survey/start/eaa21 <http://tkl-odoo14-jcafb21-vm/survey/start/eaa21>`_

        * [EAN21] JCAFB 2021 - Exames para detecção de Anemia: `http://tkl-odoo14-jcafb21-vm/survey/start/ean21 <http://tkl-odoo14-jcafb21-vm/survey/start/ean21>`_

        * [ECP21] JCAFB 2021 - JCAFB 2021 - Laboratório - Parasitologia: `http://tkl-odoo14-jcafb21-vm/survey/start/ecp21 <http://tkl-odoo14-jcafb21-vm/survey/start/ecp21>`_

        * [EDH21] JCAFB 2021- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21-vm/survey/start/edh21 <http://tkl-odoo14-jcafb21-vm/survey/start/edh21>`_

        * [EEV21] JCAFB 2021 - Laboratório - Pesquisa de Enterobius vermicularis: `http://tkl-odoo14-jcafb21-vm/survey/start/eev21 <http://tkl-odoo14-jcafb21-vm/survey/start/eev21>`_

        * [EUR21] JCAFB 2021 - Laboratório - Urinálise: `http://tkl-odoo14-jcafb21-vm/survey/start/eur21 <http://tkl-odoo14-jcafb21-vm/survey/start/eur21>`_

    #. Iniciar a Pesquisa.

.. toctree::   :maxdepth: 2
