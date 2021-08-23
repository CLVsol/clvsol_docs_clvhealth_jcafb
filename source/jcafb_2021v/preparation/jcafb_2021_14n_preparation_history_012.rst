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

================================================================================
Preparação do Banco de Dados - JCAFB-2021v-14n (Recadastramento (pré Jornada) 1)
================================================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-08-21b)
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
            # gzip -d clvhealth_jcafb_2021v_14n_2021-08-21b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-08-21b.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-21b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-21b.tar.gz

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

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_patient_aux

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o *Patient Category* de Pacientes (Aux) da JCAFB-2021v
----------------------------------------------------------------

    Critérios utilizados:

        * **Criança**: todos os Pacientes na faixa etária "3-10 anos".

        * **Idoso**: todos os Pacientes na faixa etária "60+ anos".

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient (Aux) Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient (Aux) State` » :bi:`Categories`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" :bi:`Patient (Aux) State` = "**Unavailable**" » :bi:`Category` = "**Criança**"

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **nenhuma ação**

                * *Categories*: **Remove** » **Criança**

                * *Patient (Aux) Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" :bi:`Patient (Aux) State` = "**Unavailable**" » :bi:`Category` = "**Idoso**"

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **nenhuma ação**

                * *Categories*: **Remove** » **Idoso**

                * *Patient (Aux) Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient (Aux) Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient (Aux) State` » :bi:`Categories` » :bi:`Age Ranges`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Patient (Aux) State` = "**Available**" » :bi:`Category` = "**Indefinido**" :bi:`Age Range` = "**3-10 anos**"

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **nenhuma ação**

                * *Categories*: **Set** » **Criança**

                * *Patient (Aux) Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Patient (Aux) State` = "**Available**" » :bi:`Category` = "**Indefinido**" :bi:`Age Range` = "**60+ anos**"

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Revised**

                * *State*: **nenhuma ação**

                * *Categories*: **Set** » **Idoso**

                * *Patient (Aux) Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação**

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

            * :bi:`Execution time: 0:00:16.570`

Consolidação das Entidades do Cadastro Auxiliar
-----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_080`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_030_020_020_090`"

Atualizar o *Register State* dos Pacientes já recadastrados
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes (Aux) já recadastrados
-----------------------------------------------------------------

    #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar as Crianças para o Projeto JCAFB-2021v
-------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient Mass Edit` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar a classificação dos Pacientes pelo campo :bi:`Ramdon ID`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar os 20 primeiros Pacientes listados com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Available`

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** » **Selected**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar os Idosos para o Projeto JCAFB-2021v
-----------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient Mass Edit` para os Idosos selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar a classificação dos Pacientes pelo campo :bi:`Ramdon ID`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar os 20 primeiros Pacientes listados com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Available`

        #. Executar a Ação ":bi:`Patient Mass Edit`":

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

            * :bi:`Execution time: 0:00:14.895`

Selecionar os Pacientes (Aux) para o Projeto JCAFB-2021v
--------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient (Aux) Reload` para os Pacientes (Aux) selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Verification State` = ":bi:`Warning (L1)`" » :bi:`Verification Outcome Informations` = :bi:`"State" has changed.`

        #. Executar a Ação ":bi:`Patient (Aux) Reload`":

            * Parâmetros utilizados:

                * *Update Contact Information Data*: **desmarcado**

                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

Associar os Pacientes selecionados aos Grupos da JCAFB-2021v
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Acessar a *View* *Patients*:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Responsible Employee` » :bi:`Address Name` » :bi:`Categories`

    #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`:

        * Distribuir os Idosos e Crianças selecionados pelos Grupos da JCAFB-2021v de forma que o números de Idosos e Crianças sejam equanimemente distribuido entre os Grupos.

    #. Para a verificação da distribuição dos Pacientes entre os Grupos, em uma outra *Tab*, ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Employee` » :bi:`Categories`.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-08-23a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-08-23a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-08-23a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-08-23a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-08-23a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-08-23a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-08-23a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-08-23a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-08-23a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-23a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-08-23a)
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
            # gzip -d clvhealth_jcafb_2021v_14n_2021-08-23a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-08-23a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-23a.tar.gz

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

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_residence_sync_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_residence_sync_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Executar o *External Sync Schedule* "clv.residence (clv.residence)"
-----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.residence**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.residence**":

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

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Schedule` "**clv.residence (clv.residence)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.residence (clv.residence)**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.residence (clv.residence)**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:01:31.078`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

Associar os Pacientes selecionados a uma Residência
---------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação *Patient Associate to Residence* para os Pacientes selecionados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Residence`

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido`:

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido`:

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

Atualizar o *Residence Category* de todas as Residências
--------------------------------------------------------

    Critérios utilizados:

        * **Zona Rural**: todas as Residências da Zona Rural".

        * **Zona Urbana**: todas as Residências da Zona Urbana".

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Categories`

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas na Zona Rural.

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Zona Rural**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas na Zona Urbana.


        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Zona Urbana**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o Cadastramento/Recadastramento (Consolidação das Entidades do Cadastro Principal)
-------------------------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Aplicar o descrito em :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040`"

    **Ações efetivamente executadas**:

        Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

        Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_040`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_045`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_050`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_060`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_030_070`"

        #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_040`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_040_010`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_040_110`"

            #. :doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_040_040_120`"

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:18.782`

.. toctree::   :maxdepth: 2
