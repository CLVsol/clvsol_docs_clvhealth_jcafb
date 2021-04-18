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

.. index:: Patient (Aux) Reload

==========================
:bi:`Patient (Aux) Reload`
==========================

    * *Workflow*: ":doc:`reregistration_workflow_030_020_020_010`".
    * *Workflow*: ":doc:`reregistration_workflow_030_020_020_020`".
    * *Workflow*: ":doc:`reregistration_workflow_030_020_020_022`".
    * *Workflow*: ":doc:`reregistration_workflow_030_020_020_030`".

    :bred:`IMPORTANTE`: Antes de prosseguir com a execução deste procecimento **lembre-se** de que:

        * A menos das Informações de Contato todos os outros parâmetros que porventura tenham sido atualizados no registro :bi:`Patient (Aux)` serão revertidos aos valores correntemente armazenados no registro :bi:`Patient` de forma irreversível.

    #. Acessar a *view* :bi:`Patients (Aux)`:

        * Menu de acesso:

            * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

    #. Aplicar o filtro: **Agrupar Por** » :bi:`Phase` » :bi:`Register State` » :bi:`Verification State` » :bi:`Verification Outcome Informations`.

    #. Selecionar o(s) registro(s) desejado(s).

    #. Executar a Ação ":bi:`Patient (Aux) Reload`":

        #. Parâmetros apresentados:

            * *Update Contact Information Data*: 

                * **marcado** caso se deseje reverter as Informações de Contato;

                * **desmarcado** caso contrário.

            * *Patient (Aux) Verification Execute*: **marcado**

        #. Utilizar o botão :bi:`Reload` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
