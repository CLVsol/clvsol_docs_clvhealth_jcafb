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

    * *Workflow*: ":doc:`reregistration_workflow_020_010_070`".

    #. Procurar pelo Paciente na *view* :bi:`Patients (Aux)`:

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Pesquisar pelo Paciente.

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente encontrado.

        #. Confirmar que o Paciente mudou-se para um Endereço fora da comunidade atendida pela JCAFB (ou para um Endereço desconhecido):

            #. Caso as informações do novo Endereço sejam apresentadas:

                #. **Editar** o registro associado ao Paciente.

                #. **Atualizar** as informações de :bi:`Contact Information` cadastradas para o Paciente com as novas informações de Endereço apresentadas para o mesmo.

                #. **Salvar** o registro.

            #. Caso as informações do novo Endereço sejam desconhecidas:

                #. **Editar** o registro associado ao Paciente.

                #. **Excluir** todas as informações de :bi:`Contact Information` cadastradas para o Paciente utilizando o botão :bi:`Clear Address Data`.

                #. **Indicar** o parâmetro :bi:`Contact Information is unavailable` como **marcado**.

                #. **Salvar** o registro.

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Unvailable`
                * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                * *Clear Address Data*: **marcado**
                * *Phase*: **JCAFB-2021v**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

    #. Caso necessário, editar o registro :bi:`Patient (Aux)`:

        #. Preencher os campos de *Contact Information* com informações que indiquem o novo Endereço da Pessoa fora da comunidade.

        #. Salvar o registro.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
