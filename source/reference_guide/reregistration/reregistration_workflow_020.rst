.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Cadastro Auxiliar

================================
Criação do **Cadastro Auxiliar**
================================

    Se, após a pesquisa por uma **Pessoa** nos **Cadastros**, não for identificado um registro associado à Pessoa em ":bi:`Persons (Aux)`", independentemente da Pessoa ter sido declarada "**já cadastrada**" ou "**não cadastrada**", essa Pessoa deve ser cadastrada/recadastrada e, portanto, incluída no **Cadastro Auxiliar**.

    No caso de uma Pessoa "**já cadastrada**", os registros relativos a ela serão automaticamente criados no **Cadastro Auxiliar** (:bi:`Person (Aux)` e :bi:`Address (Aux)`) a partir das informações dos registros equivalentes presentes no **Cadastro** (:bi:`Person`, :bi:`Address`).

    Neste caso, o registro ":bi:`Address (Aux)`"relativo à Pessoa pode já ter sido criado previamente (e será automaticamente associado ao registro ":bi:`Person (Aux)`") caso uma outra Pessoa resitente no mesmo Endereço já esteja em processo de recadastramento.

    No caso de uma Pessoa "**não cadastrada**", os registros no **Cadastro Auxiliar** relativos a ela (:bi:`Person (Aux)` e :bi:`Address (Aux)`) será criado com as informações apresentadas para a Pessoa.

    Neste caso, o registro ":bi:`Address (Aux)`" relativo à Pessoa pode já ter sido criado previamente (e deverá ser associado ao registro ":bi:`Person (Aux)`") caso uma outra Pessoa resitente no mesmo Endereço já esteja em processo de recadastramento.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:

   reregistration_workflow_020_010
   reregistration_workflow_020_020
