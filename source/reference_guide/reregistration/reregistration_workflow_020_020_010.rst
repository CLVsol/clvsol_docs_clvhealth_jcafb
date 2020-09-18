.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço já cadastrado

===================================================================
A **Pessoa não cadastrada** reside em um **Endereço já cadastrado**
===================================================================

**Cadastro Principal**:

    O **Cadastro** identificado poderá conter os seguintes registros:

        * :bi:`Address`: relativo ao Endereço da Pessoa

**Cadastro Auxiliar**:

    O **Cadastro Auxiliar** criado poderá conter os seguintes registros:

        * :bi:`Person (Aux)`: relativo à Pessoa
        * :bi:`Address (Aux)`: relativo ao Endereço da Pessoa

**Relacionamento entre os registros dos Cadastros**:

    * :bi:`Address (Aux)`:

        * *Related Address* » :bi:`Address`
        * *Contact Information* = Dados de Endereço de :bi:`Address`
        * Outros Dados = Outros Dados de :bi:`Address`

    * :bi:`Person (Aux)`:

        * *Address* » :bi:`Address`
        * *Family* » **vazio**
        * *Address (Aux)* » :bi:`Address (Aux)`
        * *Related Person* » **vazio**
        * *Contact Information* = Dados de Endereço de :bi:`Address`
        * Outros Dados = Outros Dados informados para a Pessoa

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_020_010`".

    Alternativamente, considerando a :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`, o processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_020_010_alt`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
