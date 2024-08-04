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

==========================================
JCAFB-2025-15 (Preparação pré Jornada [9])
==========================================

:bmaroon:`(Not Implemented)` [tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
----------------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-05-26a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-26a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(106,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,106**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,106'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                ref_code    code
                203 clv.patient_aux,106 clv.patient_aux Anisio Manoel de Araujo 212.046-16  340.708-00 

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**212.046-16**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '212.046-16'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                46   0355564963      833         212.046-16

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,106**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,46**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(269,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,269**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,269'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                ref_code    code
                141 clv.patient_aux,269 clv.patient_aux Antonio Carlos da Silva 212.052-64  340.802-79

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**212.052-64**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '212.052-64'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                52   0304852050      839         212.052-64

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,269**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,52**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(270,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,270**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,270'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                   ref_code    code
                142 clv.patient_aux,270 clv.patient_aux Olinda Bonruque Nascimento 212.436-03  340.800-07

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**212.436-03**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '212.436-03'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                436  1702394427      1223        212.052-64

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,270**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,436**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(478,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,478**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,478'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                       ref_code    code
                112 clv.patient_aux,478 clv.patient_aux Zeneide Aparecida Soares Costa 212.552-88  340.800-07

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**212.552-88**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '212.552-88'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                552  1634124671      1339        212.552-88

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,478**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,552**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(605,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,605**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,605'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                    ref_code    code
                199 clv.patient_aux,605 clv.patient_aux Berenice Aparecida Cordeiro 213.354-78  340.824-84

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**213.354-78**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '213.354-78'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                604  1451325672      1630        213.354-78

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,605**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,604**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Lab Test Results**"
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Lab Test Results`:

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(610,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,610**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_lab_test_result"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,610'
                ORDER BY ref_id

            ::

                id  ref_id              ref_model       ref_name                ref_code    code
                259 clv.patient_aux,610 clv.patient_aux Ataide Jorge dos Santos 213.358-00  340.840-02

    #. [tkl-odoo15-jcafb25-vm:12322] Em outra aba, selecionar o registro de "**clv_patient**" apontando para "**213.358-00**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_patient"
                WHERE code = '213.358-00'
                ORDER BY code

            ::

                id   random_field    partner_id  code
                608  1509368859      1639        213.358-00

    #. [tkl-odoo15-jcafb25-vm:12322] Editar o registro de "**clv_lab_test_result**" apontando para "**clv.patient_aux,610**":

        * Parâmetros utilizados:
            * **ref_id**: **clv.patient,608**
            * **ref_model**: **clv.patient**

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-08-04a.sql

            gzip clvhealth_jcafb_2025_15_2024-08-04a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-08-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-08-04a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-08-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-08-04a.sql
.. index:: clvhealth_jcafb_2025_15_2024-08-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-08-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-08-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
