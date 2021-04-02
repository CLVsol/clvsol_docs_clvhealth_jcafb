.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado Faleceu

====================================
O **Paciente já cadastrado** Faleceu
====================================

    **Cadastros**:

        * **Cadastro Principal**:

            * registro :bi:`Patient`

        * **Cadastro Auxiliar**:

            * registro :bi:`Patient (Aux)`

        * **Relacionamento entre os registros dos Cadastros**:

            * :bi:`Patient`:

                * *Contact Information* = Dados de Endereço do Paciente :red:`(antigo)`
                * Outros Dados = Outros Dados do Paciente

            * :bi:`Patient (Aux)`:

                * *Related Patient* » :bi:`Patient`
                * *Contact Information* = **vazio**.
                * Outros Dados = Outros Dados de :bi:`Patient`

    **Fluxo de Trabalho** (:bi:`Workflow`):

        O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`reregistration_procedure_020_010_080`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
