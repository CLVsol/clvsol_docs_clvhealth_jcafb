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
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-04-28a)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-04-28a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-04-28a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-04-28a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

:borange:`(**)` Atualizar o(s) módulo(s) [clv_document, clv_document_jcafb]
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_document
        * clv_document_jcafb

    #. [tkl-odoo14-jcafb21-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo14-jcafb21-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                ssh tkl-odoo14-jcafb21-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo14-jcafb21-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 2)
                #

                ssh tkl-odoo14-jcafb21-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_document
            
        #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

            ::

                # ***** tkl-odoo14-jcafb21-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Trascrição das Respostas de um Termo de Consentimento via URL genérica
----------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21-vm] usando uma das URLs:

        * [TAA21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para a Análise Físico-Química e Microbiológica da Água: `http://tkl-odoo14-jcafb21-vm/survey/start/taa21 <http://tkl-odoo14-jcafb21-vm/survey/start/taa21>`_

        * [TAN21] JCAFB 2021 - Termo de Consentimento para a Campanha de Detecção de Anemia: `http://tkl-odoo14-jcafb21-vm/survey/start/tan21 <http://tkl-odoo14-jcafb21-vm/survey/start/tan21>`_

        * [TCR21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames Coproparasitológicos: `http://tkl-odoo14-jcafb21-vm/survey/start/tcr21 <http://tkl-odoo14-jcafb21-vm/survey/start/tcr21>`_

        * [TDH21] JCAFB 2021 - Termo de Consentimento para a Campanha de Detecão de Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21-vm/survey/start/tdh21 <http://tkl-odoo14-jcafb21-vm/survey/start/tdh21>`_

        * [TID21] JCAFB 2021 - Termo de Consentimento Livre e Esclarecido para Realização de Questionário Socioeconômico e de Exames de Urina e Coproparasitológico: `http://tkl-odoo14-jcafb21-vm/survey/start/tid21 <http://tkl-odoo14-jcafb21-vm/survey/start/tid21>`_

    #. Iniciar a Pesquisa.

Trascrição das Respostas de um Questionário via URL genérica
------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21-vm] usando uma das URLs:

        * [QAN21] JCAFB 2021 - Questionário para detecção de Anemia: `http://tkl-odoo14-jcafb21-vm/survey/start/qan21 <http://tkl-odoo14-jcafb21-vm/survey/start/qan21>`_

        * [QDH21] JCAFB 2021 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21-vm/survey/start/qdh21 <http://tkl-odoo14-jcafb21-vm/survey/start/qdh21>`_

        * [QMD21] JCAFB 2021 - Questionário - Medicamentos: `http://tkl-odoo14-jcafb21-vm/survey/start/qmd21 <http://tkl-odoo14-jcafb21-vm/survey/start/qmd21>`_

        * [QSC21] JCAFB 2021 - Questionário Socioeconômico Individual (Crianças): `http://tkl-odoo14-jcafb21-vm/survey/start/qsc21 <http://tkl-odoo14-jcafb21-vm/survey/start/qsc21>`_

        * [QSF21] JCAFB 2021 - Questionário Socioeconômico Familiar (Crianças e Idosos): `http://tkl-odoo14-jcafb21-vm/survey/start/qsf21 <http://tkl-odoo14-jcafb21-vm/survey/start/qsf21>`_

        * [QSI21] JCAFB 2021 - Questionário Socioeconômico Individual (Idosos): `http://tkl-odoo14-jcafb21-vm/survey/start/qsi21 <http://tkl-odoo14-jcafb21-vm/survey/start/qsi21>`_

    #. Iniciar a Pesquisa.

Trascrição das Respostas de um Questionário ou Termo de Consentimento via Documento associado
---------------------------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* *Documents*:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` ou qualquer outro para facilitar a procura pelo(s) Documento(s) desejado(s).

    #. Selecionar os Documentos desejados.

    #. Executar a Ação ":bi:`Document Set Survey User Input`":

        #. Utilize o botão :bi:`Set Survey User Input` para executar a Ação.

    #. Acessar o *link* apresentado no campo ":bi:`Survey URL`".

    #. Iniciar a Pesquisa.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-11a)
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-11a.sql

            gzip clvhealth_jcafb_2021v_14_2021-05-11a.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-11a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-11a.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-11a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-05-11a.sql
.. index:: clvhealth_jcafb_2021v_14_2021-05-11a.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-05-11a
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-11a

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-11a)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-05-11a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-05-11a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-11a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Executar a Ação *Survey User Input Refresh* para as transcrições de Questionários do Projeto JCAFB-2021v
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Survey User Input Refresh` para as :bi:`Participations` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Participations*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

        #. Ativar o filtro **Agrupar por** » :bi:`Status` » :bi:`Survey User Input State`

        #. Pesquisar Pesquisa *for* **21**

        #. Selecionar todas as :bi:`Participations` com: :bi:`Status` = "**Concluído**" » :bi:`Survey User Input State` = ":bi:`New`"

        #. Executar a Ação ":bi:`Survey User Input Refresh`":

            #. Utilize o botão :bi:`Survey User Input Refresh` para executar a Ação.

Executar a Ação *Survey User Input Validate* para as transcrições de Questionários do Projeto JCAFB-2021v
---------------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Survey User Input Validate` para as :bi:`Participations` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Participations*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Participations` » :bi:`Participations`

        #. Ativar o filtro **Agrupar por** » :bi:`Status` » :bi:`Survey User Input State`

        #. Pesquisar Pesquisa *for* **21**

        #. Selecionar todas as :bi:`Participations` com: :bi:`Status` = "**Concluído**" » :bi:`Survey User Input State` = ":bi:`Checked`"

        #. Executar a Ação ":bi:`Survey User Input Validate`":

            #. Utilize o botão :bi:`Survey User Input Validate` para executar a Ação.

Executar a Ação *Document Type Items Set Up* para *Document Types* do Projeto JCAFB-2021v
-----------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Type Items Set Up` para os :bi:`Document Types` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Selecionar todos os :bi:`Document Types` com: :bi:`Phase` = "**JCAFB-2021v**"

        #. Executar a Ação ":bi:`Document Type Items Set Up`":

            #. Utilize o botão :bi:`Items Set Up` para executar a Ação.

Executar a Ação *Document Items Refresh* para Documentos do Projeto JCAFB-2021v
-------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Items Refresh` para os :bi:`Documents` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Document Items Refresh`":

            #. Utilize o botão :bi:`Items Refresh` para executar a Ação.

Executar a Ação *Document Items Update from Survey* para Documentos do Projeto JCAFB-2021v
------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Items Update from Survey` para os :bi:`Documents` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Document Items Update from Survey`":

            #. Utilize o botão :bi:`Update from Survey` para executar a Ação.

Executar a Ação *Document Items Ok Set Up* para Documentos do Projeto JCAFB-2021v
---------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Items Ok Set Up` para os :bi:`Documents` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State`

        #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`"

        #. Executar a Ação ":bi:`Document Items Ok Set Up`":

            #. Utilize o botão :bi:`Items Ok Set Up` para executar a Ação.

Executar a Ação *Document Mass Edit* para Documentos do Projeto JCAFB-2021v
---------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Mass Edit` para os :bi:`Documents` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Register State` » :bi:`Items Ok`

        #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2021v**" » :bi:`Register State` = ":bi:`Revised`" » :bi:`Items Ok` = ":bi:`True`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-12b)
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de criação dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #
            # data_dir = /var/lib/odoo/.local/share/Odoo
            #

            cd /opt/odoo
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-12b.sql

            gzip clvhealth_jcafb_2021v_14_2021-05-12b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-05-12b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz clvhealth_jcafb

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    Criados os seguintes arquivos:

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-12b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-05-12b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-05-12b.sql
.. index:: clvhealth_jcafb_2021v_14_2021-05-12b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-05-12b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-05-12b)
------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo14-jcafb21-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            ssh tkl-odoo14-jcafb21-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo14-jcafb21-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2021v_14_2021-05-12b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-05-12b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-05-12b.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo14-jcafb21-vm** ao modo desejado:

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [tkl-odoo14-jcafb21-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

:red:`(Não Utilizado)` Executar a Ação *Document Items Edit* para um Documento do Projeto JCAFB-2021v
-----------------------------------------------------------------------------------------------------

    * **Observação**: A Ação :bi:`Document Items Edit` não está operacional. :red:`Redefinir o uso dessa Ação para editar automaticamente o Questíonário referente ao Documento.`

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Document Items Edit` para um determinado :bi:`Document` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Documents*:

            * Menu de acesso:

                * :bi:`Base` » :bi:`Base` » :bi:`Documents`

        #. Ativar o filtro **Filtros** » :bi:`Has User Input`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document State`

        #. Abrir o Documento desejado.

        #. Executar a Ação ":bi:`Document Items Edit`":

            #. Utilize o botão :bi:`Document Update` para executar a Ação.

:green:`(**)` Executar a Ação *Lab Test Request Receive* para recebimento de uma amostra para Exame
---------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Lab Test Request Receive` para um :bi:`Lab Test Request` do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Requests*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Lab Test` » :bi:`Requests`

        #. Pesquisar pelo **Código** do :bi:`Lab Test Request` desejado.

        #. Executar a Ação ":bi:`Lab Test Request Receive`" para o registro encontrado:

            * Parâmetros utilizados:

                * Aceitar todos os parâmetros apresentados

            #. Utilize o botão :bi:`Lab Test Request Receive` para executar a Ação.

:red:`(Não Utilizado)` Trascrição dos Resultados de um Exame via URL genérica
-----------------------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor [tkl-odoo14-jcafb21-vm] usando uma das URLs:

        * [EAA21] JCAFB 2021 - Laboratório - Análise de Água: `http://tkl-odoo14-jcafb21-vm/survey/start/eaa21 <http://tkl-odoo14-jcafb21-vm/survey/start/eaa21>`_

        * [EAN21] JCAFB 2021 - Exames para detecção de Anemia: `http://tkl-odoo14-jcafb21-vm/survey/start/ean21 <http://tkl-odoo14-jcafb21-vm/survey/start/ean21>`_

        * [ECP21] JCAFB 2021 - JCAFB 2021 - Laboratório - Parasitologia: `http://tkl-odoo14-jcafb21-vm/survey/start/ecp21 <http://tkl-odoo14-jcafb21-vm/survey/start/ecp21>`_

        * [EDH21] JCAFB 2021- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia: `http://tkl-odoo14-jcafb21-vm/survey/start/edh21 <http://tkl-odoo14-jcafb21-vm/survey/start/edh21>`_

        * [EEV21] JCAFB 2021 - Laboratório - Pesquisa de Enterobius vermicularis: `http://tkl-odoo14-jcafb21-vm/survey/start/eev21 <http://tkl-odoo14-jcafb21-vm/survey/start/eev21>`_

        * [EUR21] JCAFB 2021 - Laboratório - Urinálise: `http://tkl-odoo14-jcafb21-vm/survey/start/eur21 <http://tkl-odoo14-jcafb21-vm/survey/start/eur21>`_

    #. Iniciar a Pesquisa.

.. toctree::   :maxdepth: 2
