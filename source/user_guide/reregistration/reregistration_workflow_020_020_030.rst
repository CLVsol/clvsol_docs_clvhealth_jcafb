.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço fora da comunidade atendida pela JCAFB

==============================================================================================
O **Paciente não cadastrado** reside em um **Endereço fora da comunidade** atendida pela JCAFB
==============================================================================================

    **Cadastros**:

        * **Cadastro Principal**:

            Nenhum registro será identificado.

        * **Cadastro Auxiliar**:

             * :bi:`Patient (Aux)`: relativo à Paciente

        * **Relacionamento entre os registros dos Cadastros**:

            * :bi:`Patient (Aux)`:

                * *Related Patient* » **vazio**
                * *Contact Information* = Dados com informações que indiquem o novo Endereço da Paciente fora da comunidade.
                * Outros Dados = Outros Dados informados para a Paciente

    **Fluxo de Trabalho** (:bi:`Workflow`):

        O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`reregistration_procedure_020_020_030`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
