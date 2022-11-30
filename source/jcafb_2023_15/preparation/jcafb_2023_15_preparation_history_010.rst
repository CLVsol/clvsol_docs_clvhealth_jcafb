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
JCAFB-2023-15 (Preparação pré Jornada [1])
==========================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21a)
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
            # gzip -d clvhealth_jcafb_2023_15_2022-11-21a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-21a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21a.tar.gz

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
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

Atualizar/Remover a Fase dos Funcionários
-----------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. [tkl-odoo15-jcafb23-vm] Atualizar manualmente a *Phase* dos Funcionários associados à **JCAB-2023**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Atualizar manualmente a *Phase* dos Funcionários associados à **JCAB-2023**.

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Employee Mass Edit` os Funcionários que **não** estejam associados à **JCAB-2023**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar os Funcionários associados à **JCAFB-2021v** (**23**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Phase*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Employee History* de todos os Funcionários
-------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Employee History Update` para todos os Funcionários:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar todos os Funcionários (**299**)

        #. Executar a Ação ":bi:`Employee History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **01/11/2022**
                * *Sign in date*: **01/11/2022**

            #. Utilize o botão :bi:`Employee History Update` para executar a Ação.

Redefinir a **Senha** de todos os Funcionários da **JCAFB-2023**
-----------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Employee Mass Edit` para todas os Funcionários da **JCAFB-2023**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários`

        #. Selecionar todos os Funcionários da **JCAFB-2023** (**47**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:

                * *Reset User Password*: :bi:`marcado`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Redefinir a senha do usuário de referência da JCAFB-2023
--------------------------------------------------------

    #. Redefinir a senha do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Configurações` » :bi:`Usuários e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Executar a Ação "**Alterar Senha**":

            * Parâmetros:
                * Nova Senha: *******
            
            #. Utilize o botão "**Alterar Senha**" para executar a ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21b)
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
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21b.sql

            gzip clvhealth_jcafb_2023_15_2022-11-21b.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21b.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-11-21b.sql
.. index:: clvhealth_jcafb_2023_15_2022-11-21b.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-11-21b
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21b)
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
            # gzip -d clvhealth_jcafb_2023_15_2022-11-21b.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-21b.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21b.tar.gz

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

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_partner_entity
        * clv_residence
        * clv_patient
        * clv_patient_aux

        * clv_l10n_br_base
        * clv_l10n_br_zip

        * clv_partner_entity_l10n_br
        * clv_residence_l10n_br
        * clv_patient_l10n_br
        * clv_patient_aux_l10n_br

        * clv_global_log

        * clv_partner_entity_log_jcafb
        * clv_residence_log_jcafb
        * clv_patient_log_jcafb
        * clv_patient_aux_log_jcafb

        * clv_verification

        * clv_verification_jcafb
        * clv_verification_log_jcafb
        * clv_partner_entity_verification_jcafb
        * clv_residence_verification_jcafb
        * clv_patient_verification_jcafb
        * clv_patient_aux_verification_jcafb

        * clv_processing

        * clv_processing_jcafb

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

Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2023-15*
----------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2023**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2023**

Criar as Faixas de Idades de Pacientes para a JCAFB-2023
--------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar as Faixas de Idades de Pacientes para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Age Ranges`

        * Faixas de Idades criadas:
            
            * **0-1 anos**

                * *Name*: **0-1 anos**

                * *From*: **0**

                * *To*: **1**

            * **2-9 anos**

                * *Name*: **2-9 anoss**

                * *From*: **2**

                * *To*: **9**

            * **10-17 anos**

                * *Name*: **10-17 anos**

                * *From*: **10**

                * *To*: **17**

            * **18-59 anos**

                * *Name*: **18-59 anos**

                * *From*: **18**

                * *To*: **59**

            * **60+ anos**

                * *Name*: **60+ anos**

                * *From*: **60**

                * *To*: **120**

Atualizar o *Verification Domain Filter* dos *Verification Schedules* (Current Phase)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Atualizar o *Verification Domain Filter* dos *Verification Schedules*:

        * *Verification Schedules*:

            .. * "Current Phase - clv.address [_address_verification_exec]"

            .. * "Current Phase - clv.address_aux [_address_aux_verification_exec]"

            .. * "Current Phase - clv.family [_family_verification_exec]"

            * "Current Phase - clv.patient [_patient_verification_exec]"

            * "Current Phase - clv.patient_aux [_patient_aux_verification_exec]"

            .. * "Current Phase - clv.person [_person_verification_exec]"

            .. * "Current Phase - clv.person_aux [_person_aux_verification_exec]"

            * "Current Phase - clv.residence [_residence_verification_exec]"

        * Atualização:

            * De: "**[('phase_id', '=', 0)]**"

            * Para: "**[('phase_id', '=', 7)]**" (JCAFB-2023)

Configurar as permissões do usuário de referência da JCAFB-2023
---------------------------------------------------------------

    #. Configurar as permissões do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Configurações` » :bi:`Usuários e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Configurar as permissões:

            * User Type

                * Tipos de usuário: **Utilizador Interno**

            * Marketing

                * Inquéritos: **Administrador**

            * *Human Resources*
            
                * Funcionários: **Administrador**

            * *Administration*
            
                * Administração:

            * *Other*:

                * *Employee*: :bi:`Manager (Employee)`
                * *External Sync*:
                * *File System*: :bi:`Manager (File System)`
                * *Global Tag*: :bi:`Manager (Global Tag)`
                * *Patient (Aux)*: :bi:`Manager (Patient (Aux))`
                * *Patient*: :bi:`Manager (Patient)`
                * *Phase*: :bi:`User (Phase)`
                * *Processing*:
                * *Residence*: :bi:`Manager (Residence)`
                * *Set*: :bi:`Manager (Set)`
                * *Survey*:  :bi:`Manager (Survey)`
                * *Verification*: :bi:`Manager (Verification)`

            * *Base*:

                * :bi:`Log User (Base)`,
                * :bi:`Manager (Base)` ​
                * :bi:`Register User (Base)`,
                * :bi:`Super User (Base)`,
                * :bi:`User (Base)`,

            * *Technical*:

                * **Acesso a endereços privados**
                * **Acesso para exportar recurso**
                * **Mail Template Editor**

            * *Extra Rights*:

                * **Criação de Contato**

Atualizar as permissões dos Coordenadores da JCAFB-2023
-------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação *Employee User Groups Update* para os Coordenadores da JCAFB-2023:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Funcionários**:

            * Menu de acesso:

                * **Funcionários** » **Funcionários** » **Funcionários**

        #. Selecionar os **Coordenadores** da JCAFB-2023

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21c)
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
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21c.sql

            gzip clvhealth_jcafb_2023_15_2022-11-21c.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-21c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21c.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-21c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-11-21c.sql
.. index:: clvhealth_jcafb_2023_15_2022-11-21c.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-11-21c
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21c

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-21c)
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
            # gzip -d clvhealth_jcafb_2023_15_2022-11-21c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-21c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-21c.tar.gz

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

Criar a Pesquisa "[EAN23]"
--------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EAN21]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EAN21]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EAN23]**
                * *New Survey Code*: **EAN23**
                * *New Survey Description*: **<p>JCAFB 2023 - Exames para detecção de Anemia</p>**
                * *Phase*: **JCAFB-2023**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

Criar a Pesquisa "[EDH23]"
--------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EDH21]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EDH21]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EDH23]**
                * *New Survey Code*: **EDH23**
                * *New Survey Description*: **<p>JCAFB 2023- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *Phase*: **JCAFB-2023**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

Criar a Pesquisa "[ECP23]"
--------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[ECP21]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[ECP21]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[ECP23]**
                * *New Survey Code*: **ECP23**
                * *New Survey Description*: **<p>JCAFB 2023 - Laboratório - Parasitologia</p>**
                * *Phase*: **JCAFB-2023**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

Criar a Pesquisa "[EUR23]"
--------------------------

    #. [tkl-odoo15-jcafb23-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EUR21]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EUR21]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EUR23]**
                * *New Survey Code*: **EUR23**
                * *New Survey Description*: **<p>JCAFB 2023 - Laboratório - Urinálise</p>**
                * *Phase*: **JCAFB-2023**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-29a)
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
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-29a.sql

            gzip clvhealth_jcafb_2023_15_2022-11-29a.sql
            pg_dump clvhealth_jcafb_2023_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2023_15_2022-11-29a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz clvhealth_jcafb_2023_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-29a.sql
        * /opt/odoo/clvhealth_jcafb_2023_15_2022-11-29a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz

.. index:: clvhealth_jcafb_2023_15_2022-11-29a.sql
.. index:: clvhealth_jcafb_2023_15_2022-11-29a.sql.gz
.. index:: filestore_clvhealth_jcafb_2023_15_2022-11-29a
.. index:: clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-29a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-11-29a)
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
            # gzip -d clvhealth_jcafb_2023_15_2022-11-29a.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-11-29a.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-11-29a.tar.gz

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
