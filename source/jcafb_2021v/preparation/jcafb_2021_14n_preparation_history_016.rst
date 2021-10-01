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

=========================================
JCAFB-2021v-14n (Tratamento de Surveys 1)
=========================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-12a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-12a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-12a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-12a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Trascrição das Respostas de Termos de Consentimento via URL genérica
--------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21n-vm] usando uma das URLs:

        * [TAA21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para a Análise Físico-Química e Microbiológica da Água: `http://tkl-odoo14-jcafb21n-vm/survey/start/taa21 <http://tkl-odoo14-jcafb21n-vm/survey/start/taa21>`_

        * [TAN21] JCAFB 2021 - Termo de Consentimento para a Campanha de Detecção de Anemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/tan21 <http://tkl-odoo14-jcafb21n-vm/survey/start/tan21>`_

        * [TCR21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos: `http://tkl-odoo14-jcafb21n-vm/survey/start/tcr21 <http://tkl-odoo14-jcafb21n-vm/survey/start/tcr21>`_

        * [TDH21] JCAFB 2021 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/tdh21 <http://tkl-odoo14-jcafb21n-vm/survey/start/tdh21>`_

        * [TID21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico: `http://tkl-odoo14-jcafb21n-vm/survey/start/tid21 <http://tkl-odoo14-jcafb21n-vm/survey/start/tid21>`_

    #. Iniciar a Pesquisa.

Trascrição das Respostas de Questionários via URL genérica
----------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21n-vm] usando uma das URLs:

        * [QAN21] JCAFB 2021 - Questionário para detecção de Anemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/qan21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qan21>`_

        * [QDH21] JCAFB 2021 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/qdh21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qdh21>`_

        * [QMD21] JCAFB 2021 - Questionário - Medicamentos: `http://tkl-odoo14-jcafb21n-vm/survey/start/qmd21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qmd21>`_

        * [QSC21] JCAFB 2021 - Questionário Socioeconômico Individual (Crianças): `http://tkl-odoo14-jcafb21n-vm/survey/start/qsc21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qsc21>`_

        * [QSF21] JCAFB 2021 - Questionário Socioeconômico Familiar (Crianças e Idosos): `http://tkl-odoo14-jcafb21n-vm/survey/start/qsf21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qsf21>`_

        * [QSI21] JCAFB 2021 - Questionário Socioeconômico Individual (Idosos): `http://tkl-odoo14-jcafb21n-vm/survey/start/qsi21 <http://tkl-odoo14-jcafb21n-vm/survey/start/qsi21>`_

    #. Iniciar a Pesquisa.

Trascrição das Respostas de Questionários ou Termos de Consentimento via Documentos associados
----------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Acessar a *View* *Documents*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` ou qualquer outro para facilitar a procura pelo Documento desejado.

    #. Selecionar e abrir o Documento desejado.

    #. Executar a Ação ":bi:`Document Set Survey User Input`":

        #. Utilize o botão :bi:`Set Survey User Input` para executar a Ação.

    #. Acessar o *link* apresentado no campo ":bi:`Survey URL`".

    #. Iniciar a Pesquisa.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-14a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-14a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-09-14a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-14a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-14a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-09-14a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-09-14a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-09-14a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-14a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-14a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-14a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-14a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-14a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_document_jcafb
        * clv_lab_teste_jcafb
        * clv_survey

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_teste_jcafb

                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_survey

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Atualizar o *Lab Test Types* dos *Lab Test Types* do Projeto JCAFB-2021v
----------------------------------------------------------------------------------------

    Parâmetros utilizados:

        * **EAN21**: **[EAN21]**

        * **EDH21**: **[EDH21]**.

        * **EAA21**: **[EAA21]**.

        * **ECP21**: **[ECP21]**.

        * **EEV21**: **[EEV21]**.

        * **EUR21**: **[EUR21]**.

    #. [tkl-odoo14-jcafb21n-vm] Atualizar o *Lab Test Types* dos *Lab Test Types* do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Editar todos os *Lab Test Types* com: :bi:`Phase` = "**JCAFB-2021v**".

Executar a Ação *Lab Test Request Receive* para recebimento de amostras para Exame
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Lab Test Request Receive` para um :bi:`Lab Test Request` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Pesquisar pelo **Código** do :bi:`Lab Test Request` desejado.

        #. Executar a Ação ":bi:`Lab Test Request Receive`" para o registro encontrado:

            * Parâmetros utilizados:

                * Aceitar todos os parâmetros apresentados

            #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

:red:`(Não Utilizado)` Trascrição de Respostas de Folhas de Resultados de Exames via URL genérica
-------------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21n-vm] usando uma das URLs:

        * [EAA21] JCAFB 2021 - Laboratório - Análise de Água: `http://tkl-odoo14-jcafb21n-vm/survey/start/eaa21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eaa21>`_

        * [EAN21] JCAFB 2021 - Exames para detecção de Anemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/ean21 <http://tkl-odoo14-jcafb21n-vm/survey/start/ean21>`_

        * [ECP21] JCAFB 2021 - Laboratório - Parasitologia: `http://tkl-odoo14-jcafb21n-vm/survey/start/ecp21 <http://tkl-odoo14-jcafb21n-vm/survey/start/ecp21>`_

        * [EDH21] JCAFB 2021- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21n-vm/survey/start/edh21 <http://tkl-odoo14-jcafb21n-vm/survey/start/edh21>`_

        * [EEV21] JCAFB 2021 -  Laboratório - Pesquisa de Enterobius vermicularis: `http://tkl-odoo14-jcafb21n-vm/survey/start/eev21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eev21>`_

        * [EUR21] JCAFB 2021 - Laboratório - Urinálise: `http://tkl-odoo14-jcafb21n-vm/survey/start/eur21 <http://tkl-odoo14-jcafb21n-vm/survey/start/eur21>`_

    #. Iniciar a Pesquisa.

Trascrição de Respostas de Folhas de Resultados via Resultados de Exame associados
----------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

    #. Acessar a *View* *Lab Test Results*:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Lab Test Type` ou qualquer outro para facilitar a procura pelo Resultado de Exame desejado.

    #. Selecionar e abrir o Resultado de Exame desejado.

    #. Executar a Ação ":bi:`Lab Test Result Set Survey User Input`":

        #. Utilize o botão :bi:`Set Survey User Input` para executar a Ação.

    #. Acessar o *link* apresentado no campo ":bi:`Survey URL`".

    #. Iniciar a Pesquisa.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-16a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-16a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-09-16a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-09-16a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-16a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-09-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-09-16a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-09-16a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-09-16a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-16a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-09-16a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-09-16a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-09-16a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-09-16a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_lab_test_jcafb

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_lab_test_sync_jcafb

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test_sync_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
----------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_lab_test_verification_jcafb

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_14" -m clv_lab_test_verification_jcafb
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(**)` Atualizar o(s) módulo(s) [ver lista]
----------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Lista de Módulos:

        * clv_survey

    #. [tkl-odoo14-jcafb21n-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21n-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21n-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21n-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_survey

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21n-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

:borange:`(Opcional)` Executar a Ação *Survey User Input Refresh* para os Documentos
------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Refresh` para os :bi:`Documentos` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document State`

        #. Pesquisar Pesquisa *for* **Has User Input**

        #. Selecionar todos os :bi:`Documentos` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Document State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Refresh`":

            #. Utilize o botão :bi:`Survey User Input Refresh` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-10-01a)
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-10-01a.sql

            gzip clvhealth_jcafb_2021v_14n_2021-10-01a.sql
            pg_dump clvhealth_jcafb_2021v_14n -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14n_2021-10-01a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz clvhealth_jcafb_2021v_14n

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-10-01a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14n_2021-10-01a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz

.. index:: clvhealth_jcafb_2021v_14n_2021-10-01a.sql
.. index:: clvhealth_jcafb_2021v_14n_2021-10-01a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14n_2021-10-01a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-10-01a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14n* (2021-10-01a)
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21n-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            ssh tkl-odoo14-jcafb21n-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21n-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14n_2021-10-01a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14n

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14n
            psql -f clvhealth_jcafb_2021v_14n_2021-10-01a.sql -d clvhealth_jcafb_2021v_14n -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14n
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14n_2021-10-01a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21n-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21n-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21n-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21n-vm**".

        #. Salvar o registro editado.

Executar a Ação *Survey User Input Validate* para os Documentos
---------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Validate` para os :bi:`Documentos` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document State`

        #. Pesquisar Pesquisa *for* **Has User Input**

        #. Selecionar todos os :bi:`Documentos` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Document State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Validate`":

            * Parâmetros utilizados:

                * *Survey User Input Refresh Execute*: **marcado**

            #. Utilize o botão :bi:`Survey User Input Validate` para executar a Ação.

:borange:`(Opcional)` Executar a Ação *Survey User Input Refresh* para os Resultados de Exames
----------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Refresh` para os :bi:`Resultados de Exames` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Result State`

        #. Pesquisar Pesquisa *for* **Has User Input**

        #. Selecionar todos os :bi:`Resultados de Exames` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Result State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Refresh`":

            #. Utilize o botão :bi:`Survey User Input Refresh` para executar a Ação.

Executar a Ação *Survey User Input Validate* para os Resultados de Exames
-------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Validate` para os :bi:`Resultados de Exames` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Lab Test Results*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Results`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Result State`

        #. Pesquisar Pesquisa *for* **Has User Input**

        #. Selecionar todos os :bi:`Resultados de Exames` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Result State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Validate`":

            * Parâmetros utilizados:

                * *Survey User Input Refresh Execute*: **marcado**

            #. Utilize o botão :bi:`Survey User Input Validate` para executar a Ação.

:borange:`(Opcional)` Executar a Ação *Survey User Input Refresh* para as transcrições de Questionários
-------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Refresh` para as :bi:`Participations` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Participations*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

        #. Ativar o filtro **Agrupar por** » :bi:`Status` » :bi:`Survey User Input State`

        #. Pesquisar Pesquisa *for* **21**

        #. Selecionar todas as :bi:`Participations` com: :bi:`Status` = "**Concluído**" » :bi:`Survey User Input State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Refresh`":

            #. Utilize o botão :bi:`Survey User Input Refresh` para executar a Ação.

Executar a Ação *Survey User Input Validate* para as transcrições de Questionários
----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Survey User Input Validate` para as :bi:`Participations` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Participations*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

        #. Ativar o filtro **Agrupar por** » :bi:`Status` » :bi:`Survey User Input State`

        #. Pesquisar Pesquisa *for* **21**

        #. Selecionar todas as :bi:`Participations` com: :bi:`Status` = "**Concluído**" » :bi:`Survey User Input State` = ":bi:`Checked`"

        #. Executar a Ação ":bi:`Survey User Input Validate`":

            * Parâmetros utilizados:

                * *Survey User Input Refresh Execute*: **marcado**

            #. Utilize o botão :bi:`Survey User Input Validate` para executar a Ação.

.. toctree::   :maxdepth: 2
