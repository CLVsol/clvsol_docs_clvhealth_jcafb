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
JCAFB-2025-15 (Preparação pré Jornada [7])
==========================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-19c)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-05-19c.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-19c.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-19c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-19c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Sreet Pattern Matches**"
------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Sreet Pattern Matches`:

        #. Acessar a *View* *Sreet Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Sreet Pattern Matches`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(591,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient_aux(591,)**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,591'
                ORDER BY ref_id

            ::

                id      ref_id              ref_model       ref_name        ref_code    street_pattern_id   notes   create_uid  create_date                 write_uid   write_date
                23943   clv.patient_aux,591 clv.patient_aux Jose Volquer    213.342-34  26                  NULL    2           2023-08-22 17:35:58.996398  2           2023-08-22 17:35:58.996398

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir o registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient_aux(591,)**":

        * :bi:`SQL command`:
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,591';

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Contact Information Pattern Matches**"
--------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Contact Information Pattern Matches`:

        #. Acessar a *View* *Contact Information Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information Pattern Matches`

            * Registro Ausente:
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_aux(591,), Usuário: 2)

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient_aux(591,)**":

        * :bi:`SQL command`:
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,591'
                ORDER BY ref_id

            ::

                id         ref_id              ref_model       ref_name        ref_code    conact_information_pattern_id  notes   create_uid  create_date                 write_uid   write_date
                23923      clv.patient_aux,591 clv.patient_aux Jose Volquer    213.342-34  433                            NULL    2           2023-08-22 17:35:58.996398  2           2023-08-22 17:35:58.996398

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient_aux(591,)**":

        * :bi:`SQL command`:
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_aux' AND ref_id = 'clv.patient_aux,591';

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-22a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-22a.sql

            gzip clvhealth_jcafb_2025_15_2024-05-22a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-22a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-05-22a.sql
.. index:: clvhealth_jcafb_2025_15_2024-05-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-05-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-22a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-05-22a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-22a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Sreet Pattern Matches` referentes a registros de :bi:`Patient (Aux)`
------------------------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Sreet Pattern Matches` referentes a registros de :bi:`Patient (Aux)`:

        #. Acessar a *view* :bi:`Sreet Pattern Matches`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Sreet Pattern Matches`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar todas os :bi:`Sreet Pattern Matches` referentes a "**clv.patient_aux**" (**797**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Contact Information Pattern Matches` referentes a registros de :bi:`Patient (Aux)`
--------------------------------------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Contact Information Pattern Matches` referentes a registros de :bi:`Patient (Aux)`:

        #. Acessar a *view* :bi:`Contact Information Pattern Matches`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information Pattern Matches`

        #. Ativar o filtro **Agrupar por** » :bi:`Refers to (Model)`

        #. Selecionar todas os :bi:`Contact Information Pattern Matches` referentes a "**clv.patient_aux**" (**797**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes (Aux)**
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes (Aux)**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type` caso já não esteja ativado.

        #. Selecionar todos os :bi:`Patient (Aux)` (**821**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Verification Outcomes` referentes a registros de :bi:`Patient (Aux)`:

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Model Name`

        #. Selecionar todas os :bi:`Verification Outcomes` referentes a "**clv.patient_aux**" (**1646**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Verification Outcomes` referentes a registros com :bi:`Action` = **_patient_verification_patient_aux**: 

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Action`

        #. Selecionar todas os :bi:`Verification Outcomes` com :bi:`Action` = **_patient_verification_patient_aux** (**1646**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-22b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-22b.sql

            gzip clvhealth_jcafb_2025_15_2024-05-22b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-22b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-22b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-22b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-05-22b.sql
.. index:: clvhealth_jcafb_2025_15_2024-05-22b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-05-22b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-22b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-05-22b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-22b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-22b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

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
