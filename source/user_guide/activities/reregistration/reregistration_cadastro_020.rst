.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Cadastro Auxiliar

=====================
**Cadastro Auxiliar**
=====================

O **Cadastro Auxiliar** é composto pelas 2 **Entidades (Aux)**:

    * :bi:`Person (Aux)`:

        * Um registro :bi:`Person (Aux)` possui, além dos parâmetros específicos a uma Pessoa:

            * as informações de :bi:`Contact Information`,
            * um relacionamento com um registro :bi:`Address (Aux)`,

    * :bi:`Address (Aux)`:

        * Um registro :bi:`Address (Aux)` possui, além dos parâmetros específicos a um Endereço:

            * as informações de :bi:`Contact Information`.

As informações de Endereço do :bi:`Contact Information` das 2 **Entidades (Aux)** inter-relacionadas devem ser idênticas.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
