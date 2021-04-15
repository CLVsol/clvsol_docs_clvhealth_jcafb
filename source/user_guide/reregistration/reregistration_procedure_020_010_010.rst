.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado continua a residir no mesmo Endereço

=====================================================================
O **Paciente já cadastrado** continua a residir no mesmo **Endereço**
=====================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_010_010`".

    #. Procurar pelo Paciente na *view* :bi:`Patients (Aux)`:

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Pesquisar pelo Paciente.

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente encontrado.

        #. Confirmar que as informações de :bi:`Contact Information` cadastradas para o Paciente coincidem com as informações de Endereço apresentadas para o mesmo.

        #. Verificar se os Outros Dados cadastrados para o Paciente coincidem com as informações dos Outros Dados apresentadas para o mesmo:

            #. Se for necessário atualizar alguma informação do cadastro:

                #. **Editar** o registro associado ao Paciente.

                #.  **Alterar** os parâmetros necessários.

                #. **Salvar** o registro.

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: :bi:`Phase` **atual**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
