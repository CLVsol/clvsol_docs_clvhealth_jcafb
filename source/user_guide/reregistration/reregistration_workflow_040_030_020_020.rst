.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing Residence. [_patient_verification_residence]

==========================================================
**Missing "Residence".** [_patient_verification_residence]
==========================================================

    O registro *Patient* não está associado a uma *Residence*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient**
        * *Action*: **_patient_verification_residence**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Missing "Residence".**'

    Se, por algum motivo especial não for necessário ou conveniente associar o registro *Patient* a um registro *Residence* do Cadastro Principal, indicar o campo "*Residence is unavailable*"" do registro *Patient* como **marcado** e executar a Ação "*Patient Verification Execute*".

    De qualquer forma, é possível associar o registro *Patient* a um registro *Residence* do Cadastro Principal utilizando o procedimento de correção: :doc:`reregistration_procedure_040_030_020`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
