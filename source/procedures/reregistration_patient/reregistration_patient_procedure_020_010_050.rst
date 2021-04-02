.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um ourto Endereço da Comunidade (Procedimento)

=============================================================================================
O **Paciente já cadastrado** mudou-se para um ourto **Endereço da Comunidade** (Procedimento)
=============================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_020_010_050`".

    #. Procurar pelo registro :bi:`Patient` associado ao Paciente utilizando um dos procedimentos:

        * :doc:`reregistration_patient_procedure_010_010`
        * :doc:`reregistration_patient_procedure_010_020`

    #. A partir do registro :bi:`Patient` encontrado, exercutar a Ação ":bi:`Patient Associate to Patient (Aux)`":

        #. Parâmetros apresentados:

            * *Create new Patient (Aux)*: **habilitado**

        #. Utilizar o botão [:bi:`Associate do Patient (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente apresentado na *view* :bi:`Patients (Aux)`.

    #. Editar o registro :bi:`Patient (Aux)`:

        #. Preencher os dados de :bi:`Contact Information` com as informações apresentadas para o Endereço da Paciente.

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
