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

=============================
JCAFB-2023-15 (Atualização 1)
=============================

Atualizar os fontes do projeto (2023-01-27a)
--------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

Criar uma nova instância do *CLVhealth-JCAFB-2023-15*
------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Excluir a instância do *CLVhealth-JCAFB-2023-15* existente:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2023_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb23n-vm (session 2)
            #

            ssh tkl-odoo15-jcafb23n-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        * **Execution time: 0:07:18.565**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-27b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-27b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-27b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-27b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-27b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_lab_test

        * clv_lab_test_jcafb
        * clv_lab_test_pool_jcafb

        * clv_residence_jcafb
        * clv_patient_jcafb
        * clv_patient_aux_jcafb

        * clv_lab_test_log_jcafb

        * clv_patient_export_jcafb
        * clv_person_export_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-01-28b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-01-28b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-01-28b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-01-28b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-01-28b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_partner_entity_verification_jcafb
        * clv_patient_verification_jcafb
        * clv_patient_aux_verification_jcafb
        * clv_residence_verification_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_partner_entity_verification_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_verification_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux_verification_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_residence_verification_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-02-02a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-02-02a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-02-02a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-02-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-02-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_patient_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar os fontes do projeto (2023-02-03b)
--------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo15-jcafb23n-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

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

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            # cd /opt/odoo/clvsol_odoo_addons_report
            # git pull

            # cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            # git pull

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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-02-03b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-02-03b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-02-03b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-02-03b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-02-03b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_document_pool_jcafb
        * clv_lab_test_pool_jcafb
        * clv_patient_pool_jcafb
        * clv_residence_pool_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document_pool_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test_pool_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_pool_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_residence_pool_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-02-15a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-02-15a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-02-15a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-02-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-02-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-02-15b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-02-15b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-02-15b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-02-15b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-02-15b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-02-16a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-02-16a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-02-16a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-02-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-02-16a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-03-02a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-03-02a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-03-02a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Habilitar a instalação e instalar o(s) módulo(s) "clv_patient_rec"
------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_patient_rec
        * clv_patient_rec_l10n_br
        * clv_patient_rec_jcafb
        * clv_patient_rec_log_jcafb
        * clv_patient_rec_verification_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a instalação do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Lista de Módulos:

        * clv_patient_aux
        * clv_patient_aux_log_jcafb

    #. [tkl-odoo15-jcafb23n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-03-02b)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-03-02b.sql

            gzip clvhealth_jcafb_2023_15_2023-03-02b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-03-02b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-03-02b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-03-02b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-03-02b.sql
.. index:: clvhealth_jcafb_2023_15_2023-03-02b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-03-02b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-03-02b)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-03-02b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-03-02b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

Executar o *Verification Batch* “Default Batch”
-----------------------------------------------

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:07:47.522`

Executar o *Verification Batch* “Default Batch”
-----------------------------------------------

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:12:44.497`

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-03-02c)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-03-02c.sql

            gzip clvhealth_jcafb_2023_15_2023-03-02c.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2023-03-02c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2023-03-02c.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2023-03-02c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz

.. index:: clvhealth_jcafb_2023_15_2023-03-02c.sql
.. index:: clvhealth_jcafb_2023_15_2023-03-02c.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2023-03-02c
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02c

Criar uma nova instância do *CLVhealth-JCAFB-2023-15*
------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Excluir a instância do *CLVhealth-JCAFB-2023-15* existente:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            dropdb -i clvhealth_jcafb_2023_15

            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo manual:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23n-vm** e executar o **install.py**:

        ::

            # ***** tkl-odoo15-jcafb23n-vm (session 2)
            #

            ssh tkl-odoo15-jcafb23n-vm -l odoo

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        * **Execution time: 0:07:18.565**

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm (session 1)
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2023-03-02c)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            ssh tkl-odoo15-jcafb23n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2023-03-02c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2023-03-02c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2023-03-02c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23n-vm <https://tkl-odoo15-jcafb23n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23n-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
