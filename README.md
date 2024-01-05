# Projeto-Streaming-KINESIS
Aplicações em Streaming KINESIS (em andamento)

# CONFIGURAÇÃO DO FLUXO DE DADOS - KINESIS

Para acessar o kinesis: ` https://aws.amazon.com/pt/kinesis/`

![1](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/408a7ef7-4ebf-4ee1-a70e-7709eeb0c9a0)

Primeiro passo é nomear o fluxo de dados. Deixei a capacidade sob demanda ativa. Ou seja, neste modo é uma forma que ele vai se adaptar conforme a demanda. Depois é so ir em baixo da página para criar, depois de criar ele vai estar disponível para que eu possa produzir dados. 

![2](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/7cbb20bf-1ade-4c9b-9c29-828a298fc45b)

# TRABALHANDO NO JUPYTER NOTEBOOK

Ao abrir o Jupyter Notebook, a primeira coisa que eu tenho que fazer é instalar o Boto 3

* Nomear o NoteBook como Produtor, pu seja, nesse notbook que vamos inserir os dados

```bash
!pip install boto3
```
Depois de instalar, eu preciso importar o Boto 3 e o Jason. Vou importar o Jason porque eu preciso analisar os dados nesse formato. No mesmo objeto eu vou criar um cliente do boto 3 tenho que passar as credenciais do Kinesis. 
```bash
Import boto3
Import Jason
cliente = boto3.cliente(‘kinesis’, aws_accesse_key_id=’chave’ ,aws_secret_ accesse_key= ‘chave secreta’
region_name=’us-east-1’)
```
Então a gente vai utilizar o método de Jason pro dump. A forma mais fácil de fazer isso é criar um objeto dicionário
```bash
registro = {‘ idvendedor’ : ‘999’, ‘nome’ : ‘Nelson’}
```
Para que eu possa produzir uma informação, eu tenho que chamar o método put record do meu cliente, que é um cliente do Kinesis, que vai autenticar lá na AWS, e o resultado deste método traz uma resposta, então posso fazer a leitura dessa resposta para saber se o processo foi bem sucedido.

```bash
resposta = cliente.put_record(
streamName = ‘stream1’, 
Data = jason.dumps(registro),
PartitionKey’02’
print (resposta)
```

![4](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/b267f48a-6c00-4af9-9e28-39f4ec2a5931)

# CRIANDO UM CONSUMIDOR

*  Abrir outro notebook para criar o consumidor. aqui aparecera em stream os dados inseridos pelo produtor.

```
Import boto3
cliente = boto3.cliente(‘kinesis’, aws_accesse_key_id=’chave’ ,aws_secret_ accesse_key= ‘chave secreta region_name=’us-east-1’)

shard = cliente.get_shard_interator(
           streamName=”stream1”,
           shardid = ‘shardid-000000000002’,
           shardIteratorType = ‘LATASTE’
           )[ “shardIterator”]

while shard is nor None:
  resultado = cliente.get_records(shardIterator=shard)
  registros = resultado [‘records’]
  shard = resultado[“NextShardIterator”]
  for registro in registros:
   print(registro[“SequenceNumber”])
   print(registro[“ApproximateArrivalTimestamp”])
   print(registro[“PartitionKey”])
   print(registro[“Data”])
```

# TESTE VENDEDOR E CONSUMIDOR

* Inserindo novo vendedor no Notbook Produtor

![5](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/10fba7cb-c818-4669-9313-5617fb908b9d)

* Dado recebido no Notbook Produtor

![6](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/dc1fe771-c262-463e-be4e-69b96704f33d)

# KINESES DELIVERY COM FIREHOUSE

Agora o objetivo e fazer a entrega dos dados em um bucket do S3. Então, não vou precisar codificar nada, só preciso criar um stream de entrega do firehouse e definir o bucket. 

Voltei lá na página do Kineses e fui na opção Delivery Stream.

![7](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/7a52db2b-a352-45df-afc9-fce95279a63c)

Agora ele pede para definir a origem e o destino, na origem (source) selecionei a opção Amazon Kinesis Data Streams. Ou seja, é o stream que já criei anteriormente e possuo um produtor pronto para ele. Como destino selecionei o Bucket do S3.

![8](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/e5fc660b-6a85-4bf7-9259-71121925d3a5)

Na opção abaixo o Choose Kinesis Data stream, selecionei o stream criado.

![9](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/4be095f4-86c1-40d2-83a0-c14ab1093261)



