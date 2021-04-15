.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: O Paciente já cadastradoFaleceu

====================================
O **Paciente já cadastrado** Faleceu
====================================

    * *Workflow*: ":doc:`reregistration_workflow_020_010_080`".

    #. Procurar pelo Paciente na *view* :bi:`Patients (Aux)`:

        #. Acessar a *view* :bi:`Patients (Aux)`:

            * Menu de acesso:

                * :bi:`Health` » :bi:`Health` » :bi:`Patient` » :bi:`Patients (Aux)`

        #. Pesquisar pelo Paciente.

    #. Abrir o registro :bi:`Patient (Aux)` associado ao Paciente encontrado.

        #. **Editar** o registro associado ao Paciente.

        #. Caso a Data de Falecimento do Paciente tenha sido fornecida, indicar essa data no campo :bi:`Deceased Date`.

        #. Caso a Data de Falecimento do Paciente seja desconhedica, **indicar** o parâmetro :bi:`Force Is Deceased` como **marcado**.

        #. **Salvar** o registro.

        #. Executar a Ação ":bi:`Patient (Aux) Mass Edit`":

            #. Parâmetros apresentados:

                * *Register State*: :bi:`Set` » :bi:`Revised`
                * *State*: :bi:`Set` » :bi:`Unvailable`
                * *Contact Information is unavailable*: :bi:`Set` » **marcado**
                * *Clear Address Data*: **marcado**
                * *Phase*: :bi:`Phase` **atual**
                * *Patient (Aux) Verification Execute*: **marcado**

            #. Utilizar o botão :bi:`Mass Edit` para executar a Ação.

.. toctree::
   :maxdepth: 2
   :caption: Tópicos Relacionados:
