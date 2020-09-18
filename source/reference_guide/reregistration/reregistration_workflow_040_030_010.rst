.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Missing related Person (Aux) register. [_person_verification_person_aux]

==============================================================================
**Missing related "Person (Aux)" register.** [_person_verification_person_aux]
==============================================================================

    O registro *Person* não está associado a um registro *Person (Aux)*.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person**
        * *Action*: **_person_verification_person_aux**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing related "Person (Aux)" register.**'

    Esta situação é a desejada quando o registro *Person* tiver sido "Cancelado" (*Register State* = "*Canceled*"). Neste caso, não é necessária a execução de qualquer procedimento de correção no registro *Person*.

    Para situações em que o registro *Person* não tiver sido "Cancelado" (*Register State* != "*Canceled*") e houver a possibilidade da Pessoa referenciado pelo registro vir a ser recadastrada, é conveniente a criação de um registro *Person (Aux)*, utilizando o procedimento de correção: :doc:`/procedures/reregistration/reregistration_procedure_040_030_010`.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
