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

.. index:: Contact Information Pattern was not recognised. [_patient_aux_verification]

=================================================================================
**"Contact Information Pattern" was not recognised.** [_patient_aux_verification]
=================================================================================

    :bmaroon:`Nota de advertência`: Observar se o :bi:`Outcome Information` ":doc:`reregistration_workflow_030_020_010_005`" também tenha sido reportado para o :bi:`Patient (Aux)`. Caso positivo, executar primeiro tratamento do mesmo. 

    Essa situação ocorre quando o *Contact Information Pattern* indicado no *Outcome Information* “:bi:`"Contact Information Pattern" was not recognised.` :bi:`(<contact information pattern>)`” não foi ainda incluído na Tabela ":doc:`reregistration_cadastro_100_020`".

    :bred:`Importante`: Antes de prosseguir **certifique-se** de que:

        #. As Informações de Contato inseridas/atualizadas nos campos "*Street Name*", "Casa", "Porta" e "*District*" no registro *Patient (Aux)* estejam corretas.

        #. O Endereço em questão pertença à Comunidade atendida pelo Projeto.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient_aux**
        * *Action*: **_patient_aux_verification**
        * *State*: **Warning (L0)**
        * *Outcome Information*: '**"Contact Information Pattern" was not recognised.**'

    Essa situação é corrigida, utilizando o procedimento de correção : :doc:`reregistration_procedure_030_020_006`.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
