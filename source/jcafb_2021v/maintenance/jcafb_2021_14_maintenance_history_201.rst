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
Manutenção do Banco de Dados - JCAFB-2021v-14
=============================================

[clvheatlh-jcafb-2021-aws-tst] Restaurar um backup do banco de dados *CLVhealth-JCAFB-2021v-14* (2021-02-03a)
--------------------------------------------------------------------------------------------------------------

    #. [clvheatlh-jcafb-2021-aws-tst] Estabelecer uma sessão ssh com o servidor **clvheatlh-jcafb-2021-aws-tst** e paralizar o *Odoo*:

        ::

            # ***** clvheatlh-jcafb-2021-aws-tst
            #

            ssh clvheatlh-jcafb-2021-aws-tst -l root

            /etc/init.d/odoo stop

            su odoo

    #. [clvheatlh-jcafb-2021-aws-tst] Executar os comandos de restauração dos arquivos de backup:

        ::

            # ***** clvheatlh-jcafb-2021-aws-tst
            #

            cd /opt/odoo
            gzip -d clvhealth_jcafb_2021v_14_2021-02-03a.sql.gz

            dropdb -i clvhealth_jcafb_2021v_14

            createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb_2021v_14
            psql -f clvhealth_jcafb_2021v_14_2021-02-03a.sql -d clvhealth_jcafb_2021v_14 -U postgres -h localhost -p 5432 -q

            mkdir /var/lib/odoo/.local/share/Odoo/filestore
            cd /var/lib/odoo/.local/share/Odoo/filestore
            rm -rf clvhealth_jcafb_2021v_14
            tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2021v_14_2021-02-03a.tar.gz

            mkdir /opt/odoo/clvsol_filestore
            cd /opt/odoo/clvsol_filestore
            rm -rf clvhealth_jcafb
            tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2021v_14_2021-02-03a.tar.gz

    #. Retornar a execução do *Odoo* do servidor **clvheatlh-jcafb-2021-aws-tst** ao modo desejado:

        ::

            # ***** clvheatlh-jcafb-2021-aws-tst
            #

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

            ^C

            exit

            /etc/init.d/odoo start

    #. [clvheatlh-jcafb-2021-aws-tst] Configurar o parâmetro "**web.base.url**":

        #. Conectar-se, via *browser*, ao *Odoo* do servidor `clvheatlh-jcafb-2021-aws-tst <https://clvheatlh-jcafb-2021-aws-tst>`_

        #. Acessar a *View* **Parâmetros do Sistema**:

            * Menu de acesso:
                
                * **Defilnições** » **Técnico** » **Parâmetros** » **Parâmetros do Sistema**

        #. Pesquisar pelo registro com a **Chave** "**web.base.url**"

        #. Editar o registro apresentado (**Chave**: "**web.base.url**")

        #. Alterar o campo **Valor** para:

            * "**http://clvheatlh-jcafb-2021-aws-tst.tklapp.com**".

        #. Salvar o registro editado.

.. toctree::   :maxdepth: 2
