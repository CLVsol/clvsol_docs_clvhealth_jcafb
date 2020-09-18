.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing Related Person. [_person_aux_verification_related_person]

.. _Missing Related Person. [_person_aux_verification_related_person]:

=======================================================================
**Missing "Related Person".** [_person_aux_verification_related_person]
=======================================================================

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
