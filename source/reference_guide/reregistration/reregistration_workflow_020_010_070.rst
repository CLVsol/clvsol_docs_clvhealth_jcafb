.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa já cadastrada mudou-se para um Endereço fora da comunidade atendida pela JCAFB

===============================================================================================
A **Pessoa já cadastrada** mudou-se para um **Endereço fora da comunidade** atendida pela JCAFB
===============================================================================================

    Caso **exista uma Família** associada à Pessoa, o registro *Person (Aux)* será associado a essa Família e os itens indicados como ":green:`(Opcional)`" deverão ser considerados.

    Caso **não exista uma Família** associada à Pessoa, os itens indicados como ":green:`(Opcional)`" deverão ser desconsiderados.

**Cadastro Principal**:

    O **Cadastro** identificado deverá conter os seguintes registros:

        * :bi:`Person`: relativo à Pessoa
        * :bi:`Address` :green:`(antigo)`: relativo ao antigo Endereço da Pessoa
        * :green:`(Opcional)` :bi:`Family`: relativo à Família da Pessoa

**Cadastro Auxiliar**:

    O **Cadastro Auxiliar** criado deverá conter os seguintes registros:

        * :bi:`Person (Aux)`: relativo à Pessoa

**Relacionamento entre os registros dos Cadastros**:

    * :green:`(Opcional)` :bi:`Family`:

        * *Address* » :bi:`Address` :green:`(antigo)`
        * *Contact Information* = Dados de Endereço de :bi:`Address` :green:`(antigo)`

    * :bi:`Person`:

        * *Address* » :bi:`Address` :green:`(antigo)`
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Contact Information* = Dados de Endereço de :bi:`Address` :green:`(antigo)`

    * :bi:`Person (Aux)`:

        * *Address* » **vazio**
        * *Address (Aux)* » **vazio**
        * :green:`(Opcional)` *Family* » :bi:`Family`
        * *Related Person* » :bi:`Person`
        * *Contact Information* = Dados com informações que indiquem o novo Endereço da Pessoa fora da comunidade, se disponível, ou **vazio**.
        * Outros Dados = Outros Dados de :bi:`Person`

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_010_070`".

    Alternativamente, considerando a :doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`, o processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_010_070_alt`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
