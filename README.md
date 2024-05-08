
# Docker Compose for Elasticsearch and Kibana

Este guia oferece instruções passo a passo para configurar e executar o Elasticsearch e o Kibana usando Docker Compose.

## Pré-requisitos

Antes de começar, você precisa ter o Docker e o Docker Compose instalados em sua máquina. Se você ainda não tem esses softwares instalados, siga os links abaixo para instalar:

- [Instalar Docker](https://docs.docker.com/get-docker/)
- [Instalar Docker Compose](https://docs.docker.com/compose/install/)
- [Instalar OpenSSL](https://www.openssl.org/)

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

#### Certificados SSL

Para gerar certificados SSL (.crt) e chaves privadas (.key) você pode usar ferramentas como OpenSSL, que é amplamente utilizada para criar certificados autoassinados e chaves.

Aqui está um guia passo a passo para gerar um certificado e uma chave usando OpenSSL:

#### Passo 1: Instalar o OpenSSL

###### Debian/Ubuntu

`sudo apt-get install openssl`

###### RedHat/Fedora

`sudo yum install openssl`

###### macOS (geralmente já vem instalado)

`brew install  openssl`

#### Passo 2: Gerar a Chave Privada

Gere uma chave privada RSA de 2048 bits

`openssl genrsa -out key.key 2048`

Este comando gera uma chave privada RSA e salva no arquivo `elasticsearch.key`.

Nome "elasticsearch" é apenas sugestivo.

#### Passo 3: Gerar a Solicitação de Assinatura de Certificado (CSR)

Com a chave privada, crie uma CSR (Certificate Signing Request).

Durante a criação da CSR, você será solicitado a inserir informações que serão incorporadas ao seu certificado:

`openssl req -new -key key.key -out elasticsearch.csr`

Você precisa fornecer detalhes como país, estado, localidade, nome da organização, nome comum (o nome de domínio do certificado) e email. Preencha conforme necessário para seu caso de uso.

Novamente, o nome "elasticsearch" é apenas sugestivo.

#### Passo 4: Gerar o Certificado Autoassinado

Usando a CSR e a chave privada, gere o certificado autoassinado:

`openssl x509 -req -days 365 -in elasticsearch.csr -signkey elasticsearch.key -out elasticsearch.crt`

Este comando cria um certificado (elasticsearch.crt) que é válido por 365 dias.

Novamente, tanto o nome e o número de dias pode ser ajustado conforme necessário.

#### Passo 5: Verificar o Certificado

`openssl x509 -in elasticsearch.crt -text -noout`

Este comando exibe as informações do certificado, incluindo a validade, a quem foi emitido, o emissor, etc.

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
