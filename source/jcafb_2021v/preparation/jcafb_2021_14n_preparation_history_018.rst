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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-10-01a)
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
            # gzip -d clvhealth_jcafb_2021v_14n_2021-10-01a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-10-01a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz

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

:borange:`(**)` Executar o *External Sync Schedule* "clv.lab_test.type (clv.lab_test.type)"
-------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.lab_test.type**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.lab_test.type**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Schedule` "**clv.lab_test.type (clv.lab_test.type)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.lab_test.type (clv.lab_test.type)**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.lab_test.type (clv.lab_test.type)**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:00:04.330`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` Executar o *External Sync Schedule* "clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)"
-------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.lab_test.export_xls.param**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.lab_test.export_xls.param**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Schedule` "**clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:00:02.002`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

.. toctree::   :maxdepth: 2
