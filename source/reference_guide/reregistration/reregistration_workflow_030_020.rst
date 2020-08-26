.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Person (Aux)

===================================================
:red:`(Revisar)` Consolidação de :bi:`Person (Aux)`
===================================================

:red:`(Opcional)` *Outcome Information*: '**"Person Code" is missing.**'
------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.person_aux**
		* *Action*: **_person_aux_verification**
		* *State*: **Warning (L0)**
		* *Outcome Information*: '**"Person Code" is missing.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Set Code`":

        #. Parâmetros apresentados:

            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Set Code` para executar a Ação.

*Outcome Information*: '**Missing "Address".**'
-----------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_ref_address**
        * *State*: **Error (L1)**
        * *Outcome Information*: '**Missing "Address".**'

    #. Exercutar a Ação ":bi:`Person (Aux) Associate to Address`":

        #. Parâmetros apresentados:

            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Associate to Address` para executar a Ação.

*Outcome Information*: '**Missing "Related Person".**'
-------------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.person_aux**
		* *Action*: **_person_aux_verification_related_person**
		* *State*: **Error (L1)**
		* *Outcome Information*: '**Missing "Related Person".**'

    #. Exercutar a Ação ":bi:`Person (Aux) Related Person Create`":

        #. Parâmetros apresentados:

            * *Person (Aux) Set Code*: **marcado**
            * *Person (Aux) Associate to Address*: **marcado**
            * *Related Person Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Person Create` para executar a Ação.

*Outcome Information*: '**"Phase" has changed.**'
-------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.person_aux**
		* *Action*: **_person_aux_verification_related_person**
		* *State*: **Warning (L1)**
		* *Outcome Information*: '**"Phase" has changed.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Related Person Update`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: **desmarcado**
            * *Update Address Data*: **desmarcado**
            * *Update Family Datae*: **desmarcado**
            * *Related Person Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Person Update` para executar a Ação.

*Outcome Information*: '**"State" has changed.**'
-------------------------------------------------

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

*Outcome Information*: '**"Contact Information (Address)" has changed.**'
-------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Contact Information (Address)" has changed.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Related Person Update`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: **marcado**
            * *Update Address Data*: **desmarcado**
            * *Update Family Datae*: **desmarcado**
            * *Related Person Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Person Update` para executar a Ação.

*Outcome Information*: '**"Address" has changed.**'
---------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_related_person**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**"Address" has changed.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Related Person Update`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: **desmarcado**
            * *Update Address Data*: **marcado**
            * *Update Family Datae*: **desmarcado**
            * *Related Person Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Related Person Update` para executar a Ação.

:blue:`(Nenhuma ação)` *Outcome Information*: '**Related Person "Verification State" is "Warning (L0)".**'
----------------------------------------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

		* *Model Name*: **clv.person_aux**
		* *Action*: **_person_aux_verification_related_person**
		* *State*: **Warning (L1)**
		* *Outcome Information*: '**"Related Person "Verification State" is "Warning (L0)".**'

*Outcome Information*: '**Family "Contact Information (Address)" mismatch.**'
-----------------------------------------------------------------------------

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State`.

    #. :bi:`Verification Outcome`:

        * *Model Name*: **clv.person_aux**
        * *Action*: **_person_aux_verification_family**
        * *State*: **Warning (L1)**
        * *Outcome Information*: '**Family "Contact Information (Address)" mismatch.**'

    #. Exercutar a Ação ":bi:`Person (Aux) Family Update`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: **marcado**
            * *Update Address Data*: **desmarcado**
            * *Family Verification Execute*: **marcado**
            * *Person (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Family Update` para executar a Ação.

*Outcome Information*: '**Missing "Family".**'
----------------------------------------------

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
   :caption: Procedimentos:
