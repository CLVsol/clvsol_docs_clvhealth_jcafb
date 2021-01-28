.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

=====================================================
Migração do Banco de Dados - CLVhealth-JCAFB-2021v-14
=====================================================

Criar uma nova instância do *CLVhealth-JCAFB-2021v-14*
------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh (session 1) com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Excluir a instância do *CLVhealth-JCAFB-2021v-14* existente:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2021v_14

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo manual:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **clvhealth-jcafb-2021-vm-pro** e executar o **install.py**:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro (session 2)
            #

            ssh clvhealth-jcafb-2021-vm-pro -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14"

        * **Execution time: 0:06:24.652**

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Criar o *External Sync Host* "https://192.168.25.189"
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

    #. Criar o *External Sync Host* **https://192.168.25.189**:

        * Menu de acesso:
            
            * *External Sync* > *Configuration* > *Hosts* > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**https://192.168.25.189**"
            * External Database Name: "**clvhealth_jcafb_2021v_13**"
            * External User: "**admin**"
            * External User Password: "*******"

Configurar todos os "*External Sync Schedules*""
------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.189**"
            * *Max Task Registers*: "**300.000**"

.. _Lista de Schedules instalados (10b):

Lista de *Schedules* instalados (10b)
-------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` res.users [Migration]

        * :blue:`(Enabled - Sync)` res.users (res.users)

        .. * :blue:`(Enabled - Sync)` clv.file_system.directory (clv.file_system.directory)

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

        .. * :blue:`(Enabled - Sync)` clv.address.aux (clv.address.aux)

        * :blue:`(Enabled - Sync)` clv.family.category (clv.family.category)
        * :blue:`(Enabled - Sync)` clv.family (clv.family)

        * :blue:`(Enabled - Sync)` clv.family.history (clv.family.history)

        * :blue:`(Enabled - Sync)` clv.person.category (clv.person.category)
        * :blue:`(Enabled - Sync)` clv.person.marker (clv.person.marker)
        * :blue:`(Enabled - Sync)` clv.person (clv.person)
        * :blue:`(Enabled - Sync)` clv.person.relation [Set Up]

        * :blue:`(Enabled - Sync)` clv.person.history (clv.person.history)

        .. * :blue:`(Enabled - Sync)` clv.person.aux (clv.person.aux)

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
        * :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [1]
        * :blue:`(Enabled - Sync)` clv.lab_test.request (clv.lab_test.request) [2]
        * :blue:`(Enabled - Sync)` clv.lab_test.result (clv.lab_test.result)
        * :blue:`(Enabled - Sync)` clv.lab_test.report (clv.lab_test.report)
        * :blue:`(Enabled - Sync)` clv.lab_test.report [Update Result ID]
        * :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [1]

        * :blue:`(Enabled - Sync)` clv.set (clv.set)
        * :blue:`(Enabled - Sync)` clv.set.element (clv.set.element)

        * :blue:`(Enabled - Sync)` clv.partner_entity.street_pattern (clv.partner_entity.street_pattern)

        * :blue:`(Enabled - Sync)` clv.verification.marker (clv.verification.marker)

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [10]*"
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:52:18.642`

Executar o *External Sync Batch* "*Default Batch [10]*" (método alternativo)
----------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [10]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [10]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [10]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:52:18.642`

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-01-28a)
--------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-01-28a.sql

            gzip clvhealth_jcafb_2021v_14_2021-01-28a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-01-28a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-01-28a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-01-28a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-01-28a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-01-28a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-01-28a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-01-28a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-01-28a)
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-01-28a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-01-28a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-01-28a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvhealth-jcafb-2021-vm-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

.. _Lista de Schedules instalados (30b):

Lista de *Schedules* instalados (30b)
-------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [1]
        * :blue:`(Enabled - Sync)` survey.user_input.line (survey.user_input_line) [2]

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [30]*"
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar o :bi:`External Sync Batch` "**Default Batch [30]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [30]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 3:25:27.648`

Executar o *External Sync Batch* "*Default Batch [30]*" (método alternativo)
----------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [30]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [30]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [30]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 3:14:34.075`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04b)
---------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04b.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-04b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-04b.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-04b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-04b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04b

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04b)
-------------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-04b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-04b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvhealth-jcafb-2021-vm-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

.. _Lista de Schedules instalados (40b):

Lista de *Schedules* instalados (40b)
-------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` clv.document.item (clv.document.item) [2]

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch [40]*"
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar o :bi:`External Sync Batch` "**Default Batch [40]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [40]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 3:22:57.938`

Executar o *External Sync Batch* "*Default Batch [40]*" (método alternativo)
----------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [40]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [40]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [40]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 3:37:09.405`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04c)
---------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04c.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-04c.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04c.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-04c.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-04c.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-04c
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04c

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04c)
-------------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-04c.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-04c.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvhealth-jcafb-2021-vm-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

.. _Lista de Schedules instalados (50b):

Lista de *Schedules* instalados (50b)
-------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` clv.lab_test.criterion (clv.lab_test.criterion) [2]

:red:`(Não Executado)` Executar o *External Sync Batch* "*Default Batch* [50]"
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar o :bi:`External Sync Batch` "**Default Batch [50]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [50]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 1:48:03.958`

Executar o *External Sync Batch* "*Default Batch [50]*" (método alternativo)
----------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [50]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [50]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [50]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 1:48:40.193`

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04d)
---------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04d.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-04d.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-04d.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04d.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-04d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-04d.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-04d.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-04d
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04d

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-04d)
-------------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-04d.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-04d.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-04d.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvhealth-jcafb-2021-vm-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

:red:`(Não Executado)` Desabilitar a Ação Agendada *Verification Batch: Execute [Default Batch]*
------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Desabilitar a execução da "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**":

            #. Editar o registro:

                * Ativo: **False**

.. toctree::   :maxdepth: 2
