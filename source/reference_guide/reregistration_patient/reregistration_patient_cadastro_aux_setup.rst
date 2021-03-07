.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Preparação do Cadastro Auxiliar [Pacientes]

===============================================
Preparação do **Cadastro Auxiliar** [Pacientes]
===============================================

De forma a agilizar o Processo de  **Cadastramento/Recadastramento** de todos os Pacientes é conveniente que o **Cadastro Auxiliar** seja preparado previamente.

Essa preparação se constitui basicamente em copiar todos os registros do Cadastro Principal (registros :bi:`Patient`) para o Cadastro Auxiliar (respectivamente, registros :bi:`Patient (Aux)`).

Essa preparação é, da forma descrita a seguir, realizada somente uma vez, no início de cada umna das Fases de um ciclo da JCAFB.

A Preparação do Cadastro Auxiliar é implementada através das seguintes ações:

    #. Excluir todos os registros de Pacientes do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_cadastro_aux_setup_010`".

    #. Associar todos os Pacientes a um Paciente (Aux) executando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_cadastro_aux_setup_030`".

    #. Remover a Fase de todos os Pacientes (Aux) executando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_cadastro_aux_setup_050`".

    #. :red:`(Não Executado])` Excluir todos os registros de Pacientes falecidas do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration_patient/reregistration_patient_procedure_cadastro_aux_setup_070`".
    
    #. :red:`(Não Executado])` Executar o Verification Batch “Default Batch” executando ":doc:`/procedures/verification/verification_procedure_010`".

    #. Executar o Verification Batch “Default Batch” executando ":doc:`/procedures/verification/verification_procedure_015`".

.. toctree::
   :maxdepth: 3
   :caption: Tópicos Relacionados:
