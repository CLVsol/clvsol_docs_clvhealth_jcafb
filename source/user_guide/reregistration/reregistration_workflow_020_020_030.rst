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

Cadastro
--------

    Nenhum registro será identificado no **Cadastro**.

Cadastro Auxiliar
-----------------

    O **Cadastro Auxiliar** criado conterá os seguintes registros:

        * :bi:`Person (Aux)`

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

    #. **Cadastro**:

        #. Procurar pelo(s) registro(s) :bi:`Person` e/ou :bi:`Person (Aux)` associado(s) à Pessoa utilizando o método:

            * :doc:`reregistration_workflow_010_010`

        **Observação 1**: Nenhum registro :bi:`Person` deverá ser encontrado.

        **Observação 2**: Nenhum registro :bi:`Person (Aux)` deverá ser encontrado, a menos que a nova Pessoa já esteja em processo de recadastramento.

    #. *View* :bi:`Person (Aux)`:

        #. Criar manualmente um novo registro :bi:`Person (Aux)`, preenchido com as informações apresentadas para a Pessoa, exceto as informaçôes do Endereço.

    #. Registro :bi:`Person (Aux)`:

        #. Preencher os campos de *Contact Information* com informações que indiquem o novo Endereço da Pessoa fora da comunidade.

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedure/reregistration/reregistration_procedure_020_020_030`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
