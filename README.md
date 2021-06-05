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

Assim, essa aplicação visa te ajudar nessa tarefa de organização para estar em dias com o fisco, além de disponibilizar informações para melhor gerir a sua carteira de investimentos e o fluxo de caixa dela decorrente.

Ela provê as seguintes funcionalidades:
- **Investimentos**: cadastro e consulta de administradoras, segmentos, classe de ativos, produtos financeiros, operações de compra e venda, carteira e proventos;
- **Financeiro**: cadastro e consulta de bancos, agências, contas, códigos de movimentação e movimentações financeiras.

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
