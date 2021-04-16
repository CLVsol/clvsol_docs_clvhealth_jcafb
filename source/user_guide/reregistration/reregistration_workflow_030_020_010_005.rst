.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: blue
.. role:: bmaroon
.. role:: borange
.. role:: bi

.. index:: Street Pattern was not recognised. [_patient_aux_verification]

====================================================================
**"Street Pattern" was not recognised.** [_patient_aux_verification]
====================================================================

    Essa situação ocorre quando o *Street Pattern* indicado no *Outcome Information* “:bi:`"Street Pattern" was not recognised.` :bi:`(<street pattern>)`” não foi ainda incluído  na Tabela ":doc:`reregistration_cadastro_100_010`".

    :bred:`Importante`: Antes de prosseguir **certifique-se** de que:

        #. As Informações de Contato inseridas/atualizadas nos campos "*Street Name*", e "*District*" no registro *Patient (Aux)* estejam corretas.

        #. O Endereço em questão pertença à Comunidade atendida pelo Projeto.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient_aux**
        * *Action*: **_patient_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Street Pattern" was not recognised.**'

    Essa situação é corrigida, utilizando o procedimento de correção : :doc:`reregistration_procedure_030_020_005`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
