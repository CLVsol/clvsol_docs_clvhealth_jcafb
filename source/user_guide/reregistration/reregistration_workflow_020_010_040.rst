.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um Endereço já cadastrado

======================================================================
A **Pessoa já cadastrada** mudou-se para um **Endereço já cadastrado**
======================================================================

    Caso **exista uma Família** associada ao Endereço atual da Pessoa, a Pessoa continuará associada a essa Família e os itens indicados como ":green:`(Opcional)`" deverão ser considerados.

    Caso **não exista uma Família** associada ao Endereço atual da Pessoa, os itens indicados como ":green:`(Opcional)`" deverão ser desconsiderados.

Cadastro
--------

    O **Cadastro** identificado deverá conter os seguintes registros:

        * :bi:`Person`: relativo à Pessoa
        * :bi:`Address` :green:`(antigo)`: relativo ao antigo Endereço da Pessoa
        * :bi:`Address` :green:`(novo)`: relativo ao novo Endereço da Pessoa
        * :green:`(Opcional)` :bi:`Family`: relativo à Família da Pessoa

Cadastro Auxiliar
-----------------

    O **Cadastro Auxiliar** criado deverá conter os seguintes registros:

        * :bi:`Person (Aux)`
        * :bi:`Address (Aux)`

Relacionamento entre os registros dos Cadastros
-----------------------------------------------

    * :green:`(Opcional)` :bi:`Family`:

        * *Address* » :bi:`Address` :green:`(antigo)`
        * *Contact Information* = Dados de Endereço de :bi:`Address` :green:`(antigo)`

    * :bi:`Person`:

        * *Address* » :bi:`Address` :green:`(antigo)`
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Contact Information* = Dados de Endereço de :bi:`Address` :green:`(antigo)`

    * :bi:`Address (Aux)`:

        * *Related Address* » :bi:`Address` :green:`(novo)`
        * *Contact Information* = Dados de Endereço de :bi:`Address` :green:`(novo)`
        * Outros Dados = Outros Dados de :bi:`Address` :green:`(novo)`

    * :bi:`Person (Aux)`:

        * *Address* » :bi:`Address` :green:`(antigo)`
        * *Address (Aux)* » :bi:`Address (Aux)`
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Related Person* » :bi:`Person`
        * *Contact Information* = Dados de Endereço de :bi:`Address (Aux)`
        * Outros Dados = Outros Dados de :bi:`Person`

Fluxo de Trabalho (*Workflow*)
------------------------------

    #. **Cadastro**:

        #. Procurar pelo registro :bi:`Person` associado à Pessoa utilizando um dos métodos:

            * :doc:`reregistration_workflow_010_010`
            * :doc:`reregistration_workflow_010_020`

        #. Confirmar que todos os dados do registro :bi:`Person`, relacionados à Pessoa, serão mantidos.

        #. Confirmar a mudança de Endereço da Pessoa.

        #. :green:`(Opcional)` Confirmar que todos os dados do registro :bi:`Family`, associado ao registro :bi:`Person`, serão mantidos.

    #. **Cadastro**:

        #. Procurar pelo registro :bi:`Address` :green:`(novo)` associado ao novo Endereço informado para a Pessoa utilizando um dos métodos:

            * :doc:`reregistration_workflow_010_050`
            * :doc:`reregistration_workflow_010_060`

        #. Confirmar que todos os dados do registro :bi:`Address` :green:`(novo)` serão mantidos.

    #. **Cadastro Auxiliar**:

        #. Os registros do  **Cadastro Auxiliar** relacionados à Pessoa devem ser criados a partir do registro :bi:`Person`, executando a Ação ":BI:`Person Associate to Person (Aux)`":

                * A criação de :bi:`Person (Aux)`, deve ser **habilitada**.
                * A criação de :bi:`Address (Aux)`, deve ser **desabilitada**.

    #. Registro :bi:`Person (Aux)`:

        #. Remover do campo *Address* a associação ao registro :bi:`Address` :green:`(antigo)`.

        #. Associar o registro :bi:`Address` :green:`(novo)` ao campo *Address*.

    #. Registro :bi:`Person (Aux)`:

        #. Criar um novo registro :bi:`Address (Aux)`, executando a Ação ":bi:`Person (Aux) Associate to Address (Aux)`":

            * A criação de um registro :bi:`Address (Aux)`, deve ser **habilitada**.

    #. Registro :bi:`Address (Aux)`:

        #. Não será necessário qualquer ação de atualização do registro :bi:`Address (Aux)`.

    #. Registro :bi:`Person (Aux)`:

        #. Não será necessário qualquer ação de atualização adicional do registro :bi:`Person (Aux)`.

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedure/reregistration/reregistration_procedure_020_010_040`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
