.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Os Cadastros

================
Os **Cadastros**
================

Os **Cadastros** são os elementos centrais de armazenamento das informações geradas e coletadas durante a realização das atividades da :bi:`JCAFB`.

As informações cadastrais de todos os Pacientes são armazenadas duplamente em dois repositórios denominados **Cadastro Principal** e **Cadastro Auxiliar**.

Alterações nos dados cadastrais são, em geral, aplicadas primeiramente no Cadastro Auxiliar e posteriormente consolidadas no Cadastro Principal. A inversão desse fluxo de dados é permitida, mas, em geral, não recomendada

Essa "redundância" dos dados permite a verificação/validação das alterações aplicadas no Cadastro Auxiliar, antes da consolidação definitiva no Cadastro Principal.

.. toctree::
   :maxdepth: 2
   :caption: Conteúdo:

   reregistration_cadastro_010
   reregistration_cadastro_020
