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
JCAFB-2024-15 (Preparação pré Jornada [5])
==========================================

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-08-22c)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-08-22c.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-08-22c.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-08-22c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Configurar as permissões do usuário de referência da JCAFB-2024
---------------------------------------------------------------------------------------

    #. Configurar as permissões do usuário de referência:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Users*:

            * Menu de acesso:

                * :bi:`Configurações` » :bi:`Usuários e Empresas` » :bi:`Usuários`

        #. Selecionar o usuário de referência.

        #. Configurar as permissões:

            * User Type

                * Tipos de usuário: **Utilizador Interno**

            * Marketing

                * Inquéritos: **Administrador**

            * *Human Resources*
            
                * Funcionários: **Administrador**

            * *Administration*
            
                * Administração:

            * *Other*:

                * *Employee*: :bi:`Manager (Employee)`
                * *Event*: :bi:`Manager (Event)`
                * *Export*: :bi:`Manager (Export)`
                * *External Sync*:
                * *File System*: :bi:`Manager (File System)`
                * *Global Tag*: :bi:`Manager (Global Tag)`
                * *Patient (Aux)*: :bi:`Manager (Patient (Aux))`
                * *Patient (Rec)*: :bi:`Manager (Patient (Rec))`
                * *Patient*: :bi:`Manager (Patient)`
                * *Phase*: :bi:`User (Phase)`
                * *Pool*: :bi:`User (Pool)`
                * *Processing*:
                * *Residence*: :bi:`Manager (Residence)`
                * *Set*: :bi:`Manager (Set)`
                * *Summary*: :bi:`Manager (Summary)`
                * *Survey*:  :bi:`Manager (Survey)`
                * *Verification*: :bi:`Manager (Verification)`

            * *Base*:

                * :bi:`Log User (Base)`,
                * :bi:`Manager (Base)`,
                * :bi:`Register User (Base)`,
                * :bi:`Super User (Base)`,
                * :bi:`User (Base)`,

            * *Document*:

                * :bi:`Manager (Document)`,
                * :bi:`User (Document)`,

            * *Lab Test*:

                * :bi:`Manager (Lab Test)`,
                * :bi:`User (Lab Test)`,

            * *Technical*:

                * **Acesso a endereços privados**
                * **Acesso para exportar recurso**
                * **Mail Template Editor**

            * *Extra Rights*:

                * **Criação de Contato**

[tkl-odoo15-jcafb24-vm] Atualizar as permissões dos Coordenadores da JCAFB-2024
-------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação *Employee User Groups Update* para os Coordenadores da JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Funcionários**:

            * Menu de acesso:

                * **Funcionários** » **Funcionários** » **Funcionários**

        #. Selecionar os **Coordenadores** da JCAFB-2024

        #. Executar a Ação "**Employee User Groups Update**":

            #. Selecionar o :bi:`Reference Employee`: Usuário de referência (selecionado no ítem anterior).

            #. Selecionar o parâmetro :bi:`Access Rights:` » :bi:`Set`.

            #. Precionar o botão :bi:`Get Reference Employee Access Rights`.

            #. Utilize o botão :bi:`Update` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-09-20a)
-------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-09-20a.sql

            gzip clvhealth_jcafb_2024_15_2023-09-20a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-09-20a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-09-20a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-09-20a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-09-20a.sql
.. index:: clvhealth_jcafb_2024_15_2023-09-20a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-09-20a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-09-20a)
-----------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb24-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            ssh tkl-odoo15-jcafb24-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb24-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2024_15_2023-09-20a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-09-20a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-09-20a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb24-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo15-jcafb24-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[EAN24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EAN23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EAN23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EAN24]**
                * *New Survey Code*: **EAN24**
                * *New Survey Description*: **<p>JCAFB 2024 - Exames para detecção de Anemia</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[ECP24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[ECP23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[ECP23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[ECP24]**
                * *New Survey Code*: **ECP24**
                * *New Survey Description*: **<p>JCAFB 2024 - Laboratório - Parasitologia</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[EDH24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EDH23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EDH23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EDH24]**
                * *New Survey Code*: **EDH24**
                * *New Survey Description*: **<p>JCAFB 2024 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[EEV24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EEV21]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EEV21]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EEV24]**
                * *New Survey Code*: **EEV24**
                * *New Survey Description*: **<p>JCAFB 2024 - Laboratório - Pesquisa de Enterobius vermicularis</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[EUR24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EUR23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EUR23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EUR24]**
                * *New Survey Code*: **EUR24**
                * *New Survey Description*: **<p>JCAFB 2024 - Laboratório - Urinálise</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QAN24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QAN23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QAN23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QAN24]**
                * *New Survey Code*: **QAN24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário para Detecção de Anemia</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QDH24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QDH23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QDH23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QDH24]**
                * *New Survey Code*: **QDH24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QMD24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QMD23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QMD23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QMD24]**
                * *New Survey Code*: **QMD24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário - Medicamentos</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QSC24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSC23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSC23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSC24]**
                * *New Survey Code*: **QSC24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário Socioeconômico Individual (Crianças)</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QSF24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSF23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSF23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSF24]**
                * *New Survey Code*: **QSF24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário Socioeconômico Familiar</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar a Pesquisa "[QSI24]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSI23]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSI23]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSI24]**
                * *New Survey Code*: **QSI24**
                * *New Survey Description*: **<p>JCAFB 2024 - Questionário Socioeconômico Individual (Idosos)</p>**
                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

.. toctree::   :maxdepth: 2
