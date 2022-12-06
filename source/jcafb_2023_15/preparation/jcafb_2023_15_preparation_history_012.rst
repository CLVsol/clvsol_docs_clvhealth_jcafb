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

=================================================================
JCAFB-2023-15  (Tratamento de Documentos Testes de Laboratório 1)
=================================================================

Restaurar um backup do banco de dados *CLVhealth-JCAFB-2023-15* (2022-12-05c)
-----------------------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Estabelecer uma sessão ssh com o servidor **tkl-odoo15-jcafb23-vm** e paralizar o *Odoo*:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            ssh tkl-odoo15-jcafb23-vm -l root

            /etc/init.d/odoo stop

            su odoo

    #. [tkl-odoo15-jcafb23-vm] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            # gzip -d clvhealth_jcafb_2023_15_2022-12-05c.sql.gz

            dropdb -i clvhealth_jcafb_2023_15

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2023_15
            psql -f clvhealth_jcafb_2023_15_2022-12-05c.sql -d clvhealth_jcafb_2023_15 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2023_15
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2023_15_2022-12-05c.tar.gz

    #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

        ::

            # ***** tkl-odoo15-jcafb23-vm
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. :red:`(Não Executado)` [tkl-odoo15-jcafb23-vm] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://tkl-odoo15-jcafb23-vm**".

        #. Salvar o registro editado.

Atualizar o(s) módulo(s) [ver lista]
------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_lab_test

    #. [tkl-odoo15-jcafb23-vm] **Executar** a atualização do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2021v_13" -m clv_lab_test

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Habilitar a instalação e instalar o(s) módulo(s) [ver lista]
------------------------------------------------------------

    #. [tkl-odoo15-jcafb23-vm] Lista de Módulos:

        * clv_document_survey
        * clv_lab_test_survey
    #. [tkl-odoo15-jcafb23-vm] **Executar** a instalação do(s) Módulo(s):

        #. Estabelecer uma sessão ssh (session 1) com o servidor **tkl-odoo15-jcafb23-vm** e executar o *Odoo* no modo manual:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                ssh tkl-odoo15-jcafb23-vm -l root

                /etc/init.d/odoo stop

                su odoo
                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        #. Estabelecer uma sessão ssh (session 2) com o servidor **tkl-odoo15-jcafb23-vm** e executar o **install.py**:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 2)
                #

                ssh tkl-odoo15-jcafb23-vm -l odoo

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                
                python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb_2023_15"

        #. Retornar a execução do *Odoo* do servidor **tkl-odoo15-jcafb23-vm** ao modo desejado:

            ::

                # ***** tkl-odoo15-jcafb23-vm (session 1)
                #

                cd /opt/odoo
                /usr/bin/odoo -c /etc/odoo/odoo-man.conf

                ^C

                exit

                /etc/init.d/odoo start

Criar os *Document Types* para a JCAFB-2023
-------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Document Types* para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

            * **QAN23**

                * *Document Type*: **QAN23**
                * *Document Type Code*: **QAN23**
                * *Document Type Description*: **JCAFB 2023 - Questionário para Detecção de Anemia**
                * *Phase*: **JCAFB-2023**

            * **QDH23**

                * *Document Type*: **QDH23**
                * *Document Type Code*: **QDH23**
                * *Document Type Description*: **JCAFB 2023 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Phase*: **JCAFB-2023**

            * **QMD23**

                * *Document Type*: **QMD23**
                * *Document Type Code*: **QMD23**
                * *Document Type Description*: **JCAFB 2023 - Questionário - Medicamentos**
                * *Phase*: **JCAFB-2023**

            * **QSC23**

                * *Document Type*: **QSC23**
                * *Document Type Code*: **QSC23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Individual (Crianças)**
                * *Phase*: **JCAFB-2023**

            * **QSF23**

                * *Document Type*: **QSF23**
                * *Document Type Code*: **QSF23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Familiar**
                * *Phase*: **JCAFB-2023**

            * **QSI23**

                * *Document Type*: **QSI23**
                * *Document Type Code*: **QSI23**
                * *Document Type Description*: **JCAFB 2023 - Questionário Socioeconômico Individual (Idosos)r**
                * *Phase*: **JCAFB-2023**

Criar os *Lab Test Types* para a JCAFB-2023
-------------------------------------------

    #. Conectar-se, via *browser*, ao *Odoo* do servidor `tkl-odoo15-jcafb23-vm <https://tkl-odoo15-jcafb23-vm>`_

    #. Criar os *Lab Test Types* para a **JCAFB-2023**:

        * Menu de acesso:
            
            * :bi:`Base` » :bi:`Configuration` » :bi:`Document` » :bi:`Types`

        * *Lab Test Types* criados:
            
            * **EAN23**

                * *Lab Test Type*: **EAN23**
                * *Lab Test Type Code*: **EAN23**
                * *Lab Test Type Description*: **JCAFB 2023 - Exames - Detecção de Anemia**
                * *Phase*: **JCAFB-2023**

            * **ECP23**

                * *Lab Test Type*: **ECP23**
                * *Lab Test Type Code*: **ECP23**
                * *Lab Test Type Description*: **JCAFB 2023 - Laboratório - Parasitologia**
                * *Phase*: **JCAFB-2023**

            * **EDH23**

                * *Lab Test Type*: **EDH23**
                * *Lab Test Type Code*: **EDH23**
                * *Lab Test Type Description*: **JCAFB 2023- Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
                * *Phase*: **JCAFB-2023**

            * **EUR23**

                * *Lab Test Type*: **EUR23**
                * *Lab Test Type Code*: **EUR23**
                * *Lab Test Type Description*: **JCAFB 2023 - Laboratório - Urinálise**
                * *Phase*: **JCAFB-2023**

.. toctree::   :maxdepth: 2
