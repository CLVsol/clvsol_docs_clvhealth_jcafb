.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um Endereço fora da comunidade atendida pela JCAFB

=================================================================================================
O **Paciente já cadastrado** mudou-se para um **Endereço fora da comunidade** atendida pela JCAFB
=================================================================================================

    O processo de Recadastramento de um Paciente já cadastrado que tenha mudado para um  Endereço fora da comunidade atendida pela JCAFB é descrito pelo **Fluxo de Trabalho** (:bi:`Workflow`) apresentado a seguir:

    #. Aplicação das atualizações necessárias no Cadastro Auxiliar do Paciente:

        A aplicação das atualizações necessárias no Cadastro do Paciente é feita inicialmente no registro :bi:`Patient (Aux)` associado a ele, utilizando o procedimento ":doc:`reregistration_procedure_020_010_070`".

        O conteúdo dos **Cadastros** associados ao Paciente após a aplicação dessas atualizações é o apresentado a seguir:

            * **Cadastro Principal**:

                * :bi:`Patient`:

                    * *Contact Information* = Dados de Endereço do Paciente :blue:`inalterados`
                    * *Contact Information is unavailable* = **desmarcado**
                    * Outros Dados = Outros Dados do Paciente :blue:`inalterados`
                    * *Register State* = *Register State* :blue:`inalterado`
                    * *Patient State* = *Patient State* :blue:`inalterado`
                    * *Phase* = Phase :blue:`inalterada`

            * **Cadastro Auxiliar:**

                * :bi:`Patient (Aux)`:

                    * *Related Patient* » :bi:`Patient`
                    * *Contact Information* = Dados :green:`com informações que indiquem o novo` Endereço do Paciente :green:`fora da comunidade, se disponível, ou **vazio**`
                    * *Contact Information is unavailable* = :green:`**marcado** caso *Contact Information* estiver **vazio**`
                    * Outros Dados = Outros Dados do Paciente :green:`com a aplicação das atualizações necessárias`
                    * *Register State* = ":green:`Revised`"
                    * *Patient State* = ":green:`Unavailable`"
                    * *Phase* =  :green:`Phase atual`

    #. Consolidação do Cadastro Auxiliar do Paciente:

            Referência: ":doc:`reregistration_workflow_030`"

        A Consolidação do registro :bi:`Patient (Aux)` pode ser postergada e executada coletivamente para todos os Pacientes em processo de Cadastramento/Recadastramento em um momento mais oportuno (durante as Campanhas, por exemplo, essa deve ser a regra), mas os :bi:`Verification Outcomes` reportados em cada registro :bi:`Patient (Aux)` devem ser analizados. Erros de digitação e inconsistências entre as informações nos dados apresentados para o Paciente podem ser detectados ainda nesse momento.

        Em particular, os seguintes erros/advertências devem ser analisados e, se possível, corrigidos, durante a aplicação das atualizações no Cadastro Auxiliar do Paciente:

            * :doc:`reregistration_workflow_030_020_010_001`

    #. Consolidação do Cadastro Principal do Paciente:

            Referência: ":doc:`reregistration_workflow_040`"

        A Consolidação do registro :bi:`Patient` pode ser postergada e executada coletivamente para todos os Pacientes em processo de Cadastramento/Recadastramento em um momento mais oportuno (durante as Campanhas, por exemplo, essa deve ser a regra).

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
