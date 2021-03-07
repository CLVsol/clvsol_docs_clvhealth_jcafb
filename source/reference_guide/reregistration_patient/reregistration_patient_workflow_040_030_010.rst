.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing related Patient (Aux) register. [_patient_verification_patient_aux]

=================================================================================
**Missing related "Patient (Aux)" register.** [_patient_verification_patient_aux]
=================================================================================

    O registro *Patient* não está associado a um registro *Patient (Aux)*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient**
        * *Action*: **_patient_verification_patient_aux**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing related "Patient (Aux)" register.**'

    Esta situação é a desejada quando o registro *Patient* tiver sido "Cancelado" (*Register State* = "*Canceled*"). Neste caso, não é necessária a execução de qualquer procedimento de correção no registro *Patient*.

    Para situações em que o registro *Patient* não tiver sido "Cancelado" (*Register State* != "*Canceled*") e houver a possibilidade da Pessoa referenciado pelo registro vir a ser recadastrada, é conveniente a criação de um registro *Patient (Aux)*, utilizando o procedimento de correção: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_040_030_010`.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
