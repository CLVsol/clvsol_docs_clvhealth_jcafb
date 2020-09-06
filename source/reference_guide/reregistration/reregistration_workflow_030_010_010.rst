.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Address (Aux) - (L0)

==========================================
Consolidação de :bi:`Address (Aux)` - (L0)
==========================================

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

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Address (Aux)*, uma vez que o *Address Code* será automaticamente criado por ocasião da criação do registro *Address* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Address. [_address_aux_verification_related_address]`).

    De qualquer forma é possível gerar um *Address Code* utilizando o procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_010_010`.

.. index:: Missing Related Address. [_address_aux_verification_related_address]

.. _Missing Related Address. [_address_aux_verification_related_address]:

**Missing "Related Address".** [_address_aux_verification_related_address]
--------------------------------------------------------------------------

    O registro *Address (Aux)* não possui um registro *Address* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Related Address".**'

    Se, por algum motivo especial não for necessário ou conveniente criar um registro *Address* relacionado no Cadastro Principal, indicar o campo "*Related Address is unavailable*"" do registro *Address (Aux)* como **marcado** e executar a Ação "*Address (Aux) Verification Execute*".

    Para criar um um registro *Address* relacionado no Cadastro Principal utilizar o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_030_010_020`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
