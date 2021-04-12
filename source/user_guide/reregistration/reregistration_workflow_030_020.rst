.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Consolidação de Patient (Aux)

===================================
Consolidação de :bi:`Patient (Aux)`
===================================

    O Processo de Consolidação de :bi:`Patient (Aux)` é feito guiando-se pelo :bi:`Verification State` e :bi:`Verification Outcomes` de cada registro :bi:`Patient (Aux)`.

    Quando o :bi:`Verification State` de um registro estiver reportando o estado "**Ok**", nenhuma ação ou verificação adicional será necessária para o registro.

    Os estados diferentes de "**Ok**" são classificados em 3 níveis de "**L0**", "**L1**" e "**L2**" (não existe no momento a ocorrencia do nivel "**L2**"):

    	* "**L0**": ("Error (L0)" ou "Warning (L0)") sinalizam um Erro ou Advertência ocorrendo no próprio registro :bi:`Patient (Aux)`.

    	* "**L1**": ("Error (L1)" ou "Warning (L1)") sinalizam um Erro ou Advertência ocorrendo no registro :bi:`Patient` relacionado ao registro :bi:`Patient (Aux)`.

    	* "**L2**": ("Error (L2)" ou "Warning (L1)") não utilizado.

    O campo :bi:`Verification Outcome Informations` apresenta um sumário do(s) motivo(s) que geraram a reportagem do(s) erro(s) e/ou advertência(s).

    Acessando a aba :bi:`Verification Outcomes` é possível uma verificação/análise mais detalhada das ocorrências reportadas. Nessa aba cada ocorrência é apresentada em vários campos a saber:

    	* :bi:`Record Last Update`: data em que ocorreu a última modificação do registro analizado.

    	* :bi:`Action`: ação de verificação que gerou a reportagem da ocorrẽncia.

    	* :bi:`Verification Date`: data em que a *Action* foi executada pela última vez.

    	* :bi:`State`: o *Verification State* da(s) ocorrência(s) gerada(s) pela *Action*.

    	* :bi:`Outcome Informations`: detalhamento da(s) ocorrência(s) reportadas.

    De forma geral, o Processo de Consolidação de :bi:`Patient (Aux)` segue a ordem:

      #. :doc:`reregistration_workflow_030_020_010`

      #. :doc:`reregistration_workflow_030_020_020`

      #. :doc:`reregistration_workflow_030_020_030`

.. toctree::
   :maxdepth: 2
   :caption: Conteúdo:

   reregistration_workflow_030_020_010
   reregistration_workflow_030_020_020
   reregistration_workflow_030_020_030
