.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Criação do Cadastro Auxiliar (Pessoa já cadastrada)

===========================================================
Criação do **Cadastro Auxiliar** (**Pessoa já cadastrada**)
===========================================================

O processo de criação do **Cadastro Auxiliar** associado a uma Pessoa **já cadastrada** é utilizado quando a Pessoa tiver sido declarada como **já cadastrada**.

Este processo é, basicamente, a atualização das informações em uma cópia do **Cadastro** atual associado à Pessoa. 

Portanto, quando não existir ainda um **Cadastro Auxiliar** associado à Pessoa, o mesmo deverá ser criado como uma cópia do **Cadastro** existente, associado à Pessoa.

Se porventura já existir um **Cadastro Auxiliar** associado à Pessoa, o mesmo será selecionado para dar proseguimento ao processo de recadastramento da mesma.

O **Cadastro Auxiliar** criado poderá ser composto pelas seguintes **Entidades (Aux)**:

    * :bi:`Person (Aux)`:

        * O registro será preenchido com as informações já cadastradas para a Pessoa e atualizado com as informações coletadas para a Pessoa.

    * :bi:`Address (Aux)`:

        * O registro :bi:`Address (Aux)` deverá ser **criado automaticamente** a partir do registro :bi:`Address` associado ao Endereço da Pessoa, quando se constatar que a Pessoa foi mantida no Endereço atual cadastrado.

        * O registro :bi:`Address (Aux)` deverá ser **criado automaticamente** a partir de um registro :bi:`Address` já cadastrado, quando se constatar que a Pessoa mudou-se para o Endereço associado a este registro :bi:`Address`.

        * O registro :bi:`Address (Aux)` deverá ser **criado manualmente**, quando se constatar que a Pessoa mudou-se para um Endereço não cadastrado da comunidade atendida.

        * O registro :bi:`Address (Aux)` **não será criado**, quando se constatar que a Pessoa mudou-se para um Endereço fora da comunidade atendida ou que a Pessoa faleceu.

.. toctree::
   :maxdepth: 1
   :caption: Tópicos Relacionados:

   reregistration_workflow_020_010_010
.. reregistration_workflow_020_010_020
.. reregistration_workflow_020_010_030
.. reregistration_workflow_020_010_040
.. reregistration_workflow_020_010_050
.. reregistration_workflow_020_010_060
.. reregistration_workflow_020_010_070
.. reregistration_workflow_020_010_080
.. reregistration_workflow_020_010_090
