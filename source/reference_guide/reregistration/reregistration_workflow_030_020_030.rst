.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Person (Aux) - (L2)

=========================================
Consolidação de :bi:`Person (Aux)` - (L2)
=========================================

.. index:: Family Contact Information (Address) mismatch. [_person_aux_verification_related_person]

**Family "Contact Information (Address)" mismatch.** [_person_aux_verification_related_person]
----------------------------------------------------------------------------------------------

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L2)**
        * *Outcome Information*: '**Family "Contact Information (Address)" mismatch.**'

    Para alterar o *Contact Information* do  registro *Family* associado ao registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_090`.

    Alternativamente, para alterar o *Contact Information* do  registro *Family* associado ao registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_095`.

.. index:: Missing Family. [_person_aux_verification_family]

**Missing "Family".** [_person_aux_verification_family]
-------------------------------------------------------

    O registro *Person (Aux)* não está associado a um registro *Family* no Cadastro Principal..

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L2)**
        * *Outcome Information*: '**Missing "Family".**'

    Para associar o registro *Person (Aux)* a um registro *Family* relacionado no Cadastro Principal utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_100`.

.. index:: Family Verification State is Warning (L0). [_person_aux_verification_family]

**Family "Verification State" is "Warning (L0)".** [_person_aux_verification_family]
------------------------------------------------------------------------------------

    O *Verification State* do registro registro *Family* relacionado no Cadastro Principal é "Warning (L0)".

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L2)**
        * *Outcome Information*: '**"Family "Verification State" is "Warning (L0)".**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Person (Aux)*.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
