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

.. index:: Migração do Banco de Dados [CLVhealth-JCAFB-2025n-15]"

=====================================================
Migração do Banco de Dados [CLVhealth-JCAFB-2025n-15]
=====================================================

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Upgrade the odoo software
------------------------------------------------------------------

    #. Upgrade the odoo software:

        ::

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

        ::

            apt-get update
            apt-get -y upgrade

            # apt-get install odoo

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Atualizar os fontes do projeto
-----------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb25n-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[tkl-odoo15-jcafb25n-vm] Habilitar a instalação do(s) módulo(s) [ver lista] (2024-05-30a)
-----------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25n-vm] Lista de Módulos:

        #. Odoo Addons:

            * mail
            * hr
            * contacts
            * base_address_city
            * base_address_extended
            * survey

        #. CLVsol Odoo Addons:

            * clv_base
            * clv_phase
            * clv_file_system
            * clv_global_tag
            * clv_set
            * clv_pool
            * clv_employee
            * clv_employee_history
            * clv_survey
            * clv_event
            * clv_document
            * clv_document_survey
            * clv_lab_test
            * clv_lab_test_survey
            * clv_partner_entity
            * clv_residence
            * clv_residence_history
            * clv_patient
            * clv_patient_history
            * clv_patient_aux
            * clv_patient_rec

        #. CLVsol l10n-brazil:

            * clv_l10n_br_base
            * clv_l10n_br_zip

        #. CLVsol Odoo Addons - Brazilian Localization:

            * clv_partner_entity_l10n_br
            * clv_residence_l10n_br
            * clv_patient_l10n_br
            * clv_patient_aux_l10n_br
            * clv_patient_rec_l10n_br

        #. CLVsol Odoo Addons - JCAFB customizations:

            * clv_base_jcafb
            * clv_employee_jcafb
            * clv_event_jcafb
            * clv_document_jcafb
            * clv_document_pool_jcafb
            * clv_lab_test_jcafb
            * clv_lab_test_pool_jcafb
            * clv_residence_jcafb
            * clv_residence_pool_jcafb
            * clv_patient_jcafb
            * clv_patient_pool_jcafb
            * clv_patient_aux_jcafb
            * clv_patient_rec_jcafb

        #.  CLVsol Odoo Addons - Log:

            * clv_global_log

        #. CLVsol Odoo Addons - Log - JCAFB customizations:

            * clv_document_log_jcafb
            * clv_lab_test_log_jcafb
            * clv_partner_entity_log_jcafb
            * clv_residence_log_jcafb
            * clv_patient_log_jcafb
            * clv_patient_aux_log_jcafb
            * clv_patient_rec_log_jcafb

        #. CLVsol Odoo Addons - Summary:

            * clv_summary

        #. CLVsol Odoo Addons - Summary - JCAFB customizations:

            * clv_summary_jcafb
            * clv_employee_summary_jcafb
            * clv_residence_summary_jcafb
            * clv_patient_summary_jcafb
            * clv_patient_aux_summary_jcafb

        #. CLVsol Odoo Addons - Verification:

            * clv_verification

        #. CLVsol Odoo Addons - Verification - JCAFB customizations:

            * clv_verification_jcafb
            * clv_verification_log_jcafb
            * clv_partner_entity_verification_jcafb
            * clv_patient_rec_verification_jcafb
            * clv_residence_verification_jcafb
            * clv_patient_verification_jcafb
            * clv_patient_aux_verification_jcafb
            * clv_lab_test_verification_jcafb

        #. CLVsol Odoo Addons - Export:

            * clv_export
            * clv_document_export
            * clv_lab_test_export
            * clv_patient_export

        #. CLVsol Odoo Addons - Export - JCAFB customizations:

            * clv_export_jcafb
            * clv_document_export_jcafb
            * clv_lab_test_export_jcafb
            * clv_patient_export_jcafb

        #. CLVsol Odoo Addons - Process:

            * clv_processing

        #. CLVsol Odoo Addons - Process - JCAFB customizations:

            * clv_processing_jcafb

        #. CLVsol Odoo Addons - Sync:

            * clv_external_sync
            * clv_base_sync
            * clv_phase_sync
            * clv_file_system_sync
            * clv_global_tag_sync
            * clv_set_sync
            * clv_employee_sync
            * clv_employee_history_sync
            * clv_survey_sync

        #. CLVsol Odoo Addons - Sync - JCAFB customizations:

            * clv_external_sync_jcafb
            * clv_employee_sync_jcafb

[tkl-odoo15-jcafb25n-vm] Criar uma nova instância do *CLVhealth-JCAFB-2025n-15* (2024-05-30a)
---------------------------------------------------------------------------------------------

    #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb25n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. Excluir a instância do *CLVhealth-JCAFB-2025n-15* existente:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2025n_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025n_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb25n-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb25n-vm (session 2)
            #

            ssh tkl-odoo15-jcafb25n-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2025n_15"

        * **Execution time: 0:11:25.901**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25n-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

[tkl-odoo15-jcafb25n-vm] Criar o *External Sync Host* "https://192.168.25.210"
------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

    #. Criar o *External Sync Host* **https://192.168.25.210**:

        * Menu de acesso:
            
            * :bi:`External Sync` > :bi:`Configuration` > :bi:`Hosts` > Criar

        * Parâmetros utilizados:
            
            * External Host Name: "**https://192.168.25.210**"
            * External Database Name: "**clvhealth_jcafb_2025_15**"
            * External User: "**admin**"
            * External User Password: "*******"

[tkl-odoo15-jcafb25n-vm] Configurar todos os "*External Sync Schedules*"
------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

    #. Configurar, com a ajuda da ação :bi:`External Sync Schedule Mass Edit (2)`, todos os :bi:`External Sync Schedules`:

        * Lista de *Schedules*:

            * Todos os :bi:`External Sync Schedules`

        * Menu de acesso:
            
            * :bi:`External Sync` » :bi:`Configuration` » :bi:`External Sync` » :bi:`Batch Members` » **Ação** » :bi:`External Sync Schedule Mass Edit (2)`

        * Parâmetros alterados:
            
            * *External Host*: "**https://192.168.25.210**"
            * *Max Task Registers*: "**300.000**"

[tkl-odoo15-jcafb25n-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-30a)
--------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025n_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025n_15_2024-05-30a.sql

            gzip clvhealth_jcafb_2025n_15_2024-05-30a.sql
            pg_dump clvhealth_jcafb_2025n_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025n_15_2024-05-30a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz clvhealth_jcafb_2025n_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025n_15_2024-05-30a.sql
        * /opt/odoo/clvhealth_jcafb_2025n_15_2024-05-30a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz

.. index:: clvhealth_jcafb_2025n_15_2024-05-30a.sql
.. index:: clvhealth_jcafb_2025n_15_2024-05-30a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025n_15_2024-05-30a
.. index:: clvsol_filestore_clvhealth_jcafb_2025n_15_2024-05-30a

:bmaroon:`(Not Implemented)` [tkl-odoo15-jcafb25n-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-30a)
-----------------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025n_15_2024-05-30a.sql.gz

            dropdb -i clvhealth_jcafb_2025n_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025n_15
            psql -f clvhealth_jcafb_2025n_15_2024-05-30a.sql -d clvhealth_jcafb_2025n_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025n_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025n_15_2024-05-30a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25n-vm**".

        #. Salvar o registro editado.

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Schedule* "clv.global_settings (current_filestore_path) [Sync])"
-----------------------------------------------------------------------------------------------------------------------------------

    #. :red:`(Not Used)` Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.model**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.model**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Executar o :bi:`External Sync Schedule` "**clv.global_settings (current_filestore_path) [Sync])**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. :red:`(Not Used)` Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.global_settings (current_filestore_path) [Sync])**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.global_settings (current_filestore_path) [Sync])**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:00:01.312`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Schedule* "res.users [Migration]"
----------------------------------------------------------------------------------------------------

    #. :red:`(Not Used)` Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**res.users**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**res.model**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Executar o :bi:`External Sync Schedule` "**res.users [Migration]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. :red:`(Not Used)` Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**res.users [Migration]**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**res.users [Migration]**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:02:47.018`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Schedule* "res.users (res.users) [Rec]"
----------------------------------------------------------------------------------------------------------

    #. :red:`(Not Used)` Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**res.users**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**res.users**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Executar o :bi:`External Sync Schedule` "**res.users (res.users) [Rec]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. :red:`(Not Used)` Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**res.users (res.users) [Rec]**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**res.users (res.users) [Rec]**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:02:47.018`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Schedule* "clv.phase (clv.phase) [Sync]"
-----------------------------------------------------------------------------------------------------------

    #. :red:`(Not Used)` Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.phase**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.phase**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Executar o :bi:`External Sync Schedule` "**clv.phase (clv.phase) [Sync]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. :red:`(Not Used)` Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.phase (clv.phase) [Sync]**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.phase (clv.phase) [Sync]**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:00:01.221`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

:borange:`(**)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Schedule* "clv.global_settings (current_phase_id) [Sync]"
----------------------------------------------------------------------------------------------------------------------------

    #. :red:`(Not Used)` Marcar como :bi:`Updated` o :bi:`External Synchronization` de todos os :bi:`External Syncs` do *Model* "**clv.model**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Configurar, com a ajuda da ação :bi:`External Sync Mass Edit`, todos os :bi:`External Syncs` do *Model* "**clv.model**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Syncs` » **Ação** » :bi:`External Sync Mass Edit`

            * Parâmetros alterados:
                * *External Synchronization*: **Set** "**Updated**"

    #. Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25n-vm** e executar o *Odoo* no modo manual:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            #

            ssh tkl-odoo15-jcafb25n-vm -l root

            /etc/init.d/odoo stop

            su odoo

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Executar o :bi:`External Sync Schedule` "**clv.global_settings (current_phase_id) [Sync]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. :red:`(Not Used)` Atualizar os :bi:`Object Fields` do :bi:`External Sync Schedule` "**clv.global_settings (current_phase_id) [Sync]**".

        #. Executar a ação :bi:`External Sync Schedule Exec` para o "**clv.global_settings (current_phase_id) [Sync]**":

            * Menu de acesso:
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Schedules` » **Ação** » :bi:`External Sync Schedule Exec`

            * :bi:`Execution time: 0:00:01.312`

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25n-vm** ao modo padrão:

        ::

            # ***** tkl-odoo15-jcafb25n-vm
            # 


            ^C

            exit

            /etc/init.d/odoo start

[tkl-odoo15-jcafb25n-vm] Desabilitar os "*External Sync Batch Members*" não necessários
---------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

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

Lista de *Schedules* instalados (00-25n-15)
-------------------------------------------

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

[tkl-odoo15-jcafb25n-vm] Executar o *External Sync Batch* "*Default Batch [00]*"
--------------------------------------------------------------------------------

    #. Executar o :bi:`External Sync Batch` "**Default Batch [00]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [00]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:07:12.952`
            
Lista de *Schedules* instalados (02-25n-15)
-------------------------------------------

        .. #. :blue:`(Enabled)` clv.patient (clv.patient) [2]

        .. #. :blue:`(Enabled)` clv.patient.history (clv.patient.history) [2]

:red:`(Não Executado)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Batch* "*Default Batch [02]*"
-------------------------------------------------------------------------------------------------------

    #. Executar o :bi:`External Sync Batch` "**Default Batch [02]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [02]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

Lista de *Schedules* instalados (10-25n-15)
-------------------------------------------

    * Lista de *Schedules* instalados:

        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [1] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [2] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [3] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [4] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [5] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [6] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [7] [Sync]
        #. :red:`(Disabled)` survey.user_input.line (survey.user_input.line) [8] [Sync]

:red:`(Não Executado)` [tkl-odoo15-jcafb25n-vm] Executar o *External Sync Batch* "*Default Batch [10]*"
-------------------------------------------------------------------------------------------------------

    #. Executar o :bi:`External Sync Batch` "**Default Batch [10]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25n-vm <https://tkl-odoo15-jcafb25n-vm>`_

        #. Executar a ação :bi:`External Sync Batch Exec` para o "**Default Batch [10]**":

            * Menu de acesso:
                
                * :bi:`External Sync` » :bi:`External Sync` » :bi:`External Sync` » :bi:`Batches` » **Ação** » :bi:`External Sync Batch Exec`

            * :bi:`Execution time: 0:00:00.000`

.. toctree::   :maxdepth: 2
