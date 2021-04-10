.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Cadastramento/Recadastramento de Pacientes

==========================================
Cadastramento/Recadastramento de Pacientes
==========================================

    A execuçao do processo de **Cadastramento/Recadastramento** de um Paciente inicia-se pela procura por um registro associado a ele em ":bi:`Patients (Aux)`", utilizando o procedimento ":doc:`reregistration_workflow_010_030`"

    Se, após essa pesquisa, for identificado um registro associado ao Paciente em ":bi:`Patients (Aux)`", o **Recadastramento** desse **Paciente já cadastrado** será executado a partir dos dados apresentados no registro encontrado e das novas informações apresentadas para a Paciente. O processo de Recadastramento do Paciente deve seguir o fluxo apresentado em ":doc:`reregistration_workflow_020_010`".

    Se, após a pesquisa **não for identificado** um registro associado ao Paciente em ":bi:`Patients (Aux)`", o **Cadastramento** desse **novo Paciente** será executado a partir da criação de um novo registro em :bi:`Patients (Aux)` com as informações apresentadas para a Paciente. O processo de Cadastramento do Paciente deve seguir o fluxo apresentado em ":doc:`reregistration_workflow_020_020`".

.. toctree::
   :maxdepth: 2
   :caption: Conteúdo:

   reregistration_workflow_020_010
   reregistration_workflow_020_020
