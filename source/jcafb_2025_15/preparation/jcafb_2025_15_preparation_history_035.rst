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

=============================================
JCAFB-2025-15 (Preparação pré Jornada II [6])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-09e)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2024-12-09e.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-09e.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-09e.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-15a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-15a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-15a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-15a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-15a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-15a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-15a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-15a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-06a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-06a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-07a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-07a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-07a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-09a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-09a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-09a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-09a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-09b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-09b.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-11a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-11a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-11a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-12a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-12a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2025-01-12a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2025-01-12a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2025-01-15a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb25-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            ssh tkl-odoo15-jcafb25-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb25-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2025_15_2025-01-15a.sql.gz

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

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
