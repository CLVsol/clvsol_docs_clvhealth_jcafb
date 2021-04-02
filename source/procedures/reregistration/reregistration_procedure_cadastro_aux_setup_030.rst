.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Associar todas as Pessoas a uma Pessoa (Aux) (Procedimento)

===========================================================
Associar todas as Pessoas a uma Pessoa (Aux) (Procedimento)
===========================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`".

    #. Executar a Ação :bi:`Person Associate to Person (Aux)` para todas as Pessoas:

        #. Acessar a *view* :bi:`Persons`:

            * Menu de acesso:

                * :bi:`Community` » :bi:`Community` » :bi:`Persons`

        #. Ativar o filtro **Agrupar por** » :bi:`Register State`

        #. Selecionar todos as Pessoas com :bi:`Register State` != ":bi:`Canceled`"

        #. Executar a Ação :bi:`Person Associate to Person (Aux)`:

            * Parâmetros utilizados:

                * *Create new Person (Aux)*: **marcado**

                * *Create new Address (Aux)*: **marcado**

            #. Utilize o botão :bi:`Associate to Person (Aux)` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
