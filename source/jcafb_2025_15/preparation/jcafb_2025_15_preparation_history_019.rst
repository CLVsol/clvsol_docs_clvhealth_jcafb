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

===========================================
JCAFB-2025-15 (Preparação pré Jornada [10])
===========================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-04a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-08-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-04a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Atualisar a Pesquisa "[EEV24]"
------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Pesquisas**:

        * Menu de acesso:
            * **Pesquisas** » **Pesquisas**

    #. Abrir o Formulário da Pesquisa "**[EEV24]**".

    #. Executar as atualizações necessárias para permitir a cópia da Pesquisa "[EEV24] para a JCAFB-2025:

        * Excluir as Sugestões de Respostas de "Múltipla escolha: múltiplas respostas" desnecessárias para a Questão "2.3. Examinador:".

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[EAN25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EAN24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EAN24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EAN25]**
                * *New Survey Code*: **EAN25**
                * *New Survey Description*: **<p>JCAFB 2025 - Exames para detecção de Anemia</p>**
                * *New Access Token*: **ean25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[ECP25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[ECP24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[ECP24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[ECP25]**
                * *New Survey Code*: **ECP25**
                * *New Survey Description*: **<p>JCAFB 2025 - Laboratório - Parasitologia</p>**
                * *New Access Token*: **ecp25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[EDH25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EDH24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EDH24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EDH25]**
                * *New Survey Code*: **EDH25**
                * *New Survey Description*: **<p>JCAFB 2025 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *New Access Token*: **edh25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[EEV25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EEV24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EEV24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EEV25]**
                * *New Survey Code*: **EEV25**
                * *New Survey Description*: **<p>JCAFB 2025 - Laboratório - Pesquisa de Enterobius vermicularis</p>**
                * *New Access Token*: **eev25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[EUR25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EUR24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EUR24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EUR25]**
                * *New Survey Code*: **EUR25**
                * *New Survey Description*: **<p>JCAFB 2025 - Laboratório - Urinálise</p>**
                * *New Access Token*: **eur25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QAN25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QAN24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QAN24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QAN25]**
                * *New Survey Code*: **QAN25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário para Detecção de Anemia</p>**
                * *New Access Token*: **qan25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QDH25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QDH24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QDH24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QDH25]**
                * *New Survey Code*: **QDH25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *New Access Token*: **qdh24**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QMD25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QMD24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QMD24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QMD25]**
                * *New Survey Code*: **QMD25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário - Medicamentos</p>**
                * *New Access Token*: **qmd25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QSC25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSC24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSC24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSC25]**
                * *New Survey Code*: **QSC25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário Socioeconômico Individual (Crianças)</p>**
                * *New Access Token*: **qsc25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QSF25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSF24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSF24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSF25]**
                * *New Survey Code*: **QSF25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário Socioeconômico Familiar</p>**
                * *New Access Token*: **qsf25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar a Pesquisa "[QSI25]"
--------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSI24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSI24]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSI25]**
                * *New Survey Code*: **QSI25**
                * *New Survey Description*: **<p>JCAFB 2025 - Questionário Socioeconômico Individual (Idosos)</p>**
                * *New Access Token*: **qsi25**
                * *Phase*: **JCAFB-2025**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-12a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-08-12a.sql

            gzip clvhealth_jcafb_2025_15_2024-08-12a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-08-12a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-08-12a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-08-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-08-12a.sql
.. index:: clvhealth_jcafb_2025_15_2024-08-12a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-08-12a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-12a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-08-12a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-08-12a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-08-12a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-08-12a.tar.gz

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

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Atualisar a Pesquisa "[QAN25]"
------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. Acessar a *View* **Pesquisas**:

        * Menu de acesso:
            * **Pesquisas** » **Pesquisas**

    #. Abrir o Formulário da Pesquisa "**[QAN25]**".

    #. Executar as atualizações que forem necessárias.

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**ECP25**"
--------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**ECP25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EEV25**"
--------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EEV25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EEV25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EUR25**"
--------------------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EUR25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR25**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Atualizar os "*Templates File Names*" de todas os Tipos de Exames
-----------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Lista de Tipos de Exames:

        * **EAN25**:

            #. **Template File Name (Result)**: "Resultado_EAN25_template.xls"

            #. **Template File Name (Report)**: "Laudo_EAN25_template.xls"

        * **EDH25**:

            #. **Template File Name (Result)**: "Resultado_EDH25_template.xls"

            #. **Template File Name (Report)**: "Laudo_EDH25_template.xls"

        * **ECP25**:

            #. **Template File Name (Result)**: "Resultado_ECP25_template.xls"

            #. **Template File Name (Report)**: "Laudo_ECP25_template.xls"

        * **EEV25**:

            #. **Template File Name (Result)**: "Resultado_EEV25_template.xls"

            #. **Template File Name (Report)**: "Laudo_EEV25_template.xls"

        * **EUR25**:

            #. **Template File Name (Result)**: "Resultado_EUR25_template.xls"

            #. **Template File Name (Report)**: "Laudo_EUR25_template.xls"

:red:`(Not Used)` [tkl-odoo15-jcafb25-vm] Atualizar os "*Lab Test Export XLS Parameter*" dos Tipos de Exames
------------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Lista de Tipos de Exames:

        * **EAN25**:

            * *Result*
            
            * *Report*

        * **ECP25**:

            * *Result*
            
            * *Report*

        * **EEV25**:

            * *Result*
            
            * *Report*

.. toctree::   :maxdepth: 2
