.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado continua a residir no mesmo Endereço

=====================================================================
O **Paciente já cadastrado** continua a residir no mesmo **Endereço**
=====================================================================

**Cadastro Principal**:

    O **Cadastro Principal** identificado conterá os seguintes registros:

        * :bi:`Patient`: relativo à Paciente

**Cadastro Auxiliar:**

    O **Cadastro Auxiliar** criado conterá os seguintes registros:

        * :bi:`Patient (Aux)`: relativo à Paciente

**Relacionamento entre os registros dos Cadastros**:

    * :bi:`Patient`:

        * *Contact Information* = Dados de Endereço do Paciente
        * Outros Dados = Outros Dados do Paciente

    * :bi:`Patient (Aux)`:

        * *Related Patient* » :bi:`Patient`
        * *Contact Information* = Dados de :bi:`Patient`
        * Outros Dados = Outros Dados de :bi:`Patient`

**Fluxo de Trabalho** (:bi:`Workflow`):

    O processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_020_010_010`".

    Alternativamente, considerando a :doc:`/reference_guide/reregistration_patient/reregistration_patient_cadastro_aux_setup`, o processamento deste *Workflow* é executado utilizando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_020_010_010_alt`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
