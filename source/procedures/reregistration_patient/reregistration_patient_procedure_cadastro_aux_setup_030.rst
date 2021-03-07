.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Associar todos os Pacientes a um Paciente (Aux) (Procedimento)

==============================================================
Associar todos os Pacientes a um Paciente (Aux) (Procedimento)
==============================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration_patient/reregistration_patient_cadastro_aux_setup`".

    #. Executar a Ação :bi:`Patient Associate to Patient (Aux)` para todos os Pacientes:

        #. Acessar a *view* :bi:`Patients`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health`» :bi:`Patient` » :bi:`Patients`

        #. Ativar o filtro **Agrupar por** » :bi:`Register State`

        #. Selecionar todos as Pessoas com :bi:`Register State` != ":bi:`Canceled`"

        #. Exercutar a Ação :bi:`Patient Associate to Patient (Aux)`:

            * Parâmetros utilizados:

                * *Create new Patient (Aux)*: **marcado**

            #. Utilize o botão :bi:`Associate to Patient (Aux)` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
