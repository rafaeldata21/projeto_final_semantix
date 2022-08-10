## Preparando Ambiente de Desenvolvimento do Projeto Final

- O desenvolvimento desta tarefa foi feita através dos conhecimentos adquiridos ao longo do Bootcamp. Serão apresentados abaixo as configurações/Links e aplicações utilizadas para alcançar o objetivo final.
---
### 1 – Primeira etapa: Instalação e configuração do Docker. 

[Docker Engine](https://docs.docker.com/engine/install/)

[Docker Compose](https://docs.docker.com/compose/install/)

[Tutorial de configuração]( https://github.com/rafaeldata21/projeto_final_semantix/blob/main/configura%C3%A7%C3%A3o_docker.md/)

---
### 2- Criação do diretório:

Com o comando `mkdir` criar o diretório `semantix/pjfinal` e dentro do diretório criado, montar outro com o nome `cluster-big-data` dentro do terminal.

`~/semantrix/pjfinal`

`~/semantix/pjfinal/cluster-big-data`

----

### 3- Clonar o diretório e baixar o Elastic

Como disponibilizado no curso, deve ser clonado e utilizado o git abaixo:
Obs: Realizar o comando dentro do diretório criado anteriormente. Os arquivos clonados com final `.yml` deverão ser movidos para a pasta `cluster-big-data`
`git clone https://github.com/rodrigo-reboucas/docker-bigdata.git`


Dentro do diretório `~/semantix/pjfinal`, realizar o clone

**NOTA: Para que o Docker-Compose baixado pelo Elastic execute todos os containers, é importante adicionar as informações existentes dentro do arquivo Docker-compose.yml dentro da pasta cluster-big-data. Desta forma quando executar o comando Docker-compose pull ele baixará todas as imagens necessárias para esse projeto. **

Estrutura do diretório

```~>/semantix/pjfinal
|-- cluster-big-data
|-- data
	-- hadoop  
	-- hbase  
	-- hdfs  
	-- hue  
	-- jupyter  
	-- kafka  
	-- metabase  
	-- mongo  
	-- mysql  
	-- nifi  
	-- notebooks  
	-- postgresql  
	-- util  
	-- zookeeper  
|-- input
|-- pipeline
    -- logstash.conf    
|-- settings
    -- elasticsearch.yml    
    -- kibana.yml    
    -- logstash.yml    
|-- docker-compose.yml
```

---

### 4. Configurar o vm.max_map_count com no mínimo 262144

Para realizar essa configuração, seguir as seguintes etapas:

- Digitar o comando `sudo vi /etc/sysctl.conf`

- `i` # para inserir

- `CTRL+END` # ir para o final

- `vm.max_map_count=262144` # colar esse parâmetro

- `ESC` # para sair

- `:wq!` # para salvar e sair

No terminal, usar o comando `grep vm.max_map_count /etc/sysctl.conf` para verificar se funcionou.

**Nota: É necessário utilizar o comando ‘sudo sysctl -w vm.max_map_count=262144’ ao iniciar o cluster para que o container (elastic) permaneça ativo.**

----

### 5. Baixar as imagens
`docker-compose pull`

### 6. Iniciar todos os serviços
`docker-compose up -d`

----

### 7. Configurar o jar do spark
Serão necessárias duas configurações adicionais: uma para para aceitar o formato parquet em tabelas Hive e outra de conexão com elastic. Os links para downlod dos arquivos .jar estão apresentados abaixo:
- Parquet

`curl -O https://repo1.maven.org/maven2/com/twitter/parquet-hadoop-bundle/1.6.0/parquet-hadoop-bundle-1.6.0.jar`

`docker cp parquet-hadoop-bundle-1.6.0.jar jupyter-spark:/opt/spark/jars`

- Elastic

`curl -O https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-hadoop/7.9.2/elasticsearch-hadoop-7.9.2.jar`

`docker cp elasticsearch-hadoop-7.9.2.jar jupyter-spark:/opt/spark/jars`

### 8. Aquisição dos dados

Criar uma pasta denominada dados dentro da pasta input. Dentro da pasta dados realizar os seguintes comandos:

`sudo curl -O https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar`

`sudo unrar x 04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar`

- Se necessário, instalar um descompactador de arquivo: `sudo apt-get install unrar` e executar o seguinte comando: `sudo unrar x <nomedoarquivo>.rar`
- 
### 9. Enviar arquivos para o HDFS

Para acessar o `namenode`, utilizar o comando `docker exec -it namenode bash`. Criar um diretório denominado covid, verificar a criação da pasta e enviar os arquivos obtidos na etapa anterior:

`hdfs dfs -mkdir -p /user/rafaelsantos/covid`

`hdfs dfs -ls -R /user`

`hdfs dfs -put /input/dados/*.csv /user/rafaelsantos/covid`





