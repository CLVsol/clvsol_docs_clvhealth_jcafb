.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada continua a residir no Endereço já cadastrado

===========================================================================
A **Pessoa já cadastrada** continua a residir no **Endereço já cadastrado**
===========================================================================

    Caso **exista uma Família** associada à Pessoa, o registro *Person (Aux)* será associado a essa Família e os itens indicados como ":green:`(Opcional)`" deverão ser considerados.

    Caso **não exista uma Família** associada à Pessoa, os itens indicados como ":green:`(Opcional)`" deverão ser desconsiderados.

**Cadastro Principal**:

    O **Cadastro Principal** identificado poderá conter os seguintes registros:

        * :bi:`Person`: relativo à Pessoa
        * :bi:`Address`: relativo ao Endereço da Pessoa
        * :green:`(Opcional)` :bi:`Family`: relativo à Família da Pessoa

**Cadastro Auxiliar:**

    O **Cadastro Auxiliar** criado poderá conter os seguintes registros:

        * :bi:`Person (Aux)`: relativo à Pessoa
        * :bi:`Address (Aux)`: relativo ao Endereço da Pessoa

**Relacionamento entre os registros dos Cadastros**:

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

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_010_010`".

    Alternativamente, considerando a :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`, o processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_010_010_alt`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
