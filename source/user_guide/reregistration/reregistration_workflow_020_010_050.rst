.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um outro Endereço

================================================================
O **Paciente já cadastrado** mudou-se para um outro **Endereço**
================================================================

    O processo de Recadastramento de um Paciente já cadastrado que tenha mudado para um outro Endereço dentro da comunidade atendida pela JCAFB é descrito pelo **Fluxo de Trabalho** (:bi:`Workflow`) apresentado a seguir:

    #. Aplicação das atualizações necessárias no Cadastro Auxiliar do Paciente:

        A aplicação das atualizações necessárias no Cadastro do Paciente é feita inicialmente no registro :bi:`Patient (Aux)` associado a ele, utilizando o procedimento ":doc:`reregistration_procedure_020_010_050`".

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
                    * *Contact Information* = Dados do :green:`novo` Endereço do Paciente
                    * *Contact Information is unavailable* = **desmarcado**
                    * Outros Dados = Outros Dados do Paciente :green:`com a aplicação das atualizações necessárias`
                    * *Register State* = ":green:`Revised`"
                    * *Patient State* = ":green:`Available`"
                    * *Phase* =  :green:`Phase atual`

    #. Consolidação do Cadastro Auxiliar do Paciente:

        * Referência: ":doc:`reregistration_workflow_030`"

    #. Consolidação do Cadastro Principal do Paciente:

         * Referência: ":doc:`reregistration_workflow_040`"

.. toctree::
   :maxdepth: 2
   :caption: Procedimentos:
