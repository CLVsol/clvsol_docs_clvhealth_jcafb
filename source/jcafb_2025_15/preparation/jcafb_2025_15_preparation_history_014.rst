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

==========================================
JCAFB-2025-15 (Preparação pré Jornada [5])
==========================================

:bmaroon:`(Not Implemented)` [tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-15a)
----------------------------------------------------------------------------------------------------------------------------------

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
            # gzip -d clvhealth_jcafb_2024_15_2024-05-15a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-05-15a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb25-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Document Code Pool Item Setup" para "(Global) Document Code Pool"
----------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Code Pool Item Setup` para :bi:`(Global) Document Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar *Document Code Pool* "**(Global) Document Code Pool**"

        #. Executar a Ação ":bi:`Document Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **1000**
                * *Sequence Minimum*: **1201**
                * *Sequence Maximum*: **3014**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Document Code Pool Item Seek" para todos os "Document Code Pools"
----------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Code Pool Item Seek` para todos os :bi:`Document Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar todos os *Document Code Pools* (**19**)

        #. Executar a Ação ":bi:`Document Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Document Code Pool Item Get" para "(Global) Document Code Pool"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Code Pool Item Get` para :bi:`(Global) Document Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar *Document Code Pool* "**(Global) Document Code Pool**"

        #. Executar a Ação ":bi:`Document Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Lab Test Result Code Pool Item Setup" para "(Global) Lab Test Result Code Pool"
------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Result Code Pool Item Setup` para :bi:`(Global) Lab Test Result Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar *Lab Test Result Code Pool* "**(Global) Lab Test Result Code Pool**"

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **1000**
                * *Sequence Minimum*: **601**
                * *Sequence Maximum*: **1913**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Lab Test Result Code Pool Item Seek" para todos os "Lab Test Result Code Pools"
------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Result Code Pool Item Seek` para todos os :bi:`Lab Test Result Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar todos os *Lab Test Result Code Pools* (**19**)

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Lab Test Result Code Pool Item Get" para "(Global) Lab Test Result Code Pool"
----------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Result Code Pool Item Get` para :bi:`(Global) Lab Test Result Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar *Lab Test Result Code Pool* "**(Global) Lab Test Result Code Pool**"

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Residence Code Pool Item Setup" para "(Global) Residence Code Pool"
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Residence Code Pool Item Setup` para :bi:`(Global) Residence Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Residence Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Residence Code Pool`

        #. Selecionar *Residence Code Pool* "**(Global) Residence Code Pool**"

        #. Executar a Ação ":bi:`Residence Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **1000**
                * *Sequence Minimum*: **1001**
                * *Sequence Maximum*: **1342**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Residence Code Pool Item Seek" para todos os "Residence Code Pools"
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Residence Code Pool Item Seek` para todos os :bi:`Residence Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Residence Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Residence Code Pool`

        #. Selecionar todos os *Residence Code Pools* (**1**)

        #. Executar a Ação ":bi:`Residence Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Residence Code Pool Item Get" para "(Global) Residence Code Pool"
----------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Residence Code Pool Item Get` para :bi:`(Global) Residence Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Residence Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Residence Code Pool`

        #. Selecionar *Residence Code Pool* "**(Global) Residence Code Pool**"

        #. Executar a Ação ":bi:`Residence Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Patient Code Pool Item Setup" para "(Global) Patient Code Pool"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Code Pool Item Setup` para :bi:`(Global) Patient Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patient Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Patient Code Pool`

        #. Selecionar *Patient Code Pool* "**(Global) Patient Code Pool**"

        #. Executar a Ação ":bi:`Patient Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **1000**
                * *Sequence Minimum*: **2001**
                * *Sequence Maximum*: **3587**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Patient Code Pool Item Seek" para todos os "Patient Code Pools"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Code Pool Item Seek` para todos os :bi:`Patient Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patient Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Patient Code Pool`

        #. Selecionar todos os *Patient Code Pools* (**10**)

        #. Executar a Ação ":bi:`Patient Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação "Patient Code Pool Item Get" para "(Global) Patient Code Pool"
------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Code Pool Item Get` para :bi:`(Global) Patient Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patient Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Patient Code Pool`

        #. Selecionar *Patient Code Pool* "**(Global) Patient Code Pool**"

        #. Executar a Ação ":bi:`Patient Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-16a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-16a.sql

            gzip clvhealth_jcafb_2024_15_2024-05-16a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-16a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-16a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-05-16a.sql
.. index:: clvhealth_jcafb_2024_15_2024-05-16a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-05-16a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-16a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-16a)
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
            # gzip -d clvhealth_jcafb_2024_15_2024-05-16a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-05-16a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-16a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb25-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb25-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Configurar o parâmetro "**web.base.url**":

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
