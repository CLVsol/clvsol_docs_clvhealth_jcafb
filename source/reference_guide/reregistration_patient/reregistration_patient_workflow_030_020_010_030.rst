.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing Related Patient. [_patient_aux_verification_related_patient]

.. _Missing Related Patient. [_patient_aux_verification_related_patient]:

==========================================================================
**Missing "Related Patient".** [_patient_aux_verification_related_patient]
==========================================================================

    O registro *Patient (Aux)* não possui um registro *Patient* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient_aux**
        * *Action*: **_patient_aux_verification_related_patient**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Related Patient".**'

    Se, por algum motivo especial não for necessário ou conveniente criar um registro *Patient* relacionado no Cadastro Principal, indicar o campo "*Related Patient is unavailable*"" do registro *Patient (Aux)* como **marcado** e executar a Ação "*Patient (Aux) Verification Execute*".

    Para criar um registro *Patient* relacionado no Cadastro Principal utilizar o procedimento de correção: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_030_020_030`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
