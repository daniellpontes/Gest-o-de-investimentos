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
