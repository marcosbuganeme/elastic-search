
# Docker Compose for Elasticsearch and Kibana

Este guia oferece instruções passo a passo para configurar e executar o Elasticsearch e o Kibana usando Docker Compose.

## Pré-requisitos

Antes de começar, você precisa ter o Docker e o Docker Compose instalados em sua máquina. Se você ainda não tem esses softwares instalados, siga os links abaixo para instalar:

- [Instalar Docker](https://docs.docker.com/get-docker/)
- [Instalar Docker Compose](https://docs.docker.com/compose/install/)

## Configuração

1. **Clonar/Download do Repositório**

   Clone ou faça o download deste repositório para sua máquina local.

2. **Arquivo Docker Compose**

   Navegue até o diretório onde você salvou o arquivo `docker-compose.yml`.

3. **Iniciando os Serviços**

   Abra um terminal e execute o seguinte comando para iniciar todos os serviços definidos no arquivo Docker Compose:

   ```bash
   docker-compose up
   ```

   Se desejar executar em background (modo daemon), use:

   ```bash
   docker-compose up -d
   ```

4. **Acessando o Kibana**

   Após iniciar os serviços, o Kibana estará disponível em `http://localhost:5601`. Abra seu navegador e acesse essa URL para começar a usar o Kibana.

## Gerenciamento

### Visualizar Logs

Para visualizar os logs de qualquer serviço, você pode usar o seguinte comando:

```bash
docker-compose logs -f [serviço]
```

Substitua `[serviço]` pelo nome do serviço que você deseja visualizar, por exemplo, `elasticsearch` ou `kibana`.

### Parando os Serviços

Para parar os serviços, você pode usar:

```bash
docker-compose down
```

Este comando também remove os contêineres criados, redes padrão, mas mantém seus dados.

### Removendo Dados

Se você deseja remover todos os dados persistentes, você pode remover os volumes associados com:

```bash
docker-compose down -v
```

## Suporte

Se você encontrar problemas ou tiver perguntas sobre a configuração, sinta-se à vontade para criar um issue no repositório ou consultar a documentação oficial do Elasticsearch e Kibana.
