.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrada reside em um Endereço fora da comunidade atendida pela JCAFB (Procedimento)

=============================================================================================================
O **Paciente não cadastrada** reside em um **Endereço fora da comunidade** atendida pela JCAFB (Procedimento)
=============================================================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_020_030`".

    #. Acessar a *view* :bi:`Patients (Aux)`:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. Criar um novo registro :bi:`Patient (Aux)`:

        #. Preencher o registro :bi:`Patient (Aux)` com as informações apresentadas para a Paciente, exceto informaçôes relativas ao Endereço.

        #. Salvar o registro.

        #. Exercutar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Unvailable`
                * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                * *Clear Address Data*: **marcado**
                * *Phase*: **JCAFB-2021v**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Caso necessário, editar o registro :bi:`Patient (Aux)`:

        #. Preencher os campos de *Contact Information* com informações que indiquem o novo Endereço da Paciente fora da comunidade.

        #. Salvar o registro.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
