.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Cadastro Principal

======================
**Cadastro Principal**
======================

O **Cadastro Principal** é composto pelas **Entidade de Cadastro**:

    * :bi:`Patient`:

        * Um registro :bi:`Patient` possui, além dos parâmetros específicos a um Paciente:

            * as informações de :bi:`Contact Information` do Paciente,
            * um relacionamento com um registro :bi:`Residence`.

    * :bi:`Residence`:

        * Um registro :bi:`Residence` possui, além dos parâmetros específicos a uma Residência:

            * as informações de :bi:`Contact Information` da Residência.

As informações de Endereço do :bi:`Contact Information` das duas Entidades do Cadastro Principal inter-relacionadas devem ser idênticas.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
