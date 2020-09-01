.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Address (Aux)

===================================
Consolidação de :bi:`Address (Aux)`
===================================

.. index:: Address Code is missing. [_address_aux_verification]

**"Address Code" is missing.** [_address_aux_verification]
----------------------------------------------------------

    O registro *Address (Aux)* não possui um *Address Code*.

    Essa situação ocorre para um registro *Address (Aux)* criado recentemente e que não tenha ainda um registro *Address* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Address Code" is missing.**'

    Procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_010_010`.

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_010_020`.

.. index:: Missing Related Address. [_address_aux_verification_related_address]

**Missing "Related Address".** [_address_aux_verification_related_address]
--------------------------------------------------------------------------

    O registro *Address (Aux)* não possui um registro *Address* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Related Address".**'

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_010_020`.

.. index:: Phase has changed. [_address_aux_verification_related_address]

**"Phase" has changed.** [_address_aux_verification_related_address]
--------------------------------------------------------------------

    O parâmetro *Phase* do registro *Address (Aux)* foi alterado em comparação com o parâmetro *Phase* do  registro *Address* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Phase" has changed.**'

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_010_030`.

.. index:: State has changed. [_address_aux_verification_related_address]

**"State" has changed.** [_address_aux_verification_related_address]
--------------------------------------------------------------------

    O parâmetro *State* (*Address State*) do registro *Address (Aux)* foi alterado em comparação com o parâmetro *State* do  registro *Address* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"State" has changed.**'

    Procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_010_030`.

.. index:: Related Address Verification State is Warning (L0). [_address_aux_verification_related_address]

**Related Address "Verification State" is "Warning (L0)".** [_address_aux_verification_related_address]
-------------------------------------------------------------------------------------------------------

    O *Verification State* do registro registro *Address* relacionado no Cadastro Principal é "Warning (L0)".

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Related Address "Verification State" is "Warning (L0)".**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Address (Aux)*.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
