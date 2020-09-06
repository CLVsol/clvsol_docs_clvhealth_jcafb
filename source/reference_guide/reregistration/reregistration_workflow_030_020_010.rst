.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Person (Aux) - (L0)

=========================================
Consolidação de :bi:`Person (Aux)` - (L0)
=========================================

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

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Person (Aux)*, uma vez que o *Person Code* será automaticamente criado por ocasião da criação do registro *Person* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Person. [_person_aux_verification_related_person]`).

    De qualquer forma é possível gerar um *Person Code* utilizando o procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_020_010`.

.. index:: Missing Address. [_person_aux_verification_ref_address]

**"Missing "Address".** [_person_aux_verification_ref_address]
--------------------------------------------------------------

    O registro *Person (Aux)* não está associado a um *Address*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_ref_address**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Address".**'

    Se, por algum motivo especial não for necessário ou conveniente associar o registro *Person (Aux)* a um registro *Address* do Cadastro Principal, indicar o campo "*Address is unavailable*"" do registro *Person (Aux)* como **marcado** e executar a Ação "*Person (Aux) Verification Execute*".

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Person (Aux)*, uma vez que o o registro *Person (Aux)* será automaticamente associado a um registro *Address* do Cadastro Principal por ocasião da criação do registro *Person* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Person. [_person_aux_verification_related_person]`).

    De qualquer forma se o registro *Person (Aux)* já possuir um registro *Person* relacionado no Cadastro Principal, é possível associar o registro *Person (Aux)* a um registro *Address* do Cadastro Principal utilizando o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_020`.

.. index:: Missing Related Person. [_person_aux_verification_related_person]

.. _Missing Related Person. [_person_aux_verification_related_person]:

**Missing "Related Person".** [_person_aux_verification_related_person]
-----------------------------------------------------------------------

    O registro *Person (Aux)* não possui um registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Related Person".**'

    Se, por algum motivo especial não for necessário ou conveniente criar um registro *Person* relacionado no Cadastro Principal, indicar o campo "*Related Person is unavailable*"" do registro *Person (Aux)* como **marcado** e executar a Ação "*Person (Aux) Verification Execute*".

    Para criar um registro *Person* relacionado no Cadastro Principal utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_030`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
