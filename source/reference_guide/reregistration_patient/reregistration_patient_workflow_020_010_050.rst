.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um outro Endereço

================================================================
O **Paciente já cadastrado** mudou-se para um outro **Endereço**
================================================================

**Cadastro Principal**:

    O **Cadastro** identificado deverá conter o seguinte registro:

        * :bi:`Patient`: relativo à Paciente

**Cadastro Auxiliar**:

    O **Cadastro Auxiliar** criado deverá conter o seguinte registro:

        * :bi:`Patient (Aux)`: relativo à Paciente

**Relacionamento entre os registros dos Cadastros**:

    * :bi:`Patient`:

        * *Contact Information* = Dados de Endereço do Paciente :green:`(antigo)`
        * Outros Dados = Outros Dados do Paciente

    * :bi:`Patient (Aux)`:

        * *Related Patient* » :bi:`Patient`
        * *Contact Information* = Dados de Endereço do Paciente :green:`(novo)`
        * Outros Dados = Outros Dados de :bi:`Patient`

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_020_010_050`".

    Alternativamente, considerando a :doc:`/reference_guide/reregistration_patient/reregistration_patient_cadastro_aux_setup`, o processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_020_010_050_alt`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
