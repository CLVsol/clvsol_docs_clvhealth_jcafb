.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um outro Endereço já cadastrado (Procedimento Alternativo)

=======================================================================================================
A **Pessoa já cadastrada** mudou-se para um outro **Endereço já cadastrado** (Procedimento Alternativo)
=======================================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_040`".

    #. Procurar pelo registro :bi:`Person (Aux)` associado à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_025`

    #. Procurar pelo registro :bi:`Address (Aux)` :green:`(novo)` associado ao novo Endereço da Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_065`

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Address*: :bi:`Set` » :bi:`Address` :green:`(novo)` encontrado anteriormente
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

        #. Executar a Ação ":bi:`Person (Aux) Associate to Address (Aux)`":

            #. Parâmetros apresentados:

                * *Create new Address (Aux)*: **habilitado**

            #. Utilizar o botão [:bi:`Associate do Address (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Address (Aux)` associado à Pessoa apresentado na *view* :bi:`Addresses (Aux)`.

        #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Retornar ao registro :bi:`Person (Aux)`:

        #. Executar a Ação ":bi:`Person (Aux) Verification Execute`":

            #. Utilizar o botão [:bi:`Person (Aux) Verification Execute`] para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
