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

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-18a)
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
            # gzip -d clvhealth_jcafb_2021v_14_2021-02-18a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-18a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-18a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-18a.tar.gz

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

Instalar o(s) módulo(s) [ver lista]
-----------------------------------

    #. [tkl-odoo14-jcafb21-vm] Lista de Módulos:

        * clv_patient
        * clv_patient_community
        * clv_patient_aux
        * clv_patient_jcafb
        * clv_patient_aux_jcafb
        * clv_patient_verification_jcafb
        * clv_patient_aux_verification_jcafb
        * clv_patient_community_verification_jcafb

    #. [clvhealth-jcafb-2021-vm-pro] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **clvhealth-jcafb-2021-vm-pro** e executar o *Odoo* no modo manual:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                ssh clvhealth-jcafb-2021-vm-pro -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **clvhealth-jcafb-2021-vm-pro** e executar o **install.py**:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 2)
                #

                ssh clvhealth-jcafb-2021-vm-pro -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13"
            
        #. Retornar a execução do *Odoo* do servidor **clvhealth-jcafb-2021-vm-pro** ao modo desejado:

            ::

                # ***** clvhealth-jcafb-2021-vm-pro (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Marcar as Pessoas que sejam Pacientes da JCAFB-2021v
----------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Mass Edit`:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Is Patient` » :bi:`Categories`

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`" » :bi:`Categories` = "**Criança**"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Is Patient` = ":bi:`false`" » :bi:`Categories` = "**Idoso**"

        #. Exercutar a Ação ":bi:`Person Mass Edit`":

            * Parâmetros utilizados:

                * *Is Patient*: **Set** **marcado**

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

Executar o processo de verificação para todas as Pessoas
--------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Person Verification Execute` para todas as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:
                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Selecionar todas as Pessoas

        #. Exercutar a Ação ":bi:`Person Verification Execute`":

            #. Utilize o botão :bi:`Person Verification Execute` para executar a Ação.

Associar as Pessoas a um Paciente
---------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação *Person Associate to Patient* para as Pessoas:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Persons*:

            * Menu de acesso:

                * *Community* > *Community* > *Persons*

        #. Ativar o filtro **Agrupar por** » :bi:`Verification State` » :bi:`Verification Outcome Informations`

        #. Selecionar todas as Pessoas com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Patient" register.`"

        #. Exercutar a Ação "**Person Associate to Patient**":

            * Parâmetros utilizados:

                * *Create new Patient*: **marcado**

            #. Utilize o botão *Associate to Patient* para executar a Ação.

        #. Selecionar todas as Pessoas com: :bi:`Verification State` = ":bi:`Error (L0)`" » :bi:`Verification Outcome Informations` = ":bi:`Missing related "Patient" register.`"

        #. Exercutar a Ação ":bi:`Person Verification Execute`":

            #. Utilize o botão :bi:`Person Verification Execute` para executar a Ação.

Executar o processo de verificação para todos os Patientes
----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Patientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patients`

        #. Selecionar todos os Patientes

        #. Exercutar a Ação ":bi:`Patient Verification Execute`":

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

Associar todos os Patientes a um Paciente (Aux)
-----------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Associate to Patient (Aux)` para todos os Pacientes:

        #. Acessar a *view* :bi:`Patients`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Register State`

        #. Selecionar todos os Pacientes com :bi:`Register State` != ":bi:`Canceled`"

        #. Exercutar a Ação :bi:`Patient Associate to Patient (Aux)`:

            * Parâmetros utilizados:

                * *Create new Patient (Aux)*: **marcado**

            #. Utilize o botão :bi:`Associate to Patient (Aux)` para executar a Ação.

Executar o processo de verificação para todos os Patientes
----------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient Verification Execute` para todos os Patientes:

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patients`

        #. Selecionar todos os Patientes

        #. Exercutar a Ação ":bi:`Patient Verification Execute`":

            #. Utilize o botão :bi:`Patient Verification Execute` para executar a Ação.

Executar o processo de verificação para todos os Patientes (Aux)
----------------------------------------------------------------

    #. [tkl-odoo14-jcafb21-vm] Executar a Ação :bi:`Patient (Aux) Verification Execute` para todos os Patientes (Aux):

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo14-jcafb21-vm <https://tkl-odoo14-jcafb21-vm>`_

        #. Acessar a *View* *Patients*:

            * Menu de acesso:
                * :bi:`Health` » :bi:`Health` » :bi:`Patients (Aux)`

        #. Selecionar todos os Patientes

        #. Exercutar a Ação ":bi:`Patient (Aux) Verification Execute`":

            #. Utilize o botão :bi:`Patient (Aux) Verification Execute` para executar a Ação.

.. toctree::   :maxdepth: 2
