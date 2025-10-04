# 📊 Desafio 3 - Integração Power BI com MySQL no Azure

## 📝 Descrição do Desafio
O objetivo deste projeto é criar uma **instância no Azure para MySQL**, integrar os dados com o **Power BI**, realizar a **transformação de dados** e preparar a base para análises futuras.  

As etapas incluem:
1. Criação de uma instância no **Azure para MySQL**.  
2. Criação do **banco de dados** com base disponibilizada no GitHub.  
3. Integração do **Power BI com MySQL no Azure**.  
4. Verificação e transformação da base de dados para análise.

---

## 🔹 Diretrizes de Transformação de Dados

1. Verificar **cabeçalhos e tipos de dados**.  
2. Converter valores monetários para **tipo double preciso**.  
3. Identificar e tratar **valores nulos**.  
4. Analisar colaboradores (`employees`) com **nulo em `Super_ssn`**, que podem ser gerentes, e verificar se algum colaborador não possui gerente.  
5. Verificar se algum **departamento não possui gerente**.  
6. Preencher lacunas de departamentos sem gerente, caso existam.  
7. Verificar o **número de horas** nos projetos.  
8. Separar **colunas complexas**.  
9. Mesclar as tabelas **employee** e **department** para criar uma tabela final de **employees** com o nome do departamento associado (base da mescla: tabela employee).  
10. Eliminar **colunas desnecessárias** durante o processo.  
11. Mesclar colaboradores com **nomes dos gerentes** (pode ser via SQL ou Power BI). Caso utilize SQL, incluir a query neste README.  
12. Mesclar colunas de **Nome e Sobrenome** em uma única coluna para os colaboradores.  
13. Mesclar **nomes de departamentos e localizações** para que cada combinação seja única, facilitando a criação de um **modelo estrela** no futuro.  

---

## 🚀 Entregável
- Banco de dados MySQL criado no **Azure**.  
- Base de dados transformada e integrada ao **Power BI Desktop**.  
- Tabelas preparadas para análises futuras com estrutura limpa e consistente.  

---

## 🛠️ Ferramentas Utilizadas
- **Microsoft Azure** (MySQL)  
- **Power BI Desktop**  
- **SQL** para manipulação e junção de dados (quando necessário)  
- Transformações via **Power Query**  

---

## 📌 Objetivo do Projeto
- Integrar **Power BI com base remota MySQL no Azure**.  
- Transformar dados brutos em informações **estruturadas e consistentes**.  
- Criar uma **base limpa e preparada** para análises avançadas e modelos de BI futuros.  

---

## 💻 Query SQL (Exemplo)
Caso tenha realizado junção dos colaboradores com nomes dos gerentes via SQL:

```sql
SELECT e.Employee_id,
       CONCAT(e.First_name, ' ', e.Last_name) AS Employee_Name,
       d.Department_name,
       d.Location,
       m.Employee_id AS Manager_ID,
       CONCAT(m.First_name, ' ', m.Last_name) AS Manager_Name
FROM Employee e
LEFT JOIN Employee m ON e.Super_ssn = m.Ssn
LEFT JOIN Department d ON e.Department_id = d.Department_id;

