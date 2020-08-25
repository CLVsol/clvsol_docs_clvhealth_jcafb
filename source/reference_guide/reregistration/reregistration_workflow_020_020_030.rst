.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço fora da comunidade atendida pela JCAFB

============================================================================================
A **Pessoa não cadastrada** reside em um **Endereço fora da comunidade** atendida pela JCAFB
============================================================================================

Cadastro Principal
------------------

    Nenhum registro será identificado.

Cadastro Auxiliar
-----------------

    O **Cadastro Auxiliar** criado conterá os seguintes registros:

        * :bi:`Person (Aux)`: relativo à Pessoa

Relacionamento entre os registros dos Cadastros
-----------------------------------------------

    * :bi:`Person (Aux)`:

        * *Address* » **vazio**
        * *Address (Aux)* » **vazio**
        * *Family* » **vazio**
        * *Related Person* » **vazio**
        * *Contact Information* = Dados com informações que indiquem o novo Endereço da Pessoa fora da comunidade.
        * Outros Dados = Outros Dados informados para a Pessoa

Fluxo de Trabalho (*Workflow*)
------------------------------

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_020_020_030`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
