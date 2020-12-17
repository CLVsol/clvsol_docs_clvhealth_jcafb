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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-13a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-13a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-13a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz

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

:red:`Excluir os registros "File Sistem Directories" duplicados`
----------------------------------------------------------------

    :red:`Verificar porque está ocorrendo essa duplicidade!`

     #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *File System Directories*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Directories`

    #. Excluir os :bi:`File System Directories` duplicados:

        * **Lab Test Report Files (Templates)**: "/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/reports/templates"

        * **Lab Test Report Files (XLS)**: "/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/reports/xls"

        * **Lab Test Result Files (Templates)**: "/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/results/templates"

        * **Lab Test Result Files (XLS)**: "/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/results/xls"

        * **Summary Files**: "/opt/odoo/clvsol_filestore/clvhealth_jcafb/summary_files"

Criar os Sumários para os Grupos de Campo do Projeto JCAFB-2021v
----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Employee Summary Set Up` para os Grupos de Campo do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar todos os Funcionários com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"

        #. Exercutar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

Criar os Sumários para os Endereços selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Address Summary Set Up` para os Endereços selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Addresses*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Addresses`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Address State`

        #. Selecionar todos os Endereços com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Address State` = ":bi:`Selected`"

        #. Exercutar a Ação ":bi:`Address Summary Set Up`":

            #. Utilize o botão :bi:`Address Summary Set Up` para executar a Ação.

Criar os Sumários para as Famílias selecionadas para o Projeto JCAFB-2021v
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Family Summary Set Up` para as Famílias selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Family State`

        #. Selecionar todos as Famílias com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Family State` = ":bi:`Selected`"

        #. Exercutar a Ação ":bi:`Family Summary Set Up`":

            #. Utilize o botão :bi:`Family Summary Set Up` para executar a Ação.

Criar os Sumários para as Pessoas selecionadas para o Projeto JCAFB-2021v
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Summary Set Up` para as Pessoas selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person State`

        #. Selecionar todos as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`"

        #. Exercutar a Ação ":bi:`Person Summary Set Up`":

            #. Utilize o botão :bi:`Person Summary Set Up` para executar a Ação.

.. toctree::   :maxdepth: 2
