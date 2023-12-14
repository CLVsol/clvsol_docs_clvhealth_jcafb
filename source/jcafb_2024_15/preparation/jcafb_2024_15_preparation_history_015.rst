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
JCAFB-2024-15 (Preparação pré Jornada [6])
==========================================

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-01a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-01a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-01a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01a.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Atualizar o(s) módulo(s) [clv_lab_test]
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Lista de Módulos:

        * clv_lab_test

    #. [tkl-odoo15-jcafb24-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb24-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                ssh tkl-odoo15-jcafb24-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb24-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 2)
                #

                ssh tkl-odoo15-jcafb24-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2024_15" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

[tkl-odoo15-jcafb24-vm] Criar o *Lab Test Type* "**EAN24**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EAN23**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EAN23**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EAN24**
                * *New Lab Test Type Code*: **EAN24**
                * *New Lab Test Type Description*: **JCAFB 2024 - Exames - Detecção de Anemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EAN24**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EAN24]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2024**".

[tkl-odoo15-jcafb24-vm] Criar o *Lab Test Type* "**ECP24**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**ECP23**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP23**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **ECP24**
                * *New Lab Test Type Code*: **ECP24**
                * *New Lab Test Type Description*: **JCAFB 2024 - Laboratório - Parasitologia**
                * *Template File Name (Result)*: **Resultado_ECP24_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_ECP24_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**ECP24**".

            #. Atualizar o campo :bi:`Survey Type`: "**[ECP24]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2024**".

[tkl-odoo15-jcafb24-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**ECP24**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**ECP24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**ECP24**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar o *Lab Test Type* "**EDH24**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EDH23**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EDH23**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:

                * *New Lab Test Type*: **EDH24**
                * *New Lab Test Type Code*: **EDH24**
                * *New Lab Test Type Description*: **JCAFB 2024 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Template File Name (Result)*: **vazio**
                * *Template File Name (Report)*: **vazio**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EDH24**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EDH24]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2024**".

[tkl-odoo15-jcafb24-vm] Criar o *Lab Test Type* "**EUR24**"
-----------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Duplicate` para o :bi:`Lab Test Type` "**EUR23**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:
                
                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR23**".

        #. Executar a Ação ":bi:`Lab Test Type Duplicate`":

            * Parâmetros utilizados:
 
                * *New Lab Test Type*: **EUR24**
                * *New Lab Test Type Code*: **EUR24**
                * *New Lab Test Type Description*: **JCAFB 2024 - Laboratório - Urinálise**
                * *Template File Name (Result)*: **Resultado_EUR24_nnn.nnn-dd.xls**
                * *Template File Name (Report)*: **Laudo_EUR24_nnn.nnn-dd.xls**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do *Lab Test Type* "**EUR24**".

            #. Atualizar o campo :bi:`Survey Type`: "**[EUR24]**".

            #. Atualizar o campo :bi:`Phase`: "**JCAFB-2024**".

[tkl-odoo15-jcafb24-vm] Executar a Ação *Lab Test Type Criteria Set Up* para *Lab Test Type* "**EUR24**"
--------------------------------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Lab Test Type Criteria Set Up` para *Lab Test Type* "**EUR24**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Abrir o Formulário do *Lab Test Type* "**EUR24**".

        #. Executar a Ação ":bi:`Lab Test Type Criteria Set Up`":

            #. Utilize o botão :bi:`Criteria Set Up` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-01b)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-01b.sql

            gzip clvhealth_jcafb_2024_15_2023-12-01b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-01b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-01b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-01b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-01b.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-01b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-01b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-01b

[clvheatlh-jcafb-2024n-aws-pro] :borange:`(**)` Atualisar *Patient Age Ranges* para todos os Pacientes (método alternativo)
---------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar manualmente a "Ação Agendada" "**Patient: Compute Age Reference**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Compute Age Reference**"

        #. Executar a Ação Agendada "**Patient: Compute Age Reference**", clicando no botão **Rodar Manualmente**.

    #. :red:`(Não Necessário)` [clvheatlh-jcafb-2024n-aws-pro] Executar manualmente a "Ação Agendada" "**Patient: Update Age Range**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* **Ações Agendadas**:

            * Menu de acesso:

                * **Configurações** » **Técnico** » **Automação** » **Ações Agendadas**

        #. Acessar a Ação Agendada "**Patient: Update Age Range**"

        #. Executar a Ação Agendada "**Patient: Update Age Range**", clicando no botão **Rodar Manualmente**.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-09a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-09a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-09a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-09a.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Atualizar o(s) módulo(s) [clv_patient_jcafb]
--------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Lista de Módulos:

        * clv_patient_jcafb

    #. [tkl-odoo15-jcafb24-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb24-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                ssh tkl-odoo15-jcafb24-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb24-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 2)
                #

                ssh tkl-odoo15-jcafb24-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2024_15" -m clv_patient_jcafb

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb24-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb24-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QAN24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QAN24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QAN23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QAN24**
                * *New Document Type Code*: **QAN24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário para detecção de Anemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QAN24**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QAN24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QDH24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QDH24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QDH23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QDH24**
                * *New Document Type Code*: **QDH24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QDH24**".

        #. Atualizar os campos:

            * *Categories*: **(Campanha) Questionário**
            * *Survey Type*: **[QDH24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QMD24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QMD24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QMD23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QMD24**
                * *New Document Type Code*: **QMD24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário - Medicamentos**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QMD24**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QMD24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QSC24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSC24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSC23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSC24**
                * *New Document Type Code*: **QSC24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário Socioeconômico Individual (Crianças)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSC24**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSC24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QSF24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSF24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSF23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSF24**
                * *New Document Type Code*: **QSF24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário Socioeconômico Familiar (Crianças e Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSF24**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSF24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar o *Document Type* "[QSI24]"
---------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Document Type Duplicate` para o *Document Type* "**[QSI24]**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Document Types*:

            * Menu de acesso:
                * **Base** » **Configuration** » **Document** » **Types**

        #. Abrir o Formulário do *Document Type* "**[QSI23]**".

        #. Executar a Ação ":bi:`Document Type Duplicate`":

            * Parâmetros utilizados:
                * *New Document Type*: **QSI24**
                * *New Document Type Code*: **QSI24**
                * *New Document Type Description*: **JCAFB 2024 - Questionário Socioeconômico Individual (Idosos)**

            #. Utilize o botão :bi:`Duplicate` para executar a Ação.

        #. Abrir o Formulário do Document "**QSI24**".

        #. Atualizar os campos:

            * *Categories*: **(Campo) Questionário**
            * *Survey Type*: **[QSI24]**
            * *Phase*: **JCAFB-2024**

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-10a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-10a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-10a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-10a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-10a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-10a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-10a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-10a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-10a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-10a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-10a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-10a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-10a.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024n-aws-pro] Criar o Lab Test Type "EEV24"
-------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Lab Test` » :bi:`Types`

        #. Criar o *Lab Test Type* "**EEV24**:

            * Parâmetros utilizados:

                * *Lab Test Type*: **EEV24**

                * *Lab Test Type Code*: **EEV24**

                * *Lab Test Type Description*: **JCAFB 2024 - Laboratório - Pesquisa de Enterobius vermicularis**

                * *Survey Type*: **[EEV24]**

                * *Phase*: **JCAFB-2024**

[clvheatlh-jcafb-2024n-aws-pro] Reinicializar os Parâmetros de todas as Residências
-----------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Residence` » :bi:`Residences`

        #. Selecionar todas as Residências

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Register State*: **Set** » **Done**

                * *State*: **Set** » **Unknown**

                * *Categories*: **remove** » **Zona Rural**, **Zona Urbana**

                * *Residence Verification Execute*: **marcado**

                * *Responsible Empĺoyee*: **remove**

                * *Phase*: **remove**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Criar novas "Residence Categories"
------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Lab Test Types*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Configuration` » :bi:`Residence` » :bi:`Categories`

        #. Criar as novas *Lab Test TypeResidence Categories*:

                * **Beira Rio**

                * **Centro**

                * **Ribeirao da Varzea**

                * **Sol Nascente**

                * **Vila Cesar**

                * **Vila Iolanda**

[clvheatlh-jcafb-2024n-aws-pro] Atualizar o *Residence Category* de todas as Residências
----------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Categories` » :bi:`District`

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Beira Rio**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Beira Rio**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Centro**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Centro**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Sol Nascente**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Sol Nascente**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Vila Cesar**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Vila Cesar**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-11a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-11a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-11a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-11a.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-12a)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-12a.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-12a.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-12a.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

[clvheatlh-jcafb-2024n-aws-pro] Excluir todos os "Summary Files" (JCAFB-2023)
-----------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Escluir manualmente todos os arquivos presentes no diretório "**/opt/odoo/clvsol_filestore/clvhealth_jcafb/summary_files**" do Servidor.

    #. [clvheatlh-jcafb-2024n-aws-pro] Escluir manualmente todos os :bi:`File System Files` do :bi:`File System Directory` "**Summary Files**":

        * Menu de acesso:

            * :bi:`Base` » :bi:`Base` » :bi:`File System` » :bi:`Files`

[clvheatlh-jcafb-2024n-aws-pro] Excluir os Grupos da Coordenação
----------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Escluir manualmente os Grupos da Coordenaçao:

        * Crianças (2024)

        * Idosos - Beira Rio (2024)

        * Idosos - Centro (2024)

        * Idosos - Sol Nascente (2024)

        * Idosos - Vila Iolanda (2024)

[clvheatlh-jcafb-2024n-aws-pro] Associar os Pacientes selecionados a uma Residência
-----------------------------------------------------------------------------Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Residence`

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido` (145 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Patient State` = ":bi:`Selected`" » :bi:`Residence` = :bi:`Indefinido` (53 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Associar os Pacientes em espera a uma Residência
-----------------------------------------------------------------------------Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State` » :bi:`Residence`

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Patient State` = ":bi:`Waiting`" » :bi:`Residence` = :bi:`Indefinido` (174 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **desmarcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

        #. Selecionar as Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Patient State` = ":bi:`Waiting`" » :bi:`Residence` = :bi:`Indefinido` (132 Pacientes):

        #. Executar a Ação "**Patient Associate to Residence**":

            * Parâmetros utilizados:

                * *Create new Residence*: **marcado**

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão *Associate to Residence* para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Atualizar o *Residence Category* de todas as Residências
----------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Residence Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Residences*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Residence` » :bi:`Residences`

        #. Ativar o filtro **Agrupar por** » :bi:`Categories` » :bi:`District`

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Beira Rio**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Beira Rio**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Centro**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Centro**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Sol Nascente**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Sol Nascente**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Residências com: :bi:`Category` = "**Indefinido**" e que estejam localizadas no Bairro "**Vila Cesar**".

        #. Executar a Ação ":bi:`Residence Mass Edit`":

            * Parâmetros utilizados:

                * *Categories*: **Set** » **Vila Cesar**

                * *Phase*: **vazio**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Executar a Ação *Patient Residence Update* de todas as Residências
--------------------------------------------------------------------------------------------------

    #. [tkl-odoo14-jcafb21n-vm] Executar a Ação :bi:`Patient Residence Update`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21n-vm <https://tkl-odoo14-jcafb21n-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Helth` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Patient State`

        #. Selecionar os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Patient State` = ":bi:`Selected`" ou ":bi:`Waiting`" (319 Pacientes):

        #. Executar a Ação ":bi:`Patient Residence Update`":

            * Parâmetros utilizados:

                * *Residence Verification Execute*: **marcado**

                * *Patient Verification Execute*: **marcado**

            #. Utilize o botão :bi:`Residence Update` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-13a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-13a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-13a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-13a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-13a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-13a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-13a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-13a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-13a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-13a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-13a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-13a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-13a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-13a

:red:`(Não Executado)` [clvheatlh-jcafb-2024n-aws-pro] Criar os Documentos para as Crianças selecionadas para o Projeto JCAFB-2024
----------------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Document Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QSC24**

                    #. **QSF24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

:red:`(Não Executado)` [clvheatlh-jcafb-2024n-aws-pro] Criar os Resultados de Exames para as Crianças selecionadas para o Projeto JCAFB-2024
--------------------------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Lab Teste Result Set Up [Patient]` para as Crianças selecionadas para o Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Teste Result Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP24**

                    #. **EEV24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Lab Teste Result Set Up` para executar a Ação.

:red:`(Não Executado)` [clvheatlh-jcafb-2024n-aws-pro] Criar os Documentos para os Idosos selecionados para o Projeto JCAFB-2024
--------------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Document Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Document Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Document Types*:

                    #. **QMD24**

                    #. **QSF24**

                    #. **QSI24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

:red:`(Não Executado)` [clvheatlh-jcafb-2024n-aws-pro] Criar os Resultados de Exames para os Idosos selecionados para o Projeto JCAFB-2024
------------------------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Lab Teste Result Set Up [Patient]` para os Idosos selecionados para o Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected`

        #. Executar a Ação ":bi:`Lab Teste Result Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Lab Test Types*:

                    #. **ECP24**

                    #. **EUR24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Lab Teste Result Set Up` para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Criar os Documentos e os Resultados de Exames para as Crianças incluídas no Projeto JCAFB-2024
------------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Event Set Up [Patient]` para as Crianças incluídas no Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Criança`" » :bi:`Patient State` = :bi:`Selected` ou :bi:`Waiting` (110 Pacientes)

        #. Executar a Ação ":bi:`Event Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Events*: **nenhum**

                * *Document Types*:

                    #. **QSC24**

                    #. **QSF24**

                * *Document Category*: **(Campo) Questionário**

                * *Lab Test Types*:

                    #. **ECP24**

                    #. **EEV24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

[clvheatlh-jcafb-2024n-aws-pro] Criar os Documentos e os Resultados de Exames para os Idosos incluídos no Projeto JCAFB-2024
----------------------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2024n-aws-pro] Executar a Ação :bi:`Event Set Up [Patient]` para os Idosos incluídos no Projeto JCAFB-2024:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2024n-aws-pro <https://clvheatlh-jcafb-2024n-aws-pro>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Categories` » :bi:`Patient State`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Category` = ":bi:`Idoso`" » :bi:`Patient State` = :bi:`Selected` ou :bi:`Waiting` (209 Pacientes)

        #. Executar a Ação ":bi:`Event Set Up [Patient]`":

            * Parâmetros utilizados:

                * *Events*: **nenhum**

                * *Document Types*:

                    #. **QMD24**

                    #. **QSF24**

                    #. **QSI24**

                * *Document Category*: **(Campo) Questionário**

                * *Lab Test Types*:

                    #. **ECP24**

                    #. **EUR24**

                * *Phase*: **JCAFB-2024**

            #. Utilize o botão :bi:`Document Set Up` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14a)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-14a.sql

            gzip clvhealth_jcafb_2024_15_2023-12-14a.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-14a.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14a.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14a.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-14a.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14a.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-14a.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-14a.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-14a
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14a

Criar os Sumários relativos ao Grupo de Campo "Grupo 01 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 01 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 01 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 01 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 01 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 02 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 02 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 02 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 02 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 02 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 03 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 03 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 03 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 03 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 03 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 04 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 04 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 04 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 04 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 04 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 05 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 05 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 05 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 05 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 05 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 06 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 06 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 06 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 06 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 06 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 07 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 07 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 07 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 07 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 07 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 08 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 08 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 08 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 08 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 08 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 09 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 09 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 09 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 09 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 09 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 10 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 10 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 10 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 10 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 10 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 11 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 11 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 11 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 11 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 11 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 12 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 12 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 12 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 12 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 12 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 13 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 13 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 13 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 13 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 13 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 14 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 14 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 14 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 14 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 14 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Grupo 15 (2024)"
---------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Grupo 15 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Grupo 15 (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Grupo 15 (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Grupo 15 (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

Criar os Sumários relativos ao Grupo de Campo "Idosos - Ribeirao da Varzea (2024)"
----------------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Employee Summary Set Up` para Grupo de Campo "**Idosos - Ribeirao da Varzea (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Funcionários*:

            * Menu de acesso:

                * :bi:`Funcionários` » :bi:`Funcionários` » :bi:`Funcionários`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Trabalho`

        #. Selecionar o Funcionário com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Trabalho` = ":bi:`Grupo de Campo`"» "**Nome do Funcionário**" = *Idosos - Ribeirao da Varzea (2024)**.

        #. Executar a Ação ":bi:`Employee Summary Set Up`":

            #. Utilize o botão :bi:`Employee Summary Set Up` para executar a Ação.

    #. [tkl-odoo15-jcafb24-vm] Executar a Ação :bi:`Patient Summary Set Up` para os Pacientes associados ao Grupo de Campo "**Idosos - Ribeirao da Varzea (2024)**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb24-vm <https://tkl-odoo15-jcafb24-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Phase` » :bi:`Responsible Empĺoyee`

        #. Selecionar todos os Pacientes com: :bi:`Phase` = "**JCAFB-2024**" » :bi:`Responsible Empĺoyee` ="**Idosos - Ribeirao da Varzea (2024)**" (20 Pacientes).

        #. Executar a Ação ":bi:`Patient Summary Set Up`":

            #. Utilize o botão :bi:`Patient Summary Set Up` para executar a Ação.

[tkl-odoo15-jcafb24-vm] Criar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14b)
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
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-14b.sql

            gzip clvhealth_jcafb_2024_15_2023-12-14b.sql
            pg_dump clvhealth_jcafb_2024_15 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2024_15_2023-12-14b.sql

            cd /var/lib/odoo/.local/share/Odoo/filestore
            tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz clvhealth_jcafb_2024_15

            cd /opt/odoo/clvsol_filestore
            tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz clvhealth_jcafb

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

        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-14b.sql
        * /opt/odoo/clvhealth_jcafb_2024_15_2023-12-14b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

.. index:: clvhealth_jcafb_2024_15_2023-12-14b.sql
.. index:: clvhealth_jcafb_2024_15_2023-12-14b.sql.gz
.. index:: filestore_clvhealth_jcafb_2024_15_2023-12-14b
.. index:: clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b

[tkl-odoo15-jcafb24-vm] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2024-15* (2023-12-14b)
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
            # gzip -d clvhealth_jcafb_2024_15_2023-12-14b.sql.gz

            dropdb -i clvhealth_jcafb_2024_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2024_15
            psql -f clvhealth_jcafb_2024_15_2023-12-14b.sql -d clvhealth_jcafb_2024_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2024_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2024_15_2023-12-14b.tar.gz

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

            * "**https://tkl-odoo15-jcafb24-vm**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
