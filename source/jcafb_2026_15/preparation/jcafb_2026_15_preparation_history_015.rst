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
JCAFB-2026-15 (Preparação pré Jornada [6])
==========================================

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-09b)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-09b.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-09b.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-09b.tar.gz

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

[tkl-odoo15-jcafb26-vm] Excluir a *Phase* de todas as Residências da JCAFB-2025
-------------------------------------------------------------------------------

    * (366 Residências)

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11a)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11a.sql

            gzip clvhealth_jcafb_2026_15_2025-07-11a.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11a.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-11a.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11a

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11a)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-11a.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-11a.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11a.tar.gz

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

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[EAN26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EAN25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EAN25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EAN26]**
                * *New Survey Code*: **EAN26**
                * *New Survey Description*: **<p>JCAFB 2026 - Exames para detecção de Anemia</p>**
                * *New Access Token*: **ean26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[ECP26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[ECP25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[ECP25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[ECP26]**
                * *New Survey Code*: **ECP26**
                * *New Survey Description*: **<p>JCAFB 2026 - Laboratório - Parasitologia</p>**
                * *New Access Token*: **ecp26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[EDH26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EDH25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EDH25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EDH26]**
                * *New Survey Code*: **EDH26**
                * *New Survey Description*: **<p>JCAFB 2026 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *New Access Token*: **edh26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[EEV26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EEV25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EEV25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EEV26]**
                * *New Survey Code*: **EEV26**
                * *New Survey Description*: **<p>JCAFB 2026 - Laboratório - Pesquisa de Enterobius vermicularis</p>**
                * *New Access Token*: **eev26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[EUR26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[EUR25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[EUR25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[EUR26]**
                * *New Survey Code*: **EUR26**
                * *New Survey Description*: **<p>JCAFB 2026 - Laboratório - Urinálise</p>**
                * *New Access Token*: **eur26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QAN26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QAN25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QAN25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QAN26]**
                * *New Survey Code*: **QAN26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário para Detecção de Anemia</p>**
                * *New Access Token*: **qan26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QDH26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QDH25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QDH25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QDH26]**
                * *New Survey Code*: **QDH26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia</p>**
                * *New Access Token*: **qdh25**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QMD26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QMD25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QMD25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QMD26]**
                * *New Survey Code*: **QMD26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário - Medicamentos</p>**
                * *New Access Token*: **qmd26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QSC26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSC25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSC25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSC26]**
                * *New Survey Code*: **QSC26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário Socioeconômico Individual (Crianças)</p>**
                * *New Access Token*: **qsc26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QSF26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSF25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSF25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSF26]**
                * *New Survey Code*: **QSF26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário Socioeconômico Familiar</p>**
                * *New Access Token*: **qsf26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar a Pesquisa "[QSI26]"
--------------------------------------------------

    #. Executar a Ação :bi:`Survey Duplicate` para a Pesquisa "**[QSI25]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* **Pesquisas**:

            * Menu de acesso:
                * **Pesquisas** » **Pesquisas**

        #. Abrir o Formulário da Pesquisa "**[QSI25]**".

        #. Executar a Ação ":bi:`Survey Duplicate`":

            * Parâmetros utilizados:
                * *New Survey Title*: **[QSI26]**
                * *New Survey Code*: **QSI26**
                * *New Survey Description*: **<p>JCAFB 2026 - Questionário Socioeconômico Individual (Idosos)</p>**
                * *New Access Token*: **qsi26**
                * *Phase*: **JCAFB-2026**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11b)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11b.sql

            gzip clvhealth_jcafb_2026_15_2025-07-11b.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11b.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-11b.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-11b.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-11b
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11b

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11b)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-11b.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-11b.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11b.tar.gz

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

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Type* "**EAN26**"
-----------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EAN25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EAN25**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EAN26**
                * *New Lab Test Type Code*: **EAN26**
                * *New Lab Test Type Description*: **JCAFB 2026 - Exames - Detecção de Anemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EAN26**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EAN26]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2026**".

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Type* "**ECP26**"
-----------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**ECP25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP25**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **ECP26**
                * *New Lab Test Type Code*: **ECP26**
                * *New Lab Test Type Description*: **JCAFB 2026 - Laboratório - Parasitologia**
                * *Template File Name (Result)*: **Resultado_ECP26_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_ECP26_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**ECP26**".

            #. Atualizar o campo :bi:`Survey Type`: "**[ECP26]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2026**".

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Type* "**EDH26**"
-----------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EDH25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EDH25**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EDH26**
                * *New Lab Test Type Code*: **EDH26**
                * *New Lab Test Type Description*: **JCAFB 2026 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EDH26**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EDH26]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2026**".

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Type* "**EEV26**"
-----------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EEV25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EEV25**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **EEV26**
                * *New Lab Test Type Code*: **EEV26**
                * *New Lab Test Type Description*: **JCAFB 2026 - Laboratório - Urinálise**
                * *Template File Name (Result)*: **Resultado_EEV26_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_EEV26_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EEV26**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EEV26]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2026**".

[tkl-odoo15-jcafb26-vm] Criar o *Lab Test Type* "**EUR26**"
-----------------------------------------------------------

    #. Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EUR25**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR25**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **EUR26**
                * *New Lab Test Type Code*: **EUR26**
                * *New Lab Test Type Description*: **JCAFB 2026 - Laboratório - Urinálise**
                * *Template File Name (Result)*: **Resultado_EUR26_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_EUR26_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EUR26**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EUR26]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2026**".

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QAN26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QAN26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QAN25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QAN26**
                * *New Document Type Code*: **QAN26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário para detecção de Anemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QAN26**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QAN26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QDH26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QDH26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QDH25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QDH26**
                * *New Document Type Code*: **QDH26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QDH26**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QDH26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QMD26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QMD26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QMD25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QMD26**
                * *New Document Type Code*: **QMD26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário - Medicamentos**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QMD26**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QMD26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QSC26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSC26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSC25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSC26**
                * *New Document Type Code*: **QSC26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário Socioeconômico Individual (Crianças)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSC26**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSC26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QSF26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSF26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSF25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSF26**
                * *New Document Type Code*: **QSF26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário Socioeconômico Familiar (Crianças e Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSF26**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSF26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar o *Document Type* "[QSI26]"
---------------------------------------------------------

    #. Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSI26]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb26-vm <https://tkl-odoo15-jcafb26-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSI25]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSI26**
                * *New Document Type Code*: **QSI26**
                * *New Document Type Description*: **JCAFB 2026 - Questionário Socioeconômico Individual (Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSI26**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSI26]**
            * *Phase*: **JCAFB-2026**

[tkl-odoo15-jcafb26-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11c)
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
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11c.sql

            gzip clvhealth_jcafb_2026_15_2025-07-11c.sql
            pg_dump clvhealth_jcafb_2026_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2026_15_2025-07-11c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz clvhealth_jcafb_2026_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11c.sql
        * /opt/odoo/clvhealth_jcafb_2026_15_2025-07-11c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz

.. index:: clvhealth_jcafb_2026_15_2025-07-11c.sql
.. index:: clvhealth_jcafb_2026_15_2025-07-11c.sql.gz
.. index:: filestore_clvhealth_jcafb_2026_15_2025-07-11c
.. index:: clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11c

[tkl-odoo15-jcafb26-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2026-15* (2025-07-11c)
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
            # gzip -d clvhealth_jcafb_2026_15_2025-07-11c.sql.gz

            dropdb -i clvhealth_jcafb_2026_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2026_15
            psql -f clvhealth_jcafb_2026_15_2025-07-11c.sql -d clvhealth_jcafb_2026_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2026_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2026_15_2025-07-11c.tar.gz

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
