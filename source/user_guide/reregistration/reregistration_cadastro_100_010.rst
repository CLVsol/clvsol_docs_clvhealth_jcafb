.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Street Patterns

===================
**Street Patterns**
===================

	A Tabela :bi:`Street Patterns` serve como um repositório de nomes de **Logradouros** (classificados por **Bairros**) permitidos na formação dos Endereços (:bi:`Contact Information`) de Pacientes e Residências. O conteúdo dessa Tabela é fundamental para a padronização de nomes de Logradouros por Bairros, eliminando erros de digitação e/ou variações nos textos de definição de :bi:`Contact Information`.

	A inclusão de novos registros nessa Tabela deve ser feita sempre com bastante critério e atenção de forma a minimizar (ou até mesmo eliminar) a possibilidade do surgimento de variações de textos para identificação de um mesmo Endereço real.

	A Tabela :bi:`Street Patterns` é composta pelos dois parâmetros a saber:

		* :bi:`Street`, correspondente ao parâmetro :bi:`Street Name` das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento dos Correios (CEP) o :bi:`Street` correponde ao campo **Logradouro** de um Endereço.

		* :bi:`Street 2`, correspondente ao parâmetro :bi:`District` das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento dos Correios (CEP) o :bi:`Street 2` correponde ao campo **Bairro** de um Endereço.

	Embora a insersão de novos registros na Tabela :bi:`Street Patterns` esteja habilitada, essa prática não é encorajada. Em geral, o mais comum é utilizar os mecanismos automáticos de inserção de registros a partir de registros de Cadastros de Pacientes ou Residências cujos Endereços (Informações de Contato) já tenham sido comprovados.

	No entanto, caso exista a possibilidade de se efetuar, com antecedência, o mapeamento dos Logradouros de uma nova comunidade no início de um ciclo da JCAFB, a insersão direta de novos registros na Tabela é encorajada e a utilização dos mecanismos automáticos de inserção de registros desencorajada. Esta conduta resultará em um melhor controle do processo de Cadastramento dos novos Pacientes, possibilitando a eliminação  erros de digitação e/ou variações nos textos de definição de :bi:`Contact Information`.

	Até o momento não foi estabelecido ainda qualquer procedimento para o gerenciamento direto da Tabela :bi:`Street Patterns`.

	O acesso à *view* :bi:`Street Patterns` é alcançado utilizando o Menu:

    	* :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Street Patterns`.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
