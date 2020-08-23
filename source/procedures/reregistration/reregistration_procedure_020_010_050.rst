.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um Endereço não cadastrado (Procedimento)

======================================================================================
A **Pessoa já cadastrada** mudou-se para um **Endereço não cadastrado** (Procedimento)
======================================================================================

    Caso **exista uma Família** associada ao Endereço atual da Pessoa, a Pessoa continuará associada a essa Família e os itens indicados como ":green:`(Opcional)`" deverão ser considerados.

    Caso **não exista uma Família** associada ao Endereço atual da Pessoa, os itens indicados como ":green:`(Opcional)`" deverão ser desconsiderados.

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_010_050`".

    #. Procurar pelo registro :bi:`Person` associado à Pessoa utilizando um dos procedimentos:

        * :doc:`reregistration_procedure_010_010`
        * :doc:`reregistration_procedure_010_020`

    #. Confirmar que todos os dados do registro :bi:`Person`, relacionados à Pessoa, serão mantidos.

    #. Confirmar a mudança de Endereço da Pessoa.

    #. :green:`(Opcional)` Confirmar que todos os dados do registro :bi:`Family`, associado ao registro :bi:`Person`, serão mantidos.

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

    #. A partir do registro :bi:`Person` encontrado, exercutar a Ação ":bi:`Person Associate to Person (Aux)`":

        #. Parâmetros apresentados:

            * *Create new Person (Aux)*: **habilitado**
            * *Create new Family (Aux)*: **desabilitado**

        #. Utilizar o botão [:bi:`Associate do Perton (Aux)`] para executar a Ação.

    #. Abrir o registro :bi:`Person (Aux)` associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

    #. Editar o registro :bi:`Person (Aux)`:

        #. Remover do campo *Address* a associação ao registro :bi:`Address` :green:`(antigo)`, utilizando o botão [:bi:`Remove Reference Address`].

        #. Associar, manualmente, o campo *Address (Aux)* ao registro :bi:`Address (Aux)` criado anteriormente.

        #. Preencher os campos de *Contact Information* com os dados de Endereço do registro :bi:`Address (Aux)` associado ao campo *Address*, utilizando o botão [:bi:`Get Reference Address (Aux) Data`].

        #. Salvar o registro.

    #. A partir do registro :bi:`Person (Aux)`:

        #. Não será necessário a execução de qualquer procedimento adicional no registro :bi:`Person (Aux)`.

        #. Alterar o :bi:`Register State` para ":bi:`Revised`", utilizando o botão [:bi:`Revised`].

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
