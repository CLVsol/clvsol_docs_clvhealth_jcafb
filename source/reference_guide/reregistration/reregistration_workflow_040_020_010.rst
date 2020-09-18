.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Associated Person Address mismatch. [_family_verification_associated_persons]

===================================================================================
**Associated Person "Address" mismatch.** [_family_verification_associated_persons]
===================================================================================

    O Endereço da Pessoa indicada no *Outcome Information* "**Associated Person "Address" mismatch. (<nome da pessoa> [<código da pessoa>])**" não é o mesmo Endereço da Família.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.family**
        * *Action*: **_family_verification_associated_persons**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Associated Person "Address" mismatch.**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Family*.

    Esta situação ocorre quando o Endereço da Família foi alterado mas o Endereço de pelo menos uma Pessoa que compõem essa Família não foi ainda alterado. Quando todos os registros pertinentes às Pessoas que compõem a Família forem consolidados, essa situação deixará de existir. 

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
