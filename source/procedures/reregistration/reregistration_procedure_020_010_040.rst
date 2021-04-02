.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um outro Endereço já cadastrado (Procedimento)

===========================================================================================
A **Pessoa já cadastrada** mudou-se para um outro **Endereço já cadastrado** (Procedimento)
===========================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_040`".

    #. Procurar pelo registro :bi:`Person` associado à Pessoa utilizando um dos procedimentos:

        * :doc:`reregistration_procedure_010_010`
        * :doc:`reregistration_procedure_010_020`

    #. Procurar pelo registro :bi:`Address` :green:`(novo)` associado ao novo Endereço informado para a Pessoa utilizando um dos procedimentos:

        * :doc:`/reference_guide/reregistration/reregistration_workflow_010_050`
        * :doc:`/reference_guide/reregistration/reregistration_workflow_010_060`

    #. A partir do registro :bi:`Person` encontrado, exercutar a Ação ":bi:`Person Associate to Person (Aux)`":

        #. Parâmetros apresentados:

            * *Create new Person (Aux)*: **habilitado**
            * *Create new Family (Aux)*: **desabilitado**

        #. Utilizar o botão [:bi:`Associate to Person (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

    #. Editar o registro :bi:`Person (Aux)`:

        #. Remover do campo *Address* a associação ao registro :bi:`Address` :green:`(antigo)`, utilizando o botão [:bi:`Remove Reference Address`].

        #. Associar, manualmente, o campo *Address* ao registro :bi:`Address` :green:`(novo)` encontrado anteriormente.

        #. Salvar o registro.

    #. A partir do registro :bi:`Person (Aux)` exercutar a Ação ":bi:`Person (Aux) Associate to Address (Aux)`":

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
