.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Remover a Fase de todos os Pacientes (Aux) (Procedimento)

=========================================================
Remover a Fase de todos os Pacientes (Aux) (Procedimento)
=========================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration_patient/reregistration_patient_cadastro_aux_setup`".

    #. Executar a Ação :bi:`Patient (Aux) Mass Edit` para todos os Pacientes (Aux):

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Selecionar todos os Pacientes (Aux)

        #. Executar a Ação :bi:`Patient (Aux) Mass Edit`:

            * Parâmetros utilizados:

                * *Register State*: :bi:`Set` » :bi:`Verified`
                * *State*: **nenhuma ação**
                * *Patient (Aux) Verification Execute*: **desmarcado**
                * *Phase*: :bi:`Remove`

            #. Utilize o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
