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

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-05a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-05a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-05a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-05a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Exportar as URLs (links) para acesso às Surveys
-------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Exportar as URLs (links) para acesso às Surveys:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Pesquisas** » :**Pesquisas**

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar as Pesquisas com: :bi:`Phase` = "**JCAFB-2025**"

        #. Executar a Ação ":bi:`Exportar`" (**11**):

            * Parâmetros utilizados:
                * *Campos para exportar*: » **Modelo**: "**JCAFB-2025 - Survey Public links**"

            #. Utilize o botão :bi:`Exportar` para executar a Ação.

[clvheatlh-jcafb-2025n-aws-pro] Exportar a lista de todos os Pacientes cadastrados
----------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Exportar a lista de todos os Pacientes cadastrados:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes

        #. Executar a Ação ":bi:`Exportar`" (**843**):

            * Parâmetros utilizados:
                * *Quero atualizar os dados (compatibilidade com importação e exportação)*: '**marcado**"
                * *Campos para exportar*: » **Modelo**: "**JCAFB-2025 - Cadastro de Pacientes**"

            #. Utilize o botão :bi:`Exportar` para executar a Ação.

[clvheatlh-jcafb-2025n-aws-pro] Exportar a lista de todos os Pacientes cadastrados (Referência)
-----------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025n-aws-pro] Exportar a lista de todos os Pacientes cadastrados (Referência):

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025n-aws-pro <https://clvheatlh-jcafb-2025n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes

        #. Executar a Ação ":bi:`Exportar`" (**843**):

            * Parâmetros utilizados:
                * *Quero atualizar os dados (compatibilidade com importação e exportação)*: '**marcado**"
                * *Campos para exportar*: » **Modelo**: "**JCAFB-2025 - Cadastro de Pacientes (Ref) 2**"

            #. Utilize o botão :bi:`Exportar` para executar a Ação.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-06a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-06a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-06a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-06a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-06a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-06a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-06a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-06a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-06a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-06a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-07a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-07a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-07a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-07a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-07a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-07a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-08a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-08a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-08a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-08a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-08a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-08a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-08a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-08a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-08a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-08a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-08a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-08a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-09a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-09a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-09a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-09a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-09a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-09a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-09a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-09a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-09a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-09b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-09b.sql

            gzip clvhealth_jcafb_2025_15_2025-01-09b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-09b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-09b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-09b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-09b.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-09b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-09b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09b

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-09b)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-09b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-09b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-10a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-10a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-10a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-10a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-10a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-10a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-10a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-10a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-10a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-11a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-11a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-11a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-11a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-11a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-11a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-12a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-12a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-12a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-12a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-12a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-12a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-12a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-12a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-12a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-15a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-15a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-15a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-15a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-15a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-15a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-15a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-15a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-15a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-16a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-16a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-16a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-16a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-16a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-16a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-16a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-16a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-16a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-16a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-16b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-16b.sql

            gzip clvhealth_jcafb_2025_15_2025-01-16b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-16b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-16b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-16b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-16b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-16b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-16b.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-16b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-16b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-16b

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-17a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-17a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-17a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-17a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-17a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-17a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-17a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-17a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-17a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-17a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-17a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-17a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-17a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-17a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-20a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-20a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-20a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-20a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-20a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-20a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-20a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-20a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-20a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-20a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-20a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-20a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-20a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-20a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-21a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-21a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-21a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-21a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-21a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-21a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-21a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-21a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-21a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-21a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-21a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-21a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-21a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-21a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-22a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-22a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-22a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-22a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-22a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-22a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-22a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-22a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-22a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-24a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-24a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-24a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-24a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-24a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-24a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-24a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-24a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-24a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-24a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-24a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-24a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-24a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-24a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-tst] Atualizar os fontes do projeto (2025-01-26a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2025-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2025n-aws-pro] Atualizar os fontes do projeto (2025-01-26a)
----------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2025-aws-tst] Atualizar os fontes do projeto (2025-01-27a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2025-aws-tst -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2025n-aws-pro] Atualizar os fontes do projeto (2025-01-27a)
----------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2025n-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-27a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-27a.sql

            gzip clvhealth_jcafb_2025_15_2025-01-27a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-01-27a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-27a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-01-27a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-01-27a.sql
.. index:: clvhealth_jcafb_2025_15_2025-01-27a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-01-27a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-27a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-27a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-01-27a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-27a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-27a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-03a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-03a.sql

            gzip clvhealth_jcafb_2025_15_2025-02-03a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-03a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-03a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-03a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-03a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-03a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-03a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-03a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-02-03a.sql
.. index:: clvhealth_jcafb_2025_15_2025-02-03a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-02-03a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-03a

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-04a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-04a.sql

            gzip clvhealth_jcafb_2025_15_2025-02-04a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-04a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-02-04a.sql
.. index:: clvhealth_jcafb_2025_15_2025-02-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-02-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-04a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-04a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-02-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-02-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-06a.sql

            gzip clvhealth_jcafb_2025_15_2025-02-06a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-06a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-02-06a.sql
.. index:: clvhealth_jcafb_2025_15_2025-02-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-02-06a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-06a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-06a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-02-06a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-02-06a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-15a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-15a.sql

            gzip clvhealth_jcafb_2025_15_2025-02-15a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-15a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-02-15a.sql
.. index:: clvhealth_jcafb_2025_15_2025-02-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-02-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-15a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-15a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-02-15a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-02-15a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-19a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-19a.sql

            gzip clvhealth_jcafb_2025_15_2025-02-19a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-02-19a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-19a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-02-19a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-02-19a.sql
.. index:: clvhealth_jcafb_2025_15_2025-02-19a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-02-19a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-19a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-02-19a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-02-19a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-02-19a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-02-19a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025n-aws-pro] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-03-30a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-03-30a.sql

            gzip clvhealth_jcafb_2025_15_2025-03-30a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2025-03-30a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2025-03-30a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2025-03-30a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2025-03-30a.sql
.. index:: clvhealth_jcafb_2025_15_2025-03-30a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2025-03-30a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2025-03-30a

[clvheatlh-jcafb-2025-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-03-30a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            ssh clvheatlh-jcafb-2025-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-03-30a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-03-30a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-tst <https://clvheatlh-jcafb-2025-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://54.86.57.170**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2025-aws-pro] Atualizar os fontes do projeto (2025-03-30a)
---------------------------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh clvheatlh-jcafb-2025-aws-pro -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_verification_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_verification_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull
            # cd /opt/odoo
            # rm -r  /opt/odoo/clvsol_odoo_addons_jcafb
            # git clone https://github.com/MostlyOpen/clvsol_odoo_addons_jcafb --branch 15.0

            cd /opt/odoo/clvsol_odoo_addons_log_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

[clvheatlh-jcafb-2025-aws-pro] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-03-30a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2025-aws-pro] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2025-aws-pro** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            ssh clvheatlh-jcafb-2025-aws-pro -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2025-aws-pro] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2025_15_2025-03-30a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-03-30a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-03-30a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2025-aws-pro** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2025-aws-pro
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2025-aws-pro] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2025-aws-pro <https://clvheatlh-jcafb-2025-aws-pro>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://34.224.24.169**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
