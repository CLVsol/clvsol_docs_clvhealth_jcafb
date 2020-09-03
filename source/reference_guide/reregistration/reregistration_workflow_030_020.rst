.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Person (Aux)

==================================
Consolidação de :bi:`Person (Aux)`
==================================

.. index:: Person Code is missing. [_person_aux_verification]

**"Person Code" is missing.** [_person_aux_verification]
----------------------------------------------------------

    O registro *Person (Aux)* não possui um *Person Code*.

    Essa situação ocorre para um registro *Person (Aux)* criado recentemente e que não tenha ainda um registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Person Code" is missing.**'

    Procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_020_010`.

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_030`.

_person_aux_verification_family
-------------------------------

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_090`".

_person_aux_verification_ref_address
------------------------------------

.. index:: Missing Address. [_person_aux_verification_ref_address]

**"Missing "Address".** [_person_aux_verification_ref_address]
--------------------------------------------------------------

    O registro *Person (Aux)* não está associado a um *Address*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_ref_address**
        * *State*: **Error (L1)**
        * *Outcome Information*: '**Missing "Address".**'

    Procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_020_020`.

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_030`.

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_100`".

_person_aux_verification_ref_address_aux
----------------------------------------

_person_aux_verification_related_person
---------------------------------------

.. index:: Missing Related Person. [_person_aux_verification_related_person]

**Missing "Related Person".** [_person_aux_verification_related_person]
-----------------------------------------------------------------------

    O registro *Person (Aux)* não possui um registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Error (L1)**
        * *Outcome Information*: '**Missing "Related Person".**'

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_030`.

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_040`".

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_050`".

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_060`".

    * :doc:`/procedures/reregistration/reregistration_procedure_030_020_070`".

    * :blue:`(Nenhuma ação)` :doc:`/procedures/reregistration/reregistration_procedure_030_020_080`".

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
