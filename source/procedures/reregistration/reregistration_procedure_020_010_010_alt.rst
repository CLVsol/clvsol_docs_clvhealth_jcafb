.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada continua a residir no Endereço já cadastrado (Procedimento Alternativo)

======================================================================================================
A **Pessoa já cadastrada** continua a residir no **Endereço já cadastrado** (Procedimento Alternativo)
======================================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_010`".

    #. Procurar pelo registro :bi:`Person (Aux)` associado à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_025`

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

    #. Abrir o registro :bi:`Address (Aux)` associado ao campo *Address (Aux)*:

        #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Retornar ao registro :bi:`Person (Aux)`:

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
