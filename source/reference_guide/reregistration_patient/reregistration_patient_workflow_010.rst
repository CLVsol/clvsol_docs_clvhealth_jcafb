.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Procura pelas Entidades nos Cadastros existentes [Pacientes]

====================================================================
Procura pelas **Entidades** nos **Cadastros** existentes [Pacientes]
====================================================================

De posse dos dados referentes a uma Entidade do Cadastro (Paciente), o primeiro passo é a pesquisa pela existência prévia de registros relacionados a essa Entidade tanto no **Cadastro** (Paciente) quanto no **Cadastro Auxiliar** (Paciente).

Após a execução da pesquisa por um Paciente:

    * Um Paciente será declarado como "**já cadastrado**" quando estiver associado a um registro ":bi:`Patient`", independentemente de estar ou não associado a um registro ":bi:`Patient (Aux)`".

    * Um Paciente será declarado como "**não cadastrado**" quando não estiver associado a um registro ":bi:`Patient`", independentemente de estar ou não associado a um registro ":bi:`Patient (Aux)`".

    * Um Paciente será declarado como "**em fase de recadastramento**"" quando estiver associado a um registro ":bi:`Patient (Aux)`" com informações que não tenham ainda sido consolidadas em um registro ":bi:`Patient`" a ele asssociado.

    * Um Paciente será declarado como "**recadastrado**"" quando estiver associado a um registro ":bi:`Patient (Aux)`" com informações que já tenham sido consolidadas em um registro ":bi:`Patient`" a ele asssociado.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:

   reregistration_patient_workflow_010_010
   reregistration_patient_workflow_010_020
   reregistration_patient_workflow_010_025
