.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Outcome Information: '"State" has changed.' (Procedimento)

================================================================
*Outcome Information*: '**"State" has changed.**' (Procedimento)
================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_030_020`".

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"State" has changed.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Related Person Update`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: **desmarcado**
            * *Update Address Data*: **desmarcado**
            * *Update Family Datae*: **desmarcado**
            * *Related Person Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Person Update` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
