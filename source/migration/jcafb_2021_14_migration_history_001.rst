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

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-10-04a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-10-04a.sql

            gzip clvhealth_jcafb_2021v_14_2020-10-04a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-10-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-10-04a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-10-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-10-04a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-10-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-10-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-10-04a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-10-04a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-10-04a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04a.tar.gz

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

        .. .. * :blue:`(Enabled - Sync)` hr.employee.history (hr.employee.history)

        .. * :blue:`(Enabled - Sync)` clv.document.category (clv.document.category)
        .. * :blue:`(Enabled - Sync)` clv.document.type (clv.document.type)
        .. * :blue:`(Enabled - Sync)` clv.document (clv.document)
        .. * :blue:`(Enabled - Sync)` clv.document.item (clv.document.item)

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

            * :bi:`Execution time: 0:11:06.606`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

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

            * :bi:`Execution time: 4:01:18.996`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo padrão:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ^C

            exit

            /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-10-04b)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-10-04b.sql

            gzip clvhealth_jcafb_2021v_14_2020-10-04b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-10-04b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-10-04b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-10-04b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-10-04b.sql
.. index:: clvhealth_jcafb_2021v_14_2020-10-04b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-10-04b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-10-04b)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-10-04b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-10-04b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-10-04b.tar.gz

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
