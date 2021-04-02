.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

=============================================
Preparação do Banco de Dados - JCAFB-2021v-14
=============================================

[tkl-odoo14-jcafb21-vm] Atualizar os fontes do projeto
------------------------------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo14-jcafb21-vm -l root

        ::

            /etc/init.d/odoo stop

            su odoo

        ::

            # ***** tkl-odoo14-jcafb21-vm
            #

            cd /opt/odoo/clvsol_odoo_client
            git pull

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-05a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-05a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-05a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-05a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-05a.tar.gz

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
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

Cancelar a Pessoa "Valmir Lourenço Almeida Barbosa [210.540-37]"
----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Excluir "Valmir Lourenço Almeida Barbosa [210.540-37]" do **Cadastro Auxiliar**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type`

        #. Selecionar o registro :bi:`Person (Aux)` de "Valmir Lourenço Almeida Barbosa [210.540-37]".

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação ":bi:`Person Mass Edit`" para o registro referente a "Valmir Lourenço Almeida Barbosa [210.540-37]":

        #. Acessar a *view* **Persons**:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Selecionar o registro :bi:`Person` de "Valmir Lourenço Almeida Barbosa [210.540-37]".

        #. Executar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Conceled**

                * *State*: **Set** » **Unavailable**

                * *Person Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Atualizar o *Layout* das Pesquisas da JCAFB-2021v
-------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Editar as Pesquisas da JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Families*:

            * Menu de acesso:

                * :bi:`Pesquisas` » :bi:`Pesquisas`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`.

        #. Editar, individualmente, todas as Pesquisas com: :bi:`Phase` = "**JCAFB-2021v**":

            * Parâmetro editado:

                * Perguntas » *Layout*: **One page with all the questions**

Configurar o *Survey Type* para os *Lab Test Types* do Projeto JCAFB-2021v
--------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Configurar o *Survey Type* para os *Lab Test Types* do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase`

        #. Editar todos os :bi:`Lab Test Types` com: :bi:`Phase` = "**JCAFB-21v**"

            #. **JCAFB 2021 - Exames - Detecção de Anemia**:

                * *Survey Type*: "**[EAN21]**".

            #. **JCAFB 2021 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**:

                * *Survey Type*: "**[EDH21]**".

            #. **JCAFB 2021 - Laboratório - Análise de Água**:

                * *Survey Type*: "**[EAA21]**".

            #. **JCAFB 2021 - Laboratório - Parasitologia**:

                * *Survey Type*: "**[ECP21]**".

            #. **JCAFB 2021 - Laboratório - Pesquisa de Enterobius vermicularis**:

                * *Survey Type*: "**[EEV21]**".

            #. **JCAFB 2021 - Laboratório - Urinálise**:

                * *Survey Type*: "**[EUR21]**".

Editar o *Criterion Type* para os *Lab Test Type Parameters* do Projeto JCAFB-2021v
-----------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Editar o *Criterion Type* para os *Lab Test Type Parameters* do Projeto JCAFB-2021v:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Lab Test Type Parameters*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Parameters`

        #. Editar *Criterion Type* de todos os :bi:`Lab Test Type Parameters`:

            * de "**text**"

            * de "**char_box**"

Consolidar os Documentos do Projeto JCAFB-2017
----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Register State` » :bi:`Document State` » :bi:`Items Ok`

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QAN17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**71**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QDH17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**59**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QMD17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**9**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QSC17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**11**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QSF17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**19**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**QSI17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**6**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**TCP17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**60**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**TCR-17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**11**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2017**", :bi:`Document Type` = "**TID17**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**9**".

    #. Acessar a *View* :bi:`Document Items`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Items`

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document` » **não está definido** Document Items" » **Aplicar**".

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document Type` » **não está definido** Document Items" » **Aplicar**".

        #. Excluir os registros de :bi:`Document Items` apresentados.

            * Registros Excluídos: "**240**".

Consolidar os Documentos do Projeto JCAFB-2018
----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Register State` » :bi:`Document State` » :bi:`Items Ok`

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**indefinido**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**10**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QVG18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**15**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QVI18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**3**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**TCV18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**2**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QMD18**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QMD18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**73**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QSC18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**35**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QSF18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**68**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QSI18**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**QSI18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**71**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**TAN18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**TCR18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**35**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**TID18**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**", :bi:`Document Type` = "**TID18**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**69**".

    #. Acessar a *View* :bi:`Document Items`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Items`

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document` » **não está definido** Document Items" » **Aplicar**".

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document Type` » **não está definido** Document Items" » **Aplicar**".

        #. Excluir os registros de :bi:`Document Items` apresentados.

            * Registros Excluídos: "**3657**".

Consolidar os Documentos do Projeto JCAFB-2018 (2)
--------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Items Ok`

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QAN18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**173**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QDH18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**188**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QMD18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**127**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QSC18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**87**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QSF18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**166**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`QSI18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**129**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`TAN18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**172**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`TCR18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**91**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`TDH18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**188**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2018**" » :bi:`Document Type` = ":bi:`TID18`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**132**".

Consolidar os Documentos do Projeto JCAFB-2019
----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Register State` » :bi:`Document State` » :bi:`Items Ok`

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**indefinido**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**New**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**4**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QAN19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**2**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QMD19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**117**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QMD19**", :bi:`Register State` = "**Done**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QMD19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**7**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSC19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**52**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSC19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**2**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSF19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**106**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSF19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**11**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSI19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**118**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSI19**", :bi:`Register State` = "**Done**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSI19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**8**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**QSI19**", :bi:`Register State` = "**Revised**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TAN19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TCR19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**53**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TCR19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TDH19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**3**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TID19**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**126**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TID19**", :bi:`Register State` = "**Done**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**1**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**", :bi:`Document Type` = "**TID19**", :bi:`Register State` = "**Draft**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**5**".

    #. Acessar a *View* :bi:`Document Items`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Items`

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document` » **não está definido** Document Items" » **Aplicar**".

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document Type` » **não está definido** Document Items" » **Aplicar**".

        #. Excluir os registros de :bi:`Document Items` apresentados.

            * Registros Excluídos: "**786**".

Consolidar os Documentos do Projeto JCAFB-2019 (2)
--------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Items Ok`

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QAN19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**144**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QDH19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**199**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QMD19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**136**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QSC19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**82**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QSF19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**168**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`QSI19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**136**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`TAN19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**144**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`TCR19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**87**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`TDH19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**193**".

    #. Selecionar todos os :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2019**" » :bi:`Document Type` = ":bi:`TID19`" » :bi:`Items Ok` = ":bi:`true`"

        #. Executar a Ação ":bi:`Document Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *Document State*: **Set** » **Archived**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

            * Registros Processados: "**147**".

Consolidar os Documentos do Projeto JCAFB-2020
----------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

    #. Acessar a *View* :bi:`Documents`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`Documents`

    #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Document Type` » :bi:`Register State` » :bi:`Document State` » :bi:`Items Ok`

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QAN20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**6**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QDH20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**5**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QMD20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**138**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QSC20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**59**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QSF20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**137**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**QSI20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**138**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**TAA20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**7**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**TAN20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**3**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**TCR20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**60**".

        #. Excluir os registros de :bi:`Documents` com: :bi:`Phase` = "**JCAFB-2020**", :bi:`Document Type` = "**TID20**", :bi:`Register State` = "**Cancelled**", :bi:`Document State` = "**Discarded**" e :bi:`Items Ok` = "**false**"

            * Registros Excluídos: "**135**".

    #. Acessar a *View* :bi:`Document Items`:

        * Menu de acesso:

            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Items`

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document` » **não está definido** Document Items" » **Aplicar**".

    #. **Filtros** » **Adicionar Filtro Personalizado** » :bi:`Document Type` » **não está definido** Document Items" » **Aplicar**".

        #. Excluir os registros de :bi:`Document Items` apresentados.

            * Registros Excluídos: "**89**".

Criar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-09b)
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
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-09b.sql

            gzip clvhealth_jcafb_2021v_14_2021-02-09b.sql
            pg_dump clvhealth_jcafb_2021v_14 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2021v_14_2021-02-09b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz clvhealth_jcafb_2021v_14

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-09b.sql
        * /opt/odoo/clvhealth_jcafb_2021v_14_2021-02-09b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz

.. index:: clvhealth_jcafb_2021v_14_2021-02-09b.sql
.. index:: clvhealth_jcafb_2021v_14_2021-02-09b.sql.gz
.. index:: filestore_clvhealth_jcafb_2021v_14_2021-02-09b
.. index:: clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-09b

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-09b)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-09b.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-09b.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-09b.tar.gz

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
                
                * **Configurações** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo14-jcafb21-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
