.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Contact Information

=======================
**Contact Information**
=======================

	Um elemento presente em todas as Entidades de Cadastro são as informações de :bi:`Contact Information`, composta pelos dados da localização do Endereço dos Pascientes e/ou Residências acrescidas de informações de Telefones, etc..

	A ausência ou a apresentação de dados inválidos como Informações de Contato serão sempre detetadas e reportadas durante o processo de ":doc:`reregistration_procedure_verification`".

	Nas ocasiões em que não for possível apresentar as Informações de Contato, essa situação deve ser sinalizada marcando o campo :bi:`Contact Information is unavailable`:

		* *Contact Information is unavailable*: "**marcado**".

	Nas ocasiões em que forem apresentadas as Informações de Contato, essa situação deve ser sinalizada desmarcando o campo :bi:`Contact Information is unavailable`:

		* *Contact Information is unavailable*: "**desmarcado**".

	O conjunto de dados que compõem o :bi:`Contact Information` geram (de forma automática) um identificador único para cada conjunto de Informações de Contato de um Paciente ou Residência denominado :bi:`Address Name`.

	Pacientes e Residências cujos :bi:`Contact Informations` apresentem o mesmo :bi:`Address Name` serão considerados como compartilhando o mesmo Endereço.

	A edição das Informações de Contato devem ser sempre realizadas com cuidado de forma a evitar que dados relativos a Endereços diferentes não gerem um mesmo :bi:`Address Name` ou de forma análoga que dados relativos a um mesmo Endereço não gerem :bi:`Address Names` diferentes.

	De forma a facilitar o gerenciamento dos :bi:`Address Names`, duas Tabelas de suporte devem ser utilizadas:

		* :doc:`reregistration_cadastro_100_010` e

		* :doc:`reregistration_cadastro_100_020`.

	O conteúdo dessas Tabelas são utilizados pelos processos de :doc:`reregistration_procedure_verification` de todas as Entidades de Cadastro, sendo reportadas todas as ocorrências de :bi:`Contact Informations` que não estejam consistentes com o conteúdo das duas Tabelas.

.. toctree::
   :maxdepth: 2
   :caption: Conteúdo:

   reregistration_cadastro_100_010
   reregistration_cadastro_100_020
