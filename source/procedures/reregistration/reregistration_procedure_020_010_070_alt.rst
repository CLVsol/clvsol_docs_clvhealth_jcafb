.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um Endereço fora da comunidade atendida pela JCAFB (Procedimento Alternativo)

==========================================================================================================================
A **Pessoa já cadastrada** mudou-se para um **Endereço fora da comunidade** atendida pela JCAFB (Procedimento Alternativo)
==========================================================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_070`".

    #. Procurar pelo registro :bi:`Person (Aux)` associado à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_025`

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Unvailable`
                * *Address is unavailable*: :bi:`Set` » **marcado**
                * *Address*: :bi:`Remove`
                * *Address (Aux) is unavailable*: :bi:`Set` » **marcado**
                * *Address (Aux)*: :bi:`Remove`
                * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                * *Clear Address Data*: **marcado**
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Caso necessário, editar o registro :bi:`Person (Aux)`:

        #. Preencher os campos de *Contact Information* com informações que indiquem o novo Endereço da Pessoa fora da comunidade.

        #. Salvar o registro.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
