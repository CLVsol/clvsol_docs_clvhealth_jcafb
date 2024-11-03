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
JCAFB-2025-15 (Preparação pré Jornada II [2])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-15a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-10-15a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-15a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-15a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-31a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-31a.sql

            gzip clvhealth_jcafb_2025_15_2024-10-31a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-31a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-31a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-31a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-10-31a.sql
.. index:: clvhealth_jcafb_2025_15_2024-10-31a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-10-31a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-31a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-10-31a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-31a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QSF25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSF25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSF24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSF25**
                * *New Document Type Code*: **QSF25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário Socioeconômico Familiar (Crianças e Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSF25**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSF25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QSC25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSC25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSC24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSC25**
                * *New Document Type Code*: **QSC25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário Socioeconômico Individual (Crianças)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSC25**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSC25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QSI25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSI25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSI24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSI25**
                * *New Document Type Code*: **QSI25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário Socioeconômico Individual (Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSI25**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSI25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QMD25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QMD25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QMD24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QMD25**
                * *New Document Type Code*: **QMD25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário - Medicamentos**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QMD25**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QMD25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Executar a Ação *Document Type Items Set Up* para *Document Types* dos Questionários de Campo
---------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Items Set Up` para os :bi:`Document Types` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os :bi:`Document Types` dos Questionários de Campo com: :bi:`Phase` = "**JCAFB-2025**"

        #. Executar a Ação ":bi:`Document Type Items Set Up`":

            #. Utilize o botão :bi:`Items Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QAN25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QAN25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QAN24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QAN25**
                * *New Document Type Code*: **QAN25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário para detecção de Anemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QAN25**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QAN25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Criar o *Document Type* "[QDH25]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QDH25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QDH24]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QDH25**
                * *New Document Type Code*: **QDH25**
                * *New Document Type Description*: **JCAFB 2025 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QDH25**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QDH25]**
            * *Phase*: **JCAFB-2025**

[tkl-odoo15-jcafb25-vm] Criar o *Lab Test Type* "**EAN25**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EAN24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EAN24**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EAN25**
                * *New Lab Test Type Code*: **EAN25**
                * *New Lab Test Type Description*: **JCAFB 2025 - Exames - Detecção de Anemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EAN25**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EAN25]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2025**".

[tkl-odoo15-jcafb25-vm] Criar o *Lab Test Type* "**ECP25**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**ECP24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP24**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **ECP25**
                * *New Lab Test Type Code*: **ECP25**
                * *New Lab Test Type Description*: **JCAFB 2025 - Laboratório - Parasitologia**
                * *Template File Name (Result)*: **Resultado_ECP25_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_ECP25_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**ECP25**".

            #. Atualizar o campo :bi:`Survey Type`: "**[ECP25]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2025**".

[tkl-odoo15-jcafb25-vm] Criar o *Lab Test Type* "**EDH25**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EDH24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EDH24**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EDH25**
                * *New Lab Test Type Code*: **EDH25**
                * *New Lab Test Type Description*: **JCAFB 2025 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EDH25**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EDH25]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2025**".

[tkl-odoo15-jcafb25-vm] Criar o *Lab Test Type* "**EEV25**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EEV24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EEV24**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **EEV25**
                * *New Lab Test Type Code*: **EEV25**
                * *New Lab Test Type Description*: **JCAFB 2025 - Laboratório - Urinálise**
                * *Template File Name (Result)*: **Resultado_EEV25_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_EEV25_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EEV25**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EEV25]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2025**".

[tkl-odoo15-jcafb25-vm] Criar o *Lab Test Type* "**EUR25**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EUR24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR24**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **EUR25**
                * *New Lab Test Type Code*: **EUR25**
                * *New Lab Test Type Description*: **JCAFB 2025 - Laboratório - Urinálise**
                * *Template File Name (Result)*: **Resultado_EUR25_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_EUR25_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EUR25**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EUR25]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2025**".

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-31b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-31b.sql

            gzip clvhealth_jcafb_2025_15_2024-10-31b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-10-31b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-31b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-10-31b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-10-31b.sql
.. index:: clvhealth_jcafb_2025_15_2024-10-31b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-10-31b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-10-31b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-10-31b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-10-31b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-10-31b.tar.gz

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

tkl-odoo15-jcafb25-vm] Executar a Ação *Document Type Items Set Up* para *Document Types* dos Questionários de Campanha
-----------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Document Type Items Set Up` para os :bi:`Document Types` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os :bi:`Document Types` dos Questionários de Campanha com: :bi:`Phase` = "**JCAFB-2025**"

        #. Executar a Ação ":bi:`Document Type Items Set Up`":

            #. Utilize o botão :bi:`Items Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EAN25**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EAN25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EAN25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**ECP25**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**ECP25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EDH25**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EDH25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EDH25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EEV25**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EEV25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EEV25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EUR25**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EUR25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-02a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-02a.sql

            gzip clvhealth_jcafb_2025_15_2024-11-02a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-02a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-02a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-02a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-02a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-11-02a.sql
.. index:: clvhealth_jcafb_2025_15_2024-11-02a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-11-02a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-02a

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

.. toctree::   :maxdepth: 2
