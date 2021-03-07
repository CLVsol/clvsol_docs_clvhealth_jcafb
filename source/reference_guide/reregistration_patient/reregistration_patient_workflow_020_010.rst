.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Cadastro Auxiliar (Paciente já cadastrado)

=============================================================
Criação do **Cadastro Auxiliar** (**Paciente já cadastrado**)
=============================================================

O processo de criação do **Cadastro Auxiliar** associado a um Paciente **já cadastrado** é utilizado quando não for identificado um registro associado a ela em ":bi:`Patients (Aux)`".

Portanto, quando não existir ainda um **Cadastro Auxiliar** associado ao Paciente, o mesmo deverá ser criado como uma cópia do **Cadastro Principal** existente, associado ao Paciente.

Se porventura já existir um **Cadastro Auxiliar** associado ao Paciente, o mesmo será selecionado.

O **Cadastro Auxiliar** criado poderá ser composto pelas seguintes **Entidades (Aux)**:

    * :bi:`Patient (Aux)`:

        * O registro será preenchido com as informações já cadastrados para a Paciente e atualizado com as informações coletadas para a Paciente.

.. toctree::
   :maxdepth: 1
   :caption: Tópicos Relacionados:

   reregistration_patient_workflow_020_010_010
   reregistration_patient_workflow_020_010_050
   reregistration_patient_workflow_020_010_070
