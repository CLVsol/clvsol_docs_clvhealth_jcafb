.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço fora da Comunidade atendida pela JCAFB

==============================================================================================
O **Paciente não cadastrado** reside em um **Endereço fora da Comunidade** atendida pela JCAFB
==============================================================================================

    O processo de Cadastramento de um novo Paciente que resida em um Endereço fora da comunidade atendida pela JCAFB é descrito pelo **Fluxo de Trabalho** (:bi:`Workflow`) apresentado a seguir:

    #. Inclusão das informações necessárias no novo Cadastro Auxiliar para o Paciente:

        A inclusão das informações necessárias no novo Cadastro para o Paciente é feita inicialmente em um novo registro :bi:`Patient (Aux)` associado a ele, utilizando o procedimento ":doc:`reregistration_procedure_020_020_030`".

        O conteúdo dos **Cadastros** associados ao Paciente após a aplicação dessas atualizações é o apresentado a seguir:

            * **Cadastro Principal**:

                * :bi:`Patient`:

                    :blue:`Nenhum registro será identificado`.

            * **Cadastro Auxiliar:**

                * :bi:`Patient (Aux)`:

                    * *Related Patient* » :green:`**vazio**`
                    * *Contact Information* = Dados :green:`com informações que indiquem o novo` Endereço do Paciente :green:`fora da comunidade, se disponível, ou **vazio**`
                    * *Contact Information is unavailable* = :green:`**marcado** caso *Contact Information* estiver **vazio**`
                    * Outros Dados = Outros Dados do Paciente :green:`com a aplicação das atualizações necessárias`
                    * *Register State* = ":green:`Revised`"
                    * *Patient State* = ":green:`Unavailable`"
                    * *Phase* =  :green:`Phase atual`

    #. Consolidação do Cadastro Auxiliar do Paciente:

        * Referência: ":doc:`reregistration_workflow_030`"

    #. Consolidação do Cadastro Principal do Paciente:

         * Referência: ":doc:`reregistration_workflow_040`"

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
