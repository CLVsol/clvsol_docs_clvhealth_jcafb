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

================================================
Manutenção do Banco de Dados - JCAFB-2027-16 [1]
================================================

[clvheatlh-jcafb-2026-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2027-16* (2026-05-03a)
------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2026-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2026-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            ssh clvheatlh-jcafb-2026-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2026-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2027_16_2026-05-03a.sql.gz

            # dropdb -i clvhealth_jcafb_2026_16
            dropdb -i clvhealth_jcafb_2027_16

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2027_16
            psql -f clvhealth_jcafb_2027_16_2026-05-03a.sql -d clvhealth_jcafb_2027_16 -U postgres -h localhost -p 5432 -q

            # mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            # rm -rf clvhealth_jcafb_2026_16
            rm -rf clvhealth_jcafb_2027_16
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

            # mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2027_16_2026-05-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2026-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2026-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2026-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2026-aws-tst <https://clvheatlh-jcafb-2026-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Definições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**https://100.26.91.51**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
