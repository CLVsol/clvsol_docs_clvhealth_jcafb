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
JCAFB-2025-15 (Preparação pré Jornada II [1])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-24a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-09-24a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-24a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-24a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-24a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Excluir todos os **Sets**
-------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Set Elements**:

        #. Acessar a *view* **Set Elements**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Set`» :bi:`Elements`

        #. Selecionar todos os :bi:`Set Elements` (**2036**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Sets**:

        #. Acessar a *view* **Sets**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Sets`

        #. Selecionar todos os :bi:`Sets` (**44**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Events**
---------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Event Attendees**:

        #. Acessar a *view* **Event Attendees**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Event`» :bi:`Attendees`

        #. Selecionar todos os :bi:`Event Attendees` (**326**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Events**:

        #. Acessar a *view* **Events**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Events`

        #. Selecionar todos os :bi:`Events` (**11**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todas as **Participations**
-----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todas as **Participations**:

        #. Acessar a *view* **Participations**:

            * Menu de acesso:

                * **Pesquisas** » :bi:`Participations` » :bi:`Participations`

        #. Selecionar todas as :bi:`Participations` (**1557**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Document Code Pools**
----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Document Code Pool Items**:

        #. Acessar a *view* **Document Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Document Code Pool Items`

        #. Selecionar todos os :bi:`Document Code Pool Items` (**3014**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Document Codes**:

        #. Acessar a *view* **Document Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Document Code Pool`

        #. Selecionar todos os :bi:`Document Codes` (**19**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Documents**
------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Documents**:

        #. Acessar a *view* **Documents**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Selecionar todos os :bi:`Documents` (**950**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Lab Test Result Code Pools**
-----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Lab Test Result Code Pool Items**:

        #. Acessar a *view* **Lab Test Result Code Pool Items**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Pools`» :bi:`Lab Test Result Code Pool Items`

        #. Selecionar todos os :bi:`Lab Test Result Code Pool Items` (**1903**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Lab Test Result Codes**:

        #. Acessar a *view* **Lab Test Result Code Pools**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Pools`» :bi:`Lab Test Result Code Pool`

        #. Selecionar todos os :bi:`Lab Test Result Codes` (**19**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Lab Test Results**
-------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Lab Test Results**:

        #. Acessar a *view* **Lab Test Results**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test`» :bi:`Results`

        #. Selecionar todos os :bi:`Lab Test Results` (**609**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os arquivos de **Resultados de Exames**
-----------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os arquivos presentes no diretório "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/results**" do Servidor (**289**).

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os :bi:`File System Files` do :bi:`File System Directory` "**Lab Test Result Files**":

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Files`

        #. Ativar o filtro **Agrupar por** » :bi:`Directory`

        #. Selecionar todas os :bi:`File System Files` referentes a "**Lab Test Result Files**" (**289**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os arquivos de **Laudos de Exames**
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os arquivos presentes no diretório "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/lab_test_files/reports**" do Servidor (**290**).

    #. :red:`(Não Necessário)` [tkl-odoo15-jcafb25-vm] Escluir manualmente todos os :bi:`File System Files` do :bi:`File System Directory` "**Lab Test Report Files**":

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Files`

        #. Ativar o filtro **Agrupar por** » :bi:`Directory`

        #. Selecionar todas os :bi:`File System Files` referentes a "**Lab Test Report Files**" (**290**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Contact Information Pattern Matches**
--------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Contact Information Pattern Matches**:

        #. Acessar a *view* **Contact Information Pattern Matches**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity`:bi:`Contact Information Pattern Matches`

        #. Selecionar todos os :bi:`Contact Information Pattern Matches` (**1920**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Contact Information Patterns**
-------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Contact Information Patterns**:

        #. Acessar a *view* **Contact Information Patterns**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity`:bi:`Contact Information Patterns`

        #. Selecionar todos os :bi:`Contact Information Patterns` (**570**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Street Pattern Matches**
-------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Street Pattern Matches**:

        #. Acessar a *view* **Street Pattern Matches**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity`:bi:`Street Pattern Matches`

        #. Selecionar todos os :bi:`Street Pattern Matches` (**1926**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Street Patterns**
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Street Patterns**:

        #. Acessar a *view* **Street Patterns**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity`:bi:`Street Patterns`

        #. Selecionar todos os :bi:`Street Patterns` (**72**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Residence Histories**
----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Residence Histories**:

        #. Acessar a *view* **Residence Histories**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence`» :bi:`Residence Histories`

        #. Selecionar todos os :bi:`Residence Histories` (**447**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Patient Histories**
----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Patient Histories**:

        #. Acessar a *view* **Patient Histories**:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient`» :bi:`Patient Histories`

        #. Selecionar todos os :bi:`Patient Histories` (**1268**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Residence Code Pools**
-----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Residence Code Pool Items**:

        #. Acessar a *view* **Residence Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Residence Code Pool Items`

        #. Selecionar todos os :bi:`Residence Code Pool Items` (**342**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Residence Codes**:

        #. Acessar a *view* **Residence Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Residence Code Pool`

        #. Selecionar todos os :bi:`Residence Codes` (**1**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todas as **Residences**
-------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todas as **Residences**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type` caso já não esteja ativado.

        #. Selecionar todas as :bi:`Residences` (**344**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Verification Outcomes` referentes a registros de :bi:`Patient`:

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Model Name`

        #. Selecionar todas os :bi:`Verification Outcomes` referentes a "**clv.residence**" (**344**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Patient Code Pools**
---------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Patient Code Pool Items**:

        #. Acessar a *view* **Patient Code Pool Items**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Pools`» :bi:`Patient Code Pool Items`

        #. Selecionar todos os :bi:`Patient Code Pool Items` (**1587**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb25-vm] Excluir todos os **Patient Codes**:

        #. Acessar a *view* **Patient Code Pools**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Pools`» :bi:`Patient Code Pool`

        #. Selecionar todos os :bi:`Patient Codes` (**10**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes**
------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type` caso já não esteja ativado.

        #. Selecionar todos os :bi:`Patient` (**819**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Verification Outcomes` referentes a registros de :bi:`Patient`:

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Model Name`

        #. Selecionar todas os :bi:`Verification Outcomes` referentes a "**clv.patient**" (**3315**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes (Rec)**
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Pacientes (Rec)**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type` caso já não esteja ativado.

        #. Selecionar todos os :bi:`Patient (Rec)` (**819**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os :bi:`Verification Outcomes` referentes a registros de :bi:`Patient (Rec)`:

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Model Name`

        #. Selecionar todas os :bi:`Verification Outcomes` referentes a "**clv.patient_rec**" (**822**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Global Logs**
--------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Global Logs**:

        :bmaroon:`IMPORTANTE:` **É possivel excluir somente 20.000 registros de cada vez! Repetir essa ação até que todos os registros tenham sido excluídos.**

        #. Acessar a *view* **Global Logs**:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Global Logs` » :bi:`Global Logs`

        #. Selecionar todos os :bi:`Global Logs` (**1079332**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-27a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-27a.sql

            gzip clvhealth_jcafb_2025_15_2024-09-27a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-27a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-27a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-27a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-09-27a.sql
.. index:: clvhealth_jcafb_2025_15_2024-09-27a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-09-27a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-27a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-27a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-09-27a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-27a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-27a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Excluir todos os **Undefined Document Items**
---------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Undefined Document Items**:

        #. Acessar a *view* **Document Items**:

            * Menu de acesso:

                * **Base** » **Configuration** » **Document** » **Items**

        #. Ativar o filtro **Agrupar por** » :bi:`Document Type` caso já não esteja ativado.

        :bmaroon:`IMPORTANTE:` **Excluir somente 5.000 registros de cada vez! Repetir essa ação até que todos os registros (Document Type não definidos) tenham sido excluídos.**

        #. Selecionar  (**5000**) :bi:`Indefinido` (de um total de **55364**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Excluir todos os **Undefined Lab Test Criteria**
------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Excluir todos os **Undefined Lab Test Criteria**:

        #. Acessar a *view* **Lab Test Criteria**:

            * Menu de acesso:

                * **Health** » **Configuration** » **Lab Test** » **Criteria**

        #. Ativar o filtro **Agrupar por** » :bi:`Lab Test Type` caso já não esteja ativado.

        :bmaroon:`IMPORTANTE:` **Excluir somente 5.000 registros de cada vez! Repetir essa ação até que todos os registros (Lab Test Type não definidos) tenham sido excluídos.**

        #. Selecionar  (**5000**) :bi:`Indefinido` (de um total de **23937**)

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-28a.sql

            gzip clvhealth_jcafb_2025_15_2024-09-28a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-28a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-28a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-28a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-09-28a.sql
.. index:: clvhealth_jcafb_2025_15_2024-09-28a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-09-28a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-09-28a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-28a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Atualisar **Patient Markers**
-----------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Patient Markers**:

        * Menu de acesso:
            * **Health** » **Configuration** » **Patient** » **Markers**

    #. Executar as atualizações necessárias dos **Patient Markers** para a JCAFB-2025:

        * Campanha Anemia (2025);

        * Campanha DHC (2025);

        * Familiar (2025);

        * Projeto (2025).

[tkl-odoo15-jcafb25-vm] Atualisar **Patient Tags**
--------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Patient Tags**:

        * Menu de acesso:
            * **Health** » **Configuration** » **Patient** » **Tags**

    #. Executar as atualizações necessárias dos **Patient Tags** para a JCAFB-2025:

        * Excluir Registro;

        * Paciente Duplicado;

        * Questionário QAN25 Ausente;

        * Questionário QDH25 Ausente;

        * Questionário QMD25 Ausente;

        * Questionário QSC25 Ausente;

        * Questionário QSF25 Ausente;

        * Questionário QSI25 Ausente;

        * Resultado de Exame EAN25 Ausente;

        * Resultado de Exame ECP25 Ausente;

        * Resultado de Exame EDH25 Ausente;

        * Resultado de Exame EEV25 Ausente;

        * Resultado de Exame EUR25 Ausente;

        * Verificado Ok;

        * Verificado com Alertas.

[tkl-odoo15-jcafb25-vm] Atualisar **Residence Categories**
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Residence Categories**:

        * Menu de acesso:
            * **Health** » **Configuration** » **Residence** » **Categories**

    #. Executar as atualizações necessárias dos **Residence Categories** para a JCAFB-2025:

        * Aldeia Indígena;

        * Centro;

        * Zona Rural;

        * Zona Urbana.

[tkl-odoo15-jcafb25-vm] Atualisar **Phases**
--------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Phases**:

        * Menu de acesso:
            * **Base** » **Configuration** » **Phases**

    #. Executar as atualizações necessárias dos **Phases** para a JCAFB-2025:

        * JCAFB-2025 (Primeiro ano do ciclo de Avaí).

[tkl-odoo15-jcafb25-vm] Atualisar **Events**
--------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Events**:

        * Menu de acesso:
            * **Base** » **Base** » **Events**

    #. Executar as atualizações necessárias dos **Events** para a JCAFB-2025:

        * Campanha Anemia (1) - 2025 (JCAFB-2025 - 13/01/2025 - 14:00h às 17:00h);

        * Campanha Anemia (2) - 2025 (JCAFB-2025 - 20/01/2025 - 14:00h às 17:00h);

        * Campanha DHC (1) - 2025 (JCAFB-2025 - 12/01/2025 - 07:30h às 11:30h);

        * Campanha DHC (2) - 2025 (JCAFB-2025 - 19/01/2025 - 07:30h às 11:30h;

        * Força Tarefa Anemia (1) - 2025 (JCAFB-2025 - 12/01/2025 - 14:00h às 18:00h);

        * Força Tarefa Anemia (2) - 2025 (JCAFB-2025 - 19/01/2025 - 14:00h às 18:00h);

        * Força Tarefa DHC (1) - 2025 (JCAFB-2025 - 13/01/2025 - 07:30h às 11:30h);.

        * Força Tarefa DHC (2) - 2025 (JCAFB-2025 - 12/01/2025 - 07:30h às 11:30h).

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-28b.sql

            gzip clvhealth_jcafb_2025_15_2024-09-28b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-09-28b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-28b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-09-28b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-09-28b.sql
.. index:: clvhealth_jcafb_2025_15_2024-09-28b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-09-28b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-09-28b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-09-28b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-09-28b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-09-28b.tar.gz

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
