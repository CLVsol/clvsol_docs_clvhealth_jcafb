.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um ourto Endereço não cadastrado (Procedimento)

============================================================================================
A **Pessoa já cadastrada** mudou-se para um ourto **Endereço não cadastrado** (Procedimento)
============================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_050`".

    #. Procurar pelo registro :bi:`Person` associado à Pessoa utilizando um dos procedimentos:

        * :doc:`reregistration_procedure_010_010`
        * :doc:`reregistration_procedure_010_020`

    #. Procurar por um registro :bi:`Address` associado ao Endereço da Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_050`

    #. Confirmar que o(s) registro(s) :bi:`Address` e/ou :bi:`Address (Aux)` não seja(m) encontrado(s).

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Criar um novo registro :bi:`Address (Aux)`:

        #. Preencher o registro :bi:`Address (Aux)` com as informações apresentadas para o Endereço da Pessoa.

        #. Salvar o registro.

    #. Registro :bi:`Address (Aux)`.

        #. Executar a Ação ":bi:`Address (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Available`
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. A partir do registro :bi:`Person` encontrado, exercutar a Ação ":bi:`Person Associate to Person (Aux)`":

        #. Parâmetros apresentados:

            * *Create new Person (Aux)*: **habilitado**
            * *Create new Family (Aux)*: **desabilitado**

        #. Utilizar o botão [:bi:`Associate do Perton (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

    #. Editar o registro :bi:`Person (Aux)`:

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
