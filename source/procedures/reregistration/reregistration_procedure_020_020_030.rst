.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: A Pessoa não cadastrada reside em um Endereço fora da comunidade atendida pela JCAFB (Procedimento)

===========================================================================================================
A **Pessoa não cadastrada** reside em um **Endereço fora da comunidade** atendida pela JCAFB (Procedimento)
===========================================================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_workflow_020_020_030`".

    #. Acessar a *view* :bi:`Persons (Aux)`:

        * Menu de acesso:

            * :bi:`Community` » :bi:`Auxiliary` » :bi:`Persons (Aux)`

    #. Criar um novo registro :bi:`Person (Aux)`:

        #. Preencher o registro :bi:`Person (Aux)` com as informações apresentadas para a Pessoa, exceto informaçôes relativas ao Endereço e à Família.

        #. Salvar o registro.

        #. Executar a Ação ":bi:`Person (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Unvailable`
                * *Address is unavailable*: :bi:`Set` » **marcado**
                * *Family is unavailabl*: :bi:`Set` » **marcado**
                * *Address (Aux) is unavailable*: :bi:`Set` » **marcado**
                * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                * *Clear Address Data*: **marcado**
                * *Phase*: **JCAFB-2021v**
                * *Person (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Caso necessário, editar o registro :bi:`Person (Aux)`:

        #. Preencher os campos de *Contact Information* com informações que indiquem o novo Endereço da Pessoa fora da comunidade.

        #. Salvar o registro.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
