.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Added Patient Category(ies). [_patient_aux_verification_related_patient]

==============================================================================
**Added "Patient Category(ies)".** [_patient_aux_verification_related_patient]
==============================================================================

    O parâmetro *Categories* do registro *Patient (Aux)* foi alterado (adicionado) em comparação com o parâmetro *Categories* do  registro *Patient* relacionado no Cadastro Principal.

    Isso pode ocorrer, em alguns casos, quando a Categoria do Paciente no Cadastro Principal tenha sido retirada após a última atualização do registro do Paciente no Cadastro Auxiliar. 

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient_aux**
        * *Action*: **_patient_aux_verification_related_patient**
        * *Contact Information*: **Warning (L1)**
        * *Outcome Information*: '**"Added "Patient Category(ies)".**'

    Para alterar o parâmetro *Categories* do  registro *Patient*, utilizar o procedimento de correção: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_030_020_040`.

    Para reverter o parâmetro *Categories* do  registro *Patient (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_030_020_110`.

    Para retirar o parâmetro *Categories* do  registro *Patient (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_030_020_080`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
