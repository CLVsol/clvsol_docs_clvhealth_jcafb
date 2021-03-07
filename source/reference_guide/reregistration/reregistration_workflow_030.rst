.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação das Entidades do Cadastro Auxiliar [Comunidade]

================================================================
Consolidação das Entidades do **Cadastro Auxiliar** [Comunidade]
================================================================

    Durante o processo de Consolidadação pode ser necessário a execução da verificação de **todas as entidades dos Cadastros já envolvidas no processo de recadastramento**. Essa verificação pode ser feita através do *Verification Batch* “**Current Phase - Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_020`".

    Opcionalmente pode ser necessário a execução da verificação de **todas as entidades dos Cadastros**. Essa verificação pode ser feita através do *Verification Batch* “**Default Batch**”, usando o procedimento: ":doc:`/procedures/verification/verification_procedure_010`".

    Através da *view* :bi:`Verification Outcomes` é possível vizualizar um sumário do estado de verificação de todas a Entidades do Cadastro Auxiliar (e do Cadastro Principal). Para ácesso à *view* :bi:`Verification Outcomes`, utilize o procedimento ":doc:`/procedures/verification/verification_procedure_030`".

    A marcação de :bi:`Verification Marker` dos registros referentes às Entidades de Cadastro é feita utilizando-se o procedimento ":doc:`/procedures/verification/verification_procedure_040`".

    O Processo de Consolidação das Entidades do **Cadastro Auxiliar** é feito guiando-se pelo :bi:`Verification State` e :bi:`Verification Outcomes` de cada registro referentes às Entidades do Cadastro Auxiliar.

    De forma geral, esse processo segue a ordem:

      #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_010`

      #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_010_020`

      #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_010`

      #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_020`

      #. :doc:`/reference_guide/reregistration/reregistration_workflow_030_020_030`

.. toctree::
   :maxdepth: 3
   :caption: Itens Relacionados:

   reregistration_workflow_030_010
   reregistration_workflow_030_020
