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

Existe o relacionamento entre a **Entidade (Aux)** do **Cadastro Auxiliar** e as **Entidades** do **Cadastro Principal**:

    * Um registro :bi:`Patient (Aux)` possui:

        * um relacionamento com um registro :bi:`Patient` (:bi:`Related Patient`),

As informações de Endereço do :bi:`Contact Information` do registro :bi:`Patient (Aux)` relacionada com o registro :bi:`Patient` devem ser as mesmas.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
