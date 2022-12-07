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

=================================================================
JCAFB-2023-15  (Tratamento de Documentos Testes de Laboratório 1)
=================================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-05c)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2022-12-05c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-05c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_lab_test

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_document_survey
        * clv_lab_test_survey
    #. [tkl-odoo15-jcafb23-vm] **Executar** a instalação do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar os *Document Categories* para a JCAFB-2023
------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Document Types* para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Categories`

        * *Document Categories* criadas:
            
            * **(Campanha) Questionário**

                * *Name*: **(Campanha) Questionário**

            * **(Campanha) Resultado de Exames**

                * *Name*: **(Campanha) Resultado de Exames**

            * **(Campanha) Termo de Consentimento**

                * *Name*: **(Campanha) Termo de Consentimento**

            * **(Campo) Questionário**

                * *Name*: **(Campo) Questionário**

            * **(Campo) Resultado de Exames**

                * *Name*: **(Campo) Resultado de Exames**

            * **(Campo) Termo de Consentimento**

                * *Name*: **(Campanha) Termo de Consentimento**

            * **(Laboratório de Análises) Resultado de Exames**

                * *Name*: **(Campo) Resultado de Exames**

Criar os *Document Types* para a JCAFB-2023
-------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Document Types* para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        * *Document Types* criados:
            
            * **EAN23**

                * *Categories*: **(Campanha) Resultado de Exames**
                * *Document Type*: **EAN23**
                * *Document Type Code*: **EAN23**
                * *Document Type Description*: **JCAFB 2023 - Exames - Detecção de Anemia**
                * *Survey Type*: **[EAN23]**
                * *Phase*: **JCAFB-2023**

            * **ECP23**

                * *Categories*: **(Latoratório de Análises) Resultado de Exames**
                * *Document Type*: **ECP23**
                * *Document Type Code*: **ECP23**
                * *Document Type Description*: **JCAFB 2023 - Laboratório - Parasitologia**
                * *Survey Type*: **[ECP23]**
                * *Phase*: **JCAFB-2023**

            * **EDH23**

                * *Categories*: **(Campanha) Resultado de Exames**
                * *Document Type*: **EDH23**
                * *Document Type Code*: **EDH23**
                * *Document Type Description*: **JCAFB 2023 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Survey Type*: **[EDH23]**
                * *Phase*: **JCAFB-2023**

            * **EUR23**

                * *Categories*: **(Latoratório de Análises) Resultado de Exames**
                * *Document Type*: **EUR23**
                * *Document Type Code*: **EUR23**
                * *Document Type Description*: **JCAFB 2023 - Laboratório - Urinálise**
                * *Survey Type*: **[EUR23]**
                * *Phase*: **JCAFB-2023**

            * **QAN23**

                * *Categories*: **(Campanha) Questionário**
                * *Document Type*: **QAN23**
                * *Document Type Code*: **QAN23**
                * *Document Type Description*: **JCAFB 2023 - Questionário para Detecção de Anemia**
                * *Survey Type*: **[QAN23]**
                * *Phase*: **JCAFB-2023**

            * **QDH23**

                * *Categories*: **(Campanha) Questionário**
                * *Document Type*: **QDH23**
                * *Document Type Code*: **QDH23**
                * *Document Type Description*: **JCAFB 2023 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Survey Type*: **[QDH23]**
                * *Phase*: **JCAFB-2023**

            * **QMD23**

                * *Categories*: **(Campo) Questionário**
                * *Document Type*: **QMD23**
                * *Document Type Code*: **QMD23**
                * *Document Type Description*: **JCAFB 2023 - Questionário - Medicamentos**
                * *Survey Type*: **[QMD23]**
                * *Phase*: **JCAFB-2023**

            * **QSC23**

                * *Categories*: **(Campo) Questionário**
                * *Document Type*: **QSC23**
                * *Document Type Code*: **QSC23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Individual (Crianças)**
                * *Survey Type*: **[QSC23]**
                * *Phase*: **JCAFB-2023**

            * **QSF23**

                * *Categories*: **(Campo) Questionário**
                * *Document Type*: **QSF23**
                * *Document Type Code*: **QSF23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Familiar**
                * *Survey Type*: **[QSF23]**
                * *Phase*: **JCAFB-2023**

            * **QSI23**

                * *Categories*: **(Campo) Questionário**
                * *Document Type*: **QSI23**
                * *Document Type Code*: **QSI23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Individual (Idosos)**
                * *Survey Type*: **[QSI23]**
                * *Phase*: **JCAFB-2023**

Criar os *Lab Test Types* para a JCAFB-2023
-------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Lab Test Types* para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        * *Lab Test Types* criados:
            
            * **EAN23**

                * *Lab Test Type*: **EAN23**
                * *Lab Test Type Code*: **EAN23**
                * *Lab Test Type Description*: **JCAFB 2023 - Exames - Detecção de Anemia**
                * *Survey Type*: **[EAN23]**
                * *Phase*: **JCAFB-2023**

            * **ECP23**

                * *Lab Test Type*: **ECP23**
                * *Lab Test Type Code*: **ECP23**
                * *Lab Test Type Description*: **JCAFB 2023 - Laboratório - Parasitologia**
                * *Survey Type*: **[ECP23]**
                * *Phase*: **JCAFB-2023**

            * **EDH23**

                * *Lab Test Type*: **EDH23**
                * *Lab Test Type Code*: **EDH23**
                * *Lab Test Type Description*: **JCAFB 2023 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Survey Type*: **[EDH23]**
                * *Phase*: **JCAFB-2023**

            * **EUR23**

                * *Lab Test Type*: **EUR23**
                * *Lab Test Type Code*: **EUR23**
                * *Lab Test Type Description*: **JCAFB 2023 - Laboratório - Urinálise**
                * *Survey Type*: **[EUR23]**
                * *Phase*: **JCAFB-2023**

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_patient_aux_jcafb
        * clv_patient_jcafb

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_aux_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_patient_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-07a)
-------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-07a.sql

            gzip clvhealth_jcafb_2023_15_2022-12-07a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-12-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-07a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-12-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-12-07a.sql
.. index:: clvhealth_jcafb_2023_15_2022-12-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-12-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-07a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-07a)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2022-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-07a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
