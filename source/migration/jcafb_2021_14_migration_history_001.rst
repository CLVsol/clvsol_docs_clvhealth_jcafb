.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

===========================================
Migração do Banco de Dados - JCAFB-2021v-14
===========================================

Criar uma nova instância do *CLVhealth-JCAFB-2021v-14*
------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Excluir a instância do *CLVhealth-JCAFB-2021v-14* existente:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2021v_14

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo manual:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo14-jcafb21-vm (session 2)
            #

            ssh tkl-odoo14-jcafb21-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14"

        * **Execution time: 0:05:45.146**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar o *External Sync Host* "https://192.168.25.189"
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar o *External Sync Host* **https://192.168.25.189**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**https://192.168.25.189**"
            * External Database Name: "**clvhealth_jcafb_2021v_13**"
            * External User: "**admin**"
            * External User Password: "*******"

.. _Lista de Schedules instalados (10):

Lista de *Schedules* instalados (10)
------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` res.users [Migration]

        * :blue:`(Enabled - Sync)` res.users (res.users)

        * :blue:`(Enabled - Sync)` clv.file_system.directory (clv.file_system.directory)

        * :blue:`(Enabled - Sync)` clv.phase (clv.phase)

        * :blue:`(Enabled - Sync)` clv.global_tag (clv.global_tag)

        * :blue:`(Enabled - Sync)` survey.survey (survey.survey)
        * :blue:`(Enabled - Sync)` survey.question (survey.question) [1]
        * :blue:`(Enabled - Sync)` survey.question (survey.question) [2]
        * :blue:`(Enabled - Sync)` survey.question (survey.question) [3]
        * :blue:`(Enabled - Sync)` survey.question (survey.question) [4]
        * :blue:`(Enabled - Sync)` survey.question (survey.question) [5]
        * :blue:`(Enabled - Sync)` survey.question.answer (survey.label)
        * :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [1]
        * :blue:`(Enabled - Sync)` survey.user_input (survey.user_input) [2]

        .. * :blue:`(Enabled - Sync)` clv.document (clv.document) [2]

        * :blue:`(Enabled - Sync)` hr.department (hr.department) [rec]
        * :blue:`(Enabled - Sync)` hr.department (hr.department)
        * :blue:`(Enabled - Sync)` hr.job (hr.job)
        * :blue:`(Enabled - Sync)` hr.employee (hr.employee) [rec]
        * :blue:`(Enabled - Sync)` hr.employee (hr.employee)

        * :blue:`(Enabled - Sync)` hr.employee.history (hr.employee.history)

        * :blue:`(Enabled - Sync)` res.country (res.country)
        * :blue:`(Enabled - Sync)` res.country.state (res.country.state)
        * :blue:`(Enabled - Sync)` res.city (res.city)

        * :blue:`(Enabled - Sync)` clv.address.category (clv.address.category)
        * :blue:`(Enabled - Sync)` clv.address (clv.address)

        * :blue:`(Enabled - Sync)` clv.address.history (clv.address.history)

        * :blue:`(Enabled - Sync)` clv.address.aux (clv.address.aux)

        * :blue:`(Enabled - Sync)` clv.family.category (clv.family.category)
        * :blue:`(Enabled - Sync)` clv.family (clv.family)

        * :blue:`(Enabled - Sync)` clv.family.history (clv.family.history)

        * :blue:`(Enabled - Sync)` clv.person.category (clv.person.category)
        * :blue:`(Enabled - Sync)` clv.person.marker (clv.person.marker)
        * :blue:`(Enabled - Sync)` clv.person (clv.person)
        * :blue:`(Enabled - Sync)` clv.person.relation [Set Up]

        * :blue:`(Enabled - Sync)` clv.person.history (clv.person.history)

        * :blue:`(Enabled - Sync)` clv.person.aux (clv.person.aux)

        * :blue:`(Enabled - Sync)` clv.event (clv.event)
        * :blue:`(Enabled - Sync)` clv.event.attendee (clv.event.attendee)

        * :blue:`(Enabled - Sync)` clv.document.category (clv.document.category)
        * :blue:`(Enabled - Sync)` clv.document.type (clv.document.type)
        * :blue:`(Enabled - Sync)` clv.document.type.parameter (clv.document.type.parameter)
        * :blue:`(Enabled - Sync)` clv.document (clv.document)
        * :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [1]

        * :blue:`(Enabled - Sync)` clv.lab_test.unit (clv.lab_test.unit)
        * :blue:`(Enabled - Sync)` clv.lab_test.type (clv.lab_test.type)
        * :blue:`(Enabled - Sync)` clv.lab_test.type.parameter (clv.lab_test.type.parameter)
        * :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request)
        * :blue:`(Enabled - Sync)` clv.lab_test.result (clv.lab_test.result)
        * :blue:`(Enabled - Sync)` clv.lab_test.report (clv.lab_test.report)
        * :blue:`(Enabled - Sync)` clv.lab_test.report [Update Result ID]
        * :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [1]

        * :blue:`(Enabled - Sync)` clv.set (clv.set)
        * :blue:`(Enabled - Sync)` clv.set.element (clv.set.element)

        * :blue:`(Enabled - Sync)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)

        * :blue:`(Enabled - Sync)` clv.verification.marker (clv.verification.marker)

Executar o *External Sync Batch* "*Default Batch*" (10)
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Configurar todos os :bi:`External Sync Schedules`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

            * Lista de *Schedules*:

                * :ref:`Lista de Schedules instalados (10)`

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

            * Parâmetros alterados:
                
                * *External Host*: "**https://192.168.25.189**"
                * *Max Task Registers*: "**300.000**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:56:03.285`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

Preparar *Global Settings* para o banco de dados *CLVhealth-JCAFB-2021v-14*
---------------------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2021v**

        #. Configurar o parâmetro :bi:`Person` » :bi:`Reference Date`: **31/01/2021**

:red:`(Não Executado)` Atualisar a Idade de Referência e *Person Age Ranges* para todas as Pessoas
--------------------------------------------------------------------------------------------------

    #. [ttkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para todas as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `ttkl-odoo14-jcafb21-vm <https://ttkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Communities` » :bi:`Communities` » :bi:`Persons`

        #. Selecionar todas as Pessoas

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Person Reference Age Refresh*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualisar a Idade de Referência e *Person Age Ranges* para todas as Pessoas (método alternativo)
------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Person: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Compute Age Reference**"

        #. Executar a Ação Agendada "**Person: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Person: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Update Age Range**"

        #. Executar a Ação Agendada "**Person: Update Age Range**", clicando no botão **Rodar Manualmente**.

:red:`(Não Executado)` Executar o *Verification Batch* “Default Batch”
----------------------------------------------------------------------

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`".

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

            * :bi:`Execution time: 0:28:22.481`

.. _Lista de Schedules instalados (30):

Lista de *Schedules* instalados (30)
------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [1]
        * :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [2]

Executar o *External Sync Batch* "*Default Batch*" (30)
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Configurar todos os :bi:`External Sync Schedules`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

            * Lista de *Schedules*:

                * :ref:`Lista de Schedules instalados (30)`

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

            * Parâmetros alterados:
                
                * *External Host*: "**https://192.168.25.189**"
                * *Max Task Registers*: "**300.000**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch (30)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch (30)**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 3:25:27.648`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

.. _Lista de Schedules instalados (40):

Lista de *Schedules* instalados (40)
------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [2]

Executar o *External Sync Batch* "*Default Batch*" (40)
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Configurar todos os :bi:`External Sync Schedules`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

            * Lista de *Schedules*:

                * :ref:`Lista de Schedules instalados (40)`

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

            * Parâmetros alterados:
                
                * *External Host*: "**https://192.168.25.189**"
                * *Max Task Registers*: "**300.000**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch (40)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch (40)**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 3:22:57.938`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

.. _Lista de Schedules instalados (50):

Lista de *Schedules* instalados (50)
------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [2]

Executar o *External Sync Batch* "*Default Batch*" (50)
-------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Configurar todos os :bi:`External Sync Schedules`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

            * Lista de *Schedules*:

                * :ref:`Lista de Schedules instalados (50)`

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

            * Parâmetros alterados:
                
                * *External Host*: "**https://192.168.25.189**"
                * *Max Task Registers*: "**300.000**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. [tkl-odoo14-jcafb21-vm] Executar o :bi:`External Sync Batch` "**Default Batch (50)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch (50)**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 1:48:03.958`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

Marcar o *Active Log* de todos os Objetos
-----------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Global Log Client Mass Edit` para todos os Objetos:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Global Log Clients*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Global Logs` » :bi:`Global Log Clients`

        #. Selecionar todos os :bi:`Global Log Clients`

        #. Exercutar a Ação ":bi:`Global Log Client Mass Edit`":

            * Parâmetros utilizados:

                * *Active Log*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-11-07a)
--------------------------------------------------------------------------

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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-11-07a.sql

            gzip clvhealth_jcafb_2021v_14_2020-11-07a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-11-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-11-07a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-11-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-11-07a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-11-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-11-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-07a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-11-07a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-11-07a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-11-07a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-07a.tar.gz

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

Desabilitar a Ação Agendada *Verification Batch: Execute [Default Batch]*
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Desabilitar a execução da "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**":

            #. Editar o registro:

                * Ativo: **False**

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-11-08a)
--------------------------------------------------------------------------

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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-11-08a.sql

            gzip clvhealth_jcafb_2021v_14_2020-11-08a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-11-08a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-11-08a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-11-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-11-08a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-11-08a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-11-08a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-08a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-11-08a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-11-08a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-11-08a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-11-08a.tar.gz

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

Executar a "Preparação do Cadastro Auxiliar"
--------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`".

.. toctree::   :maxdepth: 2
