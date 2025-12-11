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

.. index:: JCAFB-2026-16 (Preparação pré Jornada [1])

==========================================
JCAFB-2026-16 (Preparação pré Jornada [1])
==========================================

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-11-01b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-11-01b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-01b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-01b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo16-jcafb26-vm**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-20a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-11-20a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-20a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-20a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-11-29a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-29a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29b)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-11-29b.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-29b.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-11-29c)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-11-29c.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-11-29c.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-11-29c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-02a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-02a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-02a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-12-02b)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-02b.sql

            gzip clvhealth_jcafb_2026_16_2025-12-02b.sql
            pg_dump clvhealth_jcafb_2026_16 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_16_2025-12-02b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz clvhealth_jcafb_2026_16

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-02b.sql
        * /opt/odoo/clvhealth_jcafb_2026_16_2025-12-02b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02b.tar.gz

.. index:: clvhealth_jcafb_2026_16_2025-12-02b.sql
.. index:: clvhealth_jcafb_2026_16_2025-12-02b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_16_2025-12-02b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-02b

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-06a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-06a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-06a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-06a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-07a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-07a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-09c)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-09c.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-09c.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-09c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-10a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-10a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-10a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-10a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

:red:`(Não Executado)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Document Type Items Set Up* para os *Document Types*
--------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Document Type Items Set Up` para os :bi:`Document Types`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        #. Selecionar os :bi:`Document Types` da JCAFB-2026 (**6**)

        #. Executar a Ação ":bi:`Document Type Items Set Up`":

            #. Utilize o botão :bi:`Items Set Up` para executar a Ação.

:red:`(Não Executado)` [tkl-odoo16-jcafb26-vm] Executar a Ação *Lab Test Type Criteria Set Up* para os *Lab Test Types*
-----------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para os *Lab Test Types*:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Selecionar os :bi:`Lab Test Types` da JCAFB-2026 (**5**)

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo16-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-16* (2025-12-11a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo16-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo16-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            ssh tkl-odoo16-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo16-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_16_2025-12-11a.sql.gz

            dropdb -i clvhealth_jcafb_2026_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_16
            psql -f clvhealth_jcafb_2026_16_2025-12-11a.sql -d clvhealth_jcafb_2026_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_16_2025-12-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_16_2025-12-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo16-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo16-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo16-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo16-jcafb26-vm <https://tkl-odoo16-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://192.168.25.222**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
