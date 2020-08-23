.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Procura por uma Pessoa em Contatos (Procedimento)

=========================================================
Procura por uma **Pessoa** em **Contatos** (Procedimento)
=========================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_010_010`".

    #. Procurar pela Pessoa na *view* :bi:`Contatos`:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Selecionar a **visualização em lista**.

        #. Aplicar o filtro: **Agrupar Por** » :bi:`Address Type`.

        #. Pesquisar pela Pessoa.

    #. **Caso um registro associado a essa Pessoa seja encontrado** com *Address Type* ":bi:`Person`", independentemente da existência ou não de um registro com *Address Type* ":bi:`Person (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Person`.

        #. Acionar o botão **[** :bi:`Person` **]**.

        #. Utilizar o registro associado à Pessoa apresentado na *view* :bi:`Persons`.

        #. A Pessoa será declarada como "**já cadastrada**".

    #. **Caso um registro associado a essa Pessoa seja encontrado** somente com *Address Type* ":bi:`Person (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Person (Aux)`".

        #. Acionar o botão **[** :bi:`Person (Aux)` **]**.

        #. Utilizar o registro associado à Pessoa apresentado na *view* :bi:`Persons (Aux)`.

        #. A Pessoa será declarada como "**em fase de recadastramento**".

    #.  **Caso um registro associado a essa Pessoa NÃO seja encontrado** com qualquer *Address Type*:

        #. A Pessoa será declarada como "**não cadastrada**".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
