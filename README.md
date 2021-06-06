# Gestão de investimentos
## Motivação
Se você investe em renda variável, como **Fundos de Investimento Imobiliários (FIIs) e ações**, você já perdeu uma parte do seu precioso tempo fazendo o seguinte:
- Juntando notas de corretagem; 
- Identificando taxa de liquidação, emolumentos e imposto retido;
- Calculando preço médio;
- Apurando resultado mensal;
- Calculando proventos, dividendos e juros sobre capital próprio recebidos;
- Avaliando, em caso de lucro, se esse resultado é tributável ou isento; e
- Levantando informações para preencher a declaração anual de imposto de renda.

Nesse último caso, diferentemente da renda fixa, em que é só transcrever o informe de rendimentos para a declaração, na renda variável as corretoras não informam para você o seu preço médio por ativo, o imposto retido e o seu resultado mensal. Isso compete a você e requer organização, pois inconsistências nessas informações podem acarretar problemas com a Receita.

Assim, esse sistema visa te ajudar nessa tarefa de organização para estar em dias com o fisco, além de disponibilizar informações para melhor gerir a sua carteira de investimentos e o fluxo de caixa dela decorrente.

Ele provê as seguintes funcionalidades:
- **Investimentos**: cadastro e consulta de administradoras, segmentos, classe de ativos, produtos financeiros, operações de compra e venda, carteira e proventos;
- **Financeiro**: cadastro e consulta de bancos, agências, contas, códigos de movimentação e movimentações financeiras.

## Tecnologias utilizadas
O sistema Gestão de Investimentos utiliza as seguintes tecnologias:


![docker](https://user-images.githubusercontent.com/56877733/120907322-ca547b80-c636-11eb-9c9a-20c33bad3521.png)
![postgresql](https://user-images.githubusercontent.com/56877733/120907332-dd674b80-c636-11eb-8391-b84e8d25f87c.png)
![python](https://user-images.githubusercontent.com/56877733/120907339-eb1cd100-c636-11eb-8ff8-4a976b1ab2d1.jpeg)
![django](https://user-images.githubusercontent.com/56877733/120907343-f53ecf80-c636-11eb-8336-6bee57ac85c2.png)
![django rest](https://user-images.githubusercontent.com/56877733/120907350-fec83780-c636-11eb-90ef-7ac1d8458339.png)

A fim de prover mais informações e funcionalidades ao menor custo de desenvolvimento possível, foi utilizada a interface administrativa disponibilizada pelo Django, onde, a partir da qual, utilizamos os seguintes recursos built-in:
- Gestão de usuários e permissões;
- Criação de tabelas de bancos de dados com as seguintes funcionalidades: chaves estrangeiras compostas, atributos sem repetição de valor, verbose_name_plural e tabelas da app vinculadas ao schema correspondente do banco;
- Criação de formulários com as seguintes funcionalidades: list_display, list_filter, search_fields, autocomplete_fields, readonly_fields, raw_id_fields, fieldsets e inlines;
- Criação de urls para chamada de métodos da API que exportam dados via arquivo *.csv;
- Criação de signals onde um evento em uma tabela gera ações em outras tabelas a partir de uma regra de negócio.

## Uso do sistema
Antes de instalar, veja como o sistema funciona. Para tal, acesse XXXXXX e forneça as seguintes credenciais:
- Usuário
- Senha

Lembramos que no endereço fornecido, o sistema apenas disponibiliza o cadastro de movimentação financera, a compra e a venda de ativos e o recebimento de proventos. Já os demais itens, apenas para consulta. 

Esteja você acessando o sistema na sua máquina ou no servidor, para uma melhor experiência, busque seguir o roteiro listado abaixo:
- **Financeiro**:
   - Cadastre/consulte o banco, agência e conta;
   - Importe/consulte os códigos de movimentação;
   - Faça depósitos e/ou retiradas da movimentação da conta. Teste os filtros e o campo de busca;
   - Consulte o formulário de contas e verifique que o saldo vai sendo atualizado.
- **Investimentos**:
   - Cadastre/consulte: tipos de rentabilidade, tipos de provento, tipos de mandato, tipos de gestão, segmentos e classes de ativo;
   - Cadastre/consulte as administradoras dos ativos que você venha a operar;
   - Cadastre/consulte os produtos financeiros (ativos) que você venha a operar;
      - Para obter os dados exigidos no cadastro, consulte os informes mensais do FII na [B3](http://www.b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel/fundos-de-investimentos/fii/fiis-listados/);
      - Essa é uma alternativa para avaliar a saúde financeiro do FII. [Exemplo de informe](https://fnet.bmfbovespa.com.br/fnet/publico/visualizarDocumento?id=176594).


## Estrutura de diretórios
``` 
GestaoInvestimentos
|___aplicacao
    |___back-end
        |___install-packages.sh
        |___.env
        |___requirements.txt
        |___manage.py
        |___app_x
    |___docker-compose.yml
    |___Dockerfile
    |___.env.postgres
|___documentacao

``` 
## Instalação - ambiente Linux
1. **Docker**: 
   - Logue como super-usuário: `sudo su`
   - Verifique se existe alguma versão do Docker instalada: `service docker.io status`
   - Verifique se o kernel do Linux é >= 3.8 e 64 bits: `uname -a`
   - Atualize os índices de repositórios de pacote: `apt-get update`
   - Instale o Docker: `apt-get install -y docker.io`
   - Verifique o Docker foi instalado: `docker info`
   - Adicione o seu usuário ao grupo Docker para não precisar sempre executar como sudo: `sudo gpasswd -a seu_usuario docker`
      - Efetue logoff para atualizar as permissões.
   - Instale o docker-compose: [roteiro](https://docs.docker.com/compose/install/);
   - Verifique se o docker-compose foi instalado: `docker-compose --version`

2. **Banco de dados**:
   - Acesse o diretório aplicacao e execute:
      - `docker exec -it banco bash`
      - `psql -h localhost -U administrador gest-investimentos`
      - `CREATE SCHEMA investimentos AUTHORIZATION administrador;`
      - `CREATE SCHEMA financeiro AUTHORIZATION administrador;`
      - Verifique os schemas criados: `\dn`
      - `exit`
      - `exit`
      - `docker exec -it django bash`
      - `python manage.py makemigrations`
      - `python manage.py migrate`
      - Crie o super usuário e a senha: `python manage.py createsuperuser`
      - `exit`
