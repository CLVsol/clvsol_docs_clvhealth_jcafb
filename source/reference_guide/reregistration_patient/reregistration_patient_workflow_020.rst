.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Cadastro Auxiliar [Pacientes]

============================================
Criação do **Cadastro Auxiliar** [Pacientes]
============================================

    Se, após a pesquisa por um **Paciente** nos **Cadastros**, não for identificado um registro associado a ele em ":bi:`Patients (Aux)`", esse Paciente deve ser incluído no **Cadastro Auxiliar**.

    No caso de um Paciente "**já cadastrado**", os registro relativos a ele será automaticamente criado no **Cadastro Auxiliar** (:bi:`Patient (Aux)`) a partir das informações do registro equivalente presente no **Cadastro Principal** (:bi:`Patient`).

    No caso de um Paciente "**não cadastrado**", o registro no **Cadastro Auxiliar** relativo a ele (:bi:`Patient (Aux)`) será criado com as informações apresentadas para a Paciente.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:

   reregistration_patient_workflow_020_010
   reregistration_patient_workflow_020_020
