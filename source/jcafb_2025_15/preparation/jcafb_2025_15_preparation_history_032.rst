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
JCAFB-2025-15 (Preparação pré Jornada II [3])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-02a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-11-02a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-11-02a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz

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


[tkl-odoo15-jcafb25-vm] Importar *Patient Markers*  (**14**)
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Patient Markers**:

        * Menu de acesso:
            * **Health** » **Configuration** » **Patient** » **Markers**

    #. Executar a importação do arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/patient_marker.xlsx**":

        * Menu de acesso:
            * **Favoritos** » **Importar registros**

        #. Utilizar o botão :bi:`Upload File`.

        #. Selecionar o arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/patient_marker.xlsx**".

        #. Utilize o botão :bi:`Importar` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Importar *Street Patterns*  (**61**)
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Street Patterns**:

        * Menu de acesso:
            * **Base** » **Configuration** » **Partner Entity** » **Street Patterns**

    #. Executar a importação do arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/street_pattern.xlsx**":

        * Menu de acesso:
            * **Favoritos** » **Importar registros**

        #. Utilizar o botão :bi:`Upload File`.

        #. Selecionar o arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/street_pattern.xlsx**".

        #. Utilize o botão :bi:`Importar` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Importar *Contact Information Patterns*  (**624**)
--------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Contact Information Patternss**:

        * Menu de acesso:
            * **Base** » **Configuration** » **Partner Entity** » **Contact Information Patterns**

    #. Executar a importação do arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/contact_information_pattern.xlsx**":

        * Menu de acesso:
            * **Favoritos** » **Importar registros**

        #. Utilizar o botão :bi:`Upload File`.

        #. Selecionar o arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/contact_information_pattern.xlsx**".

        #. Utilize o botão :bi:`Importar` para executar a Ação.

:borange:`Repetir duas vezes o procedimento:` [tkl-odoo15-jcafb25-vm] Importar o Cadastro de Paciente incial de Avaí (**843**)
------------------------------------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Patients**:

        * Menu de acesso:
            * **Health** » **Health** » **Patient** » **Patients**

    #. Executar a importação do arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/jcafb_cadastro_odoo.xlsx**":

        * Menu de acesso:
            * **Favoritos** » **Importar registros**

        #. Utilizar o botão :bi:`Upload File`.

        #. Selecionar o arquivo "**/opt/clvsol/jupyter/jcafb_2025/cadastro/data/jcafb_cadastro_odoo.xlsx**".

        #. Utilize o botão :bi:`Importar` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Marcar *Contact Information is unavailable* dos Pacientes sem Logradouro definido
---------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Pacientes sem Logradouro definido`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Street`

        #. Selecionar os :bi:`Patients` com: :bi:`Street` = "**Indefinido**" (**2**)

        #. Marcar o ":bi:`Contact Information is unavailable`" para os Pacientes selecionados.

[tkl-odoo15-jcafb25-vm] Atualizar o *State* dos Pacientes sem Logradouro definido
---------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Pacientes sem Logradouro definido`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Street`

        #. Selecionar os :bi:`Patients` com: :bi:`Street` = "**Indefinido**" (**2**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** **Unvailable**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *State* dos Pacientes com formato de Endereço inválido
------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Pacientes com formato de Endereço inválido`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Pesquisar pelos registros com :bi:`Address Name` = "**.**" ou :bi:`Address Name` = "**Fundos /**" ou :bi:`Address Name` = "**CH Manoel Rodrigues**" ou :bi:`Address Name` = "**Cohab**"

        #. Selecionar os :bi:`Patients` com: :bi:`Patient State` = "**New**" (**23**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** **Unvailable**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *State* dos Pacientes com Logradouro definido
---------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Pacientes com Logradouro definido`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Selecionar os :bi:`Patients` com: :bi:`Patient State` = "**New**" (**818**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *State*: **Set** **Available**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Verificação de todos os Pacientes
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**843**)

        #. Executar a Ação ":bi:`Patient Verification Execute`":

            * Parâmetros utilizados:

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Criação de todos os Pacientes (Rec)
----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Create` para todos os Pacientes:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Selecionar todos os Pacientes (**843**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Create`":

            * Parâmetros utilizados:
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Related Patient (Rec) Create` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *Register State* dos Pacientes *Available*
------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit` para os Pacientes :bi:`Available`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`

        #. Selecionar os :bi:`Patients` com: :bi:`Patient State` = "**Available**" (**818**)

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** **Done**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *Register State* dos Pacientes (Rec) *Available*
------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Rec) Mass Edit` para os Pacientes (Rec) :bi:`Available`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patient (Rec)s*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient (Rec)` » :bi:`Patient (Rec)s`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient (Rec) State`

        #. Selecionar os :bi:`Patient (Rec)s` com: :bi:`Patient (Rec) State` = "**Available**" (**818**)

        #. Executar a Ação ":bi:`Patient (Rec) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** **Done**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-10a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-10a.sql

            gzip clvhealth_jcafb_2025_15_2024-11-10a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-10a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-11-10a.sql
.. index:: clvhealth_jcafb_2025_15_2024-11-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-11-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-10a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-10a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-11-10a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-11-10a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-10a.tar.gz

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
