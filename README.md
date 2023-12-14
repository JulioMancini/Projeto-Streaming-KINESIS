# Projeto-Streaming-KINESIS
Aplicações em Streaming KINESIS (em andamento)

# CONFIGURAÇÃO DO FLUXO DE DADOS - KINESIS

Para acessar o kinesis: ` https://aws.amazon.com/pt/kinesis/`

![1](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/408a7ef7-4ebf-4ee1-a70e-7709eeb0c9a0)

Primeiro passo é nomear o fluxo de dados. Deixei a capacidade sob demanda ativa. Ou seja, neste modo é uma forma que ele vai se adaptar conforme a demanda. Depois é so ir em baixo da página para criar, depois de criar ele vai estar disponível para que eu possa produzir dados. 

![2](https://github.com/JulioMancini/Projeto-Streaming-KINESIS/assets/145502330/7cbb20bf-1ade-4c9b-9c29-828a298fc45b)

# TRABALHANDO NO JUPYTER NOTEBOOK

Ao abrir o Jupyter Notebook, a primeira coisa que eu tenho que fazer é instalar o Boto 3

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

