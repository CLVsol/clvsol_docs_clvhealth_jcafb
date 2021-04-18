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

.. index:: Contact Information should not be set. [_patient_verification]

====================================================================
**"Contact Information" should not be set.** [_patient_verification]
====================================================================

    Essa situação ocorre quando as Informações de Contato do Paciente estão disponíveis e o campo :bi:`Contact Information is unavailable` foi erroneamente marcado.

    :bi:`Verification Outcome`:

        * *Model Name*: **clv.patient**
        * *Action*: **_patient_verification**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**"Contact Information" should not be set.**'

    Essa situação é corrigida, indicando o campo :bi:`Contact Information is unavailable` como **desmarcado**.

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
