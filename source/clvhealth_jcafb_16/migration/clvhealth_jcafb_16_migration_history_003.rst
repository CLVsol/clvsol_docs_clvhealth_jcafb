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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-16]" (3)

===================================================
Migração do Banco de Dados [CLVhealth-JCAFB-16] (3)
===================================================

[tkl-odoo16-vm-18] Preparação do conteúdo do arquivo "host.csv" (2024-11-12a)
-----------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Editar manualmente um registro (*row*) do arquivo "/opt/odoo/clvsol_clvhealth_jcafb/project/host.csv", informando as credenciais:

        * name: "**tkl-odoo16-vm-18**"
        * server: "**https://192.168.25.212**"
        * dbname: "**clvhealth_jcafb_16**"
        * user: "**admin**"
        * user_pw: "*******"
        * user_apikey: "**vazio**"
        * data_user_pw: "*******"
        * data_user_apikey: "**vazio**"
        * master_pw: "*******"
        * notes: "**vazio**"
 
[tkl-odoo16-vm-18] Criar uma nova instância do *CLVhealth-JCAFB-16* (2024-12-27a)
---------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Excluir a instância do *CLVhealth-JCAFB-16* existente:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_16

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo manual:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo16-vm-18** e executar o **install.py**:

        ::

            # ***** tkl-odoo16-vm-18 (session 2)
            #

            ssh tkl-odoo16-vm-18 -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py

        * **Execution time: 0:15:03.863550**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18 (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` Criar o *External Sync Host* "http://192.168.25.210:8069"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

    #. Criar o *External Sync Host* **http://192.168.25.210:8069**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**http://192.168.25.210:8069**"
            * External Database Name: "**clvhealth_jcafb_2025_15**"
            * External User: "**admin**"
            * External User Password: "*******"

:borange:`(**)` Configurar todos os "*External Sync Schedules*"
---------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**http://192.168.25.210:8069**"
            * *Max Task Registers*: "**300.000**"

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06a)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06a.sql

            gzip clvhealth_jcafb_16_2025-02-06a.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2025-02-06a.sql
        * /opt/odoo/clvhealth_jcafb_16_2025-02-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz

.. index:: clvhealth_jcafb_16_2025-02-06a.sql
.. index:: clvhealth_jcafb_16_2025-02-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2025-02-06a
.. index:: clvsol_filestore_clvhealth_jcafb_16_2025-02-06a

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06a)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2025-02-06a.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2025-02-06a.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

:borange:`(**)` Lista de *Schedules* instalados (00-16-18)
----------------------------------------------------------

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

        #. :red:`(Enabled)` clv.residence.history (clv.residence.history) [1] [Inc]

        #. :blue:`(Enabled)` clv.patient.age_range (clv.patient.age_range)
        #. :blue:`(Enabled)` clv.patient.category (clv.patient.category)
        #. :blue:`(Enabled)` clv.patient.marker (clv.patient.marker)
        #. :blue:`(Enabled)` clv.patient (clv.patient) [1] [Inc]

        #. :blue:`(Enabled)` clv.patient.history (clv.patient.history) [1] [Inc]

        #. :blue:`(Enabled)` clv.patient_rec (clv.patient_rec) [1] [Inc]

        #. :blue:`(Enabled)` clv.lab_test.export_xls.param (clv.lab_test.export_xls.param)

        #. :blue:`(Enabled)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)
        #. :blue:`(Enabled)` clv.partner_entity.contact_information_pattern (clv.partner_entity.contact_information_pattern)

        #. :blue:`(Enabled)` clv.verification.marker (clv.verification.marker)
        #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [1]
        #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [2]
        #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [3]
        #. :blue:`(Enabled)` clv.verification.outcome (clv.verification.outcome) [4]

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [00]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [00]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [00]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:27:13.932`
            
[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06b)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06b.sql

            gzip clvhealth_jcafb_16_2025-02-06b.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2025-02-06b.sql
        * /opt/odoo/clvhealth_jcafb_16_2025-02-06b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz

.. index:: clvhealth_jcafb_16_2025-02-06b.sql
.. index:: clvhealth_jcafb_16_2025-02-06b.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2025-02-06b
.. index:: clvsol_filestore_clvhealth_jcafb_16_2025-02-06b

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06b)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2025-02-06b.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2025-02-06b.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

:borange:`(**)` Lista de *Schedules* instalados (02-16-18)
----------------------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.set.element (clv.set.element) [2] [Sync]

        #. :green:`(Enabled)` survey.user_input (survey.user_input) [2] [Sync]

        #. :green:`(Enabled)` clv.event.attendee (clv.event.attendee) [2] [Sync]

        #. :green:`(Enabled)` clv.document.type (clv.document.type) [2]
        #. :green:`(Enabled)` clv.document (clv.document) [3] [Sync]

        #. :green:`(Enabled)` clv.lab_test.type (clv.lab_test.type) [2] [Sync]
        #. :green:`(Enabled)` clv.lab_test.result (clv.lab_test.result) [2] [Sync]

        #. :green:`(Enabled)` clv.residence (clv.residence) [2] [Sync]

        #. :red:`(Enabled)` clv.residence.history (clv.residence.history) [2] [Sync]

        #. :green:`(Enabled)` clv.patient (clv.patient) [2] [Sync]

        #. :green:`(Enabled)` clv.patient.history (clv.patient.history) [2] [Sync]

        #. :green:`(Enabled)` clv.patient_rec (clv.patient_rec) [2] [Sync]

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [02]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [02]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [02]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:12:16.119`

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06c)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06c.sql

            gzip clvhealth_jcafb_16_2025-02-06c.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-02-06c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2025-02-06c.sql
        * /opt/odoo/clvhealth_jcafb_16_2025-02-06c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz

.. index:: clvhealth_jcafb_16_2025-02-06c.sql
.. index:: clvhealth_jcafb_16_2025-02-06c.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2025-02-06c
.. index:: clvsol_filestore_clvhealth_jcafb_16_2025-02-06c

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06c)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2025-02-06c.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2025-02-06c.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-02-06c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

:borange:`(**)` Lista de *Schedules* instalados (04-16-18)
----------------------------------------------------------

    * Lista de *Schedules* instalados:

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [04]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [04]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [04]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

:borange:`(**)` Lista de *Schedules* instalados (10-16-18)
----------------------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [1] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [2] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [3] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [4] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [5] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [6] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [7] [Sync]
        #. :green:`(Enabled)` survey.user_input.line (survey.user_input.line) [8] [Sync]

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [10]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: **`

:borange:`(**)` Lista de *Schedules* instalados (20-16-18)
----------------------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.document.item (clv.document.item) [1]
        #. :green:`(Enabled)` clv.document.item (clv.document.item) [2]

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [20]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [20]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [20]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:07:20.289`

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-28e)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-01-28e.sql

            gzip clvhealth_jcafb_16_2025-01-28e.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-01-28e.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2025-01-28e.sql
        * /opt/odoo/clvhealth_jcafb_16_2025-01-28e.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz

.. index:: clvhealth_jcafb_16_2025-01-28e.sql
.. index:: clvhealth_jcafb_16_2025-01-28e.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2025-01-28e
.. index:: clvsol_filestore_clvhealth_jcafb_16_2025-01-28e

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-28e)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2025-01-28e.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2025-01-28e.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28e.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

:borange:`(**)` Lista de *Schedules* instalados (30-16-18)
----------------------------------------------------------

    * Lista de *Schedules* instalados:

        #. :green:`(Enabled)` clv.lab_test.criterion (clv.lab_test.criterion) [1] [Sync]
        #. :green:`(Enabled)` clv.lab_test.criterion (clv.lab_test.criterion) [2] [Sync]

:borange:`(**)` Executar o *External Sync Batch* "*Default Batch [30]*"
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch [30]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb21-vm <https://tkl-odoo15-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [30]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:02:30.123`

[tkl-odoo16-vm-18] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-28d)
--------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-01-28d.sql

            gzip clvhealth_jcafb_16_2025-01-28d.sql
            pg_dump clvhealth_jcafb_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_16_2025-01-28d.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz clvhealth_jcafb_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_16_2025-01-28d.sql
        * /opt/odoo/clvhealth_jcafb_16_2025-01-28d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz

.. index:: clvhealth_jcafb_16_2025-01-28d.sql
.. index:: clvhealth_jcafb_16_2025-01-28d.sql.gz
.. index:: filestore_clvhealth_jcafb_16_2025-01-28d
.. index:: clvsol_filestore_clvhealth_jcafb_16_2025-01-28d

[tkl-odoo16-vm-18] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-28d)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-vm-18] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-vm-18** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-vm-18
            #

            ssh tkl-odoo16-vm-18 -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-vm-18] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_16_2025-01-28d.sql.gz

            dropdb -i clvhealth_jcafb_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_16
            psql -f clvhealth_jcafb_16_2025-01-28d.sql -d clvhealth_jcafb_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_16_2025-01-28d.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-vm-18** ao modo desejado:

        ::

            # ***** tkl-odoo16-vm-18
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-vm-18] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-vm-18 <https://tkl-odoo16-vm-18>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-vm-18**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
