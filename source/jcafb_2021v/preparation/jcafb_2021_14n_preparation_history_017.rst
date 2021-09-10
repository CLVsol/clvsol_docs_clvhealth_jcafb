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

====================================================
JCAFB-2021v-14n (Tratamento de Resultados de Exames)
====================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-10a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-10a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-10a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Executar a Ação *Lab Test Request Receive* para recebimento de amostras para Exame
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Request Receive` para um :bi:`Lab Test Request` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Pesquisar pelo **Código** do :bi:`Lab Test Request` desejado.

        #. Executar a Ação ":bi:`Lab Test Request Receive`" para o registro encontrado:

            * Parâmetros utilizados:

                * Aceitar todos os parâmetros apresentados

            #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

Trascrição de Respostas de Folhas de Resultados de Exames via URL genérica
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21n-vm] usando uma das URLs:

        * [EAA21] JCAFB 2021 - Laboratório - Análise de Água: `http://tkl-odoo14-jcafb21n-vm/survey/start/eaa21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eaa21>`_

        * [EAN21] JCAFB 2021 - Exames para detecção de Anemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/ean21 <http://tkl-odoo14-jcafb21n-vm/survey/start/ean21>`_

        * [ECP21] JCAFB 2021 - Laboratório - Parasitologia: `http://tkl-odoo14-jcafb21n-vm/survey/start/ecp21 <http://tkl-odoo14-jcafb21n-vm/survey/start/ecp21>`_

        * [EDH21] JCAFB 2021- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/edh21 <http://tkl-odoo14-jcafb21n-vm/survey/start/edh21>`_

        * [EEV21] JCAFB 2021 -  Laboratório - Pesquisa de Enterobius vermicularis: `http://tkl-odoo14-jcafb21n-vm/survey/start/eev21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eev21>`_

        * [EUR21] JCAFB 2021 - Laboratório - Urinálise: `http://tkl-odoo14-jcafb21n-vm/survey/start/eur21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eur21>`_

    #. Iniciar a Pesquisa.

:borange:`(**)` Atualizar o *Lab Test Types* dos *Lab Test Types* do Projeto JCAFB-2021v
----------------------------------------------------------------------------------------

    Parâmetros utilizados:

        * **EAN21**: **[EAN21]**

        * **EDH21**: **[EDH21]**.

        * **EAA21**: **[EAA21]**.

        * **ECP21**: **[ECP21]**.

        * **EEV21**: **[EEV21]**.

        * **EUR21**: **[EUR21]**.

    #. [tkl-odoo14-jcafb21n-vm] Atualizar o *Lab Test Types* dos *Lab Test Types* do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Editar todos os *Lab Test Types* com: :bi:`Phase` = "**JCAFB-2021v**".

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_survey
        * clv_document_jcafb
        * clv_lab_test_jcafb

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_survey

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Executar a Ação *Lab Test Request Receive* para recebimento de amostras para Exame
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Request Receive` para um :bi:`Lab Test Request` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Pesquisar pelo **Código** do :bi:`Lab Test Request` desejado.

        #. Executar a Ação ":bi:`Lab Test Request Receive`" para o registro encontrado:

            * Parâmetros utilizados:

                * Aceitar todos os parâmetros apresentados

            #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

Trascrição de Respostas de Folhas de Resultados via Resultados de Exame associados
----------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Acessar a *View* *Lab Test Results*:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Lab Test Type` ou qualquer outro para facilitar a procura pelo Resultado de Exame desejado.

    #. Selecionar e abrir o Resultado de Exame desejado.

    #. Executar a Ação ":bi:`Lab Test Result Set Survey User Input`":

        #. Utilize o botão :bi:`Set Survey User Input` para executar a Ação.

    #. Acessar o *link* apresentado no campo ":bi:`Survey URL`".

    #. Iniciar a Pesquisa.

Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Types* do Projeto JCAFB-2021v
--------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para os :bi:`Lab Test Types` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os :bi:`Lab Test Types` com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

Executar a Ação *Lab Test Result Criteria Refresh* para Resultados de Exames do Projeto JCAFB-2021v
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Result Criteria Refresh` para os :bi:`Lab Test Results` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Lab Test Results` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Lab Test Result Criteria Refresh`":

            #. Utilize o botão :bi:`Criteria Refresh` para executar a Ação.

Executar a Ação *Lab Test Result Items Update from Survey* para Resultados de Exames do Projeto JCAFB-2021v
-----------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Result Items Update from Survey` para os :bi:`Lab Test Results` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Lab Test Results` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Lab Test Result Items Update from Survey`":

            #. Utilize o botão :bi:`Update from Survey` para executar a Ação.

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_lab_test

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

.. toctree::   :maxdepth: 2
