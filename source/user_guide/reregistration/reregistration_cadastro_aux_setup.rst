.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Preparação do Cadastro Auxiliar

===================================
Preparação do **Cadastro Auxiliar**
===================================

De forma a agilizar o Processo de  **Cadastramento/Recadastramento** de todas as Pessoas atendidas, concomitantemente ao **Cadastramento/Recadastramento** dos respectivos Endereços, quando estes estiverem localizados na comunidade atendida pela :bi:`JCAFB`, é conveniente que o **Cadastro Auxiliar** seja preparado previamente.

Essa preparação se constitui pela execução das seguintes ações:

    #. Excluir todos os registros :bi:`Person (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_010`".

    #. Excluir todos os registros :bi:`Address (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_020`".

    #. Associar todos os registros :bi:`Person` a um registro :bi:`Person (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_030`".

    #. Associar todos os registros :bi:`Address (Aux)` a um registro :bi:`Address (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_040`".

    #. Remover a Fase de todos os registros :bi:`Person (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_050`".

    #. Remover a Fase de todos os registros :bi:`Address (Aux)` executando ":doc:`/procedure/reregistration/reregistration_procedure_cadastro_aux_setup_060`".

    #. Executar o Verification Batch “Default Batch”

.. toctree::
   :maxdepth: 3
   :caption: Tópicos Relacionados:
