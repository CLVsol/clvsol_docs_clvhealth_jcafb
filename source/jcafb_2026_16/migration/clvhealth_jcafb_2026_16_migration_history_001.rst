.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .bgreen {font-weight: bold; color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bblue {font-weight: bold; color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: bgreen
.. role:: blue
.. role:: bblue
.. role:: bmaroon
.. role:: borange
.. role:: bi

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2026-16]" (1)

========================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2026-16] (1)
========================================================

[tkl-odoo16-jcafb26-vm] Preparação do conteúdo do arquivo "host.csv" (2025-05-02a)
----------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Editar manualmente um registro (*row*) do arquivo "/opt/odoo/clvsol_clvhealth_jcafb/project/host.csv", informando as credenciais:

        * name: "**tkl-odoo16-jcafb26-vm**"
        * server: "**https://192.168.25.222**"
        * dbname: "**clvhealth_jcafb_2026_16**"
        * user: "**admin**"
        * user_pw: "*******"
        * user_apikey: "**vazio**"
        * data_user_pw: "*******"
        * data_user_apikey: "**vazio**"
        * master_pw: "*******"
        * notes: "**vazio**"
 
[tkl-odoo16-jcafb26-vm] Criar uma nova instância do *CLVhealth-JCAFB-2026-16*
-----------------------------------------------------------------------------

    #. Criar uma nova instância do :bi:`CLVhealth-JCAFB-2026-16` executando o *Workbook* "**Criação/Manutenção do Banco de Dados "clvhealth_jcafb_2026_16"**" (/opt/clvsol/clvsol_jcafb_odoo16/project/clvsol_jcafb_odoo16.ipynb).

        * **Execution time: 0:09:32.532952**

Criar o *External Sync Host* "http://192.168.25.220:8069"
---------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

    #. Criar o *External Sync Host* **http://192.168.25.220:8069**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**http://192.168.25.220:8069**"
            * External Database Name: "**clvhealth_jcafb_2026_15**"
            * External User: "**admin**"
            * External User Password: "*******"

Configurar todos os "*External Sync Schedules*"
-----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules` (**74**)

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**http://192.168.25.220:8069**"
            * *Max Task Registers*: "**300.000**"

Lista de *Schedules* instalados (00-16-16-18)
---------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled)` clv.global_settings (current_filestore_path) [Sync]

        #. :blue:`(Enabled)` res.users [Migration]
        #. :blue:`(Enabled)` res.users (res.users) [Rec]

        #. :blue:`(Enabled)` clv.phase (clv.phase) [Sync]
        #. :blue:`(Enabled)` clv.global_settings (current_phase_id) [Sync]

        #. :blue:`(Enabled)` clv.file_system.directory (clv.file_system.directory) [Rec]
        #. :blue:`(Enabled)` clv.file_system.directory (clv.file_system.directory) [Sync]

        #. :blue:`(Enabled)` clv.global_tag (clv.global_tag) [Sync]
        #. :blue:`(Enabled)` clv.set (clv.set) [Sync]
        #. :blue:`(Enabled)` clv.set.element (clv.set.element) [1] [Inc]

        #. :blue:`(Enabled)` hr.department (hr.department) [1] [Rec]
        #. :blue:`(Enabled)` hr.department (hr.department) [2] [Sync]
        #. :blue:`(Enabled)` hr.job (hr.job) [Sync]
        #. :blue:`(Enabled)` hr.employee (hr.employee) [1] [Rec]
        #. :blue:`(Enabled)` hr.employee (hr.employee) [2] [Sync]

        #. :blue:`(Enabled)` hr.employee.history (hr.employee.history) [Sync]

        #. :blue:`(Enabled)` survey.survey (survey.survey) [Sync]
        #. :blue:`(Enabled)` survey.question (survey.question) [1] [Sync]
        #. :blue:`(Enabled)` survey.question (survey.question) [2] [Sync]
        #. :blue:`(Enabled)` survey.question.answer (survey.question.answer) [Sync]
        #. :blue:`(Enabled)` survey.user_input (survey.user_input) [1] [Inc]

        #. :blue:`(Enabled)` clv.event (clv.event) [Sync]
        #. :blue:`(Enabled)` clv.event.attendee (clv.event.attendee) [1] [Inc]

        #. :blue:`(Enabled)` clv.document.category (clv.document.category) [Sync]
        #. :blue:`(Enabled)` clv.document.marker (clv.document.marker) [Sync]
        #. :blue:`(Enabled)` clv.document.type (clv.document.type) [1] [Inc]
        #. :blue:`(Enabled)` clv.document.type.parameter (clv.document.type.parameter) [Sync]
        #. :blue:`(Enabled)` clv.document (clv.document) [1] [Inc]
        #. :blue:`(Enabled)` clv.document (clv.document) [2] [Inc]

        #. :blue:`(Enabled)` clv.lab_test.type (clv.lab_test.type) [1] [Inc]
        #. :blue:`(Enabled)` clv.lab_test.type.parameter (clv.lab_test.type.parameter) [Sync]
        #. :blue:`(Enabled)` clv.lab_test.result (clv.lab_test.result) [1] [Inc]

        #. :blue:`(Enabled)` res.country (res.country)
        #. :blue:`(Enabled)` res.country.state (res.country.state)
        #. :blue:`(Enabled)` res.city (res.city)

        #. :blue:`(Enabled)` clv.residence.category (clv.residence.category)
        #. :blue:`(Enabled)` clv.residence.marker (clv.residence.marker)
        #. :blue:`(Enabled)` clv.residence (clv.residence) [1] [Inc]

        #. :blue:`(Enabled)` clv.global_settings (current_date_reference) [Sync]
        #. :blue:`(Enabled)` clv.patient.age_range (clv.patient.age_range)
        #. :blue:`(Enabled)` clv.patient.category (clv.patient.category)
        #. :blue:`(Enabled)` clv.patient.marker (clv.patient.marker)
        #. :blue:`(Enabled)` clv.patient.tag (clv.patient.tag)
        #. :blue:`(Enabled)` clv.patient (clv.patient) [1] [Inc]

        #. :blue:`(Enabled)` clv.patient.history (clv.patient.history) [1] [Inc]

        #. :blue:`(Enabled)` clv.patient_rec (clv.patient_rec) [1] [Inc]

        #. :blue:`(Enabled)` clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)

        #. :blue:`(Enabled)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)
        #. :blue:`(Enabled)` clv.partner_entity.contact_information_pattern (clv.partner_entity.contact_information_pattern)

        #. :blue:`(Enabled)` clv.verification.marker (clv.verification.marker)

Executar o *External Sync Batch* "*Default Batch [00]*"
-------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [00]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [00]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:28:41.449`
            
Lista de *Schedules* instalados (02-16-16-18)
---------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.set.element (clv.set.element) [2] [Sync]

        #. :green:`(Enabled)` survey.user_input (survey.user_input) [2] [Sync]

        #. :green:`(Enabled)` clv.event.attendee (clv.event.attendee) [2] [Sync]

        #. :green:`(Enabled)` clv.document.type (clv.document.type) [2]
        #. :green:`(Enabled)` clv.document (clv.document) [3] [Sync]

        #. :green:`(Enabled)` clv.lab_test.type (clv.lab_test.type) [2] [Sync]
        #. :green:`(Enabled)` clv.lab_test.result (clv.lab_test.result) [2] [Sync]

        #. :green:`(Enabled)` clv.residence (clv.residence) [2] [Sync]

        #. :green:`(Enabled)` clv.patient (clv.patient) [2] [Sync]

        #. :green:`(Enabled)` clv.patient.history (clv.patient.history) [2] [Sync]

        #. :green:`(Enabled)` clv.patient_rec (clv.patient_rec) [2] [Sync]

Executar o *External Sync Batch* "*Default Batch [02]*"
-------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [02]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [02]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:13:37.873`

:borange:`(**)` Lista de *Schedules* instalados (04-16-16-18)
-------------------------------------------------------------

    * Lista de *Schedules* instalados:

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [04]*"
-----------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [04]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [04]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

Lista de *Schedules* instalados (10-16-16-18)
---------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [1] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [2] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [3] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [4] [Sync]

Executar o *External Sync Batch* "*Default Batch [10]*"
-------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:28:09.050`

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Document Type Items Set Up* para os *Document Types*
----------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Document Type Items Set Up` para os :bi:`Document Types`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        #. Selecionar todos os :bi:`Document Types` (**18**)

        #. Executar a Ação ":bi:`Document Type Items Set Up`":

            #. Utilize o botão :bi:`Items Set Up` para executar a Ação.

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Document Items Refresh* para os Documentos
------------------------------------------------------------------------------------------------------------

    #. [[tkl-odoo16-vm-1] Executar a Ação :bi:`Document Items Refresh` para os :bi:`Documents`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `[tkl-odoo16-vm-1 <https://[tkl-odoo16-vm-1>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Items Ok`

        #. Selecionar o primeiro registro com  :bi:`Items Ok` = **Sim**

        #. Executar a Ação ":bi:`Document Items Refresh`":

            #. Adicionar uma linha.

                #. Ativar o filtro :bi:`Items Ok`

                #. Selecionar todos os registros (**500**)

                #. Utilize o botão **Selecionar**.

            #. Utilize o botão :bi:`Items Refresh` para executar a Ação.

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Document Items Update from Survey* para os Documentos
-----------------------------------------------------------------------------------------------------------------------

    #. [[tkl-odoo16-vm-1] Executar a Ação :bi:`Document Items Update from Survey` para os :bi:`Documents`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `[tkl-odoo16-vm-1 <https://[tkl-odoo16-vm-1>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Items Ok`

        #. Selecionar o primeiro registro com  :bi:`Items Ok` = **Sim**

        #. Executar a Ação ":bi:`Document Items Update from Survey`":

            #. Adicionar uma linha.

                #. Ativar o filtro :bi:`Items Ok`

                #. Selecionar todos os registros (**500**)

                #. Utilize o botão **Selecionar**.

            #. Utilize o botão :bi:`Update from Survey` para executar a Ação.

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Lab Test Type Criteria Set Up* para os *Lab Test Types*
-------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para os *Lab Test Types*:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Selecionar todos os :bi:`Lab Test Types` (**14**)

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Lab Test Result Criteria Refresh* para Resultados de Exames
-----------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Lab Test Result Criteria Refresh` para os :bi:`Lab Test Results` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por**» :bi:`Result State`

        #. Selecionar todos os :bi:`Lab Test Results` com: :bi:`Result State` = ":bi:`Approved`" (**244**)

        #. Executar a Ação ":bi:`Lab Test Result Criteria Refresh`":

            #. Utilize o botão :bi:`Criteria Refresh` para executar a Ação.

:red:`(*Não utilizado*)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Lab Test Result Items Update from Survey* para Resultados de Exames
-------------------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Lab Test Result Criteria Refresh` para os :bi:`Lab Test Results` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por**» :bi:`Result State`

        #. Selecionar todos os :bi:`Lab Test Results` com: :bi:`Result State` = ":bi:`Approved`" (**244**)

        #. Executar a Ação ":bi:`Lab Test Result Items Update from Survey`":

            #. Utilize o botão :bi:`Update from Survey` para executar a Ação.

Lista de *Schedules* instalados (20-16-16-18)
---------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.document.item (clv.document.item) [1]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [2]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [3]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [4]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [5]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [6]

Executar o *External Sync Batch* "*Default Batch [20]*"
-------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [20]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [20]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:15:17.410`

Lista de *Schedules* instalados (30-16-16-18)
---------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.lab_test.criterion (clv.lab_test.criterion) [1] [Sync]
        #. :green:`(Enabled)` clv.lab_test.criterion (clv.lab_test.criterion) [2] [Sync]
        #. :green:`(Enabled)` clv.lab_test.criterion (clv.lab_test.criterion) [3] [Sync]

Executar o *External Sync Batch* "*Default Batch [30]*"
-------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar o :bi:`External Sync Batch` "**Default Batch [30]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [30]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:05:55.040`

[tkl-odoo16-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-05-04a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-05-04a.sql

            gzip clvhealth_jcafb_2026_16_2025-05-04a.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-05-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-05-04a.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-05-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-05-04a.sql
.. index:: clvhealth_jcafb_2026_16_2025-05-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-05-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04a

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-05-04a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-05-04a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-05-04a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-jcafb26-vm**".

        #. Salvar o registro editado.

:red:`(Não Executado)` [tkl-odoo16-jcafb26-vm] Atualizar *street2* e *street_number2* da tabela *res_partner*
-------------------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo16-jcafb26-vm:12322 <https://tkl-odoo16-jcafb26-vm:12322>`_.

    #. [tkl-odoo16-jcafb26-vm] Limpar :bi:`street_number2` da tabela :bi:`res_partner`:

        * :bi:`SQL command`:
            ::

                UPDATE res_partner SET
                    street2 = street_number2;

        * :bi:`SQL command`:
            ::

                UPDATE res_partner SET
                    street_number2 = NULL;

[tkl-odoo16-jcafb26-vm] Executar a Verificação de todos os Pacientes (Rec)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Patient (Rec) Verification Execute` para todos os Pacientes (Rec):

        #. Acessar a *View* *Patients (Rec)*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Patients (Rec)`

        #. Selecionar todos os Pacientes (Rec) (**843**)

        #. Executar a Ação ":bi:`Patient (Rec) Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient (Rec) Verification Execute` para executar a Ação.

[tkl-odoo16-jcafb26-vm] Executar a Verificação de todas as Residências
----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Residence Verification Execute` para todas as Residências:

        #. Acessar a *View* *Residences*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as Residências (**366**)

        #. Executar a Ação ":bi:`Residence Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Residence Verification Execute` para executar a Ação.

[tkl-odoo16-jcafb26-vm] Executar a Verificação de todos os Pacientes
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**905**)

        #. Executar a Ação ":bi:`Patient Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

[tkl-odoo16-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-05-04b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-05-04b.sql

            gzip clvhealth_jcafb_2026_16_2025-05-04b.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-05-04b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-05-04b.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-05-04b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-05-04b.sql
.. index:: clvhealth_jcafb_2026_16_2025-05-04b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-05-04b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04b

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-05-04b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-05-04b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-05-04b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-05-04b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-jcafb26-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
