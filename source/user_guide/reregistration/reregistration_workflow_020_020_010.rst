.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço na Comunidade

=====================================================================
O **Paciente não cadastrado** reside em um **Endereço na Comunidade**
=====================================================================

    **Cadastros**:

        * **Cadastro Principal**:

            Nenhum registro será identificado.

        **Cadastro Auxiliar**:

            * registro :bi:`Patient (Aux)`

        * **Relacionamento entre os registros dos Cadastros**:

            * :bi:`Patient (Aux)`:

                * *Related Patient* » **vazio**
                * *Contact Information* = Dados de Endereço do Paciente
                * Outros Dados = Outros Dados informados para a Paciente

    **Fluxo de Trabalho** (:bi:`Workflow`):

        O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`reregistration_procedure_020_020_010`".

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
