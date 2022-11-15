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

===========================================
JCAFB-2023-15 (Recadastramento pré Jornada)
===========================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-10a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2022-11-10a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-10a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_partner_entity
        * clv_residence
        * clv_patient
        * clv_patient_aux

        * clv_l10n_br_base
        * clv_l10n_br_zip

        * clv_partner_entity_l10n_br
        * clv_residence_l10n_br
        * clv_patient_l10n_br
        * clv_patient_aux_l10n_br

        * clv_global_log

        * clv_partner_entity_log_jcafb
        * clv_residence_log_jcafb
        * clv_patient_log_jcafb
        * clv_patient_aux_log_jcafb

        * clv_verification
        * clv_verification_jcafb
        * clv_verification_log_jcafb
        * clv_partner_entity_verification_jcafb
        * clv_residence_verification_jcafb
        * clv_patient_verification_jcafb
        * clv_patient_aux_verification_jcafb

        * clv_processing
        * clv_processing_jcafb

    #. [tkl-odoo15-jcafb23-vm] **Executar** a instalação do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2023-15*
----------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2023**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2023**

Criar as Faixas de Idades de Pacientes para a JCAFB-2023
--------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar as Faixas de Idades de Pacientes para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Age Ranges`

        * Faixas de Idades criadas:
            
            * **0-2 anos**

                * *Name*: **0-1 anos**

                * *From*: **0**

                * *To*: **1**

            * **2-9 anos**

                * *Name*: **2-9 anoss**

                * *From*: **2**

                * *To*: **9**

            * **10-17 anos**

                * *Name*: **10-17 anos**

                * *From*: **10**

                * *To*: **17**

            * **18-59 anos**

                * *Name*: **18-59 anos**

                * *From*: **18**

                * *To*: **59**

            * **60+ anos**

                * *Name*: **60+ anos**

                * *From*: **60**

                * *To*: **120**

Atualizar o *Verification Domain Filter* dos *Verification Schedules* (Current Phase)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Atualizar o *Verification Domain Filter* dos *Verification Schedules*:

        * *Verification Schedules*:

            .. * "Current Phase - clv.address [_address_verification_exec]"

            .. * "Current Phase - clv.address_aux [_address_aux_verification_exec]"

            .. * "Current Phase - clv.family [_family_verification_exec]"

            * "Current Phase - clv.patient [_patient_verification_exec]"

            * "Current Phase - clv.patient_aux [_patient_aux_verification_exec]"

            .. * "Current Phase - clv.person [_person_verification_exec]"

            .. * "Current Phase - clv.person_aux [_person_aux_verification_exec]"

            * "Current Phase - clv.residence [_residence_verification_exec]"

        * Atualização:

            * De: "**[('phase_id', '=', 0)]**"

            * Para: "**[('phase_id', '=', 7)]**" (JCAFB-2023)

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-14a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-14a.sql

            gzip clvhealth_jcafb_2023_15_2022-11-14a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-14a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-14a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-11-14a.sql
.. index:: clvhealth_jcafb_2023_15_2022-11-14a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-11-14a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-14a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-14a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2022-11-14a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-14a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-14a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

:red:`(Não Executado)` Executar o Cadastramento/Recadastramento (Preparação dos Pacientes (Aux))
------------------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento:

        * Workbook: "**JCAFB02021v - clv.patient - Recadastramento (pré Jornada).xlsx**"

        * Planilha: "**Recadastramento (pré Jornada) 1**"

    #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_020`"

    **Método Alternativo Executado**:

        #. [mint20] Copiar manualmente, se necessário, o arquivo "**JCAFB02021v - clv.patient - Recadastramento (pré Jornada).xls**":

            * de: **/home/mint20/Downloads**

            * para: **sftp://odoo@tkl-odoo15-jcafb23-vm/opt/odoo/clvsol_filestore/clvhealth_jcafb** 

        #. [tkl-odoo15-jcafb23-vm] Executar manualmente os *Processing Schedule* **Reregistration Import XLS - Patient (1)** e **Reregistration Import XLS - Patient (2)**:

            #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

            #. Acessar a *View* :bi:`Processing Schedules`:

                * Menu de acesso:

                    * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - Patient (1)**"

            #. Executar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.532`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - Patient (2)**"

            #. Executar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:04.489`

:red:`(Não Executado)` Executar o *Verification Batch* “Current Phase - Default Batch”
--------------------------------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:04.419`

Atualizar o(s) módulo(s) [clv_processing_jcafb]
-----------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_processing_jcafb

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" - m clv_processing_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Executar o Cadastramento/Recadastramento (Preparação dos Pacientes (Aux))
-------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Utilizar como fonte de dados para o Cadastramento/Recadastramento:

        * Workbook: "**Mapeamento IP.xls**"

        * Planilha: "**Geral**"

    #. Aplicar o descrito em :doc:`/user_guide/reregistration/reregistration_workflow_020`"

    **Método Alternativo Executado**:

        #. [mint20] Copiar manualmente, se necessário, o arquivo "**Mapeamento IP.xls**":

            * de: **/home/mint20/Downloads**

            * para: **sftp://odoo@tkl-odoo15-jcafb23-vm/opt/odoo/clvsol_filestore/clvhealth_jcafb** 

        #. [tkl-odoo15-jcafb23-vm] Executar manualmente os *Processing Schedule* **Reregistration Import XLS - JCAFB-2023**:

            #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

            #. Acessar a *View* :bi:`Processing Schedules`:

                * Menu de acesso:

                    * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

            #. Selecionar o *Processing Schedule* "**Reregistration Import XLS - JCAFB-2023**"

            #. Executar a Ação :bi:`Processing Schedule Execute`:

                #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

                * :bi:`Execution time: 0:00:34.392`

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:35.243`

Atualisar *Patient (Aux) Age Ranges* para todos os Pacientes (Aux) (método alternativo)
---------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar manualmente a "Ação Agendada" "**Patient (Aux): Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient (Aux): Compute Age Reference**"

        #. Executar a Ação Agendada "**Patient (Aux): Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb23-vm] Executar manualmente a "Ação Agendada" "**Patient (Aux): Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient (Aux): Update Age Range**"

        #. Executar a Ação Agendada "**Patient (Aux): Update Age Range**", clicando no botão **Rodar Manualmente**.

Atualisar *Patient Age Ranges* para todos os Pacientes (método alternativo)
---------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar manualmente a "Ação Agendada" "**Patient: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Compute Age Reference**"

        #. Executar a Ação Agendada "**Patient: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb23-vm] Executar manualmente a "Ação Agendada" "**Patient: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Update Age Range**"

        #. Executar a Ação Agendada "**Patient: Update Age Range**", clicando no botão **Rodar Manualmente**.

.. toctree::   :maxdepth: 2
