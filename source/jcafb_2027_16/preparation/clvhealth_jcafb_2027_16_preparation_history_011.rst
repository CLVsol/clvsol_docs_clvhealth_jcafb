.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .bgreen {font-weight: bold; color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bblue {font-weight: bold; color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: bgreen
.. role:: blue
.. role:: bblue
.. role:: bmaroon
.. role:: borange
.. role:: bi

.. index:: JCAFB-2027-16 (Preparação pré Jornada [2])

==========================================
JCAFB-2027-16 (Preparação pré Jornada [2])
==========================================

[tkl-odoo16-jcafb27-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-05-03a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2027_16_2026-05-03a.sql.gz

            dropdb -i clvhealth_jcafb_2027_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2027_16
            psql -f clvhealth_jcafb_2027_16_2026-05-03a.sql -d clvhealth_jcafb_2027_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2027_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb27-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.223**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb27-vm] Criar a "*Phase*" (**2027**) para a *CLVhealth-JCAFB-2027-16*
-------------------------------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Configurations` » :bi:`Phases`

        #. Criar um novo Registro:

            * :bi:`Phase`: "**JCAFB-2027**" (id = 11)

            * :bi:`Description`: "**Primeiro ano do ciclo de xxxx**"

[tkl-odoo16-jcafb27-vm] Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2027-16*
----------------------------------------------------------------------------------------

    #. :red:`(Não Executado - não está funcionando)` Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2027**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2027**

    #. Conectar-se, via *browser*, ao :bi:`Adminer` do servidor `tkl-odoo16-jcafb27-vm:12322 <https://tkl-odoo16-jcafb27-vm:12322>`_.

        #. Acessar a tabela "**ir_config_parameter**" e alterar manualmente os registros:

            #. **"key" = "clv.global_settings.current_phase_id"**:

                * **"value" = "11"** (**JCAFB-2027**)

            #. **"key" = "clv.global_settings.current_date_reference"**:

                * **"value" = "2027-01-31"**

[tkl-odoo16-jcafb27-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-06-22a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-06-22a.sql

            gzip clvhealth_jcafb_2027_16_2026-06-22a.sql
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-06-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz clvhealth_jcafb_2027_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2027_16_2026-06-22a.sql
        * /opt/odoo/clvhealth_jcafb_2027_16_2026-06-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz

.. index:: clvhealth_jcafb_2027_16_2026-06-22a.sql
.. index:: clvhealth_jcafb_2027_16_2026-06-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2027_16_2026-06-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22a

[tkl-odoo16-jcafb27-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-06-22a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2027_16_2026-06-22a.sql.gz

            dropdb -i clvhealth_jcafb_2027_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2027_16
            psql -f clvhealth_jcafb_2027_16_2026-06-22a.sql -d clvhealth_jcafb_2027_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2027_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb27-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.223**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb27-vm] Atualizar o *Employee History* de todos os Funcionários
-------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Executar a Ação :bi:`Employee History Update` para todos os Funcionários:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar todos os Funcionários (**443**)

        #. Executar a Ação ":bi:`Employee History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **03/07/2025**
                * *Sign in date*: **03/07/2025**

            #. Utilize o botão :bi:`Employee History Update` para executar a Ação.

[tkl-odoo16-jcafb27-vm] Atualizar/Remover a Fase dos Funcionários
-----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

    #. [tkl-odoo16-jcafb27-vm] Atualizar manualmente a *Phase* dos Funcionários associados à **JCAFB-2027**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Atualizar manualmente as informações de "*Phase*", "*Job*" e "*Department*" dos Funcionários associados à **JCAB-2027**.

    #. [tkl-odoo16-jcafb27-vm] Executar a Ação :bi:`Employee Mass Edit` os Funcionários que **não** estejam associados à **JCAB-2027**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar os Funcionários associados à **JCAFB-2026** (**65**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Phase*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo16-jcafb27-vm] Atualizar o *Employee History* de todos os Funcionários
-------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Executar a Ação :bi:`Employee History Update` para todos os Funcionários:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* *Employees*:

            * Menu de acesso:

                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar todos os Funcionários (**443**)

        #. Executar a Ação ":bi:`Employee History Update`":

            * Parâmetros utilizados:

                * *Sign out date*: **03/05/2026**
                * *Sign in date*: **03/05/2026**

            #. Utilize o botão :bi:`Employee History Update` para executar a Ação.

[tkl-odoo16-jcafb27-vm] Remover Função dos Funcionários não associados à JCAFB-2027
-----------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

    #. [tkl-odoo16-jcafb27-vm] Executar a Ação :bi:`Employee Mass Edit` os Funcionários que **não** estejam associados à **JCAB-2027**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar os Funcionários não associados à **JCAFB-2027**, mas com o campo :bi:`Job` definido (**65**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Job*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo16-jcafb27-vm] Remover Departamento dos Funcionários não associados à JCAFB-2027
-----------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

    #. [tkl-odoo16-jcafb27-vm] Executar a Ação :bi:`Employee Mass Edit` os Funcionários que **não** estejam associados à **JCAB-2027**:

        #. Acessar a *View* *Employees*:

            * Menu de acesso:
                * **Funcionários** » :bi:`Employees` » :bi:`Employees`

        #. Selecionar os Funcionários não associados à **JCAFB-2027**, mas com o campo :bi:`Department` definido (**46**)

        #. Executar a Ação ":bi:`Employee Mass Edit`":

            * Parâmetros utilizados:
                * *Department*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo16-jcafb27-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-06-22b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-06-22b.sql

            gzip clvhealth_jcafb_2027_16_2026-06-22b.sql
            pg_dump clvhealth_jcafb_2027_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2027_16_2026-06-22b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz clvhealth_jcafb_2027_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2027_16_2026-06-22b.sql
        * /opt/odoo/clvhealth_jcafb_2027_16_2026-06-22b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz

.. index:: clvhealth_jcafb_2027_16_2026-06-22b.sql
.. index:: clvhealth_jcafb_2027_16_2026-06-22b.sql.gz
.. index:: filestore_clvhealth_jcafb_2027_16_2026-06-22b
.. index:: clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22b

[tkl-odoo16-jcafb27-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-06-22b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb27-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb27-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            ssh tkl-odoo16-jcafb27-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb27-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2027_16_2026-06-22b.sql.gz

            dropdb -i clvhealth_jcafb_2027_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2027_16
            psql -f clvhealth_jcafb_2027_16_2026-06-22b.sql -d clvhealth_jcafb_2027_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2027_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-06-22b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb27-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb27-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb27-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb27-vm <https://tkl-odoo16-jcafb27-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.223**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
