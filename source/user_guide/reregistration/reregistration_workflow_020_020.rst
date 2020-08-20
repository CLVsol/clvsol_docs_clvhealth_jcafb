.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Cadastro Auxiliar (Pessoa não cadastrada)

============================================================
Criação do **Cadastro Auxiliar** (**Pessoa não cadastrada**)
============================================================

O processo de criação do **Cadastro Auxiliar** para uma Pessoa **não cadastrada** é utilizado quando a Pessoa tiver sido declarada como **não cadastrada**.

Portanto, quando não existir ainda um **Cadastro Auxiliar** para a Pessoa, o mesmo deverá ser manualmente criado para conter as informações disponíveis para a Pessoa. Essas informações serão manualmente inseridas nos registros pertinentes.

Se porventura já existir um **Cadastro Auxiliar** associado à Pessoa, o mesmo será selecionado para dar proseguimento ao processo de recadastramento da mesma.

O **Cadastro Auxiliar** criado poderá ser composto pelas **Entidades (Aux)**:

    * :bi:`Person (Aux)`:

        * O registro será preenchido com as informações coletadas para a Pessoa.

    * :bi:`Address (Aux)`:

        * O registro :bi:`Address (Aux)` deverá ser **criado automaticamente** a partir de um registro :bi:`Address` já cadastrado, quando se constatar que a Pessoa reside no Endereço associado a este registro :bi:`Address`.

        * O registro :bi:`Address (Aux)` deverá ser **criado manualmente**, quando se constatar que a Pessoa reside em um Endereço não cadastrado da comunidade atendida.

        * O registro :bi:`Address (Aux)` **não será criado**, quando se constatar que a Pessoa reside em um Endereço fora da comunidade atendida.

.. toctree::
   :maxdepth: 1
   :caption: Tópicos Relacionados:

.. reregistration_workflow_020_020_010
.. reregistration_workflow_020_020_020
.. reregistration_workflow_020_020_030
