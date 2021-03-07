.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Preparação do Cadastro Auxiliar [Comunidade]

================================================
Preparação do **Cadastro Auxiliar** [Comunidade]
================================================

De forma a agilizar o Processo de  **Cadastramento/Recadastramento** de todas as Pessoas, concomitantemente ao de seus respectivos Endereços é conveniente que o **Cadastro Auxiliar** seja preparado previamente.

Essa preparação se constitui basicamente em copiar todos os registros do Cadastro Principal (registros :bi:`Person` e :bi:`Address`) para o Cadastro Auxiliar (respectivamente, registros :bi:`Person (Aux)` e :bi:`Address (Aux)`).

Essa preparação é, da forma descrita a seguir, realizada somente uma vez, no início de cada umna das Fases de um ciclo da JCAFB.

A Preparação do Cadastro Auxiliar é implementada através das seguintes ações:

    #. Excluir todos os registros de Pessoas do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_010`".

    #. Excluir todos os registros de Endereços do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_020`".

    #. Excluir todos os registros :bi:`Verification Outcomes` executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_025`".

    #. Associar todas as Pessoas a uma Pessoa (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_030`".

    #. Associar todos os Endereços a um Endereço (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_040`".

    #. Remover a Fase de todas as Pessoas (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_050`".

    #. Remover a Fase de todos os Endereços (Aux) executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_060`".

    #. :red:`(Não Executado])` Excluir todos os registros de Pessoas falecidas do Cadastro Auxiliar executando o procedimento ":doc:`/procedures/reregistration/reregistration_procedure_cadastro_aux_setup_070`".
    
    #. :red:`(Não Executado])` Executar o Verification Batch “Default Batch” executando ":doc:`/procedures/verification/verification_procedure_010`".

    #. Executar o Verification Batch “Default Batch” executando ":doc:`/procedures/verification/verification_procedure_015`".

.. toctree::
   :maxdepth: 3
   :caption: Tópicos Relacionados:
