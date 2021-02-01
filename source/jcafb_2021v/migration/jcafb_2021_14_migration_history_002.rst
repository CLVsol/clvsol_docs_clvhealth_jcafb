.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

===========================================
Migração do Banco de Dados - JCAFB-2021v-14
===========================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-01-31c)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-01-31c.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-01-31c.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-01-31c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-01-31c.tar.gz

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

Atualizar o *Verification Domain Filter* dos *Verification Schedules* (Current Phase)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

    #. Atualizar o *Verification Domain Filter* dos *Verification Schedules*:

        * *Verification Schedules*:

            * "Current Phase - clv.address [_address_verification_exec]"

            * "Current Phase - clv.address_aux [_address_aux_verification_exec]"

            * "Current Phase - clv.family [_family_verification_exec]"

            * "Current Phase - clv.person [_person_verification_exec]"

            * "Current Phase - clv.person_aux [_person_aux_verification_exec]"

        * Atualização:

            * De: "**[('phase_id', '=', 0)]**"

            * Para: "**[('phase_id', '=', 5)]**" (JCAFB-2021v)

Excluir o endereço "Sem endereço S/N/[morador de rua] (Centro) [140.333-80]"
----------------------------------------------------------------------------

    #. Excluir o endereço "Sem endereço S/N/[morador de rua] (Centro) [140.333-80]" dos Cadastros Auxiliar e Principal:

        * :red:`(Não Executado)` *Verification Outcomes*: pesquisar por *Reference Name* "Sem endereço" [6 registros excluídos].

        * :red:`(Não Executado)` *Address (Aux)* (*view* **Contatos**): pesquisar por *Name* "Sem endereço" [1 registro excluído].

        * *Address History*: pesquisar por *Address* "Sem endereço" [1 registro excluído].

        * *Person History*: pesquisar por *Address* "Sem endereço" [1 registro excluído].

        * *Address* (*view* **Contatos**): pesquisar por *Name* "Sem endereço" [1 registro excluído].

Preparar *Global Settings* para o banco de dados *CLVhealth-JCAFB-2021v-14*
---------------------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2021v**

        #. Configurar o parâmetro :bi:`Person` » :bi:`Reference Date`: **31/01/2021**

:red:`(Não Executado)` Atualisar a Idade de Referência e *Person Age Ranges* para todas as Pessoas
--------------------------------------------------------------------------------------------------

    #. [tclvhealth-jcafb-2021-vm-pro] Executar a Ação :bi:`Person Mass Edit` para todas as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Communities` » :bi:`Communities` » :bi:`Persons`

        #. Selecionar todas as Pessoas

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Person Reference Age Refresh*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualisar a Idade de Referência e *Person Age Ranges* para todas as Pessoas (método alternativo)
------------------------------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**Person: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Compute Age Reference**"

        #. Executar a Ação Agendada "**Person: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [clvhealth-jcafb-2021-vm-pro] Executar manualmente a "Ação Agendada" "**Person: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Definições** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Update Age Range**"

        #. Executar a Ação Agendada "**Person: Update Age Range**", clicando no botão **Rodar Manualmente**.

Marcar o *Active Log* de todos os Objetos
-----------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Executar a Ação :bi:`Global Log Client Mass Edit` para todos os Objetos:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvhealth-jcafb-2021-vm-pro <https://clvhealth-jcafb-2021-vm-pro>`_

        #. Acessar a *View* *Global Log Clients*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Global Logs` » :bi:`Global Log Clients`

        #. Selecionar todos os :bi:`Global Log Clients`

        #. Exercutar a Ação ":bi:`Global Log Client Mass Edit`":

            * Parâmetros utilizados:

                * *Active Log*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-01a)
--------------------------------------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Estabelecer uma sessão ssh com o servidor **clvhealth-jcafb-2021-vm-pro** e paralizar o *Odoo*:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            ssh clvhealth-jcafb-2021-vm-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvhealth-jcafb-2021-vm-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-01a.sql

            gzip clvhealth_jcafb_2021v_14_2021-02-01a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-01a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

        ::

            # ***** clvhealth-jcafb-2021-vm-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-01a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-01a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-02-01a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-02-01a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-02-01a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-01a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-01a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-01a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-01a.tar.gz

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
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvhealth-jcafb-2021-vm-pro**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
