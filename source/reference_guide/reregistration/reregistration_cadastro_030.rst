.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Relacionamento entre o Cadastro Auxiliar e o Cadastro Principal

=======================================================================
Relacionamento entre o **Cadastro Auxiliar** e o **Cadastro Principal**
=======================================================================

Além do inter-relacionamento entre as **Entidades** que compõem cada um dos Cadastros, existe o relacionamento entre as **Entidades (Aux)** do **Cadastro Auxiliar** e as **Entidades** do **Cadastro Principal**:

    * Um registro :bi:`Person (Aux)` possui:

        * um relacionamento com um registro :bi:`Person` (:bi:`Related Person`),
        * um relacionamento com um registro :bi:`Address`
        * um relacionamento com um registro :bi:`Family`.

    * Um registro :bi:`Address (Aux)` possui:

        * um relacionamento com um registro :bi:`Address` (:bi:`Related Address`).

As informações de Endereço do :bi:`Contact Information` das 2 Entidades do Cadastro (Aux) relacionadas com as 3 Entidades do Cadastro Principal devem ser as mesmas.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
