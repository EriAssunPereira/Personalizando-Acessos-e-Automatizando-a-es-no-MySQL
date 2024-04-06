# Personalizando-Acessos-e-Automatizando-a-es-no-MySQL
**Personalização de Acessos e Gatilhos para Cenário de E-Commerce**

---

## Parte 1: Personalizando Acessos com Views

Neste desafio, vamos criar visões (ou views) para os seguintes cenários:

1. **Número de Empregados por Departamento e Localidade**
   - Essa visão mostrará quantos empregados existem em cada departamento e localidade.

2. **Lista de Departamentos e Seus Gerentes**
   - Aqui, exibiremos uma lista dos departamentos juntamente com os nomes de seus gerentes.

3. **Projetos com Maior Número de Empregados (Ordenação Descendente)**
   - Essa visão apresentará os projetos com o maior número de empregados, ordenados de forma descendente.

4. **Lista de Projetos, Departamentos e Gerentes**
   - Mostraremos uma lista que inclui informações sobre projetos, seus respectivos departamentos e os gerentes associados.

5. **Empregados com Dependentes que Também São Gerentes**
   - Essa visão identificará quais empregados possuem dependentes e se eles também ocupam cargos de gerência.

Além disso, definiremos permissões de acesso às views de acordo com o tipo de conta de usuário. Lembre-se de que as views são armazenadas no banco de dados como "tabelas", permitindo que definamos permissões de acesso específicas a esses itens.

Para ilustrar, vamos criar um usuário chamado "gerente" que terá acesso às informações de empregados e departamentos. No entanto, os empregados não terão acesso às informações relacionadas aos departamentos ou gerentes.

Exemplo de criação de usuário e definição de permissões:

```sql
-- Criação do usuário "gerente"
CREATE USER 'gerente'@'localhost' IDENTIFIED BY 'senha_gerente';

-- Concedendo permissões para visualizar as views de empregados e departamentos
GRANT SELECT ON nome_do_banco_de_dados.view_empregados TO 'gerente'@'localhost';
GRANT SELECT ON nome_do_banco_de_dados.view_departamentos TO 'gerente'@'localhost';
```

Lembre-se de adaptar o código acima ao seu ambiente específico e ao nome do banco de dados que você está utilizando.

---

## Parte 2: Criando Gatilhos para Cenário de E-Commerce

### Objetivo

A criação de triggers está associada a ações que podem ser executadas antes ou depois da inserção ou atualização de dados. Além disso, em casos de remoção, também podemos utilizar triggers. Vamos criar as seguintes triggers para o cenário de e-commerce:

1. **Triggers de Remoção (Before Delete)**
   - Essas triggers serão acionadas antes da remoção de registros.

2. **Triggers de Atualização (Before Update)**
   - Essas triggers serão acionadas antes da atualização de registros.

### Exemplo de Trigger para Base

```sql
-- Trigger para remoção (before delete)
DELIMITER //
CREATE TRIGGER before_delete_usuario
BEFORE DELETE ON usuarios
FOR EACH ROW
BEGIN
    -- Realize as ações necessárias antes da remoção do usuário
    -- Por exemplo, fazer backup dos dados ou registrar a exclusão
END;
//
DELIMITER ;

-- Trigger para atualização (before update)
DELIMITER //
CREATE TRIGGER before_update_colaborador
BEFORE UPDATE ON colaboradores
FOR EACH ROW
BEGIN
    -- Realize as ações necessárias antes da atualização do colaborador
    -- Por exemplo, verificar se o salário está dentro de limites aceitáveis
END;
//
DELIMITER ;
```

Lembre-se de adaptar o código acima às suas tabelas e necessidades específicas no cenário de e-commerce.
