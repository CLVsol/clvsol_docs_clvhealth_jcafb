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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2021v-15]"

=====================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2021v-15]
=====================================================

Upgrade the odoo software
-------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

:borange:`(**)` Atualizar os fontes do projeto
----------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb21-vm -l root

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

            # cd /opt/odoo/clvsol_odoo_addons_process
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            # git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Criar uma nova instância do *CLVhealth-JCAFB-2021v-15*
------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Excluir a instância do *CLVhealth-JCAFB-2021v-15* existente:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2021v_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb21-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb21-vm (session 2)
            #

            ssh tkl-odoo15-jcafb21-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_15"

        * **Execution time: 0:01:27.058**

        * **Execution time: 0:10:28.342** (Compĺeto)

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar o *External Sync Host* "https://192.168.25.203"
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

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

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.203**"
            * *Max Task Registers*: "**300.000**"

Lista de *Schedules* instalados (00-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` clv.global_settings (current_filestore_path) [Sync]

        #. :blue:`(Enabled - Sync)` res.users [Migration]
        #. :blue:`(Enabled - Sync)` res.users (res.users)

        #. :blue:`(Enabled - Sync)` clv.phase (clv.phase)
        #. :blue:`(Enabled - Sync)` clv.global_settings (current_phase_id) [Sync]

        #. :blue:`(Enabled - Sync)` survey.survey (survey.survey)
        #. :blue:`(Enabled - Sync)` survey.question (survey.question) [2]
        #. :blue:`(Enabled - Sync)` survey.question (survey.question) [5]
        #. :blue:`(Enabled - Sync)` survey.question.answer (survey.question.answer)
        #. :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [2]

        #. :blue:`(Enabled - Sync)` clv.file_system.directory (clv.file_system.directory) [rec]
        #. :blue:`(Enabled - Sync)` clv.file_system.directory (clv.file_system.directory)

        #. :blue:`(Enabled - Sync)` clv.global_tag (clv.global_tag)

        #. :blue:`(Enabled - Sync)` clv.set (clv.set)
        #. :blue:`(Enabled - Sync)` clv.set.element (clv.set.element) [1]

        #. :blue:`(Enabled - Sync)` hr.department (hr.department) [rec]
        #. :blue:`(Enabled - Sync)` hr.department (hr.department)
        #. :blue:`(Enabled - Sync)` hr.job (hr.job)
        #. :blue:`(Enabled - Sync)` hr.employee (hr.employee) [rec]
        #. :blue:`(Enabled - Sync)` hr.employee (hr.employee) [1]

        #. :blue:`(Enabled - Sync)` hr.employee.history (hr.employee.history)

        #. :blue:`(Enabled - Sync)` clv.event (clv.event)
        #. :blue:`(Enabled - Sync)` clv.event.attendee (clv.event.attendee) [1]

        #. :blue:`(Enabled - Sync)` clv.document.category (clv.document.category) [Sync]
        #. :blue:`(Enabled - Sync)` clv.document.marker (clv.document.marker) [Sync]
        #. :blue:`(Enabled - Sync)` clv.document.type (clv.document.type) [1] [Inc]
        #. :blue:`(Enabled - Sync)` clv.document.type.parameter (clv.document.type.parameter) [Sync]
        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [1] [Inc]
        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [2] [Inc]

        #. :blue:`(Enabled - Sync)` clv.lab_test.type (clv.lab_test.type) [1]
        #. :blue:`(Enabled - Sync)` clv.lab_test.type.parameter (clv.lab_test.type.parameter)
        #. :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [1]
        #. :blue:`(Enabled - Sync)` clv.lab_test.result (clv.lab_test.result) [1]
        #. :blue:`(Enabled - Sync)` clv.lab_test.report (clv.lab_test.report) [1]

        .. #. :blue:`(Enabled - Sync)` res.country (res.country)
        .. #. :blue:`(Enabled - Sync)` res.country.state (res.country.state)
        .. #. :blue:`(Enabled - Sync)` res.city (res.city)

        .. #. :blue:`(Enabled - Sync)` clv.residence.category (clv.residence.category)
        .. #. :blue:`(Enabled - Sync)` clv.residence.marker (clv.residence.marker)
        .. #. :blue:`(Enabled - Sync)` clv.residence (clv.residence) [1]

        .. #. :blue:`(Enabled - Sync)` clv.residence.history (clv.residence.history) [1]

        .. #. :blue:`(Enabled - Sync)` clv.patient.age_range (clv.patient.age_range)
        .. #. :blue:`(Enabled - Sync)` clv.patient.category (clv.patient.category)
        .. #. :blue:`(Enabled - Sync)` clv.patient.marker (clv.patient.marker)
        .. #. :blue:`(Enabled - Sync)` clv.patient (clv.patient) [1]

        .. #. :blue:`(Enabled - Sync)` clv.patient.history (clv.patient.history) [1]

        .. #. :blue:`(Enabled - Sync)` clv.patient_aux (clv.patient_aux)

        .. #. :blue:`(Enabled - Sync)` clv.address.category (clv.address.category)
        .. #. :blue:`(Enabled - Sync)` clv.address.marker (clv.address.marker)
        .. #. :blue:`(Enabled - Sync)` clv.address (clv.address)

        .. #. :blue:`(Enabled - Sync)` clv.address.history (clv.address.history)

        .. #. :blue:`(Enabled - Sync)` clv.family.category (clv.family.category)
        .. #. :blue:`(Enabled - Sync)` clv.family (clv.family)

        .. #. :blue:`(Enabled - Sync)` clv.family.history (clv.family.history)

        .. #. :blue:`(Enabled - Sync)` clv.person.age_range (clv.person.age_range)
        .. #. :blue:`(Enabled - Sync)` clv.person.category (clv.person.category)
        .. #. :blue:`(Enabled - Sync)` clv.person.marker (clv.person.marker)
        .. #. :blue:`(Enabled - Sync)` clv.person (clv.person)

        .. #. :blue:`(Enabled - Sync)` clv.person.relation.type (clv.person.relation.type)
        .. #. :blue:`(Enabled - Sync)` clv.person.relation (clv.person.relation)

        .. #. :blue:`(Enabled - Sync)` clv.person.history (clv.person.history)

        .. #. :blue:`(Enabled - Sync)` clv.address_aux (clv.address_aux)

        .. #. :blue:`(Enabled - Sync)` clv.person_aux (clv.person_aux)

        .. #. :blue:`(Enabled - Sync)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)
        .. #. :blue:`(Enabled - Sync)` clv.partner_entity.contact_information_pattern (clv.partner_entity.contact_information_pattern)

        .. #. :blue:`(Enabled - Sync)` clv.verification.marker (clv.verification.marker)
        .. #. :blue:`(Enabled - Sync)` clv.verification.outcome (clv.verification.outcome) [1]
        .. #. :blue:`(Enabled - Sync)` clv.verification.outcome (clv.verification.outcome) [2]
        .. #. :blue:`(Enabled - Sync)` clv.verification.outcome (clv.verification.outcome) [3]
        .. #. :blue:`(Enabled - Sync)` clv.verification.outcome (clv.verification.outcome) [4]

Executar o *External Sync Batch* "*Default Batch [00]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [00]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [00]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:13:17.419`
            
            * :bi:`Execution time: 1:03:08.221` (Completo)

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-25a)
--------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-25a.sql

            gzip clvhealth_jcafb_2021v_15_2022-03-25a.sql
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-25a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz clvhealth_jcafb_2021v_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-25a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-25a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz

.. index:: clvhealth_jcafb_2021v_15_2022-03-25a.sql
.. index:: clvhealth_jcafb_2021v_15_2022-03-25a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_15_2022-03-25a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-25a)
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_15_2022-03-25a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_15
            psql -f clvhealth_jcafb_2021v_15_2022-03-25a.sql -d clvhealth_jcafb_2021v_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb21-vm**".

        #. Salvar o registro editado.

Lista de *Schedules* instalados (02-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [3]

        #. :blue:`(Enabled - Sync)` clv.set.element (clv.set.element) [2]

        #. :blue:`(Enabled - Sync)` clv.event.attendee (clv.event.attendee) [2]

        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [3] [Sync]

        #. :blue:`(Enabled - Sync)` clv.lab_test.type (clv.lab_test.type) [2]
        #. :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [2]
        #. :blue:`(Enabled - Sync)` clv.lab_test.result (clv.lab_test.result) [2]
        #. :blue:`(Enabled - Sync)` clv.lab_test.report (clv.lab_test.report) [2]

        .. #. :blue:`(Enabled - Sync)` clv.residence (clv.residence) [2]

        .. #. :blue:`(Enabled - Sync)` clv.residence.history (clv.residence.history) [2]

        .. #. :blue:`(Enabled - Sync)` clv.patient (clv.patient) [2]

        .. #. :blue:`(Enabled - Sync)` clv.patient.history (clv.patient.history) [2]

Executar o *External Sync Batch* "*Default Batch [02]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [02]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [02]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:04:25.552`

            * :bi:`Execution time: 0:40:10.547` (Completo)

Lista de *Schedules* instalados (04-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` hr.employee (hr.employee) [2]

        #. :blue:`(Enabled - Sync)` clv.document.type (clv.document.type) [2]

        #. :blue:`(Enabled - Sync)` clv.document (clv.document) [4] [Sync]

Executar o *External Sync Batch* "*Default Batch [04]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [04]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [04]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:57.972`

Lista de *Schedules* instalados (10-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [4]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [5]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [6]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [7]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [8]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [9]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [10]
        #. :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input.line) [11]

Executar o *External Sync Batch* "*Default Batch [10]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 2:45:18.968`

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-25b)
--------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-25b.sql

            gzip clvhealth_jcafb_2021v_15_2022-03-25b.sql
            pg_dump clvhealth_jcafb_2021v_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_15_2022-03-25b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz clvhealth_jcafb_2021v_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-25b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_15_2022-03-25b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz

.. index:: clvhealth_jcafb_2021v_15_2022-03-25b.sql
.. index:: clvhealth_jcafb_2021v_15_2022-03-25b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_15_2022-03-25b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-15* (2022-03-25b)
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            ssh tkl-odoo15-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_15_2022-03-25b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_15
            psql -f clvhealth_jcafb_2021v_15_2022-03-25b.sql -d clvhealth_jcafb_2021v_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_15_2022-03-25b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb21-vm**".

        #. Salvar o registro editado.

Lista de *Schedules* instalados (20-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [1]
        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [2]
        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [3]
        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [4]
        #. :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [5]

Executar o *External Sync Batch* "*Default Batch [20]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [20]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [20]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 2:10:49.001`

Lista de *Schedules* instalados (30-21v-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [1]
        #. :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [2]

Executar o *External Sync Batch* "*Default Batch [30]*"
-------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [30]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [30]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:53:47.642`

.. toctree::   :maxdepth: 2
