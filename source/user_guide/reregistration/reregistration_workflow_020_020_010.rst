.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço na Comunidade

=====================================================================
O **Paciente não cadastrado** reside em um **Endereço na Comunidade**
=====================================================================

    O processo de Cadastramento de um novo Paciente que resida em um Endereço dentro da comunidade atendida pela JCAFB é descrito pelo **Fluxo de Trabalho** (:bi:`Workflow`) apresentado a seguir:

    #. Inclusão das informações necessárias no novo Cadastro Auxiliar para o Paciente:

        A inclusão das informações necessárias no novo Cadastro para o Paciente é feita inicialmente em um novo registro :bi:`Patient (Aux)` associado a ele, utilizando o procedimento ":doc:`reregistration_procedure_020_020_010`".

        O conteúdo dos **Cadastros** associados ao Paciente após a aplicação dessas atualizações é o apresentado a seguir:

            * **Cadastro Principal**:

                * :bi:`Patient`:

                    :blue:`Nenhum registro será identificado`.

            * **Cadastro Auxiliar:**

                * :bi:`Patient (Aux)`:

                    * *Related Patient* » :green:`**vazio**`
                    * *Contact Information* = :green:`Dados do Endereço do Paciente`
                    * *Contact Information is unavailable* = **desmarcado**
                    * Outros Dados = :green:`Outros Dados informados para a Paciente`
                    * *Register State* = ":green:`Revised`"
                    * *Patient State* = ":green:`Available`"
                    * *Phase* =  :green:`Phase atual`

    #. Consolidação do Cadastro Auxiliar do Paciente:

            Referência: ":doc:`reregistration_workflow_030`"

        A Consolidação do registro :bi:`Patient (Aux)` pode ser postergada e executada coletivamente para todos os Pacientes em processo de Cadastramento/Recadastramento em um momento mais oportuno (durante as Campanhas, por exemplo, essa deve ser a regra), mas os :bi:`Verification Outcomes` reportados em cada registro :bi:`Patient (Aux)` devem ser analizados. Erros de digitação e inconsistências entre as informações nos dados apresentados para o Paciente podem ser detectados ainda nesse momento.

    #. Consolidação do Cadastro Principal do Paciente:

            Referência: ":doc:`reregistration_workflow_040`"

        A Consolidação do registro :bi:`Patient` pode ser postergada e executada coletivamente para todos os Pacientes em processo de Cadastramento/Recadastramento em um momento mais oportuno (durante as Campanhas, por exemplo, essa deve ser a regra).

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
