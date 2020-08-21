.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação individualizada do Cadastro Auxiliar (Pessoa já cadastrada)

==================================================================
A **Pessoa já cadastrada** reside em um **Endereço já cadastrado**
==================================================================

    Caso **exista uma Família** associada à Pessoa, o registro *Person (Aux)* será associada a essa Família e os itens indicados como ":green:`(Opcional)`" deverão ser considerados.

    Caso **não exista uma Família** associada à Pessoa, os itens indicados como ":green:`(Opcional)`" deverão ser desconsiderados.

Cadastro
--------

    O **Cadastro** identificado poderá conter os seguintes registros:

        * :bi:`Person`: relativo à Pessoa
        * :bi:`Address`: relativo ao Endereço da Pessoa
        * :green:`(Opcional)` :bi:`Family`: relativo à Família da Pessoa

Cadastro Auxiliar
-----------------

    O **Cadastro Auxiliar** criado poderá conter os seguintes registros:

        * :bi:`Person (Aux)`
        * :bi:`Address (Aux)`

Relacionamento entre os registros dos Cadastros
-----------------------------------------------

    * :green:`(Opcional)` :bi:`Family`:

        * *Address* » :bi:`Address`
        * *Contact Information* = Dados de Endereço de :bi:`Address`

    * :bi:`Person`:

        * *Address* » :bi:`Address`
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Contact Information* = Dados de Endereço de :bi:`Address`

    * :bi:`Address (Aux)`:

        * *Related Address* » :bi:`Address`
        * *Contact Information* = Dados de Endereço de :bi:`Address`
        * Outros Dados = Outros Dados de :bi:`Address`

    * :bi:`Person (Aux)`:

        * *Address* » :bi:`Address`
        * *Address (Aux)* » :bi:`Address (Aux)`
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Related Person* » :bi:`Person`
        * *Contact Information* = Dados de Endereço de :bi:`Address`
        * Outros Dados = Outros Dados de :bi:`Person`

Fluxo de Trabalho (*Workflow*)
------------------------------

    #. **Cadastro**:

        #. Procurar pelo registro :bi:`Person` associado à Pessoa utilizando um dos métodos:

            * :doc:`reregistration_workflow_010_010`
            * :doc:`reregistration_workflow_010_020`

        #. Confirmar que todos os dados do registro :bi:`Person` associado à Pessoa serão mantidos.

        #. Confirmar que todos os dados do registro :bi:`Address`, associado ao registro :bi:`Person`, serão mantidos.

        #. :green:`(Opcional)` Confirmar que todos os dados do registro :bi:`Family`, associado ao registro :bi:`Person`, serão mantidos.

    #. **Cadastro Auxiliar**:

        #. Os registros do  **Cadastro Auxiliar** relacionados à Pessoa devem ser criados a partir do registro :bi:`Person`, executando a Ação ":BI:`Person Associate to Person (Aux)`":

                * A criação de :bi:`Person (Aux)`, deve ser **habilitada**.
                * A criação de :bi:`Address (Aux)`, deve ser **habilitada**.

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`reregistration_procedure_020_010_010`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
