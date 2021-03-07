.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Procura por um Paciente em Contatos (Procedimento)

==========================================================
Procura por um **Paciente** em **Contatos** (Procedimento)
==========================================================

    * *Workflow*: ":doc:`/reference_guide/reregistration_patient/reregistration_patient_workflow_010_010`".

    #. Procurar pelo Paciente na *view* :bi:`Contatos`:

        #. Acesser a *view* **Contatos**:

            * Menu de acesso:

                * **Contatos** » **Contatos**

        #. Selecionar a **visualização em lista**.

        #. Aplicar o filtro: **Agrupar Por** » :bi:`Address Type`.

        #. Pesquisar pelo Paciente.

    #. **Caso um registro associado a esse Paciente seja encontrado** com *Address Type* ":bi:`Patient`", independentemente da existência ou não de um registro com *Address Type* ":bi:`Patient (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Patient`.

        #. Acionar o botão **[** :bi:`Patient` **]**.

        #. Utilizar o registro associado ao Paciente apresentado na *view* :bi:`Patients`.

    #. **Caso um registro associado a esse Paciente seja encontrado** com *Address Type* ":bi:`Patient (Aux)`":

        #. Abrir o registro de contato encontrado com *Address Type* ":bi:`Patient (Aux)`".

        #. Acionar o botão **[** :bi:`Patient (Aux)` **]**.

        #. Utilizar o registro associado ao Paciente apresentado na *view* :bi:`Patients (Aux)`.

    #.  **Caso um registro associado a esse Paciente NÃO seja encontrado** com qualquer *Address Type*:

        #. Será necessário realizar o cadastramento da Paciente.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
