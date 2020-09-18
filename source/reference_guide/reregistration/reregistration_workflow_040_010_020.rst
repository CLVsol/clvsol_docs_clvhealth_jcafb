.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Please, verify Address State. [_address_verification_associated_persons]

==============================================================================
**Please, verify "Address State".** [_address_verification_associated_persons]
==============================================================================

    O *Address State* do registro *Address* é incompatível com o *Person State* da(s) Pessoa(s) residente(s) no Endereço relacionado ao registro *Address*.

    Um caso especial desse alerta ocorre quando o *Address State* do Endereço é marcado como :bi:`Available` mas não existe ainda nenhuma Pessoa declarada como residente nesse Endereço.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address**
        * *Action*: **_address_verification_associated_persons**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**Please, verify "Address State".**'

    Não é necessária a execução de qualquer procedimento de correção no registro *Address*.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
