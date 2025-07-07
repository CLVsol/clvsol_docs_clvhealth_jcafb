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
JCAFB-2026-15 (Preparação pré Jornada [3])
==========================================

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-04a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-04a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-04a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-04a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Document Code Pools**
----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. :red:`(Não Executado)` Excluir todos os **Document Code Pool Items**:

        #. Acessar a *view* **Document Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Document Code Pool Items`

        #. Selecionar todos os :bi:`Document Code Pool Items`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Excluir todos os **Document Code Pools**:

        #. Acessar a *view* **Document Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Document Code Pool`

        #. Selecionar todos os :bi:`Document Codes`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Documents** descartados
------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Excluir todos os **Documents** descartados:

        #. Acessar a *view* **Documents**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Selecionar todos os :bi:`Documents` com *Document State* = **Discarded**.

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar o *Document Code Pool* "(Global) Document Code Pool"
----------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Criar o *Document Code Pool* **(Global) Document Code Pool**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        * *Document Code Pool* criado:
            
            * **(Global) Document Code Pool**

                * *Name*: **(Global) Document Code Pool**
                * *Code Sequence*: **clv.document.code**

[tkl-odoo15-jcafb26-vm] Executar a Ação *Document Code Pool Item Get* para "(Global) Document Code Pool"
--------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Document Code Pool Item Get` para :bi:`(Global) Document Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar *Document Code Pool* "**(Global) Document Code Pool**"

        #. Executar a Ação ":bi:`Document Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Executar a Ação "Document Code Pool Item Setup" para "(Global) Document Code Pool"
----------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Document Code Pool Item Setup` para :bi:`(Global) Document Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar *Document Code Pool* "**(Global) Document Code Pool**"

        #. Executar a Ação ":bi:`Document Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **2000**
                * *Sequence Minimum*: **3.015**
                * *Sequence Maximum*: **4.187**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

:red:`(Não Executado)` [tkl-odoo15-jcafb26-vm] Executar a Ação "Document Code Pool Item Seek" para todos os "Document Code Pools"
---------------------------------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Document Code Pool Item Seek` para todos os :bi:`Document Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Document Code Pool`

        #. Selecionar todos os *Document Code Pools*

        #. Executar a Ação ":bi:`Document Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Lab Test Result Code Pools**
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. :red:`(Não Executado)` Excluir todos os **Lab Test Result Code Pool Items**:

        #. Acessar a *view* **Lab Test Result Code Pool Items**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Pools`» :bi:`Lab Test Result Code Pool Items`

        #. Selecionar todos os :bi:`Lab Test Result Code Pool Items`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Excluir todos os **Lab Test Result Code Pools**:

        #. Acessar a *view* **Lab Test Result Code Pools**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Pools`» :bi:`Lab Test Result Code Pool`

        #. Selecionar todos os :bi:`Lab Test Result Codes`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Lab Test Result** descartados
------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Excluir todos os **Lab Test Results** descartados:

        #. Acessar a *view* **Lab Test Results**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test`» :bi:`Results`

        #. Selecionar todos os :bi:`Lab Test Results` com *Result State* = **Discarded**.

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Result Code Pool* "(Global) Lab Test Result Code Pool"
------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. Criar o *Lab Test Result Code Pool* **(Global) Lab Test Result Code Pool**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        * *Lab Test Result Code Pool* criado:
            
            * **(Global) Lab Test Result Code Pool**

                * *Name*: **(Global) Lab Test Result Code Pool**
                * *Code Sequence*: **clv.lab_test.result.code**

[tkl-odoo15-jcafb26-vm] Executar a Ação *Lab Test Result Code Pool Item Get* para "(Global) Lab Test Result Code Pool"
----------------------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Result Code Pool Item Get` para :bi:`(Global) Lab Test Result Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar *Lab Test Result Code Pool* "**(Global) Lab Test Result Code Pool**"

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Get`":

            #. Utilize o botão :bi:`Code Pool Item Get` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Executar a Ação "Lab Test Result Code Pool Item Setup" para "(Global) Lab Test Result Code Pool"
------------------------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Result Code Pool Item Setup` para :bi:`(Global) Lab Test Result Code Pool`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar *Lab Test Result Code Pool* "**(Global) Lab Test Result Code Pool**"

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Setup`":

            * Parâmetros utilizados:

                * *Code Quantity*: **1000**
                * *Sequence Minimum*: **1.914**
                * *Sequence Maximum*: **2.848**

            #. Utilize o botão :bi:`Code Pool Item Setup` para executar a Ação.

:red:`(Não Executado)` [tkl-odoo15-jcafb26-vm] Executar a Ação "Lab Test Result Code Pool Item Seek" para todos os "Lab Test Result Code Pools"
-----------------------------------------------------------------------------------------------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Result Code Pool Item Seek` para todos os :bi:`Lab Test Result Code Pools`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Result Code Pools*:

            * Menu de acesso:

                * **Base** » :bi:`Base` » :bi:`Pools` » :bi:`Lab Test Result Code Pool`

        #. Selecionar todos os *Lab Test Result Code Pools*

        #. Executar a Ação ":bi:`Lab Test Result Code Pool Item Seek`":

            #. Utilize o botão :bi:`Code Pool Item Seek` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Residence Code Pools**
-----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. :red:`(Não Executado)` Excluir todos os **Residence Code Pool Items**:

        #. Acessar a *view* **Residence Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Residence Code Pool Items`

        #. Selecionar todos os :bi:`Residence Code Pool Items`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Excluir todos os **Residence Code Pools**:

        #. Acessar a *view* **Residence Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Residence Code Pool`

        #. Selecionar todos os :bi:`Residence Codes`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Excluir todos os **Patient Code Pools**
----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

    #. :red:`(Não Executado)` Excluir todos os **Patient Code Pool Items**:

        #. Acessar a *view* **Patient Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Patient Code Pool Items`

        #. Selecionar todos os :bi:`Patient Code Pool Items`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Excluir todos os **Patient Code Pools**:

        #. Acessar a *view* **Patient Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Patient Code Pool`

        #. Selecionar todos os :bi:`Patient Codes`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07a.sql

            gzip clvhealth_jcafb_2026_15_2025-07-07a.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07a.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-07a.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07a

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-07a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb26-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb26-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            ssh tkl-odoo15-jcafb26-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb26-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2026_15_2025-07-07a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-07a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-07a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb26-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb26-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Not Used)` [tkl-odoo15-jcafb26-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb26-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
