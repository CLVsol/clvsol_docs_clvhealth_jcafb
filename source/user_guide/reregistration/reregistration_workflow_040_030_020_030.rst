.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Residence Contact Information mismatch. [_patient_verification_residence]

===============================================================================
**Residence "Contact Information" mismatch.** [_patient_verification_residence]
===============================================================================

    O Contact Information do registro *Patient* foi alterado em comparação com o Contact Information do registro Residence relacionado no Cadastro Principal. Essa situaçao, em geral, ocorre quando o Paciente mudou para uma outra Residẽncia.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient**
        * *Action*: **_patient_verification_residence**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Residence "Contact Information" mismatch.**'

    Se, por algum motivo especial não for necessário ou conveniente associar o registro *Patient* a um registro *Residence* do Cadastro Principal, apagar a associação do registro *Patient* a um registro *Residence*, e indicar o campo "*Residence is unavailable*"" do registro *Patient* como **marcado** e executar a Ação "*Patient Verification Execute*".

    Para associar o registro *Patient* a um outro registro *Residence* do Cadastro Principal utilizando o procedimento de correção: :doc:`reregistration_procedure_040_030_020`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
