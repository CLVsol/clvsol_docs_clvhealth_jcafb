.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente não cadastrado reside em um Endereço da Comunidade

=====================================================================
O **Paciente não cadastrado** reside em um **Endereço da Comunidade**
=====================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_020_010`".

    #. Procurar pelo Paciente na *view* :bi:`Patients (Aux)`:

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Pesquisar pelo Paciente.

        #. Certificar-se de que não existe qualquer registro :bi:`Patient (Aux)` associado ao Paciente.

    #. Caso nenhum registro seja encontrado:

        #. Criar um novo registro :bi:`Patient (Aux)`:

            #. Preencher o registro :bi:`Patient (Aux)` com as informações apresentadas para o Paciente, exceto informaçôes relativas ao Endereço.

            #. Preencher os dados de :bi:`Contact Information` com as informações apresentadas para o Endereço da Paciente.

            #. Salvar o registro.

        #. Certificar-se que as informações de Endereço apresentadas para o Paciente apontam para um local dentro da Comunidade atendida pela JCAFB:

            #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

                #. Parâmetros apresentados:

                    * *Register State*: :bi:`Set` » :bi:`Revised`
                    * *State*: :bi:`Set` » :bi:`Available`
                    * *Phase*: **JCAFB-2021v**
                    * *Patient (Aux) Verification Execute*: **marcado**

                #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
