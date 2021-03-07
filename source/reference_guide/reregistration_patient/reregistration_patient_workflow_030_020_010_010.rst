.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Patient Code is missing. [_patient_aux_verification]

==========================================================
**"Patient Code" is missing.** [_patient_aux_verification]
==========================================================

    O registro *Patient (Aux)* não possui um *Patient Code*.

    Essa situação ocorre para um registro *Patient (Aux)* criado recentemente e que não tenha ainda um registro *Patient* relacionado no Cadastro Principal.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient_aux**
        * *Action*: **_patient_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Patient Code" is missing.**'

    De maneira geral não é necessária a execução de qualquer procedimento de correção para o registro *Patient (Aux)*, uma vez que o *Patient Code* será automaticamente criado por ocasião da criação do registro *Patient* relacionado no Cadastro Principal (verificar o item :ref:`Missing Related Patient. [_patient_aux_verification_related_patient]`).

    De qualquer forma é possível gerar um *Patient Code* utilizando o procedimento de correção :green:`(Opcional)`: :doc:`/procedures/reregistration_patient/reregistration_patient_procedure_030_020_010`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
