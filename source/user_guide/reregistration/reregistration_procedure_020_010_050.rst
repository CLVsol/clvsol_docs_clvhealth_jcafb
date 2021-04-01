.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um outro Endereço da Comunidade (Procedimento)

=============================================================================================
O **Paciente já cadastrado** mudou-se para um outro **Endereço da Comunidade** (Procedimento)
=============================================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_010_050`".

    #. Procurar pelo registro :bi:`Patient (Aux)` associado ao Paciente utilizando o procedimento:

        * :doc:`reregistration_procedure_010_030`

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente apresentado na *view* :bi:`Patients (Aux)`.

        #. Preencher os dados de :bi:`Contact Information` com as informações apresentadas para o Endereço da Paciente.

        #. Exercutar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
