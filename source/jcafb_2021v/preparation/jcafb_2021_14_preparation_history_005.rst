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

=============================================
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-24a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-24a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-24a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-24a.tar.gz

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

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_export
        * clv_document_export
        * clv_lab_test_export
        * clv_person_export
        * clv_patient_export
        * clv_export_jcafb
        * clv_document_export_jcafb
        * clv_lab_test_export_jcafb
        * clv_person_export_jcafb
        * clv_patient_export_jcafb
        * clv_patient_community_export_jcafb
        * clv_export_sync_jcafb

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14" -m clv_external_sync_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Configurar todos os "*External Sync Schedules*""
------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Confituration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.189**"
            * *Max Task Registers*: "**300.000**"

.. _Lista de Schedules instalados (60b):

Lista de *Schedules* instalados (60b)
-------------------------------------

    * Lista de *Schedules* instalados:

        * :blue:`(Enabled - Sync)` ir.model (ir.model)
        * :blue:`(Enabled - Sync)` ir.model.fields (ir.model.fields)
        * :blue:`(Enabled - Sync)` clv.model_export.template (clv.model_export.template)
        * :blue:`(Enabled - Sync)` clv.model_export.template.field (clv.model_export.template.field)
        * :blue:`(Enabled - Sync)` clv.model_export.template.document_item (clv.model_export.template.document_item)
        * :blue:`(Enabled - Sync)` clv.model_export.template.lab_test_criterion (clv.model_export.template.lab_test_criterion)
        * :blue:`(Enabled - Sync)` clv.model_export (clv.model_export)

Executar o *External Sync Batch* "*Default Batch [60]*" (método alternativo)
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**External Sync Batch: Execute [Default Batch [60]]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**External Sync Batch: Execute [Default Batch [60]]**"

        #. Executar a Ação Agendada "**External Sync Batch: Execute [Default Batch [60]]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:05:41.856`

Configurar as permissões do usuário de referência da JCAFB-2021v
----------------------------------------------------------------

    #. Configurar as permissões do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Definições` » :bi:`Usuários e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Configurar as permissões:

            * Marketing

                * Inquéritos: **Administrador**

            * *Human Resources*
            
                * Funcionários: **Administrador**

            * *Administration*
            
                * Administração:

            * Other

                * *Address (Aux)*: :bi:`Manager (Address (Aux))`
                * *Address*: :bi:`Manager (Address)`
                * *Community*: :bi:`Manager (Community)`
                * *Employee*: :bi:`Manager (Employee)`
                * *Event*: :bi:`Manager (Event)`
                * *Export*: :bi:`Manager (Export)`
                * *External Sync*:
                * *Family*: :bi:`Manager (Family)`
                * *File System*: :bi:`Manager (File System)`
                * *Global Tag*: :bi:`Manager (Global Tag)`
                * *Patient (Aux)*: :bi:`Manager (Patient (Aux))`
                * *Patient*: :bi:`Manager (Patient)`
                * *Person (Aux)*: :bi:`Manager (Person (Aux))`
                * *Person*: :bi:`Manager (Person)`
                * *Phase*: :bi:`User (Phase)`
                * *Processing*:
                * *Residence*: :bi:`Manager (Residence)`
                * *Set*: :bi:`Manager (Set)`
                * *Summary*: :bi:`Manager (Summary)`
                * *Survey*:  :bi:`Manager (Survey)`
                * *Verification*: :bi:`Manager (Verification)`

            * *Base*:

                * :bi:`Annotation User (Base)`,
                * :bi:`Log User (Base)`,
                * :bi:`Manager (Base)` ​
                * :bi:`Register User (Base)`,
                * :bi:`Super User (Base)`,
                * :bi:`User (Base)`,

            * *Document*:

                * :bi:`Manager (Document)` ​
                * :bi:`User (Document)` ​
            
            * *Lab Test*:

                * :bi:`Manager (Lab Test)`
                * :bi:`User (Lab Test)`

            * *Technical*:

                * **Acesso a endereços privados**
                * **Acesso para exportar recurso**

            * *Extra Rights*:

                * **Criação de Contato**

Atualizar as permissões de todos os Usuários da JCAFB-2021v
-----------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar a Ação *Employee User Groups Update* para os *Employees* da JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * *Funcionários* » *Funcionários* » *Funcionários*

        #. Selecionar os *Employees* da JCAFB-2021v

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-25a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-25a.sql

            gzip clvhealth_jcafb_2021v_14_2021-03-25a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-25a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-25a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-25a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-03-25a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-03-25a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-03-25a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-25a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-25a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-25a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-25a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-25a.tar.gz

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
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

[clvhealth-jcafb-2021-vm-pro] Atualizar os fontes do projeto
-------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvhealth-jcafb-2021-vm-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

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

Atualizar o(s) módulo(s) [clv_document, clv_document_jcafb]
-----------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Lista de Módulos:

        * clv_document
        * clv_document_jcafb

    #. [clvhealth-jcafb-2021-vm-pro] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **clvhealth-jcafb-2021-vm-pro** e executar o *Odoo* no modo manual:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                ssh clvhealth-jcafb-2021-vm-pro -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **clvhealth-jcafb-2021-vm-pro** e executar o **install.py**:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 2)
                #

                ssh clvhealth-jcafb-2021-vm-pro -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-12a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-12a.sql

            gzip clvhealth_jcafb_2021v_14_2021-05-12a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-12a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-12a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-05-12a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-05-12a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-05-12a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-12a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-05-12a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-05-12a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12a.tar.gz

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
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [clv_lab_test, clv_lab_test_jcafb]
-----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_lab_test
        * clv_lab_test_jcafb

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_survey]
-------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_survey

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_survey
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar Pesquisas [ECP21, EEV21, EUR21]
-----------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Pesquisas:

        * ECP21

        * EEV21

        * EUR21

Atualizar Lab Test Type [ECP21]
-------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Lab Test Types:

        * ECP21

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-17a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-17a.sql

            gzip clvhealth_jcafb_2021v_14_2021-05-17a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-17a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-17a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-17a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-05-17a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-05-17a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-05-17a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-17a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-17a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-05-17a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-05-17a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-17a.tar.gz

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
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

Atualizar Pesquisas [ECP21, EEV21, EUR21]
-----------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Pesquisas:

        * EAA21

        * EAN21

        * ECP21

        * EDH21

        * EEV21

        * EUR21

        * QAN21

        * QDH21

        * QMD21

        * QSC21

        * QSF21

        * QSI21

        * TAA21

        * TAN21

        * TCR21

        * TDH21

        * TID21

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-06-16a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-06-16a.sql

            gzip clvhealth_jcafb_2021v_14_2021-06-16a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-06-16a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-06-16a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-06-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-06-16a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-06-16a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-06-16a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-06-16a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-06-16a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-06-16a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-06-16a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-06-16a.tar.gz

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
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
