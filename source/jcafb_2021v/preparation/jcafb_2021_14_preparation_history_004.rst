.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

=============================================
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-20a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-20a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-20a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20a.tar.gz

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

Habilitar a instalação e instalars o(s) módulo(s) [ver lista]
-------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_residence
        * clv_residence_community
        * clv_residence_jcafb
        * clv_residence_verification_jcafb
        * clv_residence_community_verification_jcafb
        * clv_patient
        * clv_patient_community
        * clv_patient_aux
        * clv_patient_jcafb
        * clv_patient_aux_jcafb
        * clv_patient_verification_jcafb
        * clv_patient_aux_verification_jcafb
        * clv_patient_community_verification_jcafb


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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13"
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_processing_jcafb]
-----------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Lista de Módulos:

        * clv_processing_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" - m clv_processing_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o *Verification Domain Filter* dos *Verification Schedules* (Current Phase)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

    #. Atualizar o *Verification Domain Filter* dos *Verification Schedules*:

        * *Verification Schedules*:

            * "Current Phase - clv.patient [_patient_verification_exec]"

            * "Current Phase - clv.patient_aux [_patient_aux_verification_exec]"

            * "Current Phase - clv.residence [_residence_verification_exec]"

        * Atualização:

            * De: "**[('phase_id', '=', 0)]**"

            * Para: "**[('phase_id', '=', 5)]**" (JCAFB-2021v)

Criar as Categorias de Residências para a JCAFB-2021v
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar as Categorias de Residências para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Residence` » :bi:`Categories`

        * Categorias criadas:
            
            * **Zona Rural**

                * *Name*: **Zona Rural**

            * **Zona Urbana**

                * *Name*: **Zona Urbana**

Criar os Marcadores de Residências para a JCAFB-2021v
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar os Marcadores de Residências para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Residence` » :bi:`Markers`

        * Marcadores criados:
            
            * **Selected (JCAFB-2017)**

                * *Name*: **Selected (JCAFB-2017)**

            * **Selected (JCAFB-2018)**

                * *Name*: **Selected (JCAFB-2019)**

            * **Selected (JCAFB-2019)**

                * *Name*: **Selected (JCAFB-2020)**

            * **Selected (JCAFB-2020)**

                * *Name*: **Selected (JCAFB-2018)**

Criar as Categorias de Pacientes para a JCAFB-2021v
---------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar as Categorias de Pacientes para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Categories`

        * Categorias criadas:
            
            * **Criança**

                * *Name*: **Criança**

            * **Idoso**

                * *Name*: **Idoso**

Criar os Marcadores de Pacientes para a JCAFB-2021v
---------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar os Marcadores de Pacientes para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Markers`

        * Marcadores criados:
            
            * **Campanha Anemia (JCAFB-2017)**

                * *Name*: **Campanha Anemia (JCAFB-2017)**

            * **Campanha Anemia (JCAFB-2018)**

                * *Name*: **Campanha Anemia (JCAFB-2019)**

            * **Campanha Anemia (JCAFB-2019)**

                * *Name*: **Campanha Anemia (JCAFB-2020)**

            * **Campanha Anemia (JCAFB-2020)**

                * *Name*: **Campanha Anemia (JCAFB-2018)**

            * **Campanha DHC (JCAFB-2017)**

                * *Name*: **Campanha DHC (JCAFB-2017)**

            * **Campanha DHC (JCAFB-2018)**

                * *Name*: **Campanha DHC (JCAFB-2019)**

            * **Campanha DHC (JCAFB-2019)**

                * *Name*: **Campanha DHC (JCAFB-2020)**

            * **Campanha DHC (JCAFB-2020)**

                * *Name*: **Campanha DHC (JCAFB-2018)**

            * **Não Participante (JCAFB)**

                * *Name*: **Não Participante (JCAFB)**

            * **Selected (JCAFB-2017)**

                * *Name*: **Selected (JCAFB-2017)**

            * **Selected (JCAFB-2018)**

                * *Name*: **Selected (JCAFB-2019)**

            * **Selected (JCAFB-2019)**

                * *Name*: **Selected (JCAFB-2020)**

            * **Selected (JCAFB-2020)**

                * *Name*: **Selected (JCAFB-2018)**

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

        #. Exercutar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-20b)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-20b.sql

            gzip clvhealth_jcafb_2021v_14_2021-03-20b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-20b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-20b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-20b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-03-20b.sql
.. index:: clvhealth_jcafb_2021v_14_2021-03-20b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-03-20b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-20b)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-20b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-20b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20b.tar.gz

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

Marcar os Endereços das Pessoas que participaram do Projeto da JCAFB (2017 - 2020)
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Selected**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Residence`

        #. Selecionar todos os Endereços com: :bi:`Is Residence` = ":bi:`false`"

        #. Exercutar a Ação ":bi:`Address Mass Edit`":

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

                * :bi:`Community` » :bi:`Community` » :bi:` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todos os Endereços com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Residence" register.`"

        #. Exercutar a Ação "**Address Associate to Patient**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Address Verification Execute*: **marcado**

                * *Residence Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Residence" register.`"

        #. Exercutar a Ação ":bi:`Address Verification Execute`":

            #. Utilize o botão :bi:`Address Verification Execute` para executar a Ação.

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

        #. Exercutar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Residence Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação** » **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Marcar as Pessoas que foram Pacientes da JCAFB-2021v
----------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Selected**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Patient`

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Campanha Anemia**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Patient`

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Campanha DHC**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Patient`

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Marker Names` » **contém** » **Não Participante**

        #. Ativar o filtro **Agrupar por** » :bi:`Is Patient`

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Associar as Pessoas a um Paciente
---------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Person Associate to Patient* para as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * *Community* > *Community* > *Persons*

        #. Ativar o filtro **Agrupar por** » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pessoas com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Patient" register.`"

        #. Exercutar a Ação "**Person Associate to Patient**":

            * Parâmetros utilizados:

                * *Create new Patient*: **marcado**

                * *Person Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Patient* para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Patient" register.`"

        #. Exercutar a Ação ":bi:`Person Verification Execute`":

            #. Utilize o botão :bi:`Person Verification Execute` para executar a Ação.

Atualizar o *Register State* de todos os Pacientes
--------------------------------------------------

    Critérios utilizados:

        * **Done**: todos os Pacientes.

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patients`

        #. Selecionar todos os Pacientes

        #. Exercutar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Patient Verification Execute*: **marcado**

                * *Phase*: **nenhuma ação** » **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Associar todos os Pacientes a um Paciente (Aux)
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Associate to Patient (Aux)` para todos os Pacientes:

        #. Acessar a *view* :bi:`Patients`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Register State`

        #. Selecionar todos os Pacientes com :bi:`Register State` != ":bi:`Canceled`"

        #. Exercutar a Ação :bi:`Patient Associate to Patient (Aux)`:

            * Parâmetros utilizados:

                * *Create new Patient (Aux)*: **marcado**

                * *Patient Verification Execute*: **marcado**

                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Associate to Patient (Aux)` para executar a Ação.

Remover a Fase de todos os Pacientes (Aux)
------------------------------------------

    #. Executar a Ação :bi:`Patient (Aux) Mass Edit` para todos os Pacientes (Aux):

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux)

        #. Exercutar a Ação :bi:`Patient (Aux) Mass Edit`:

            * Parâmetros utilizados:

                * *Register State*: :bi:`Set` » :bi:`Verified`
                * *State*: **nenhuma ação**
                * *Person (Aux) Verification Execute*: **marcado**
                * *Phase*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-20c)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-20c.sql

            gzip clvhealth_jcafb_2021v_14_2021-03-20c.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-03-20c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-20c.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-03-20c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-03-20c.sql
.. index:: clvhealth_jcafb_2021v_14_2021-03-20c.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-03-20c
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20c

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-03-20c)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-03-20c.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-03-20c.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-03-20c.tar.gz

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

.. toctree::   :maxdepth: 2
