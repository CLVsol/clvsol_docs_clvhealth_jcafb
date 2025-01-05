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

================================================
Manutenção do Banco de Dados - JCAFB-2025-15 [3]
================================================

[clvheatlh-jcafb-2025n-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-15a)
-------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-15a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-15a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025n-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Atualizar as Senhas dos Jornadeiros não Coordenadores
-------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar a Ação :bi:`Employee Mass Edit` para os Jornadeiros não Coordenadores:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Campálises***".

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Análises***".

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Campo***".

        #. Executar a Ação ":bi:`Employee Mass Edit`" (**39**):

            * Parâmetros utilizados:
                * *Reset User Password*: "**marcado**"

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[clvheatlh-jcafb-2025n-aws-pro] Exportar as credenciais de logiln dos Jornadeiros não Coordenadores
---------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Exportar as credenciais de logiln dos Jornadeiros não Coordenadores:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Campálises***".

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Análises***".

        #. Selecionar as Funcionários com: :bi:`Phase` = "**JCAFB-2025**" » ***Trabalho*** = "***Jornadeiros de Campo***".

        #. Executar a Ação ":bi:`Exportar`" (**39**):

            * Parâmetros utilizados:
                * *Campos para exportar*: » **Modelo**: "**JCAFB-2025 - Login Jornadeiros**"

            #. Utilize o botão :bi:`Exportar` para executar a Ação.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-05a)
---------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025n-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025n-aws-pro] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-05a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-05a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-05a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025n-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025n-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-05a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-05a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-05a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-05a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-05a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-05a

.. toctree::   :maxdepth: 2
