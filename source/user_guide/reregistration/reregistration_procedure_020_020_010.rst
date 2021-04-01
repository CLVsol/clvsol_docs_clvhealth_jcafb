.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço da Comunidade (Procedimento)

====================================================================================
O **Paciente não cadastrado** reside em um **Endereço da Comunidade** (Procedimento)
====================================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_020_010`".

    #. Acessar a *view* :bi:`Patients (Aux)`:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. Criar um novo registro :bi:`Person (Aux)`:

        #. Preencher o registro :bi:`Person (Aux)` com as informações apresentadas para a Pessoa, exceto informaçôes relativas ao Endereço.

        #. Salvar o registro.

        #. Editar o registro :bi:`Patient (Aux)`:

            #. Preencher os dados de :bi:`Contact Information` com as informações apresentadas para o Endereço da Paciente.

            #. Salvar o registro.

        #. Exercutar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
