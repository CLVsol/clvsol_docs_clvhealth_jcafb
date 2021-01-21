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

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-11c)
-------------------------------------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-11c.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-11c.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-11c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-11c.tar.gz

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

Criar os Grupos para a JCAFB-2021v
----------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Criar os Departamentos para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Departamentos`

        * Departamentos Criados:
            
            * **Grupo 01 (2021v)**

                * Nome do Departamento: "**Grupo 01 (2021v)**"

            * **Grupo 02 (2021v)**

                * Nome do Departamento: "**Grupo 02 (2021v)**"

            * **Grupo 03 (2021v)**

                * Nome do Departamento: "**Grupo 03 (2021v)**"

            * **Grupo 04 (2021v)**

                * Nome do Departamento: "**Grupo 04 (2021v)**"

    #. Criar os Funcionários para a **JCAFB-2021v**:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        * Funcionários Criados:
            
            * **Grupo 01 (2021v)**

                * Nome do Funcionário: "**Grupo 01 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 01 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 02 (2021v)**

                * Nome do Funcionário: "**Grupo 02 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 02 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 03 (2021v)**

                * Nome do Funcionário: "**Grupo 03 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 03 (2021v)**
                * Cargo: **Grupo de Campo**

            * **Grupo 04 (2021v)**

                * Nome do Funcionário: "**Grupo 04 (2021v)**"
                * *Phase*: **JCAFB-2021v**
                * Departamento: **Grupo 04 (2021v)**
                * Cargo: **Grupo de Campo**

    #. Associar os Funcionários aos Departamentos:

        * Menu de acesso:
            
            * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        * Beatriz Rossi Bonin (Coordenador Geral): **Grupo 01 (2021v)**
        * Sofia Schalka (Coordenador Geral): **Grupo 01 (2021v)**

        * Beatriz Cerdá Mendes de Araujo (Coordenador de Campo): **Grupo 02 (2021v)**
        * Sarah de Araújo Sprenge (Coordenador de Campo): **Grupo 02 (2021v)**

        * Felipe Barboza Galhard (Coordenador de Campanha): **Grupo 03 (2021v)**
        * Guilherme Souza Macário (Coordenador de Campanha): **Grupo 03 (2021v)**

        * Luís Carlos Fogaça dos Santos (Coordenador de Análises): **Grupo 04 (2021v)**
        * Suelen Martins da Costa (Coordenador de Análises): **Grupo 04 (2021v)**
        * Rodrigo Gonçalves Queijo (Coordenador de Comunicação): **Grupo 04 (2021v)**

Associar as Pessoas selecionadas aos Grupos da JCAFB-2021v
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *Persons*:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Community` » :bi:`Persons`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Person State` » :bi:`Responsible Employee` » :bi:`Categories`

    #. Selecionar as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`» :bi:`Category` = :bi:`Criança`:

        * Distribuir as Crianças selecionados pelos Grupos da JCAFB-2021v de forma que o número de Crianças seja equanimemente distribuido entre os Grupos.

    #. Selecionar as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Person State` = ":bi:`Selected`" » :bi:`Responsible Employee` = :bi:`Indefinido`» :bi:`Category` = :bi:`Idoso`:

        * Distribuir os Idosos selecionados pelos Grupos da JCAFB-2021v de forma que o número de Idosos seja equanimemente distribuido entre os Grupos.

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-12a)
---------------------------------------------------------------------------------------------------

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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-12a.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-12a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-12a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-12a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-12a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-12a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-12a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-12a

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-12a)
-------------------------------------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2021v_14_2020-12-12a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2020-12-12a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-12a.tar.gz

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

Criar os Documentos para as Crianças selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Person]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Person]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSC21**

                    #. **TCR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para os Idosos selecionados para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Person]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Person]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QMD21**

                    #. **QSI21**

                    #. **TID21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar os Documentos para as Famílias selecionadas para o Projeto JCAFB-2021v
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Set Up [Family]` para as Famílias selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Families`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Family State`

        #. Selecionar todas as Famílias com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Family State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Document Set Up [Family]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSF21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

Criar as Requisições de Exames para as Crianças selecionadas para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Person]` para as Crianças selecionadas para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Lab Test Request Set Up [Person]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EEV21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

Criar as Requisições de Exames para os Idosos selecionados para o Projeto JCAFB-2021v
---------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Set Up [Person]` para os Idosos selecionados para o Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Person State`

        #. Selecionar todas as Pessoas com: :bi:`Phase` = "**JCAFB-20201v**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Person State` = :bi:`Selected`

        #. Exercutar a Ação ":bi:`Lab Test Request Set Up [Person]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP21**

                    #. **EUR21**

                * *Phase*: **JCAFB-2021v**

            #. Utilize o botão :bi:`Lab Test Request Set Up` para executar a Ação.

:red:`(Backup Excluido)` Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-13a)
---------------------------------------------------------------------------------------------------

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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-13a.sql

            gzip clvhealth_jcafb_2021v_14_2020-12-13a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2020-12-13a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-13a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2020-12-13a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-13a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2020-12-13a.sql
.. index:: clvhealth_jcafb_2021v_14_2020-12-13a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2020-12-13a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2020-12-13a

:red:`(Backup Excluido)` Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2020-12-13a)
-------------------------------------------------------------------------------------------------------

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

.. toctree::   :maxdepth: 2
