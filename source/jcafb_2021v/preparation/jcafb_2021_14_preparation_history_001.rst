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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-01b)
------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-01b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-01b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvhealth-jcafb-2021-vm-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

:red:`(Não Executado)` Executar a "Preparação do Cadastro Auxiliar" (Fase 1)
----------------------------------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`"

    #. Excluir todos os registros de Pessoas do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_010`".

    #. Excluir todos os registros de Endereços do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_020`".

Executar a "Preparação do Cadastro Auxiliar" (Fase 2)
-----------------------------------------------------

    * Referência :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`"

    #. Associar todas as Pessoas a uma Pessoa (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_030`".

    #. Associar todos os Endereços a um Endereço (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_040`".

    #. Remover a Fase de todas as Pessoas (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_050`".

    #. Remover a Fase de todos os Endereços (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_060`".

Adicionar novos *Street Patterns*
---------------------------------

    #. Adicionar os novos *Street Patterns* listados a seguir, utilizando o procedimento :doc:`/procedures/reregistration/reregistration_procedure_030_010_025`:

        * *Address (Aux)* "Estância Nossa Senhora Aparecida (Porto)" [140.498-99].

        * *Address (Aux)* "Fazenda Luvre, casa 2 (Porto)" [140.324-90].

:red:`(Não Executado)` Executar o *Verification Batch* “Default Batch”
----------------------------------------------------------------------

    #. Executar o *Verification Batch* “Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:29:26.517`

Executar o *Verification Batch* “Default Batch” (método alternativo)
--------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**Verification Batch: Execute [Default Batch]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Verification Batch: Execute [Default Batch]**"

        #. Executar a Ação Agendada "**Verification Batch: Execute [Default Batch]**", clicando no botão **Rodar Manualmente**.

            * :bi:`Execution time: 0:29:29.802`

Redefinir a **Senha** de todos os Funcionários da **JCAFB-2021v**
-----------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar a Ação :bi:`Employee Mass Edit` para todas os Funcionários da **JCAFB-2021v**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários`

        #. Selecionar todos os Funcionários da **JCAFB-2021v**

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:

                * *Reset User Password*: :bi:`marcado`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Redefinir a senha do usuário de referência da JCAFB-2021v
---------------------------------------------------------

    #. Redefinir a senha do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Definições` » :bi:`Utilizadores e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Executar a Ação "**Alterar Senha**":

            * Parâmetros:
                * Nova Senha: *******
            
            #. Utilize o botão "**Alterar Senha**" para executar a ação.

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

            * Outro

                * *Address (Aux)*: :bi:`Manager (Address (Aux))`
                * *Address*: :bi:`Manager (Address)`
                * *Community*: :bi:`Manager (Community)`
                * *Employee*: :bi:`Manager (Employee)`
                * *Event*: :bi:`Manager (Event)`
                * *External Sync*:
                * *Family*: :bi:`Manager (Family)`
                * *Family*: :bi:`Manager (Family)`
                * *File System*: :bi:`Manager (File System)`
                * *Global Tag*: :bi:`Manager (Global Tag)`
                * *Person (Aux)*: :bi:`Manager (Person (Aux))`
                * *Person*: :bi:`Manager (Person)`
                * *Phase*: :bi:`User (Phase)`
                * *Processing*:
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

Atualizar o(s) módulo(s) [clv_employee]
---------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Lista de Módulos:

        * clv_employee

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" - m clv_employee
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar as permissões de todos os Usuários da JCAFB-2021v
-----------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar a Ação *Employee User Groups Update* para os *Employees* da JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * *Funcionários* » *Employees* » *Employees*

        #. Selecionar os *Employees* da JCAFB-2021v

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

.. toctree::   :maxdepth: 2
