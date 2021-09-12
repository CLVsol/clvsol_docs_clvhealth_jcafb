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

===============================================
JCAFB-2021v-14n (Recadastramento de Campanha 1)
===============================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-10a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-10a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-10a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

:borange:`(**)` Criar os Eventos para o Projeto JCAFB-2021v
-----------------------------------------------------------

    #. **Conectar-se**, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Acessar a *View* *Events*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Events`

    #. [tkl-odoo14-jcafb21n-vm] Lista de novos Eventos:

        #. **Campanha Anemia (1) - 2021v**:

            * **Event Name**: "Campanha Anemia (1) - 2021v"
            * **Phase**: "JCAFB-2021v"
            * **State**: "Confirmed"

        #. **Campanha DHC (1) - 2021v**:

            * **Event Name**: "Campanha DHC (1) - 2021v"
            * **Phase**: "JCAFB-2021v"
            * **State**: "Confirmed"

:borange:`(**)` Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_patient_aux_summary_jcafb

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14" -m clv_patient_aux_summary_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

[Camanha] Recadastrar um Paciente do Projeto JCAFB-2021v (Sem alterações de Cadastro)
-------------------------------------------------------------------------------------

    * Referência :doc:`/user_guide/reregistration/reregistration_workflow`"

    #. **Conectar-se**, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. **Identificar o Paciente a ser recadastrado durante uma Campanha:**

        #. Utilizar a *View* *Patients (Aux)*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. **Executar o Recadastramento** (Sem alterações de Cadastro) **do Paciente**, considerando as informações apresentadas para o mesmo.

        #. Usar como referência: :doc:`/user_guide/reregistration/reregistration_workflow_020_010_010`", considerando:

            * O :bi:`Register State` do Paciente (Aux) **será alterado (ou mantido)** para :bi:`Revised`.

            * O :bi:`Patient (Aux) State` do Paciente (Aux) **será mantido** como :bi:`Selected`.

            * :bmaroon:`NÃO executar, durante a Campanha, a Consolidação do Cadastro Principal do Paciente.`

    #. **Associar o Paciente ao Evento de Campanha**


        #. Executar a Ação :bi:`Event Set Up [Patient (Aux)]`:

            #. Acessar a *View* *Patients (Aux)*:

                * Menu de acesso:

                    * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

            #. Selecionar o Paciente (Aux).

            #. Executar a Ação ":bi:`Event Set Up [Patient (Aux)]`":

                * Parâmetros utilizados:

                    * *Document Types* (Campanha de Anemia):

                        #. **Campanha Anemia (1) - 2021v**

                    * *Document Types* (Campanha de DHC):

                        #. **Campanha DHC (1) - 2021v**

                    * *Phase*: **JCAFB-2021v**

                #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

    #. **Criar os Documentos de Campanha para o Paciente**


        #. Executar a Ação :bi:`Document Set Up [Patient (Aux)]`:

            #. Acessar a *View* *Patients (Aux)*:

                * Menu de acesso:

                    * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

            #. Selecionar o Paciente (Aux).

            #. Executar a Ação ":bi:`Document Set Up [Patient (Aux)]`":

                * Parâmetros utilizados:

                    * *Document Types* (Campanha de Anemia):

                        #. **QAN21**

                        #. **TAN21**

                    * *Document Types* (Campanha de DHC):

                        #. **QDH21**

                        #. **TDH21**

                    * *Phase*: **JCAFB-2021v**

                #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

    #. **Criar a Requisição de Exames de Campanha para o Paciente**

        #. Executar a Ação :bi:`Lab Test Request Set Up [Patient (Aux)]` para o Paciente:

            #. Acessar a *View* *Patients (Aux)*:

                * Menu de acesso:

                    * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

            #. Selecionar o Paciente (Aux).

            #. Executar a Ação ":bi:`Lab Test Request Set Up [Patient (Aux)]`":

                * Parâmetros utilizados:

                    * *Lab Test Types* (Campanha de Anemia):

                        #. **EAN21**

                    * *Lab Test Types* (Campanha de DHC):

                        #. **EDH21**

                    * *Phase*: **JCAFB-2021v**

                #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

    #. **Executar a Recepção da Requisição de Exames de Campanha do Paciente**

        #. Executar a Ação :bi:`Lab Test Request Receive` para o :bi:`Lab Test Request` dos Exames de Campanha:

            #. Acessar a *View* *Lab Test Requests*:

                * Menu de acesso:

                    * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

            #. Selecionar o :bi:`Lab Test Request` dos Exames de Campanha.

            #. Executar a Ação ":bi:`Lab Test Request Receive`" para a Requisição:

                * Parâmetros utilizados:

                    * Aceitar todos os parâmetros apresentados

                #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

    #. **Criar/Reprocessar o Sumário para o Paciente (Aux).**

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-11a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-11a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-09-11a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-11a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-09-11a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-09-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-09-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-11a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-11a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-11a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-11a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Atualizar o *Register State* dos Pacientes já recadastrados
-----------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* das Residências já recadastrados
-------------------------------------------------------------

    #. Executar a Ação ":bi:`Residence Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Residence Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Register State* dos Pacientes (Aux) já recadastrados
-----------------------------------------------------------------

    #. Executar a Ação ":bi:`Patient Mass Edit`":

        * Parâmetros utilizados:

            * *Register State*: **Set** » **Done**

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::   :maxdepth: 2
