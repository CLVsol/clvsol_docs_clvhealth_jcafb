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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-01a)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-01a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-01a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Executar a "Preparação do Cadastro Auxiliar" (Fase 1)
-----------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`"

    #. Excluir todos os registros de Pessoas do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_010`".

    #. Excluir todos os registros de Endereços do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_020`".

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05a)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05a.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-05a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-05a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-05a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-05a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05a

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05a)
-------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-05a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-05a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Executar a "Preparação do Cadastro Auxiliar" (Fase 2)
-----------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`"

    #. Associar todas as Pessoas a uma Pessoa (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_030`".

    #. Associar todos os Endereços a um Endereço (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_040`".

    #. Remover a Fase de todas as Pessoas (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_050`".

    #. Remover a Fase de todos os Endereços (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_060`".

Adicionar novos *Street Patterns*
---------------------------------

    #. Adicionar os novos *Street Patterns* listados a seguir, utilizando o procedimento :doc:`/procedures/reregistration/reregistration_procedure_030_010_025`:

        * *Family (Aux)* "Estância Nossa Senhora Aparecida (Porto)" [140.498-99].

        * *Family (Aux)* "Fazenda Luvre, casa 2 (Porto)" [140.324-90].

:red:`(Não Executado)` Executar o *Verification Batch* “Default Batch”
----------------------------------------------------------------------

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:29:26.517`

Executar o *Verification Batch* “Default Batch” (método alternativo)
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:32:01.916`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05b)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05b.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-05b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-05b.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-05b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-05b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05b

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05b)
-------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-05b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-05b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Executar a Criação do Cadastro Auxiliar (Fase 1 - Criação do Cadastro Auxiliar)
-------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento (Fase 1):

        * Workbook: "**JCAFB02021v - clv.person - Recadastramento (pré Jornada).xlsx**"

        * Planilha: "**Recadastramento (pré Jornada) 1**"

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration/reregistration_workflow_020`"

    **Método Alternativo**:

    #. [mint19] Copiar manualmente o arquivo "**JCAFB02021v - clv.person - Recadastramento (pré Jornada).xls**":

        * de: **/home/mint19/Downloads**

        * para: **sftp://odoo@tkl-odoo14-jcafb21-vm/opt/odoo/clvsol_filestore/clvhealth_jcafb** 

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente os *Processing Schedules* **Regegistration Import XLS (1)** e **Regegistration Import XLS (2)**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar os *Processing Schedules* "**Regegistration Import XLS (1)**" e "**Regegistration Import XLS (2)**"

        #. Exercutar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

:red:`(Não Executado)` Executar o *Verification Batch* “Current Phase - Default Batch”
--------------------------------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:15.537`

Executar o *Verification Batch* “Current Phase - Default Batch” (método alternativo)
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Current Phase - Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:00:58.126`

Adicionar novos *Street Patterns*
---------------------------------

    #. Adicionar os novos *Street Patterns* listados a seguir, utilizando o procedimento :doc:`/procedures/reregistration/reregistration_procedure_030_010_025`:

        * *Family (Aux)* "Rua Nova Batatais, 98 (Centro)" [].

        * *Family (Aux)* "Rua Nova Fernão, 84 (Centro)" [].

        * *Family (Aux)* "Rua Nova Olinda, 95 (Centro)" [].

Executar o *Verification Batch* “Current Phase - Default Batch” (método alternativo)
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Current Phase - Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:00:55.170`

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

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Current Phase - Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:02:02.146`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05c)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05c.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-05c.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-05c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05c.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-05c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-05c.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-05c.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-05c
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05c

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-05c)
-------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-05c.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-05c.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-05c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Executar o *Verification Batch* “Default Batch” (método alternativo)
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:30:07.783`

Atualizar a Fase de Famílias afetadas pelo Recadastramento
----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Mass Edit` para Famílias afetadas pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Address "Phase" mismatch.`"

        #. Exercutar a Ação ":bi:`Family Mass Edit`":

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

        #. Exercutar a Ação ":bi:`Family Mass Edit`":

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

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:01:58.870`

Atualizar o *State* de Endereços afetados pelo Recadastramento
--------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit` para Endereços afetados pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Information`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = :bi:`Warning (L0)` » :bi:`Verification Outcome Information` = ":bi:`Please, verify "Address State".`"

        #. Exercutar a Ação ":bi:`Address Mass Edit`":

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

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:31:59.622`

Atualizar o *State* de Endereços (Aux) afetados pelo Recadastramento
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address (Aux) Reload` para Endereços (Aux) afetados pelo Recadastramento:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**Indefinido**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"State" has changed.`

        #. Exercutar a Ação ":bi:`Address (Aux) Reload`":

            * Parâmetros utilizados:

                * *Address (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

Atualizar o *Register State* dos Endereços já recadastrados
-----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit` para os Endereços já recadastrados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`Ok`

        #. Exercutar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Address Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Famílias já recadastradas
-----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Mass Edit` para as Famílias já recadastradas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`Ok`

        #. Exercutar a Ação ":bi:`Family Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Family Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Pessoas já recadastradas
-----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para as Pessoas já recadastradas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`Ok`

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Endereços (Aux) já recadastrados
-----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address (Aux) Mass Edit` para os Endereços (Aux) já recadastrados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todos os Endereços (Aux) com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`Ok`

        #. Exercutar a Ação ":bi:`Address (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Address (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Pessoas (Aux) já recadastradas
---------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person (Aux) Mass Edit` para as Pessoas (Aux) já recadastradas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todas as Pessoas (Aux) com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`Ok`

        #. Exercutar a Ação ":bi:`Person (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Cancelar a Pessoa "Valmir Lourenço Almeida Barbosa [210.540-37]"
----------------------------------------------------------------

    Está sendo assumido que "Valmir Lourenço Almeida Barbosa [210.540-37]" já possui um registro válido como "Valmir Lourenço Almeida Barbosa [210.541-18]".

    #. Cancelar a Pessoa "Valmir Lourenço Almeida Barbosa [210.540-37]" nos Cadastros Auxiliar e Principal:

        #. Acessar a *view* :bi:`Persons (Aux)`:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

        #. Procurar pelo registro :bi:`Person (Aux)` associado a "Valmir Lourenço Almeida Barbosa [210.540-37]".

        #. Abrir o registro :bi:`Person (Aux)` encontrado.

            #. Exercutar a Ação ":bi:`Person (Aux) Mass Edit`":

                #. Parâmetros apresentados:

                    * *Register State*: :bi:`Set` » :bi:`Canceled`
                    * *State*: :bi:`Set` » :bi:`Unvailable`
                    * *Address is unavailable*: :bi:`Set` » **marcado**
                    * *Address*: :bi:`Remove`
                    * *Address (Aux) is unavailable*: :bi:`Set` » **marcado**
                    * *Address (Aux)*: :bi:`Remove`
                    * *Family is unavailable*: :bi:`Set` » **marcado**
                    * *Family*: :bi:`Remove`
                    * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                    * *Clear Address Data*: **marcado**
                    * *Phase*: **JCAFB-2021v**
                    * *Person (Aux) Verification Execute*: **marcado**

                #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

            #. Exercutar a Ação ":bi:`Person (Aux) Related Person Update`":

                #. Parâmetros apresentados:

                    * *Update Contact Information Data*: **marcado**
                    * *Update Address Data*: **marcado**
                    * *Update Family Data*: **marcado**
                    * *Related Person Verification Execute*: **marcado**
                    * *Person (Aux) Verification Execute*: **marcado**

                #. Utilizar o botão :bi:`Related Person Update` para executar a Ação.

        #. Acessar a *view* :bi:`Addresses (Aux)`:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`


        #. Procurar pelo registro :bi:`Address (Aux)` associado a "Estância Nossa Senhora Aparecida (Porto) [140.498-99]".

        #. Abrir o registro :bi:`Address (Aux)` encontrado.

            #. Exercutar a Ação ":bi:`Address (Aux) Mass Edit`":

                #. Parâmetros apresentados:

                    * *Register State*: :bi:`Set` » :bi:`Done`
                    * *Address (Aux) Verification Execute*: **marcado**

                #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

        #. Acessar a *view* :bi:`Persons (Aux)`:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Verification State` = :bi:`[Warning (L1)]`

        #. Exercutar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Done`
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Exercutar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:01:57.474`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-11a)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-11a.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-11a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-11a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-11a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-11a

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-11a)
-------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-11a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-11a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2