.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Person Code is missing. [_person_aux_verification]

========================================================
**"Person Code" is missing.** [_person_aux_verification]
========================================================

    O registro *Person (Aux)* não possui um *Person Code*.

    Essa situação ocorre para um registro *Person (Aux)* criado recentemente e que não tenha ainda um registro *Person* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Person Code" is missing.**'

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Person (Aux)*, uma vez que o *Person Code* será automaticamente criado por ocasião da criação do registro *Person* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Person. [_person_aux_verification_related_person]`).

    De qualquer forma é possível gerar um *Person Code* utilizando o procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration/reregistration_procedure_030_020_010`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
