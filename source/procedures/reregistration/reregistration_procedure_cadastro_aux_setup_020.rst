.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Excluir todos os Endereços do Cadastro Address (Aux) (Procedimento)

===========================================================================
Excluir todos os registros de Endereços do Cadastro Auxiliar (Procedimento)
===========================================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration/reregistration_cadastro_aux_setup`".

    #. Excluir todos os **Endereços** do **Cadastro Auxiliar**:

        #. Acessar a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Ativar o filtro **Agrupar por** » :bi:`Address Type`

        #. Selecionar todas os :bi:`Addresses (Aux)`

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

    #. Excluir todos os :bi:`Verification Outcomes` referentes a registros de :bi:`Address (Aux)`:

        #. Acessar a *view* :bi:`Verification Outcomes`:

            * Menu de acesso:

                * :bi:`Verification` » :bi:`Verification` » :bi:`Verification Outcomes`

        #. Ativar o filtro **Agrupar por** » :bi:`Model Name`

        #. Selecionar todas os :bi:`Verification Outcomes` referentes a "**clv.address_aux**"

        #. Executar a Ação **Excluir**:

            #. Utilize o botão :bi:`Ok` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
