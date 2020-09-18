.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing related Address (Aux) register. [_address_verification_address_aux]

=================================================================================
**Missing related "Address (Aux)" register.** [_address_verification_address_aux]
=================================================================================

    O registro *Address* não está associado a um registro *Address (Aux)*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.address**
        * *Action*: **_address_verification_address_aux**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing related "Address (Aux)" register.**'

    Esta situação é a desejada quando o registro *Address* tiver "Cancelado" (*Register State* = "*Canceled*"). Neste caso, não é necessária a execução de qualquer procedimento de correção no registro *Address*.

    Para situações em que o registro *Address* não tiver sido "Cancelado" (*Register State* != "*Canceled*") e houver a possibilidade do Endereço referenciado pelo registro vir a ser recadastrado, é conveniente a criação de um registro *Address (Aux)*, utilizando o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_040_010_010`.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
