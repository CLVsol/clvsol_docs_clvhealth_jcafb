.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Associated Person (Aux) Phase mismatch. [_address_aux_verification_associated_persons_aux]

================================================================================================
**Associated Person (Aux) "Phase" mismatch.** [_address_aux_verification_associated_persons_aux]
================================================================================================

    A Fase da Pessoa (Aux) indicada no *Outcome Information* "**Associated Person (Aux) "Phase" mismatch. (<nome da pessoa> [<código da pessoa>])**" não é a mesma Fase do Endereço (Aux).

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_associated_persons_aux**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Associated Person (Aux) "Phase" mismatch.**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Address (Aux)*.

    Esta situação ocorre quando a Fase do Endereço (Aux) foi alterada mas o Fase de pelo menos uma Pessoa (Aux) associada a esse Endereço (Aux) não foi ainda alterada. Quando todos os registros pertinentes às Pessoas (Aux) associadas ao Endereço (Aux) forem consolidados, essa situação deixará de existir. 

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
