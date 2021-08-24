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

======================================================
Migração do Banco de Dados - CLVhealth-JCAFB-2021v-14n
======================================================

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

:borange:`(**)` Atualizar os fontes do projeto
----------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21n-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            # ***** tkl-odoo14-jcafb21n-vm
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

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Criar uma nova instância do *CLVhealth-JCAFB-2021v-14n*
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Excluir a instância do *CLVhealth-JCAFB-2021v-14n* existente:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2021v_14n

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo manual:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo14-jcafb21n-vm (session 2)
            #

            ssh tkl-odoo14-jcafb21n-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14n"

        * **Execution time: 0:10:06.097**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar o *External Sync Host* "https://192.168.25.201"
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Criar o *External Sync Host* **https://192.168.25.201**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**https://192.168.25.201**"
            * External Database Name: "**clvhealth_jcafb_2021v_14**"
            * External User: "**admin**"
            * External User Password: "*******"

Configurar todos os "*External Sync Schedules*"
-----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.201**"
            * *Max Task Registers*: "**300.000**"

.. _Lista de Schedules instalados (10c):

Lista de *Schedules* instalados (10c)
-------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` res.users [Migration]

        #. :blue:`(Enabled - Sync)` res.users (res.users)

        #. :blue:`(Enabled - Sync)` clv.file_system.directory (clv.file_system.directory) [rec]

        #. :blue:`(Enabled - Sync)` clv.phase (clv.phase)
        #. :blue:`(Enabled - Sync)` clv.global_settings [Sync]

        #. :blue:`(Enabled - Sync)` clv.global_tag (clv.global_tag)

        #. :blue:`(Enabled - Sync)` survey.survey (survey.survey)

            .. #. :borange:`(Enabled - Sync)` survey.question (survey.question) [1]

        #. :blue:`(Enabled - Sync)` survey.question (survey.question) [2]

            .. #. :borange:`(Enabled - Sync)` survey.question (survey.question) [3]

            .. #. :borange:`(Enabled - Sync)` survey.question (survey.question) [4]

        #. :blue:`(Enabled - Sync)` survey.question (survey.question) [5]
        #. :blue:`(Enabled - Sync)` survey.question.answer (survey.question.answer)

            .. #. :borange:`(Enabled - Sync)` survey.user_input (survey.user_input) [1]

        #. :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [2]

            .. #. :borange:`(Enabled - Sync)` clv.document (clv.document) [2]

        #. :blue:`(Enabled - Sync)` hr.department (hr.department) [rec]
        #. :blue:`(Enabled - Sync)` hr.department (hr.department)
        #. :blue:`(Enabled - Sync)` hr.job (hr.job)
        #. :blue:`(Enabled - Sync)` hr.employee (hr.employee) [rec]
        #. :blue:`(Enabled - Sync)` hr.employee (hr.employee)

        #. :blue:`(Enabled - Sync)` hr.employee.history (hr.employee.history)

        #. :blue:`(Enabled - Sync)` res.country (res.country)
        #. :blue:`(Enabled - Sync)` res.country.state (res.country.state)
        #. :blue:`(Enabled - Sync)` res.city (res.city)

        #. :blue:`(Enabled - Sync)` clv.address.category (clv.address.category)
        #. :blue:`(Enabled - Sync)` clv.address.marker (clv.address.marker)
        #. :blue:`(Enabled - Sync)` clv.address (clv.address)

        #. :blue:`(Enabled - Sync)` clv.address.history (clv.address.history)

        #. :blue:`(Enabled - Sync)` clv.address.aux (clv.address.aux)

        #. :blue:`(Enabled - Sync)` clv.family.category (clv.family.category)
        #. :blue:`(Enabled - Sync)` clv.family (clv.family)

        #. :blue:`(Enabled - Sync)` clv.family.history (clv.family.history)

        #. :blue:`(Enabled - Sync)` clv.person.age_range (clv.person.age_range)
        #. :blue:`(Enabled - Sync)` clv.person.category (clv.person.category)
        #. :blue:`(Enabled - Sync)` clv.person.marker (clv.person.marker)
        #. :blue:`(Enabled - Sync)` clv.person (clv.person)
        #. :blue:`(Enabled - Sync)` clv.person.relation.type (clv.person.relation.type)
        #. :blue:`(Enabled - Sync)` clv.person.relation (clv.person.relation)

        #. :blue:`(Enabled - Sync)` clv.person.history (clv.person.history)

        #. :blue:`(Enabled - Sync)` clv.person.aux (clv.person.aux)

        #. :blue:`(Enabled - Sync)` clv.residence.category (clv.residence.category)
        #. :blue:`(Enabled - Sync)` clv.residence.marker (clv.residence.marker)
        #. :blue:`(Enabled - Sync)` clv.residence (clv.residence)

        #. :blue:`(Enabled - Sync)` clv.residence.history (clv.residence.history)

        #. :blue:`(Enabled - Sync)` clv.patient.age_range (clv.patient.age_range)
        #. :blue:`(Enabled - Sync)` clv.patient.category (clv.patient.category)
        #. :blue:`(Enabled - Sync)` clv.patient.marker (clv.patient.marker)
        #. :blue:`(Enabled - Sync)` clv.patient (clv.patient)

        #. :blue:`(Enabled - Sync)` clv.patient.history (clv.patient.history)

        #. :blue:`(Enabled - Sync)` clv.patient.aux (clv.patient.aux)

        #. :blue:`(Enabled - Sync)` clv.event (clv.event)
        #. :blue:`(Enabled - Sync)` clv.event.attendee (clv.event.attendee)

        #. :blue:`(Enabled - Sync)` clv.document.category (clv.document.category)
        #. :blue:`(Enabled - Sync)` clv.document.marker (clv.document.marker)
        #. :blue:`(Enabled - Sync)` clv.document.type (clv.document.type)
        #. :blue:`(Enabled - Sync)` clv.document.type.parameter (clv.document.type.parameter)
        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [1]
        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [2]
        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [1]

        #. :blue:`(Enabled - Sync)` clv.lab_test.unit (clv.lab_test.unit)
        #. :blue:`(Enabled - Sync)` clv.lab_test.type (clv.lab_test.type)
        #. :blue:`(Enabled - Sync)` clv.lab_test.type.parameter (clv.lab_test.type.parameter)
        #. :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [1]
        #. :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [2]
        #. :blue:`(Enabled - Sync)` clv.lab_test.result (clv.lab_test.result)
        #. :blue:`(Enabled - Sync)` clv.lab_test.report (clv.lab_test.report)

            .. #. :blue:`(Enabled - Sync)` clv.lab_test.report [Update Result ID]

        #. :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [1]

        #. :blue:`(Enabled - Sync)` clv.set (clv.set)
        #. :blue:`(Enabled - Sync)` clv.set.element (clv.set.element)

        #. :blue:`(Enabled - Sync)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)

        #. :blue:`(Enabled - Sync)` clv.verification.marker (clv.verification.marker)
        #. :blue:`(Enabled - Sync)` clv.verification.outcome (clv.verification.outcome)

Executar o *External Sync Batch* "*Default Batch [10]*"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Açã0o** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 1:15:30.991`

Atualizar o *Verification Domain Filter* dos *Verification Schedules* (Current Phase)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Atualizar o *Verification Domain Filter* dos *Verification Schedules*:

        * *Verification Schedules*:

            * "Current Phase - clv.address [_address_verification_exec]"

            * "Current Phase - clv.address_aux [_address_aux_verification_exec]"

            * "Current Phase - clv.family [_family_verification_exec]"

            * "Current Phase - clv.patient [_patient_verification_exec]"

            * "Current Phase - clv.patient_aux [_patient_aux_verification_exec]"

            * "Current Phase - clv.person [_person_verification_exec]"

            * "Current Phase - clv.person_aux [_person_aux_verification_exec]"

            * "Current Phase - clv.residence [_residence_verification_exec]"

        * Atualização:

            * De: "**[('phase_id', '=', 0)]**"

            * Para: "**[('phase_id', '=', 5)]**" (JCAFB-2021v)

.. _Lista de Schedules instalados (20c):

Lista de *Schedules* instalados (20c)
-------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [3]

Executar o *External Sync Batch* "*Default Batch [20]*"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [20]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [20]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:04:03.149`

Excluir a Fase das Pessoas (Aux)
--------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Person (Aux) Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Persons (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Person` » :bi:`Persons (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todas as Pessoas (Aux) com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Phase*: **Remove**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Excluir a Fase dos Endereços (Aux)
----------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Address (Aux) Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Addresses (Aux)*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Address` » :bi:`Addresses (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os Endereços (Aux) com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Phase*: **Remove**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Excluir a Fase dos Pacientes (Aux)
----------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient (Aux) Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os Pacientes (Aux) com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            * Parâmetros utilizados:

                * *Phase*: **Remove**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Marcar o *Active Log* de todos os Objetos
-----------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Global Log Client Mass Edit` para todos os Objetos:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Global Log Clients*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Global Logs` » :bi:`Global Log Clients`

        #. Selecionar todos os :bi:`Global Log Clients`

        #. Executar a Ação ":bi:`Global Log Client Mass Edit`":

            * Parâmetros utilizados:

                * *Active Log*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-08-24a)
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
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-08-24a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-08-24a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-08-24a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-08-24a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-08-24a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-08-24a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-08-24a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-08-24a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-24a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-08-24a)
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
            # gzip -d clvhealth_jcafb_2021v_14n_2021-08-24a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-08-24a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-08-24a.tar.gz

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

.. _Lista de Schedules instalados (30c):

Lista de *Schedules* instalados (30c)
-------------------------------------

    * Lista de *Schedules* instalados:

            .. * :borange:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [1]

        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [2]

Executar o *External Sync Batch* "*Default Batch [30]*"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [30]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [30]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 2:30:26.397`

.. _Lista de Schedules instalados (40c):

Lista de *Schedules* instalados (40c)
-------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [2]

Executar o *External Sync Batch* "*Default Batch [40]*"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [40]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [40]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 3:35:04.019`

.. _Lista de Schedules instalados (50c):

Lista de *Schedules* instalados (50c)
-------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [2]

Executar o *External Sync Batch* "*Default Batch* [50]"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [50]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [50]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 1:45:51.582`

.. _Lista de Schedules instalados (60c):

Lista de *Schedules* instalados (60c)
-------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` ir.model (ir.model)
        #. :blue:`(Enabled - Sync)` ir.model.fields (ir.model.fields)
        #. :blue:`(Enabled - Sync)` clv.model_export.template (clv.model_export.template)
        #. :blue:`(Enabled - Sync)` clv.model_export.template.field (clv.model_export.template.field)
        #. :blue:`(Enabled - Sync)` clv.model_export.template.document_item (clv.model_export.template.document_item)
        #. :blue:`(Enabled - Sync)` clv.model_export.template.lab_test_criterion (clv.model_export.template.lab_test_criterion)
        #. :blue:`(Enabled - Sync)` clv.model_export (clv.model_export)

Executar o *External Sync Batch* "*Default Batch [60]*"
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Batch` "**Default Batch [60]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [60]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:06:57.129`

Marcar o *Active Log* de todos os Objetos
-----------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Global Log Client Mass Edit` para todos os Objetos:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Global Log Clients*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Global Logs` » :bi:`Global Log Clients`

        #. Selecionar todos os :bi:`Global Log Clients`

        #. Executar a Ação ":bi:`Global Log Client Mass Edit`":

            * Parâmetros utilizados:

                * *Active Log*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::   :maxdepth: 2

:bmaroon:`Buffer:`
------------------

:red:`(Não Executado)` Desabilitar a Ação Agendada *Verification Batch: Execute [Default Batch]*
------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Desabilitar a execução da "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**":

            #. Editar o registro:

                * Ativo: **False**

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [10]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [10]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [10]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [10]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 1:17:13.892`

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [20]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [20]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [20]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [20]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:03:55.375`

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [30]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [30]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [30]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [30]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 2:30:26.397`

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [40]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [40]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [40]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [40]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 3:35:04.019`

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [50]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [50]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [50]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [50]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 1:45:51.582`

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [60]*" (método alternativo)
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [60]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [60]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [60]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:06:57.129`

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_base

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_base

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_patient_aux_sync_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux_sync_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Executar o *External Sync Schedule* "clv.patient_aux (clv.patient_aux)"
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.patient_aux**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.patient_aux**":

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

    #. [tkl-odoo14-jcafb21n-vm] Executar o :bi:`External Sync Schedule` "**clv.patient_aux (clv.patient_aux)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.patient_aux (clv.patient_aux)**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.patient_aux (clv.patient_aux)**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:03:50.013`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

