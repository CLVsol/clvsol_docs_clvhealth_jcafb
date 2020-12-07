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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-06a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-06a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-06a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-06a.tar.gz

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

Atualisar a *Person Age Ranges* para todas as Pessoas (método alternativo)
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar manualmente a "Ação Agendada" "**Person: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Person: Update Age Range**"

        #. Executar a Ação Agendada "**Person: Update Age Range**", clicando no botão **Rodar Manualmente**.

Atualizar o *Person Category* de todas as Pessoas
-------------------------------------------------

    Critérios utilizados:

        * **Criança**: todas as Pessoas na faixa etária "3-10 anos".

        * **Idoso**: todas as Pessoas na faixa etária "60+ anos".

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para todas as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Age Ranges` » :bi:`Categories`

          #. Ativar o filtro **Agrupar por** » :bi:`Age Ranges` » :bi:`Categories`

          #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**0-2 anos**" » :bi:`Category` = "**Criança**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Remove** » **Criança**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**3-10 anos**" » :bi:`Category` = "**indefinido**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Set** » **Criança**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**11-17 anos**" » :bi:`Category` = "**Gestante**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Remove** » **Gestante**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**18-59 anos**" » :bi:`Category` = "**Gestante**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Remove** » **Gestante**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**18-59 anos**" » :bi:`Category` = "**Idoso**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Remove** » **Idoso**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**160+ anos**" » :bi:`Category` = "**indefinido**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Set** » **Idoso**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            #. Selecionar todas as Pessoas com: :bi:`Age Range` = "**indefinido**" » :bi:`Category` = "**Idoso**"

            #. Exercutar a Ação ":bi:`Person Mass Edit`":

                * Parâmetros utilizados:

                    * *Categories*: **Remove** » **Idoso**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar as Crianças para o Projeto JCAFB-2021v
-------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Available`

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Person State*: **Set** » **Selected**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Selecionar os Idosos para o Projeto JCAFB-2021v
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit` para os Idosos selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Available`

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Person State*: **Set** » **Selected**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::   :maxdepth: 2
