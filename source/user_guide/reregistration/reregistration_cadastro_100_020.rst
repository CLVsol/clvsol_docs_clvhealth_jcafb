.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

.. index:: Contact Information Patterns

================================
**Contact Information Patterns**
================================

	A Tabela :bi:`Contact Information Patterns` serve como um repositório de :bi:`Address Names` permitidos na formação dos Endereços (:bi:`Contact Information`) de Pacientes e Residências. O conteúdo dessa Tabela é fundamental para a gestão dos nomes dos Endereços associados às Entidades de Cadastro, eliminando erros de digitação e/ou variações nos textos de definição de :bi:`Contact Information`.

	A inclusão de novos registros nessa Tabela deve ser feita sempre com bastante critério e atenção de forma a minimizar (ou até mesmo eliminar) a possibilidade do surgimento de variações de textos para identificação dos Endereços reais.

	A Tabela :bi:`Contact Information Patterns` é composta pelos quatro parâmetros a saber:

		* :bi:`Street`, correspondente ao parâmetro :bi:`Street Name` das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento dos Correios (CEP) o :bi:`Street` correponde ao campo **Logradouro** de um Endereço.

		* :bi:`Street Number`, correspondente ao parâmetro **Casa** das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento brasileiro o :bi:`Street Number` correponde ao campo **Número** de um Endereço.

		* :bi:`Street Number 2`, correspondente ao parâmetro **Porta** das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento brasileiro o :bi:`Street Number 2` correponde ao campo **Complemento** de um Endereço.

		* :bi:`Street 2`, correspondente ao parâmetro :bi:`District` das Informações de Contato de um Paciente ou Residência. No padrão de endereçamento dos Correios (CEP) o :bi:`Street 2` correponde ao campo **Bairro** de um Endereço.

	Embora a insersão de novos registros na Tabela :bi:`Contact Information Patterns` esteja habilitada, essa prática não é encorajada. Em geral, o mais comum é utilizar os mecanismos automáticos de inserção de registros a partir de registros de Cadastros de Pacientes ou Residências cujos Endereços (Informações de Contato) já tenham sido comprovados

	É importante observar que, embora a Tabela :bi:`Contact Information Patterns` compartilhe com a Tabela :bi:`Street Patterns` os campos :bi:`Street` e :bi:`Street 2`, não foi estabelecido qualquer vínculo em elas. Seus conteúdos são adminstrados e utilizados de forma totalmente independente.

	Até o momento não foi estabelecido ainda qualquer procedimento para o gerenciamento direto da Tabela :bi:`Contact Information Patterns`.

	O acesso à *view* :bi:`Contact Information Patterns` é alcançado utilizando o Menu:

    	* :bi:`Base` » :bi:`Configuration` » :bi:`Partner Entity` » :bi:`Contact Information Patterns`.

.. toctree::
   :maxdepth: 2
   :caption: Itens Relacionados:
