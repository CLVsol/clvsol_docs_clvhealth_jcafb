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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-04-27b)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-04-27b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-04-27b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-04-27b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-27b.tar.gz

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

Criar os Documentos para as Crianças selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSC21**

                    #. **QSF21**

                    #. **TCR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para os Idosos selecionados para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QMD21**

                    #. **QSF21**

                    #. **QSI21**

                    #. **TID21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar as Requisições de Exames para as Crianças selecionadas para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Test Request Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EEV21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Criar as Requisições de Exames para os Idosos selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Test Request Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EUR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Executar o *Verification Batch* “Current Phase - Default Batch”
---------------------------------------------------------------

    #. Executar o *Verification Batch* “Current Phase - Default Batch”:

        #. Acessar a *view* :bi:`Verification Batches`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification` » :bi:`Batches`

        #. Selecionar o :bi:`Verification Batch` ":bi:`Current Phase - Default Batch`"

        #. Executar a Ação :bi:`Verification Batch Exec`:

            #. Utilize o botão :bi:`Verification Batch Exec` para executar a Ação.

            * :bi:`Execution time: 0:00:19.032`

Criar os Sumários para os Grupos de Campo do Projeto JCAFB-2021v
----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Employee Summary Set Up` para os Grupos de Campo do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar todos os Funcionários com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

Criar os Sumários para as Residências selecionados para o Projeto JCAFB-2021v
-----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Residence Summary Set Up` para as Residências selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Residence State`

        #. Selecionar todos as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Residence State` = ":bi:`Selected`"

        #. Executar a Ação ":bi:`Residence Summary Set Up`":

            #. Utilize o botão :bi:`Residence Summary Set Up` para executar a Ação.

Criar os Sumários para os Pacientes selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State`

        #. Selecionar todos as Pacientes com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Patient State` = ":bi:`Selected`"

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-04-28a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-04-28a.sql

            gzip clvhealth_jcafb_2021v_14_2021-04-28a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-04-28a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-04-28a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-04-28a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-04-28a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-04-28a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-04-28a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-28a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-04-28a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-04-28a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-04-28a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz

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
