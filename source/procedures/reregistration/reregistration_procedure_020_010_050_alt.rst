.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um ourto Endereço não cadastrado (Procedimento Alternativo)

========================================================================================================
A **Pessoa já cadastrada** mudou-se para um ourto **Endereço não cadastrado** (Procedimento Alternativo)
========================================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_050`".

    #. Procurar pelo registro :bi:`Person (Aux)` associado à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_025`

    #. Procurar por um registro :bi:`Address` associado ao Endereço da Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_065`

    #. Confirmar que o registro :bi:`Address (Aux)` não seja encontrado.

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Criar um novo registro :bi:`Address (Aux)`:

        #. Preencher o registro :bi:`Address (Aux)` com as informações apresentadas para o Endereço da Pessoa.

        #. Salvar o registro.

        #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Address*: :bi:`Remove`
                * *Address (Aux)*: :bi:`Set` » :bi:`Address (Aux)` :green:`(novo)` criado anteriormente
                * *Get Reference Address (Aux) Data*: **marcado**
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
