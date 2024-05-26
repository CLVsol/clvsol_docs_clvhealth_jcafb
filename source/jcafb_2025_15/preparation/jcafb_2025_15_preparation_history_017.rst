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
JCAFB-2025-15 (Preparação pré Jornada [8])
==========================================

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

[tkl-odoo15-jcafb25-vm] Excluir todos os **Summaries**
------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os arquivos presentes no diretório "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/summary_files**" do Servidor.

    #. [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os :bi:`File System Files` do :bi:`File System Directory` "**Summary Files**":

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Files`

        #. Ativar o filtro **Agrupar por** » :bi:`Directory`

        #. Selecionar todas os :bi:`File System Files` referentes a "**Summary Files**" (**335**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para todos os :bi:`Patients`:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * **Health** » :bi:`Health` » :bi:`Patients`

        #. Selecionar todos os :bi:`Patients` (**819**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Summary*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Employee Mass Edit` para todos os :bi:`Funcionários`:

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Funcionários` » :bi:`Funcionários`

        #. Selecionar todos os :bi:`Funcionários` (**349**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Summary*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Summaries**:

        #. Acessar a *view* **Summaries**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Summaries`

        #. Selecionar todos os :bi:`Summaries` (**355**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-24a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-24a.sql

            gzip clvhealth_jcafb_2025_15_2024-05-24a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-24a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-24a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-24a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-05-24a.sql
.. index:: clvhealth_jcafb_2025_15_2024-05-24a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-05-24a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-24a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-24a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-05-24a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-24a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-24a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Atualizar o *Register State* de todas as **Residências**
--------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *view* **Residences**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as :bi:`Residences` (**332**)

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Sreet Pattern Matches**"
------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Sreet Pattern Matches` para "**clv.patient_rec**":

        #. Acessar a *View* *Sreet Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Sreet Pattern Matches`

            * Registro Ausente (1):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_rec(309,), Usuário: 2)

            * Registro Ausente (2):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_rec(751,), Usuário: 2)

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient_rec**":

        * :bi:`SQL command` (1):
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,309'
                ORDER BY ref_id

                clv.patient_rec,309 clv.patient_rec Jose Volquer    213.342-34

        * :bi:`SQL command` (2):
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,751'
                ORDER BY ref_id

                clv.patient_rec,751 clv.patient_rec Erick Bonrruque Rodrigues   213.539-64

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir o registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient_rec**":

        * :bi:`SQL command` (1):
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,309';

        * :bi:`SQL command` (2):
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,751';

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Sreet Pattern Matches` para "**clv.patient**":

        #. Acessar a *View* *Sreet Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Sreet Pattern Matches`

            * Registro Ausente (1):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(589,), Usuário: 2)

            * Registro Ausente (2):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(778,), Usuário: 2)

            * Registro Ausente (3):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(782,), Usuário: 2)

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar os registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient**":

        * :bi:`SQL command` (1):
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,589'
                ORDER BY ref_id

                clv.patient,589 clv.patient Jose Volquer    213.342-34

        * :bi:`SQL command` (2):
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,778'
                ORDER BY ref_id

                clv.patient,778 clv.patient Flavio Augusto Fitz de Almeida  213.535-30

        * :bi:`SQL command` (3):
            ::

                SELECT *
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,782'
                ORDER BY ref_id

                clv.patient,782 clv.patient Erick Bonrruque Rodrigues   213.539-64

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir os registro de "**clv_partner_entity_street_pattern_match**" apontando para "**clv.patient**":

        * :bi:`SQL command` (1):
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,589';

        * :bi:`SQL command` (2):
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,778';

        * :bi:`SQL command` (3):
            ::

                DELETE
                FROM "clv_partner_entity_street_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,782';

[tkl-odoo15-jcafb25-vm] Restaurar a integridade de "**Contact Information Pattern Matches**"
--------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_.

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo15-jcafb25-vm:12322 <https://tkl-odoo15-jcafb25-vm:12322>`_.

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Contact Information Pattern Matches` para "**clv.patient**":

        #. Acessar a *View* *Contact Information Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information Pattern Matches`

            * Registro Ausente (1):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(589,), Usuário: 2)

            * Registro Ausente (2):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(778,), Usuário: 2)

            * Registro Ausente (3):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_rec(309,), Usuário: 2)

            * Registro Ausente (4):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient(782,), Usuário: 2)

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient**":

        * :bi:`SQL command` (1):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,589'
                ORDER BY ref_id

                clv.patient,589 clv.patient Jose Volquer    213.342-34

        * :bi:`SQL command` (2):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,778'
                ORDER BY ref_id

                clv.patient,778 clv.patient Flavio Augusto Fitz de Almeida  213.535-30

        * :bi:`SQL command` (3):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,309'
                ORDER BY ref_id

                clv.patient,309 clv.patient Lorena Vitoria Jeremias Camargo 212.309-60

        * :bi:`SQL command` (4):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,782'
                ORDER BY ref_id

                clv.patient,782 clv.patient Erick Bonrruque Rodrigues   213.539-64

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient**":

        * :bi:`SQL command` (1):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,589';

        * :bi:`SQL command` (2):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,778';

        * :bi:`SQL command` (3):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,309';

        * :bi:`SQL command` (4):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient' AND ref_id = 'clv.patient,782';

    #. [tkl-odoo15-jcafb25-vm] Verificar a integridade de :bi:`Contact Information Pattern Matches` para "**clv.patient_rec**":

        #. Acessar a *View* *Contact Information Pattern Matches*:

            * Menu de acesso:
                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information Pattern Matches`

            * Registro Ausente (1):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_rec(309,), Usuário: 2)

            * Registro Ausente (2):
                ::

                    Registro não existe ou foi apagado.
                    (Registro: clv.patient_rec(751,), Usuário: 2)

    #. [tkl-odoo15-jcafb25-vm:12322] Selecionar o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient_rec**":

        * :bi:`SQL command` (1):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,309'
                ORDER BY ref_id

                clv.patient_rec,309 clv.patient_rec Jose Volquer    213.342-34

        * :bi:`SQL command` (2):
            ::

                SELECT *
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,751'
                ORDER BY ref_id

                clv.patient_rec,751 clv.patient_rec Erick Bonrruque Rodrigues   213.539-64

    #. [tkl-odoo15-jcafb25-vm:12322] Excluir o registro de "**clv_partner_entity_contact_information_pattern_match**" apontando para "**clv.patient_rec**":

        * :bi:`SQL command` (1):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,309';

        * :bi:`SQL command` (2):
            ::

                DELETE
                FROM "clv_partner_entity_contact_information_pattern_match"
                WHERE ref_model = 'clv.patient_rec' AND ref_id = 'clv.patient_rec,751';

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-25a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-25a.sql

            gzip clvhealth_jcafb_2025_15_2024-05-25a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-25a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-25a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-25a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-05-25a.sql
.. index:: clvhealth_jcafb_2025_15_2024-05-25a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-05-25a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-25a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-25a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-05-25a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-05-25a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-25a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Excluir os :bi:`Contact Information Patterns` sem :bi:`Matches`
---------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir os :bi:`Contact Information Patterns` sem :bi:`Matches`:

        #. Acessar a *view* :bi:`Contact Information Patterns`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information`

        #. Selecionar os :bi:`Contact Information Patterns` com :bi:`Number of Matches` = **0** (**13**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir os :bi:`Street Patterns` sem :bi:`Matches`
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir os :bi:`Street Patterns` sem :bi:`Matches`:

        #. Acessar a *view* :bi:`Street Patterns`:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Street`

        #. Selecionar os :bi:`Street Patterns` com :bi:`Number of Matches` = **0** (**1**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *Residence State* de todas as **Residências**
---------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *view* **Residences**:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

    #. Selecionar todas as :bi:`Residences` (**332**)

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Residence State*: **Set** » **Unknown**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-26a.sql

            gzip clvhealth_jcafb_2025_15_2024-05-26a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-05-26a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-26a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-05-26a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-05-26a.sql
.. index:: clvhealth_jcafb_2025_15_2024-05-26a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-05-26a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-05-26a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-26a)
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
