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
JCAFB-2025-15 (Preparação pré Jornada [4])
==========================================

:bmaroon:`(Not Implemented)` [tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-14a)
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
            # gzip -d clvhealth_jcafb_2024_15_2024-05-14a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-05-14a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-14a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-14a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização de todos os Pacientes (Rec)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Update` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Remover a Residência dos Pacientes
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Residence is unavailable*: :bi:`Set` **marcado**
                * *Residence*: :bi:`Remove`
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Remover o Grupo dos Pacientes
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Responsible Empĺoyee*: :bi:`Remove`
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *Patient State* dos Pacientes
-----------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Selected**" (**145**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Available**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Waiting**" (**125**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Patient State*: **Set** » **Available**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização de todos os Pacientes (Rec)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Update` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Remover o *Patient Tags* dos Pacientes
--------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**).

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Patient Tag*: :bi:`Set` **lista vazia**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Renovar o *Random ID* de todos os Pacientes
-------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-v] Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Random ID*: :bi:`Set` "**/**"

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes (Aux)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Aux) Verification Execute` para todos os Pacientes (Aux):

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux) (**819**)

        #. Executar a Ação ":bi:`Patient (Aux) Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient (Aux) Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização (*Reload*) de todos os Pacientes (Aux)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Aux) Reload` para todos os Pacientes (Aux):

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux) (**819**)

        #. Executar a Ação ":bi:`Patient (Aux) Reload`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-15a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-15a.sql

            gzip clvhealth_jcafb_2024_15_2024-05-15a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-15a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-15a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-05-15a.sql
.. index:: clvhealth_jcafb_2024_15_2024-05-15a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-05-15a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-15a)
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

[tkl-odoo15-jcafb25-vm] Atualizar o "*Global Settings*" para a *CLVhealth-JCAFB-2025-15*
----------------------------------------------------------------------------------------

    #. Acessar a *View* *Global Settings*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Global Settings` » :bi:`Global Settings`

        #. Configurar o parâmetro :bi:`Phase` » :bi:`Phase`: **JCAFB-2025**

        #. Configurar o parâmetro :bi:`Patient` » :bi:`Reference Date`: **31/01/2025**

[tkl-odoo15-jcafb25-vm] Atualizar a Idade de Referência dos Pacientes
---------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:
                * *Patient Reference Age Refresh*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Incrementar a "Idade Estimada" dos Pacientes sem "Data de Nascimento"
---------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar manualmente o *Processing Schedule* **Patient Estilmated Age Updt**:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* :bi:`Processing Schedules`:

            * Menu de acesso:

                * :bi:`Processing` » :bi:`Processing` » :bi:`Schedules`

        #. Selecionar o *Processing Schedule* "**Patient Estilmated Age Updt**"

        #. Executar a Ação :bi:`Processing Schedule Execute`:

            #. Utilize o botão :bi:`Processing Schedule Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização de todos os Pacientes (Rec)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Update` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**819**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes (Aux)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Aux) Verification Execute` para todos os Pacientes (Aux):

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux) (**819**)

        #. Executar a Ação ":bi:`Patient (Aux) Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient (Aux) Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização (*Reload*) de todos os Pacientes (Aux)
-------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Aux) Reload` para todos os Pacientes (Aux):

        #. Acessar a *View* *Patients (Aux)*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Configuration` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux) (**819**)

        #. Executar a Ação ":bi:`Patient (Aux) Reload`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Reload` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-15b)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-15b.sql

            gzip clvhealth_jcafb_2024_15_2024-05-15b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2024-05-15b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-15b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2024-05-15b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2024-05-15b.sql
.. index:: clvhealth_jcafb_2024_15_2024-05-15b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2024-05-15b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-05-15b)
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
            # gzip -d clvhealth_jcafb_2024_15_2024-05-15b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2024-05-15b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2024-05-15b.tar.gz

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
