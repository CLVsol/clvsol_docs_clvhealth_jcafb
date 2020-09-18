.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço não cadastrado

====================================================================
A **Pessoa não cadastrada** reside em um **Endereço não cadastrado**
====================================================================

**Cadastro Principal**:

    Nenhum registro será identificado.

**Cadastro Auxiliar**:

    O **Cadastro Auxiliar** criado poderá conter os seguintes registros:

        * :bi:`Person (Aux)`: relativo à Pessoa
        * :bi:`Address (Aux)`: relativo ao Endereço da Pessoa

**Relacionamento entre os registros dos Cadastros**:

    * :bi:`Address (Aux)`:

        * *Related Address* » **vazio**
        * *Contact Information* = Dados informados para o Endereço da Pessoa
        * Outros Dados = Outros Dados informados para o Endereço da Pessoa

    * :bi:`Person (Aux)`:

        * *Address* » **vazio**
        * *Family* » **vazio**
        * *Address (Aux)* » :bi:`Address (Aux)`
        * *Related Person* » **vazio**
        * *Contact Information* = Dados de Endereço de :bi:`Address (Aux)`
        * Outros Dados = Outros Dados informados para a Pessoa

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_020_020`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
