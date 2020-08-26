.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Address (Aux)

====================================================
:red:`(Revisar)` Consolidação de :bi:`Address (Aux)`
====================================================

:red:`(Opcional)` *Outcome Information*: '**"Address Code" is missing.**'
-------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.address_aux**
		* *Action*: **_address_aux_verification**
		* *State*: **Warning (L0)**
		* *Outcome Information*: '**"Address Code" is missing.**'

    #. Exercutar a Ação ":bi:`Address (Aux) Set Code`":

        #. Parâmetros apresentados:

            * *Address (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Set Code` para executar a Ação.

*Outcome Information*: '**Missing "Related Address".**'
-------------------------------------------------------

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

*Outcome Information*: '**"Phase" has changed.**'
-------------------------------------------------

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.address_aux**
		* *Action*: **_address_aux_verification_related_address**
		* *State*: **Warning (L0)**
		* *Outcome Information*: '**"Phase" has changed.**'

    #. Exercutar a Ação ":bi:`Address (Aux) Related Address Update`":

        #. Parâmetros apresentados:

            * *Related Address Verification Execute*: **marcado**
            * *Address (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Address Update` para executar a Ação.

*Outcome Information*: '**"State" has changed.**'
-------------------------------------------------

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.address_aux**
		* *Action*: **_address_aux_verification_related_address**
		* *State*: **Warning (L0)**
		* *Outcome Information*: '**"State" has changed.**'

    #. Exercutar a Ação ":bi:`Address (Aux) Related Address Update`":

        #. Parâmetros apresentados:

            * *Related Address Verification Execute*: **marcado**
            * *Address (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Address Update` para executar a Ação.

:blue:`(Nenhuma ação)` *Outcome Information*: '**Related Address "Verification State" is "Warning (L0)".**'
-----------------------------------------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Addresses (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Addresses (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.address_aux**
		* *Action*: **_address_aux_verification_related_address**
		* *State*: **Warning (L1)**
		* *Outcome Information*: '**"Related Address "Verification State" is "Warning (L0)".**'

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
