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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-09b)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-09b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-09b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz

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

Atualizar o(s) módulo(s) [clv_document]
---------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Lista de Módulos:

        * clv_document

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" - m clv_document
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Atualizar o(s) módulo(s) [clv_processing_jcafb]
-----------------------------------------------

    #. [clvhealth-jcafb-2021-vm-pro] Lista de Módulos:

        * clv_processing_jcafb

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
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" - m clv_processing_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-10a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-10a.sql

            gzip clvhealth_jcafb_2021v_14_2021-02-10a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-10a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-02-10a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-02-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-02-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-10a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-10a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-10a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-10a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-10a.tar.gz

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

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-15a)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-15a.sql

            gzip clvhealth_jcafb_2021v_14_2021-02-15a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-15a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-02-15a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-02-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-02-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-15a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-15a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-15a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-15a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-15a.tar.gz

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
