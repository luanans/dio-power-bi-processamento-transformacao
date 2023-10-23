**Desafio Módulo 3 - Processamento de Dados Simplificado com Power BI**

## Primeiros Passos

1. Crie uma instância na Azure para o MySQL.
2. Utilize o bash na Azure para criar o Banco de dados com base nos arquivos `script_bd_company.sql` e `insercao_de_dados_e_queries_sql.sql` disponíveis no GitHub.
3. Integre o Power BI com o MySQL na Azure.
4. Verifique e corrija possíveis problemas na base de dados para facilitar a transformação dos dados.

## Diretrizes para Transformação dos Dados

1. Verificação de Cabeçalhos e Tipos de Dados:

    Ambos estavam corretos.

2. Modificação dos Valores Monetários para Tipo Double Preciso:

    As colunas `emp_salary` na tabela `employee` e `works_on_hours` na tabela `works_on` foram alteradas para o tipo double preciso.

3. Verificação e Remoção de Valores Nulos:

    Na tabela `employee`, foram identificados e removidos 1 nulo em cada uma das colunas `emp_ssn` e `emp_super_ssn`.

4. Identificação de Colaboradores sem Gerente:

    Apenas um colaborador tinha o campo `super_ssn` nulo. John Smith é o gerente do departamento 5.

5. Verificação de Departamentos sem Gerente:

    Não foram encontrados departamentos sem gerente na tabela `departament`.

6. Preenchimento de Lacunas em Departamentos sem Gerente:

    Não foi necessário realizar preenchimentos.

7. Verificação do Número de Horas dos Projetos:

    O projeto "ProductZ" possui o maior número de horas, totalizando 40.

    | project_name    | total_hours |
    | --------------- | ----------- |
    | ProductX        | 39.5        |
    | ProductY        | 7.5         |
    | ProductZ        | 40.0        |
    | Computerization | 20.0        |
    | Reorganization  | 10.0        |
    | Newbenefits     | 30.0        |

8. Separação de Colunas Complexas:

    As colunas complexas `emp_address` e `dept_location` foram divididas em `city`, `state` e `number`.

9. Mesclagem de Consultas para Associar Colaboradores a Departamentos:

    Foi realizada uma mesclagem entre as tabelas `employee` e `departament` usando uma junção externa esquerda. A nova tabela criada contém o nome do departamento associado a cada colaborador.

10. Eliminação de Colunas Desnecessárias:

    Foram removidas as colunas `emp_dept_id` (já contida em `dept_name`) e `emp_super_ssn` (não necessária para o SSN do gerente).

11. Junção de Colaboradores e Nomes dos Gerentes:

    Foi feita uma seleção da tabela "employee" e realizada uma mesclagem consigo mesma usando as colunas `super_ssn` na primeira instância e `ssn` na segunda como chaves de ligação. A junção foi do tipo "Externa Esquerda".

12. Fusão de Nomes e Sobrenomes:

    As colunas de nome e sobrenome foram combinadas usando um underscore como separador.

13. Fusão de Nomes de Departamentos e Localizações:

    A tabela "Departament" foi mesclada com a tabela "dept_location", usando as colunas "Dnumber" como chaves de ligação. A junção foi do tipo "Externa Esquerda". A nova tabela resultante contém o nome da localização. Em seguida, as colunas "Dlocation" e "Dname" foram combinadas com um espaço como separador.

14. Explicação sobre o Uso de Mesclar em Vez de Atribuir:

    No caso em questão, a mesclagem é utilizada em vez de atribuir porque estamos criando uma nova coluna com base em duas colunas existentes. Ao atribuir, estaríamos substituindo uma das colunas existentes.

15. Agrupamento de Dados por Gerente:

    Foram agrupados os dados para contar quantos colaboradores estão associados a cada gerente.

    | manager_name     | total_employees |
    | ---------------- | --------------- |
    | John Smith       | 2               |
    | Franklin Wong    | 1               |
    | Alicia Zelaya    | 1               |
    | Jennifer Wallace | 1               |
    | Ramesh Narayan   | 1               |

16. Eliminação de Colunas Desnecessárias:

    Não foram eliminadas colunas desnecessárias das tabelas.
