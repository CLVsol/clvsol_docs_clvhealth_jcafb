.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço não cadastrado (Procedimentos)

====================================================================================
A **Pessoa não cadastrada** reside em um **Endereço não cadastrado** (Procedimentos)
====================================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_020_020`".

    #. Procurar pelo(s) registro(s) :bi:`Person` e/ou :bi:`Person (Aux)` associado(s) à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_010`

    #. Confirmar que o(s) registro(s) :bi:`Person` e/ou :bi:`Person (Aux)` não seja(m) encontrado(s).

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

        #. Não será necessário a execução de qualquer procedimento adicional no registro :bi:`Address (Aux)`.

        #. Alterar o :bi:`Register State` para ":bi:`Revised`", utilizando o botão [:bi:`Revised`].

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Criar um novo registro :bi:`Person (Aux)`:

        #. Preencher o registro :bi:`Person (Aux)` com as informações apresentadas para a Pessoa, exceto informaçôes relativas ao Endereço e à Família.

        #. Salvar o registro.

    #. Editar o registro :bi:`Person (Aux)`:

        #. Associar, manualmente, o campo *Address (Aux)* ao registro :bi:`Address (Aux)` criado anteriormente.

        #. Preencher os campos de *Contact Information* com os dados de Endereço do registro :bi:`Address (Aux)` associado ao campo *Address*, utilizando o botão [:bi:`Get Reference Address (Aux) Data`].

        #. Salvar o registro.

    #. Retornar ao registro :bi:`Person (Aux)`.

        #. Não será necessário a execução de qualquer procedimento adicional no registro :bi:`Person (Aux)`.

        #. Alterar o :bi:`Register State` para ":bi:`Revised`", utilizando o botão [:bi:`Revised`].

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
