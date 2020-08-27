.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Outcome Information: 'Missing "Family".' (Procedimento)

=============================================================
*Outcome Information*: '**Missing "Family".**' (Procedimento)
=============================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_030_020`".

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Missing "Family".**'

    #. Exercutar a Ação ":bi:`Person (Aux) Associate to Family`":

        #. Parâmetros apresentados:

            * *Create new Family*: **marcado**
            * *Associate all Persons from Reference Address*: **desmarcado**
            * *Family Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Associate to Family` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
