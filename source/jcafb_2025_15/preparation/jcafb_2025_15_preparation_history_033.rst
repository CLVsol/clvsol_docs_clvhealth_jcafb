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
JCAFB-2025-15 (Preparação pré Jornada II [4])
=============================================

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-16b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-11-16b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-11-16b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-16b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-16b.tar.gz

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

[tkl-odoo15-jcafb25-vm] Atualizar o *Patient Category* dos Pacientes
--------------------------------------------------------------------

    Critérios utilizados:

        * **Criança**: todos os Pacientes nas faixas etárias "**2 anos**", "**3-5 anos**" "**6 anos**" e "**7-8 anos**".

        * **Idoso**: todos os Pacientes na faixa etária "**60+ anos**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`Categories`

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**2 anos**", "**3-5 anos**" "**6 anos**" e "**7-8 anos**" » :bi:`Category` = "**indefinido**"

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Criança**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todos os Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`Category` = "**indefinido**"

        #. Executar a Ação ":bi:`Patient Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Idoso**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Executar a Atualização de Pacientes (Rec)
-----------------------------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Related Patient (Rec) Update`:

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Categories`

        #. Selecionar os :bi:`Patient (Rec)s` com: :bi:`Categories` = "**Criança**" (**218**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

        #. Selecionar os :bi:`Patient (Rec)s` com: :bi:`Categories` = "**Idoso**" (**610**)

        #. Executar a Ação ":bi:`Patient Related Patient (Rec) Update`":

            * Parâmetros utilizados:
                * *Update Contact Information Data*: **desmarcado**
                * *Related Patient (Rec) Verification Execute*: **marcado**
                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Patient Related Patient (Rec) Update` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Atualizar o *Register State* de Pacientes (Rec)
-----------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient (Rec) Mass Edit` para os Pacientes (Rec):

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patient (Rec)s*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient (Rec)` » :bi:`Patient (Rec)s`

        #. Ativar o filtro **Agrupar por** » :bi:`Categories`

        #. Selecionar os :bi:`Patient (Rec)s` com: :bi:`Categories` = "**Criança**" (**218**)

        #. Executar a Ação ":bi:`Patient (Rec) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** **Done**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar os :bi:`Patient (Rec)s` com: :bi:`Categories` = "**Idoso**" (**610**)

        #. Executar a Ação ":bi:`Patient (Rec) Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** **Done**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-22a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-22a.sql

            gzip clvhealth_jcafb_2025_15_2024-11-22a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-11-22a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-22a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-11-22a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-11-22a.sql
.. index:: clvhealth_jcafb_2025_15_2024-11-22a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-11-22a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-22a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-11-22a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-11-22a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-11-22a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-11-22a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Definir a Lista de Pacientes Selecionados para a JCAFB-2025
-----------------------------------------------------------------------------------

    Critérios utilizados:

        * **88**: Pacientes na faixa etária "**60+ anos**", distrribuidos pelos Bairros:

            * Baixada: **17**
            * Centro: **35**
            * Cohabs: **19**
            * Vila Oliveira: **17**

        * **72**: Pacientes na faixa etária "**3-5 anos**", distrribuidos pelos Bairros:

            * Baixada: **17**
            * Centro: **24**
            * Cohabs: **17**
            * Vila Oliveira: **14**

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ordenar os Pacientesa pelo campo :bi:`Random ID`.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`District`

        #. **Idosos** (**88**):

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **35** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **19** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Selected**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças** (**72**):

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **24** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **14** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Selected**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-02a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-02a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-02a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-02a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-02a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-02a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-02a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-02a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-02a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-02a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-02a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-02a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-02a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-02a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Alocar 6 dos Pacientes Selecionados para o Grupo 15 (JCAFB-2025)
----------------------------------------------------------------------------------------

    Critérios utilizados:

        * **4**: Pacientes Selelcionados na faixa etária "**60+ anos**", residindo próximo à Escola Municipal.

        * **2**: Pacientes Selelcionados na faixa etária "**3-5 anos**", residindo próximo à Escola Municipal.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee` » :bi:`District`  » :bi:`Address Name`

            #. Selecionar **6** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**" » :bi:`District` = "**Centro**", seguilndo os critérios definidos anteriormente.

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo 15 (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-03a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-03a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-03a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-03a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-03a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-03a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-03a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-03a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-03a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-03a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-03a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-03a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-03a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-03a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Alocar os Pacientes Selecionados que compartilhem um mesmo endereço, nos Grupos de Campo (JCAFB-2025)
-----------------------------------------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Selected**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee` » :bi:`District` » :bi:`Address Name`  » :bi:`Age Range`

            #. Selecionar separadamente cada grupo de Pacientes com o mesmo endereço.

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Alocar os demais Pacientes Selecionados nos Grupos de Campo (JCAFB-2025)
------------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Selected**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

            #. Selecionar **até 11** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**" » :bi:`Age Range` = "**consultar Planilha**" » :bi:`District` = "**consultar Planilha**".

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Verificar a duplicidade de *Responsible Employee* em um mesmo endereço
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Verificar a duplicidade de :bi:`Responsible Employee` em um mesmo endereço:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee`  » :bi:`Age Range`

            #. Verificar a situação dos Endereços (*Address Name*) com 2 ou mais Paciemtes. Situações onde ocorrer a duplicidade de :bi:`Responsible Employee` deverão ser corrigidas.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-04a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-04a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-04a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-04a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-04a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-04a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-04a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-04a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-04a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-04a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-04a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-04a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-04a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-04a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Definir a Lista de Pacientes em Espera para a JCAFB-2025
--------------------------------------------------------------------------------

    Critérios utilizados:

        * **88**: Pacientes na faixa etária "**60+ anos**", distrribuidos pelos Bairros:

            * Baixada: **17**
            * Centro: **35**
            * Cohabs: **19**
            * Vila Oliveira: **17**

        * **43**: Pacientes na faixa etária "**3-5 anos**", distrribuidos pelos Bairros:

            * Baixada: **10**
            * Centro: **14**
            * Cohabs: **10**
            * Vila Oliveira: **9**

        * **29**: Pacientes na faixa etária "**6 anos**", distrribuidos pelos Bairros:

            * Baixada: **9**
            * Centro: **10**
            * Cohabs: **4**
            * Vila Oliveira: **6**

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ordenar os Pacientesa pelo campo :bi:`Random ID`.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`District`

        #. **Idosos** (**88**):

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **35** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **19** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **17** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças 3-5 anos** (**43**):

            #. Selecionar os primeiros **10** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **14** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **10** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **9** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**3-5 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças 6 anos** (**29**):

            #. Selecionar os primeiros **9** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **10** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **6** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-06a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-06a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-06a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-06a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-06a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-06a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Alocar 6 dos Pacientes em Espera para o Grupo 15 (JCAFB-2025)
-------------------------------------------------------------------------------------

    Critérios utilizados:

        * **4**: Pacientes Selelcionados na faixa etária "**60+ anos**", residindo próximo à Escola Municipal.

        * **2**: Pacientes Selelcionados na faixa etária "**3-5 anos**", residindo próximo à Escola Municipal.

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por** » :bi:`Responsible Employee` » :bi:`District`  » :bi:`Address Name`

            #. Selecionar **6** Pacientes com: :bi:`Responsible Employee` = "**indefinido**" » :bi:`District` = "**Centro**", seguilndo os critérios definidos anteriormente.

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo 15 (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06b.sql

            gzip clvhealth_jcafb_2025_15_2024-12-06b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-06b.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-06b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-06b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-06b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-06b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06b.tar.gz

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

[tkl-odoo15-jcafb25-vm] Alocar os Pacientes em Espera que compartilhem um mesmo endereço, nos Grupos de Campo (JCAFB-2025)
--------------------------------------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por** » :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee` » :bi:`Age Range`

            #. Selecionar separadamente cada grupo de Pacientes com o mesmo endereço.

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Alocar os demais Pacientes em Espera nos Grupos de Campo (JCAFB-2025)
---------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

            #. Selecionar **até 11** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**" » :bi:`Age Range` = "**consultar Planilha**" » :bi:`District` = "**consultar Planilha**".

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Verificar a duplicidade de *Responsible Employee* em um mesmo endereço
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Verificar a duplicidade de :bi:`Responsible Employee` em um mesmo endereço:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por**» :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee`  » :bi:`Age Range`

            #. Verificar a situação dos Endereços (*Address Name*) com 2 ou mais Paciemtes. Situações onde ocorrer a duplicidade de :bi:`Responsible Employee` deverão ser corrigidas.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06c)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06c.sql

            gzip clvhealth_jcafb_2025_15_2024-12-06c.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-06c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06c.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-06c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-06c.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-06c.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-06c
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06c

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-06c)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-06c.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-06c.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-06c.tar.gz

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

[tkl-odoo15-jcafb25-vm] Complementar a Lista de Pacientes em Espera para a JCAFB-2025
-------------------------------------------------------------------------------------

    Critérios utilizados:

        * **29**: Pacientes na faixa etária "**6 anos**", distrribuidos pelos Bairros:

            * Baixada: **9**
            * Centro: **10**
            * Cohabs: **4**
            * Vila Oliveira: **6**

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ordenar os Pacientesa pelo campo :bi:`Random ID`.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`District`

        #. **Crianças 6 anos** (**29**):

            #. Selecionar os primeiros **9** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **10** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **6** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Alocar os Pacientes em Espera que compartilhem um mesmo endereço, nos Grupos de Campo (JCAFB-2025)
--------------------------------------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por** » :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee` » :bi:`Age Range`

            #. Selecionar separadamente cada grupo de Pacientes com o mesmo endereço.

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Alocar os demais Pacientes em Espera nos Grupos de Campo (JCAFB-2025)
---------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

            #. Selecionar **até 11** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**" » :bi:`Age Range` = "**consultar Planilha**" » :bi:`District` = "**consultar Planilha**".

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Grupo nn (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Verificar a duplicidade de *Responsible Employee* em um mesmo endereço
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Verificar a duplicidade de :bi:`Responsible Employee` em um mesmo endereço:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por**» :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee`  » :bi:`Age Range`

            #. Verificar a situação dos Endereços (*Address Name*) com 2 ou mais Paciemtes. Situações onde ocorrer a duplicidade de :bi:`Responsible Employee` deverão ser corrigidas.

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07a)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07a.sql

            gzip clvhealth_jcafb_2025_15_2024-12-07a.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07a.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-07a.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-07a.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-07a
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07a

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07a)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-07a.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-07a.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07a.tar.gz

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

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07b)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07b.sql

            gzip clvhealth_jcafb_2025_15_2024-12-07b.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07b.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-07b.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-07b.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-07b
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07b

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07b)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-07b.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-07b.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07b.tar.gz

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

[tkl-odoo15-jcafb25-vm] Definir a Lista de Pacientes em Espera (Coord 01) para a JCAFB-2025
-------------------------------------------------------------------------------------------

    Critérios utilizados:

        * **22**: Pacientes na faixa etária "**60+ anos**", distrribuidos pelos Bairros:

            * Baixada: **4**
            * Centro: **9**
            * Cohabs: **5**
            * Vila Oliveira: **4**

        * **11**: Pacientes na faixa etária "**6 anos**", distrribuidos pelos Bairros:

            * Baixada: **2**
            * Centro: **4**
            * Cohabs: **2**
            * Vila Oliveira: **2**

        * **7**: Pacientes na faixa etária "**7-8 anos**", distrribuidos pelos Bairros:

            * Baixada: **1**
            * Centro: **2**
            * Cohabs: **2**
            * Vila Oliveira: **2**

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ordenar os Pacientesa pelo campo :bi:`Random ID`.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`District`

        #. **Idosos** (**22**):

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **9** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **5** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças 6 anos** (**11**):

            #. Selecionar os primeiros **3** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **2** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **2** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças 7-8 anos** (**7**):

            #. Selecionar os primeiros **1** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **2** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **2** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **2** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Verificar a duplicidade de *Responsible Employee* em um mesmo endereço
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Verificar a duplicidade de :bi:`Responsible Employee` em um mesmo endereço:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por**» :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee`  » :bi:`Age Range`

            #. Verificar a situação dos Endereços (*Address Name*) com 2 ou mais Paciemtes. Situações onde ocorrer a duplicidade de :bi:`Responsible Employee` deverão ser corrigidas. 

[tkl-odoo15-jcafb25-vm] Alocar os demais Pacientes em Espera no Grupo Coord 01 (JCAFB-2025)
-------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting (Reserva)**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`

            #. Selecionar **até 40** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**".

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Coord 01 (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07c)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07c.sql

            gzip clvhealth_jcafb_2025_15_2024-12-07c.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07c.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07c.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-07c.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-07c.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-07c
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07c

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07c)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-07c.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-07c.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07c.tar.gz

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

[tkl-odoo15-jcafb25-vm] Definir a Lista de Pacientes em Espera (Coord 02) para a JCAFB-2025
-------------------------------------------------------------------------------------------

    Critérios utilizados:

        * **22**: Pacientes na faixa etária "**60+ anos**", distrribuidos pelos Bairros:

            * Baixada: **4**
            * Centro: **9**
            * Cohabs: **5**
            * Vila Oliveira: **4**

        * **18**: Pacientes na faixa etária "**7-8 anos**", distrribuidos pelos Bairros:

            * Baixada: **4**
            * Centro: **6**
            * Cohabs: **4**
            * Vila Oliveira: **4**

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ordenar os Pacientesa pelo campo :bi:`Random ID`.

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State`  » :bi:`Age Ranges` » :bi:`District`

        #. **Idosos** (**22**):

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **9** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **5** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**60+ anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. **Crianças 7-8 anos** (**18**):

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Baixada**"

            #. Selecionar os primeiros **6** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Centro**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Cohabs**"

            #. Selecionar os primeiros **4** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Age Range` = "**6 anos**" » :bi:`District` = "**Vila Oliveira**"

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Patient State*: **Set** » **Waiting**
                    * *Patient Verification Execute*: **marcado**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb25-vm] Verificar a duplicidade de *Responsible Employee* em um mesmo endereço
----------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb25-vm] Verificar a duplicidade de :bi:`Responsible Employee` em um mesmo endereço:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro :bi:`Patient State` = "**Selected**" ou "**Waiting**"

        #. Ativar o filtro **Agrupar por**» :bi:`District` » :bi:`Address Name` » :bi:`Responsible Employee`  » :bi:`Age Range`

            #. Verificar a situação dos Endereços (*Address Name*) com 2 ou mais Paciemtes. Situações onde ocorrer a duplicidade de :bi:`Responsible Employee` deverão ser corrigidas. 

[tkl-odoo15-jcafb25-vm] Alocar os demais Pacientes em Espera no Grupo Coord 02 (JCAFB-2025)
-------------------------------------------------------------------------------------------

    Critérios utilizados:

        * Conforme definido na Planilha "**Waiting (Reserva)**" do Workbook "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/Seleção de Pacientes - JCAFB-2025.xlsx**".

    #. [tkl-odoo15-jcafb25-vm] Executar a Ação :bi:`Patient Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`

            #. Selecionar **até 40** Pacientes com: :bi:`Patient State` = "**Available**" » :bi:`Responsible Employee` = "**indefinido**".

            #. Executar a Ação ":bi:`Patient Mass Edit`":

                * Parâmetros utilizados:

                    * *Responsible Employee*: **Set** » **Coord 02 (JCAFB-2025)**

                #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

    #. [tkl-odoo15-jcafb25-vm] Para verificação da alocação de Pacientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb25-vm <https://tkl-odoo15-jcafb25-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Patient State` » :bi:`Responsible Employee`  » :bi:`Age Range` » :bi:`District`

[tkl-odoo15-jcafb25-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07d)
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
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07d.sql

            gzip clvhealth_jcafb_2025_15_2024-12-07d.sql
            pg_dump clvhealth_jcafb_2025_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2025_15_2024-12-07d.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz clvhealth_jcafb_2025_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07d.sql
        * /opt/odoo/clvhealth_jcafb_2025_15_2024-12-07d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz

.. index:: clvhealth_jcafb_2025_15_2024-12-07d.sql
.. index:: clvhealth_jcafb_2025_15_2024-12-07d.sql.gz
.. index:: filestore_clvhealth_jcafb_2025_15_2024-12-07d
.. index:: clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07d

[tkl-odoo15-jcafb25-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2025-15* (2024-12-07d)
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
            # gzip -d clvhealth_jcafb_2025_15_2024-12-07d.sql.gz

            dropdb -i clvhealth_jcafb_2025_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2025_15
            psql -f clvhealth_jcafb_2025_15_2024-12-07d.sql -d clvhealth_jcafb_2025_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2025_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2025_15_2024-12-07d.tar.gz

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
