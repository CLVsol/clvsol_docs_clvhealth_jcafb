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

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

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

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Employee User Groups Update* para os *Employees* da JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * *Funcionários* » *Funcionários* » *Funcionários*

        #. Selecionar os *Employees* da JCAFB-2021v

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_document
        * clv_document_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

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

Atualizar o(s) módulo(s) [clv_base]
-------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_base

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_base
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_global_tag]
-----------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_global_tag

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_global_tag
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_base
        * clv_address
        * clv_address_aux
        * clv_address_history
        * clv_family
        * clv_family_history
        * clv_person
        * clv_person_aux
        * clv_person_history

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_base
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalars o(s) módulo(s) [clv_patient_history]
-----------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_patient_history

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14"
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_patient_history]
----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_patient_history

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_history

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_processing_jcafb]
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_processing_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_processing_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalars o(s) módulo(s) [clv_residence_history]
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_residence_history

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14"
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_processing_jcafb]
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_processing_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_processing_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_person_jcafb]
-------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_person_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_person_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Marcar os Endereços visitados durante o Projeto da JCAFB (2017 - 2020)
----------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Related Address Set Marker`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)` » :bi:`Phase` » :bi:`Document Type` » :bi:`Items Ok`

        #. Selecionar todos os Documentos com: :bi:`Refers to (Model)` = ":bi:`clv.address`" »  :bi:`Phase` = ":bi:`JCAFB-2017`" » :bi:`Document Type` = "**QSF17**" » :bi:`Items Ok` = "**true**"

        #. Executar a Ação ":bi:`Document Related Address Set Marker`":

            * Parâmetros utilizados:

                * *Markers*: **Add** » **Selected (JCAFB-2017)**

            #. Utilize o botão :bi:`Related Person Set Marker` para executar a Ação.

        #. Selecionar todos os Documentos com: :bi:`Refers to (Model)` = ":bi:`clv.address`" »  :bi:`Phase` = ":bi:`JCAFB-2018`" » :bi:`Document Type` = "**QSF18**" » :bi:`Items Ok` = "**true**"

        #. Executar a Ação ":bi:`Document Related Address Set Marker`":

            * Parâmetros utilizados:

                * *Markers*: **Add** » **Selected (JCAFB-2018)**

            #. Utilize o botão :bi:`Related Person Set Marker` para executar a Ação.

        #. Selecionar todos os Documentos com: :bi:`Refers to (Model)` = ":bi:`clv.address`" »  :bi:`Phase` = ":bi:`JCAFB-2019`" » :bi:`Document Type` = "**QSF19**" » :bi:`Items Ok` = "**true**"

        #. Executar a Ação ":bi:`Document Related Address Set Marker`":

            * Parâmetros utilizados:

                * *Markers*: **Add** » **Selected (JCAFB-2019)**

            #. Utilize o botão :bi:`Related Person Set Marker` para executar a Ação.

        #. Selecionar todos os Documentos com: :bi:`Refers to (Model)` = ":bi:`clv.address`" »  :bi:`Phase` = ":bi:`JCAFB-2020`" » :bi:`Document Type` = "**TAA20**" » :bi:`Items Ok` = "**true**"

        #. Executar a Ação ":bi:`Document Related Address Set Marker`":

            * Parâmetros utilizados:

                * *Markers*: **Add** » **Selected (JCAFB-2020)**

            #. Utilize o botão :bi:`Related Person Set Marker` para executar a Ação.

Marcar os Endereços que participaram do Projeto da JCAFB (2017 - 2020)
----------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Selected**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Residence`

        #. Selecionar todos os Endereços com: :bi:`Is Residence` = ":bi:`false`"

        #. Executar a Ação ":bi:`Address Mass Edit`":

            * Parâmetros utilizados:

                * *Is Residence*: **Set** **marcado**

                * *Address Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Associar os Endereços a uma Residência
--------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Address Associate to Residence* para os Endereços:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Residence" register.`"

        #. Executar a Ação "**Address Associate to Patient**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Address Verification Execute*: **marcado**

                * *Residence Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

Atualizar o *Register State* de todas as Residências
----------------------------------------------------

    Critérios utilizados:

        * **Done**: todas as Residências.

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as Residências

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Residence Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação** » **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_residence_history_community
        * clv_patient_history_community
        * clv_residence_community_jcafb
        * clv_patient_community_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14"
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_document
        * clv_processing_jcafb
        * clv_patient_history

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_processing_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_history
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_survey
        * clv_document_jcafb
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

Atualizar os parâmetros "*parameter*" das Questoões de todas as Pesquisas
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Pesquisas:

        * **EAA21**:

            #. [EAA21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [EAA21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [EAA21_01_05]: **parameter_2** (1.5. Código do Local)

        * **EAN21**:

            #. [EAN21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [EAN21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [EAN21_01_05]: **parameter_2** (1.5. Código do Código do Paciente)

        * **ECP21**:

            #. [ECP21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [ECP21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [ECP21_01_05]: **parameter_2** (1.5. Código do Código do Paciente)


        * **EDH21**:

            #. [EDH21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [EDH21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [EDH21_01_05]: **parameter_2** (1.5. Código do Código do Paciente)

        * **EEV21**:

            #. [EEV21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [EEV21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [EEV21_01_05]: **parameter_2** (1.5. Código do Código do Paciente)

        * **EUR21**:

            #. [EUR21_01_01]: **parameter_3** (1.1. Código da Requisição de Exames)

            #. [EUR21_01_03]: **parameter_1** (1.3. Código do Resusltado de Exames)

            #. [EUR21_01_05]: **parameter_2** (1.5. Código do Código do Paciente)

        * **QAN17**:

            #. [QAN17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QAN17_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QAN17_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QAN18**:

            #. [QAN18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QAN18_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QAN18_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QAN19**:

            #. [QAN19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QAN19_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QAN19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QAN20**:

            #. [QAN20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QAN20_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QAN21**:

            #. [QAN21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QAN21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QDH17**:

            #. [QDH17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QDH17_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QDH17_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QDH18**:

            #. [QDH18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QDH18_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QDH18_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QDH19**:

            #. [QDH19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QDH19_01_04]: **parameter_3** (1.4. Código da Requisição de Exames)

            #. [QDH19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QDH20**:

            #. [QDH20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QDH20_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QDH21**:

            #. [QDH21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QDH21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QMD17**:

            #. [QMD17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QMD17_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QMD18**:

            #. [QMD18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QMD18_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QMD19**:

            #. [QMD19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QMD19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QMD20**:

            #. [QMD20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QMD20_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QMD21**:

            #. [QMD21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QMD21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC17**:

            #. [QSC17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC17_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC18**:

            #. [QSC18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC18_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC19**:

            #. [QSC19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC20**:

            #. [QSC20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC20_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC21**:

            #. [QSC21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSF17**:

            #. [QSF17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSF17_02_02]: **parameter_2** (2.2. Código do Endereço)

        * **QSC18**:

            #. [QSC18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC18_02_02]: **parameter_2** (2.2. Código do Endereço)

        * **QSC19**:

            #. [QSC19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSC20**:

            #. [QSC20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC20_02_02]: **parameter_2** (2.2. Código da Família)

        * **QSC21**:

            #. [QSC21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSC21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSI17**:

            #. [QSI17_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSI17_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSI18**:

            #. [QSI18_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSI18_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSI19**:

            #. [QSI19_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSI19_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSI20**:

            #. [QSI20_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSI20_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **QSI21**:

            #. [QSI21_01_01]: **parameter_1** (1.1. Código do Questionário)

            #. [QSI21_02_02]: **parameter_2** (2.2. Código do Paciente)

        * **TAA21**:

            #. [TAA21_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TAA21_02_02]: **parameter_2** (2.2. Código do Endereço/Residência)

        * **TAN21**:

            #. [TAN21_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TAN21_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TCP17**:

            #. [TCP17_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TCP17_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TCR17**:

            #. [TCR17_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TCR17_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TCR21**:

            #. [TCR21_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TCR21_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TDH21**:

            #. [TDH21_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TDH21_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TID17**:

            #. [TID17_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TID17_02_02]: **parameter_2** (2.2. Código do Indivíduo)

        * **TID21**:

            #. [TID21_01_01]: **parameter_1** (1.1. Código do Termo de Consentimento)

            #. [TID21_02_02]: **parameter_2** (2.2. Código do Indivíduo)

Associar as referências para as Participações
---------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Survey User Input Get Reference* para as :bi:`Paritipations`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Paritipations*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Paritipations`

        #. Ativar o filtro **Agrupar por** » :bi:`Survey User Input State`

        #. Selecionar as Participações desejadas com: :bi:`Survey User Input State` = ":bi:`Validated`"

        #. Executar a Ação "**Survey User Input Get Reference**":

            #. Utilize o botão *Survey User Input Get Reference* para executar a Ação.

Executar o *Processing Schedule* "Patient History updt_from Person History"
---------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente o *Processing Schedule* **Patient History updt_from Person History**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar o *Processing Schedule* "**Patient History updt_from Person History**"

        #. Executar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

Executar o *Processing Schedule* "Residence History updt_from Address History"
------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente o *Processing Schedule* **Residence History updt_from Address History**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar o *Processing Schedule* "**Residence History updt_from Address History**"

        #. Executar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

Transferir Documentos associados a um Endereço para a Residência relacionada
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Document Associate from Address to Residence* para os Documentos desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Documentos desejados com: :bi:`Refers to (Model)` = ":bi:`clv.address`"

        #. Executar a Ação "**Document Associate from Address to Residence**":

            #. Utilize o botão *Associate from Address to Residence* para executar a Ação.

Transferir Documentos associados a uma Família para a Residência relacionada
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Document Associate from Family to Residence* para os Documentos desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Documentos desejados com: :bi:`Refers to (Model)` = ":bi:`clv.family`"

        #. Executar a Ação "**Document Associate from Family to Residence**":

            #. Utilize o botão *Associate from Family to Residence* para executar a Ação.

Transferir Documentos associados a uma Pessoa para o Paciente relacionado
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Document Associate from Person to Patient* para os Documentos desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Documentos desejados com: :bi:`Refers to (Model)` = ":bi:`clv.person`"

        #. Executar a Ação "**Document Associate from Person to Patient**":

            #. Utilize o botão *Associate from Person to Patient* para executar a Ação.

Executar o *Processing Schedule* "Copy QSF from Residence to Patient"
---------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente o *Processing Schedule* **Copy QSF from Residence to Patient**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar o *Processing Schedule* "**Copy QSF from Residence to Patient**"

        #. Executar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

Transferir Requisições de Exames associadas a um Endereço para a Residência relacionada
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Request Associate from Address to Residence* para as Requisições de Exames desejadas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar as Requisições de Exames desejadas com: :bi:`Refers to (Model)` = ":bi:`clv.address`"

        #. Executar a Ação "**Lab Test Request Associate from Address to Residence**":

            #. Utilize o botão *Associate from Address to Residence* para executar a Ação.

Transferir Requisições de Exames associadas a uma Pessoa para o Paciente relacionado
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Request Associate from Person to Patient* para as Requisições de Exames desejadas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar as Requisições de Exames desejadas com: :bi:`Refers to (Model)` = ":bi:`clv.person`"

        #. Executar a Ação "**Lab Test Request Associate from Person to Patient**":

            #. Utilize o botão *Associate from Person to Patient* para executar a Ação.

Transferir Resultados de Exames associados a um Endereço para a Residência relacionada
--------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Result Associate from Address to Residence* para os Resultados de Exames desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Resultados de Exames desejados com: :bi:`Refers to (Model)` = ":bi:`clv.address`"

        #. Executar a Ação "**Lab Test Result Associate from Address to Residence**":

            #. Utilize o botão *Associate from Address to Residence* para executar a Ação.

Transferir Resultados de Exames associados a uma Pessoa para o Paciente relacionado
-----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Result Associate from Person to Patient* para os Resultados de Exames desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Resultados de Exames desejados com: :bi:`Refers to (Model)` = ":bi:`clv.person`"

        #. Executar a Ação "**Lab Test Result Associate from Person to Patient**":

            #. Utilize o botão *Associate from Person to Patient* para executar a Ação.

Transferir Laudos de Exames associados a um Endereço para a Residência relacionada
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Report Associate from Address to Residence* para os Laudos de Exames desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Reports*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Reports`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Laudos de Exames desejados com: :bi:`Refers to (Model)` = ":bi:`clv.address`"

        #. Executar a Ação "**Lab Test Report Associate from Address to Residence**":

            #. Utilize o botão *Associate from Address to Residence* para executar a Ação.

Transferir Laudos de Exames associados a uma Pessoa para o Paciente relacionado
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Lab Test Report Associate from Person to Patient* para os Laudos de Exames desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Reports*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Reports`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Laudos de Exames desejados com: :bi:`Refers to (Model)` = ":bi:`clv.person`"

        #. Executar a Ação "**Lab Test Report Associate from Person to Patient**":

            #. Utilize o botão *Associate from Person to Patient* para executar a Ação.

Transferir Eventos associados a uma Pessoa para o Paciente relacionado
----------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Event Attendee Associate from Person to Patient* para os Eventos desejados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Event Attendees*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configurarion` » :bi:`Event` » :bi:`Attendees`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar os Eventos desejados com: :bi:`Refers to (Model)` = ":bi:`clv.person`"

        #. Executar a Ação "**Event Attendee Associate from Person to Patient**":

            #. Utilize o botão *Associate from Person to Patient* para executar a Ação.

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_summary_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_summary_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_survey
        * clv_document_jcafb
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_lab_test

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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_base

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_base

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_summary_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_summary_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o parâmetro "*description*" de todas os Tipos de Pesquisas
--------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Tipos de Pesquisas:

        * **QAN17**:

            #. **description**: "JCAFB 2017 - Questionário para detecção de Anemia"

        * **QAN18**:

            #. **description**: "JCAFB 2018 - Questionário para detecção de Anemia"

        * **QAN19**:

            #. **description**: "JCAFB 2019 - Questionário para detecção de Anemia"

        * **QAN20**:

            #. **description**: "JCAFB 2020 - Questionário para detecção de Anemia"

        * **QAN21**:

            #. **description**: "JCAFB 2021 - Questionário para detecção de Anemia"

        * **QDH17**:

            #. **description**: "JCAFB 2017 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **QDH18**:

            #. **description**: "JCAFB 2018 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **QDH19**:

            #. **description**: "JCAFB 2019 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **QDH20**:

            #. **description**: "JCAFB 2020 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **QDH21**:

            #. **description**: "JCAFB 2021 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **QMD17**:

            #. **description**: "JCAFB 2017 - Questionário - Medicamentos"

        * **QMD18**:

            #. **description**: "JCAFB 2018 - Questionário - Medicamentos"

        * **QMD19**:

            #. **description**: "JCAFB 2019 - Questionário - Medicamentos"

        * **QMD20**:

            #. **description**: "JCAFB 2020 - Questionário - Medicamentos"

        * **QMD21**:

            #. **description**: "JCAFB 2021 - Questionário - Medicamentos"

        * **QSC17**:

            #. **description**: "JCAFB 2017 - Questionário Socioeconômico Individual (Crianças)"

        * **QSC18**:

            #. **description**: "JCAFB 2018 - Questionário Socioeconômico Individual (Crianças)"

        * **QSC19**:

            #. **description**: "JCAFB 2019 - Questionário Socioeconômico Individual (Crianças)"

        * **QSC20**:

            #. **description**: "JCAFB 2020 - Questionário Socioeconômico Individual (Crianças)"

        * **QSC21**:

            #. **description**: "JCAFB 2021 - Questionário Socioeconômico Individual (Crianças)"

        * **QSF17**:

            #. **description**: "JCAFB 2017 - Questionário Socioeconômico Familiar (Crianças e Idosos)"

        * **QSC18**:

            #. **description**: "JCAFB 2018 - Questionário Socioeconômico Familiar (Crianças e Idosos)"

        * **QSC19**:

            #. **description**: "JCAFB 2019 - Questionário Socioeconômico Familiar (Crianças e Idosos)"

        * **QSC20**:

            #. **description**: "JCAFB 2020 - Questionário Socioeconômico Familiar (Crianças e Idosos)"

        * **QSC21**:

            #. **description**: "JCAFB 2021 - Questionário Socioeconômico Familiar (Crianças e Idosos)"

        * **QSI17**:

            #. **description**: "JCAFB 2017 - Questionário Socioeconômico Individual (Idosos)"

        * **QSI18**:

            #. **description**: "JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)"

        * **QSI19**:

            #. **description**: "JCAFB 2019 - Questionário Socioeconômico Individual (Idosos)"

        * **QSI20**:

            #. **description**: "JCAFB 2020 - Questionário Socioeconômico Individual (Idosos)"

        * **QSI21**:

            #. **description**: "JCAFB 2021 - Questionário Socioeconômico Individual (Idosos)"

        * **TAA20**:

            #. **description**: "JCAFB 2020 - Termo de Consentimento Livre e Esclarecido para a Análise Físico-Química e Microbiológica da Água"

        * **TAA21**:

            #. **description**: "JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para a Análise Físico-Química e Microbiológica da Água"

        * **TAN18**:

            #. **description**: "JCAFB 2018 - Termo de Consentimento para a Campanha de Detecção de Anemia"

        * **TAN19**:

            #. **description**: "JCAFB 2019 - Termo de Consentimento para a Campanha de Detecção de Anemia"

        * **TAN20**:

            #. **description**: "JCAFB 2020 - Termo de Consentimento para a Campanha de Detecção de Anemia"

        * **TAN21**:

            #. **description**: "JCAFB 2021 - Termo de Consentimento para a Campanha de Detecção de Anemia"

        * **TCP17**:

            #. **description**: "JCAFB 2017 - TERMO DE CONSENTIMENTO PARA A CAMPANHA DE DETECÇÃO DE DIABETES, HIPERTENSÃO ARTERIAL E HIPERCOLESTEROLEMIA"

        * **TCR17**:

            #. **description**: "JCAFB 2017 - TERMO DE CONSENTIMENTO LIVRE E ESCLARECIDO PARA REALIZAÇÃO DE EXAMES COPROPARASITOLÓGICOS, DETECÇÃO DE ANEMIA E QUESTIONÁRIO SOCIOECONÔMICO"

        * **TCR18**:

            #. **description**: "JCAFB 2018 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos"

        * **TCR19**:

            #. **description**: "JCAFB 2019 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos"

        * **TCR20**:

            #. **description**: "JCAFB 2020 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos"

        * **TCR21**:

            #. **description**: "JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos"

        * **TDH18**:

            #. **description**: "JCAFB 2018 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **TDH19**:

            #. **description**: "JCAFB 2019 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **TDH20**:

            #. **description**: "JCAFB 2020 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **TDH21**:

            #. **description**: "JCAFB 2021 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia"

        * **TID17**:

            #. **description**: "JCAFB 2017 - TERMO DE CONSENTIMENTO LIVRE E ESCLARECIDO PARA REALIZAÇÃO DE EXAME DE URINA, COPROPARASITOLÓGICO, DETECÇÃO DE ANEMIA E QUESTIONÁRIO SOCIOECONÔMICO"

        * **TID18**:

            #. **description**: "JCAFB 2018 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico"

        * **TID19**:

            #. **description**: "JCAFB 2019 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico"

        * **TID20**:

            #. **description**: "JCAFB 2020 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico"

        * **TID21**:

            #. **description**: "JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico"

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_patient_aux_summary_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14" -m clv_patient_aux_summary_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_lab_test
        * clv_event

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

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_event

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_document_jcafb
        * clv_lab_test_jcafb
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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" 
                --db "clvhealth_jcafb_2021v_13" -m clv_lab_test_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" 
                --db "clvhealth_jcafb_2021v_13" -m clv_survey

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_lab_test_verification_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14" -m clv_lab_test_verification_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar os "*Templates File Names*" de todas os Tipos de Exames
-----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Tipos de Exames:

        * **EAN21**:

            #. **Template File Name (Result)**: "Resultado_EAN21_template.xls"

            #. **Template File Name (Report)**: "Laudo_EAN21_template.xls"

        * **EDH21**:

            #. **Template File Name (Result)**: "Resultado_EDH21_template.xls"

            #. **Template File Name (Report)**: "Laudo_EDH21_template.xls"

        * **EAA21**:

            #. **Template File Name (Result)**: "Resultado_EAA21_template.xls"

            #. **Template File Name (Report)**: "Laudo_EAA21_template.xls"

        * **ECP21**:

            #. **Template File Name (Result)**: "Resultado_ECP21_template.xls"

            #. **Template File Name (Report)**: "Laudo_ECP21_template.xls"

        * **EEV21**:

            #. **Template File Name (Result)**: "Resultado_EEV21_template.xls"

            #. **Template File Name (Report)**: "Laudo_EEV21_template.xls"

        * **EUR21**:

            #. **Template File Name (Result)**: "Resultado_EUR21_template.xls"

            #. **Template File Name (Report)**: "Laudo_EUR21_template.xls"

Atualizar os "*Lab Test Export XLS Parameter*" dos Tipos de Exames
------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Tipos de Exames:

        * **EAN21**:

            * *Result*
            
            * *Report*

        * **ECP21**:

            * *Result*
            
            * *Report*

        * **EEV21**:

            * *Result*
            
            * *Report*

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

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

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-01a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-01a.sql

            gzip clvhealth_jcafb_2021v_14_2021-10-01a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-01a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-01a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-01a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-10-01a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-10-01a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-10-01a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-01a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-01a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-10-01a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-10-01a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-01a.tar.gz

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

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_processing_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_processing_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-04a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-04a.sql

            gzip clvhealth_jcafb_2021v_14_2021-10-04a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-04a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-10-04a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-10-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-10-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-04a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-04a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-10-04a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-10-04a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-04a.tar.gz

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

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
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

Atualizar o(s) módulo(s) [clv_export]
-------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_export

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_export

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-07a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-07a.sql

            gzip clvhealth_jcafb_2021v_14_2021-10-07a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-10-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-07a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-10-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-10-07a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-10-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-10-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-07a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-10-07a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-10-07a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-10-07a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-10-07a.tar.gz

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
