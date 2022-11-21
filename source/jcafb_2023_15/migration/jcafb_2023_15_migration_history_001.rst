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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2023-15]"

====================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2023-15]
====================================================

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

:borange:`(**)` Atualizar os fontes do projeto
----------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb23-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            su odoo

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_export
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Habilitar a instalação do(s) módulo(s) [ver lista]
--------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * mail
        * hr
        * contacts
        * base_address_city
        * base_address_extended
        * survey

        * clv_base
        * clv_phase
        * clv_file_system
        * clv_global_tag
        * clv_set
        * clv_employee
        * clv_employee_history
        * clv_survey

        * clv_base_jcafb
        * clv_employee_jcafb

        * clv_external_sync
        * clv_base_sync
        * clv_phase_sync
        * clv_file_system_sync
        * clv_global_tag_sync
        * clv_set_sync
        * clv_employee_sync
        * clv_employee_history_sync
        * clv_survey_sync

        * clv_external_sync_jcafb
        * clv_employee_sync_jcafb

Criar uma nova instância do *CLVhealth-JCAFB-2023-15*
------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Excluir a instância do *CLVhealth-JCAFB-2023-15* existente:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2023_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb23-vm (session 2)
            #

            ssh tkl-odoo15-jcafb23-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        * **Execution time: 0:02:19.464**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar o *External Sync Host* "https://192.168.25.203"
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar o *External Sync Host* **https://192.168.25.203**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**https://192.168.25.203**"
            * External Database Name: "**clvhealth_jcafb_2021v_14n**"
            * External User: "**admin**"
            * External User Password: "*******"

Configurar todos os "*External Sync Schedules*"
-----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.203**"
            * *Max Task Registers*: "**300.000**"

Desabilitar os "*External Sync Batch Members*" não necessários
--------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Lista de *External Sync Batch Members*:

        #. *External Sync Batch* "*Default Batch [00]*":

            #. :red:`(Disabled)` clv.global_settings (current_phase_id) [Sync]

            #. :red:`(Disabled)` clv.file_system.directory (clv.file_system.directory) [Rec]
            #. :red:`(Disabled)` clv.file_system.directory (clv.file_system.directory) [Sync]

            #. :red:`(Disabled)` clv.global_tag (clv.global_tag) [Sync]

            #. :red:`(Disabled)` clv.set (clv.set) [Sync]
            #. :red:`(Disabled)` clv.set.element (clv.set.element) [1] [Inc]

            #. :red:`(Disabled)` survey.user_input (survey.user_input) [1] [Inc]

        #. *External Sync Batch* "*Default Batch [02]*":

            #. :red:`(Disabled)` clv.set.element (clv.set.element) [2] [Sync]

            #. :red:`(Disabled)` survey.user_input (survey.user_input) [2] [Sync]

        #. *External Sync Batch* "*Default Batch [10]*":

            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [1] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [2] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [3] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [4] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [5] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [6] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [7] [Sync]
            #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [8] [Sync]

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, os :bi:`External Sync Batch Members` não necessários:

        * Lista de *Schedules*:

            * Marcar os :bi:`External Sync Batch Members` não necessários e que se deseja desabilitar.

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Batch Member Mass Edit`

        * Parâmetros alterados:
            
            * *Enabled*: "**desabilitado**"

Lista de *Schedules* instalados (00-23-15)
------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled)` clv.global_settings (current_filestore_path) [Sync]

        #. :blue:`(Enabled)` res.users [Migration]
        #. :blue:`(Enabled)` res.users (res.users) [Rec]

        #. :blue:`(Enabled)` clv.phase (clv.phase) [Sync]
        #. :red:`(Disabled)` clv.global_settings (current_phase_id) [Sync]

        #. :red:`(Disabled)` clv.file_system.directory (clv.file_system.directory) [Rec]
        #. :red:`(Disabled)` clv.file_system.directory (clv.file_system.directory) [Sync]

        #. :red:`(Disabled)` clv.global_tag (clv.global_tag) [Sync]

        #. :red:`(Disabled)` clv.set (clv.set) [Sync]
        #. :red:`(Disabled)` clv.set.element (clv.set.element) [1] [Inc]

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
        #. :red:`(Disabled)` survey.user_input (survey.user_input) [1] [Inc]

        .. #. :blue:`(Enabled)` clv.event (clv.event) [Sync]
        .. #. :blue:`(Enabled)` clv.event.attendee (clv.event.attendee) [1] [Inc]

        .. #. :blue:`(Enabled)` clv.document.category (clv.document.category) [Sync]
        .. #. :blue:`(Enabled)` clv.document.marker (clv.document.marker) [Sync]
        .. #. :blue:`(Enabled)` clv.document.type (clv.document.type) [1] [Inc]
        .. #. :blue:`(Enabled)` clv.document.type.parameter (clv.document.type.parameter) [Sync]
        .. #. :blue:`(Enabled)` clv.document (clv.document) [1] [Inc]
        .. #. :blue:`(Enabled)` clv.document (clv.document) [2] [Inc]

        .. #. :blue:`(Enabled)` clv.lab_test.type (clv.lab_test.type) [1] [Inc]
        .. #. :blue:`(Enabled)` clv.lab_test.type.parameter (clv.lab_test.type.parameter) [Sync]
        .. #. :blue:`(Enabled)` clv.lab_test.request (clv.lab_test.request) [1] [Inc]
        .. #. :blue:`(Enabled)` clv.lab_test.result (clv.lab_test.result) [1] [Inc]
        .. #. :blue:`(Enabled)` clv.lab_test.report (clv.lab_test.report) [1] [Inc]

        .. #. :blue:`(Enabled)` res.country (res.country)
        .. #. :blue:`(Enabled)` res.country.state (res.country.state)
        .. #. :blue:`(Enabled)` res.city (res.city)

        .. #. :blue:`(Enabled)` clv.residence.category (clv.residence.category)
        .. #. :blue:`(Enabled)` clv.residence.marker (clv.residence.marker)
        .. #. :blue:`(Enabled)` clv.residence (clv.residence) [1]

        .. #. :blue:`(Enabled)` clv.residence.history (clv.residence.history) [1]

        .. #. :blue:`(Enabled)` clv.patient.age_range (clv.patient.age_range)
        .. #. :blue:`(Enabled)` clv.patient.category (clv.patient.category)
        .. #. :blue:`(Enabled)` clv.patient.marker (clv.patient.marker)
        .. #. :blue:`(Enabled)` clv.patient (clv.patient) [1]

        .. #. :blue:`(Enabled)` clv.patient.history (clv.patient.history) [1]

        .. #. :blue:`(Enabled)` clv.patient_aux (clv.patient_aux)

        .. #. :blue:`(Enabled)` clv.address.category (clv.address.category)
        .. #. :blue:`(Enabled)` clv.address.marker (clv.address.marker)
        .. #. :blue:`(Enabled)` clv.address (clv.address)

        .. #. :blue:`(Enabled)` clv.address.history (clv.address.history)

        .. #. :blue:`(Enabled)` clv.family.category (clv.family.category)
        .. #. :blue:`(Enabled)` clv.family (clv.family)

        .. #. :blue:`(Enabled)` clv.family.history (clv.family.history)

        .. #. :blue:`(Enabled)` clv.person.age_range (clv.person.age_range)
        .. #. :blue:`(Enabled)` clv.person.category (clv.person.category)
        .. #. :blue:`(Enabled)` clv.person.marker (clv.person.marker)
        .. #. :blue:`(Enabled)` clv.person (clv.person)

        .. #. :blue:`(Enabled)` clv.person.relation.type (clv.person.relation.type)
        .. #. :blue:`(Enabled)` clv.person.relation (clv.person.relation)

        .. #. :blue:`(Enabled)` clv.person.history (clv.person.history)

        .. #. :blue:`(Enabled)` clv.address_aux (clv.address_aux)

        .. #. :blue:`(Enabled)` clv.person_aux (clv.person_aux)

        .. #. :blue:`(Enabled)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)
        .. #. :blue:`(Enabled)` clv.partner_entity.contact_information_pattern (clv.partner_entity.contact_information_pattern)

        .. #. :blue:`(Enabled)` clv.verification.marker (clv.verification.marker)
        .. #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [1]
        .. #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [2]
        .. #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [3]
        .. #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [4]

Executar o *External Sync Batch* "*Default Batch [00]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar o :bi:`External Sync Batch` "**Default Batch [00]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [00]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:07:12.952`
            
Lista de *Schedules* instalados (02-23-15)
------------------------------------------

    * Lista de *Schedules* instalados:

        #. :red:`(Disabled)` clv.set.element (clv.set.element) [2] [Sync]

        #. :red:`(Disabled)` survey.user_input (survey.user_input) [2] [Sync]

        .. #. :blue:`(Enabled)` clv.event.attendee (clv.event.attendee) [2] [Sync]

        .. #. :blue:`(Enabled)` clv.document.type (clv.document.type) [2]
        .. #. :blue:`(Enabled)` clv.document (clv.document) [3] [Sync]

        .. #. :blue:`(Enabled)` clv.lab_test.type (clv.lab_test.type) [2] [Sync]
        .. #. :blue:`(Enabled)` clv.lab_test.request (clv.lab_test.request) [2] [Sync]
        .. #. :blue:`(Enabled)` clv.lab_test.result (clv.lab_test.result) [2] [Sync]
        .. #. :blue:`(Enabled)` clv.lab_test.report (clv.lab_test.report) [2] [Sync]

        .. #. :blue:`(Enabled)` clv.residence (clv.residence) [2]

        .. #. :blue:`(Enabled)` clv.residence.history (clv.residence.history) [2]

        .. #. :blue:`(Enabled)` clv.patient (clv.patient) [2]

        .. #. :blue:`(Enabled)` clv.patient.history (clv.patient.history) [2]

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [02]*"
------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar o :bi:`External Sync Batch` "**Default Batch [02]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [02]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

Lista de *Schedules* instalados (10-23-15)
------------------------------------------

    * Lista de *Schedules* instalados:

        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [1] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [2] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [3] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [4] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [5] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [6] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [7] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [8] [Sync]

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [10]*"
------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21a)
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
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21a.sql

            gzip clvhealth_jcafb_2023_15_2022-11-21a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-11-21a.sql
.. index:: clvhealth_jcafb_2023_15_2022-11-21a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-11-21a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21a)
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
            # gzip -d clvhealth_jcafb_2023_15_2022-11-21a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-21a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
