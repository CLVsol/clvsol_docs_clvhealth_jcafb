.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing Address. [_person_aux_verification_ref_address]

==============================================================
**"Missing "Address".** [_person_aux_verification_ref_address]
==============================================================

    O registro *Person (Aux)* não está associado a um *Address*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_ref_address**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Address".**'

    Se, por algum motivo especial não for necessário ou conveniente associar o registro *Person (Aux)* a um registro *Address* do Cadastro Principal, indicar o campo "*Address is unavailable*"" do registro *Person (Aux)* como **marcado** e executar a Ação "*Person (Aux) Verification Execute*".

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Person (Aux)*, uma vez que o o registro *Person (Aux)* será automaticamente associado a um registro *Address* do Cadastro Principal por ocasião da criação do registro *Person* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Person. [_person_aux_verification_related_person]`).

    De qualquer forma se o registro *Person (Aux)* já possuir um registro *Person* relacionado no Cadastro Principal, é possível associar o registro *Person (Aux)* a um registro *Address* do Cadastro Principal utilizando o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_020_020`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
