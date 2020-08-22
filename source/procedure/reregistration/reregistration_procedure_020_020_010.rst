.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço já cadastrado (Procedimento)

==================================================================================
A **Pessoa não cadastrada** reside em um **Endereço já cadastrado** (Procedimento)
==================================================================================

    * *Workflow*: ":doc:`/user_guide/reregistration/reregistration_workflow_020_020_010`".

    #. Procurar pelo(s) registro(s) :bi:`Person` e/ou :bi:`Person (Aux)` associado(s) à Pessoa utilizando o procedimento:

        * :doc:`reregistration_procedure_010_010`

    #. Confirmar que o(s) registro(s) :bi:`Person` e/ou :bi:`Person (Aux)` não seja(m) encontrado(s).

    #. Procurar por um registro :bi:`Address` associado ao Endereço da Pessoa utilizando um dos procedimentos:

        * :doc:`reregistration_procedure_010_050`
        * :doc:`reregistration_procedure_010_060`

    #. Confirmar que todos os dados do registro :bi:`Address`, relacionado ao Endereço da Pessoa, serão mantidos.

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Criar um novo registro :bi:`Person (Aux)`:

        #. Preencher o registro :bi:`Person (Aux)` com as informações apresentadas para a Pessoa, exceto informaçôes relativas ao Endereço.

        #. Salvar o registro.

    #. Editar o registro :bi:`Person (Aux)`:

        #. Associar, manualmente, o campo *Address* ao registro :bi:`Address` encontrado anteriormente.

        #. Preencher os campos de *Contact Information* com os dados de Endereço do registro :bi:`Address` associado ao campo *Address*, utilizando o botão [:bi:`Get Reference Address Data`].

        #. Salvar o registro.

    #. A partir do registro :bi:`Person (Aux)` exercutar a Ação ":bi:`Person (Aux) Associate to Address (Aux)`":

        #. Parâmetros apresentados:

            * *Create new Address (Aux)*: **habilitado**

        #. Utilizar o botão [:bi:`Associate do Address (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Address (Aux)` associado à Pessoa apresentado na *view* :bi:`Addresses (Aux)`.

        #. Não será necessário a execução de qualquer procedimento adicional no registro :bi:`Address (Aux)`.

        #. Alterar o :bi:`Register State` para ":bi:`Revised`", utilizando o botão [:bi:`Revised`].

    #. Retornar ao registro :bi:`Person (Aux)`.

        #. Não será necessário a execução de qualquer procedimento adicional no registro :bi:`Person (Aux)`.

        #. Alterar o :bi:`Register State` para ":bi:`Revised`", utilizando o botão [:bi:`Revised`].

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
