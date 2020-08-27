.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Outcome Information: 'Missing "Related Address".' (Procedimento)

======================================================================
*Outcome Information*: '**Missing "Related Address".**' (Procedimento)
======================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_030_010`".

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.address_aux**
        * *Action*: **_address_aux_verification_related_address**
        * *State*: **Error (L0)**
        * *Outcome Information*: '**Missing "Related Address".**'

    #. Exercutar a Ação ":bi:`Address (Aux) Related Address Create`":

        #. Parâmetros apresentados:

            * *Address (Aux) Set Code*: **marcado**
            * *Related Address Verification Execute*: **marcado**
            * *Address (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Address Create` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
