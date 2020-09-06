.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Person (Aux) - (L1)

=========================================
Consolidação de :bi:`Person (Aux)` - (L1)
=========================================

.. index:: Phase has changed. [_person_aux_verification_related_person]

**"Phase" has changed.** [_person_aux_verification_related_person]
------------------------------------------------------------------

    O parâmetro *Phase* do registro *Person (Aux)* foi alterado em comparação com o parâmetro *Phase* do  registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Phase" has changed.**'

    Para alterar o parâmetro *Phase* do  registro *Person*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_040`.

    Para reverter o parâmetro *Phase* do  registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_110`.

.. index:: State has changed. [_person_aux_verification_related_person]

**"State" has changed.** [_person_aux_verification_related_person]
------------------------------------------------------------------

    O parâmetro *State* do registro *Person (Aux)* foi alterado em comparação com o parâmetro *State* do  registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"State" has changed.**'

    Para alterar o parâmetro *State* do  registro *Person*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_040`.

    Para reverter o parâmetro *State* do  registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_110`.

.. index:: Contact Information (Address) has changed. [_person_aux_verification_related_person]

**"Contact Information (Address)" has changed.** [_person_aux_verification_related_person]
------------------------------------------------------------------------------------------

    O *Contact Information* do registro *Person (Aux)* foi alterado em comparação com o *Contact Information* do  registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *Contact Information*: **Warning (L1)**
        * *Outcome Information*: '**"Contact Information (Address)" has changed.**'

    Para alterar o *Contact Information* do  registro *Person*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_040`.

    Para reverter o *Contact Information* do  registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_110`.

.. index:: Address has changed. [_person_aux_verification_related_person]

**"Address" has changed.** [_person_aux_verification_related_person]
--------------------------------------------------------------------

    O *Address* do registro *Person (Aux)* foi alterado em comparação com o *Address* do  registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *Address*: **Warning (L1)**
        * *Outcome Information*: '**"Address" has changed.**'

    Para alterar o *Address* do  registro *Person*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_070`.

    Para reverter o *Address* do  registro *Person (Aux)*, utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_110`.

.. index:: Family Contact Information (Address) mismatch. [_person_aux_verification_related_person]

**Family "Contact Information (Address)" mismatch.** [_person_aux_verification_related_person]
----------------------------------------------------------------------------------------------

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L1)**
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
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Missing "Family".**'

    Para associar o registro *Person (Aux)* a um registro *Family* relacionado no Cadastro Principal utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_100`.

.. index:: Related Person Verification State is Warning (L0). [_person_aux_verification_related_person]

**Related Person "Verification State" is "Warning (L0)".** [_person_aux_verification_related_person]
----------------------------------------------------------------------------------------------------

    O *Verification State* do registro registro *Address* relacionado no Cadastro Principal é "Warning (L0)".

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Related Person "Verification State" is "Warning (L0)".**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Person (Aux)*.

.. index:: Family Verification State is Warning (L0). [_person_aux_verification_family]

**Family "Verification State" is "Warning (L0)".** [_person_aux_verification_family]
------------------------------------------------------------------------------------

    O *Verification State* do registro registro *Family* relacionado no Cadastro Principal é "Warning (L0)".

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Family "Verification State" is "Warning (L0)".**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Person (Aux)*.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
