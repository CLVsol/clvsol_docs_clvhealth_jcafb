.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Procura por um Endereço em Contatos (Procedimento)

======================================================
Procura por um Endereço em **Contatos** (Procedimento)
======================================================

    * *Workflow*: ":doc:`reregistration_workflow_010_050`".

    #. Procurar pelo Endereço na *view* :bi:`Contatos`:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Selecionar a **visualização em lista**.

        #. Aplicar o filtro: **Agrupar Por** » :bi:`Address Type`.

        #. Pesquisar pelo Endereço.

    #. **Caso um registro associado a esse Endereço seja encontrado** com *Address Type* ":bi:`Address`", independentemente da existência ou não de um registro com *Address Type* ":bi:`Address (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Address`.

        #. Acionar o botão **[** :bi:`Address` **]**.

        #. Utilizar o registro associado ao Endereço apresentado na *view* :bi:`Addresses`.

        #. O Endereço será declarado como "**já cadastrado**".

    #. **Caso um registro associado a esse Endereço seja encontrado** somente com *Address Type* ":bi:`Address (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Address (Aux)`".

        #. Acionar o botão **[** :bi:`Address (Aux)` **]**.

        #. Utilizar o registro associado ao Endereço apresentado na *view* :bi:`Addresses (Aux)`.

        #. O Endereço será declarado como **em fase de recadastramento**.

    #.  **Caso um registro associado a esse Endereço NÃO seja encontrado** com qualquer *Address Type*:

        #. O Endereço será declarado como "**não cadastrado**".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
