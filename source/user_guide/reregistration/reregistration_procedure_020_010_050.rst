.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastrado mudou-se para um outro Endereço da Comunidade

==============================================================================
O **Paciente já cadastrado** mudou-se para um outro **Endereço da Comunidade**
==============================================================================

    * *Workflow*: ":doc:`reregistration_workflow_020_010_050`".

    #. Procurar pelo Paciente na *view* :bi:`Patients (Aux)`:

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Pesquisar pelo Paciente.

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente encontrado.

        #. Confirmar que as informações de :bi:`Contact Information` cadastradas para o Paciente NÃO coincidem com as informações de Endereço (dentro da Comunidade atendida pela JCAFB) apresentadas para o mesmo:

            #. Aplicar as atualizações necessárias:

                #. **Editar** o registro associado ao Paciente.

                #. **Atualizar** as informações de :bi:`Contact Information` cadastradas para o Paciente com as novas informações de Endereço apresentadas para o mesmo.

                #. **Salvar** o registro.

        #. Verificar se os Outros Dados cadastrados para o Paciente coincidem com as informações dos Outros Dados apresentadas para o mesmo:

            #. Se for necessário atualizar alguma informação do cadastro:

                #. **Editar** o registro associado ao Paciente.

                #.  **Alterar** os parâmetros necessários.

                #. **Salvar** o registro.

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
