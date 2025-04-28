# Exercícios

## Exercício 1

### Exercício 1.1

``` bash
db.client.insertMany([
{
  "full_name": "Maria Silva",
  "cpf": "12345678901",
  "email": "maria.silva@email.com",
  "phone": "11987654321",
  "address": "Rua das Flores, 123",
  "city": "São Paulo",
  "state": "SP",
  "zip_code": "01001000",
  "created_by": "user_id_do_admin_1",
  "enterprise": null,
  "cnpj_enterprise": null,
  "description": "Cliente individual"
},
{
  "full_name": "Empresa Soluções Ltda",
  "cpf": null,
  "email": "contato@solucoes.com.br",
  "phone": "21998765432",
  "address": "Avenida Principal, 456",
  "city": "Rio de Janeiro",
  "state": "RJ",
  "zip_code": "20010020",
  "created_by": "user_id_do_manager_2",
  "enterprise": "Soluções Ltda",
  "cnpj_enterprise": "12345678000190",
  "description": "Cliente corporativo"
}]);
```
### 1.2

``` bash
db.client_processes.insertMany([
{
  "client_id": "id_do_cliente_maria_silva",
  "number": "PROC-2023-001",
  "value": 1500.00,
  "status": "ativo",
  "class": "Cobrança",
  "description": "Processo de cobrança referente a fatura em aberto.",
  "created_at": ISODate("2023-10-26T10:00:00Z")
},
{
  "client_id": "id_do_cliente_empresa_solucoes",
  "number": "PROC-2023-002",
  "value": 5500.50,
  "status": "em análise",
  "class": "Contratual",
  "description": "Análise de contrato de prestação de serviços.",
  "created_at": ISODate("2023-11-15T14:30:00Z")
}]);
```

### 1.3

``` bash
db.events.insertMany([
{
  "client_id": "id_do_cliente_maria_silva",
  "enterprise": null,
  "cnpj_enterprise": null,
  "freight": 50.00,
  "amount_of_cleaning": 2,
  "cleaning_date": "2023-12-10",
  "cost_of_each_cleanin": 200.00,
  "proposal_doc": "PROP-MS-001.pdf",
  "number_proposal": "PROP-2023-001-MS",
  "proposal_expiration_date": ISODate("2023-11-30T23:59:59Z"),
  "created_proposal_by": "user_id_do_sales_3",
  "address": "Rua das Camélias, 789",
  "city": "São Paulo",
  "state": "SP",
  "zip_code": "02002000",
  "proposal_status": "accepted"
},
{
  "client_id": "id_do_cliente_empresa_solucoes",
  "enterprise": "Soluções Ltda",
  "cnpj_enterprise": "12345678000190",
  "freight": 120.00,
  "amount_of_cleaning": 5,
  "cleaning_date": "2024-01-15",
  "cost_of_each_cleanin": 150.00,
  "proposal_doc": "PROP-ESL-002.pdf",
  "number_proposal": "PROP-2023-002-ESL",
  "proposal_expiration_date": ISODate("2023-12-20T23:59:59Z"),
  "created_proposal_by": "user_id_do_sales_3",
  "address": "Avenida das Palmeiras, 1011",
  "city": "Rio de Janeiro",
  "state": "RJ",
  "zip_code": "22020030",
  "proposal_status": "pending accepted"
}]);
```

## Exercício 2

### 2.1
``` bash
db.client.find({city: "São Paulo"});
```

Resposta:
{
  "full_name": "Maria Silva",
  "cpf": "12345678901",
  "email": "maria.silva@email.com",
  "phone": "11987654321",
  "address": "Rua das Flores, 123",
  "city": "São Paulo",
  "state": "SP",
  "zip_code": "01001000",
  "created_by": "user_id_do_admin_1",
  "enterprise": null,
  "cnpj_enterprise": null,
  "description": "Cliente individual"
}

### 2.2

``` bash
db.client_processes.find({value: {$gt: 2000}});
```

Resposta:
{
  "client_id": "id_do_cliente_empresa_solucoes",
  "number": "PROC-2023-002",
  "value": 5500.50,
  "status": "em análise",
  "class": "Contratual",
  "description": "Análise de contrato de prestação de serviços.",
  "created_at": ISODate("2023-11-15T14:30:00Z")
}

### 2.3

``` bash
db.event.find({proposal_status: {$in: ["pending accepted", "accepted"]}});
```

Resposta:
{
  "client_id": "id_do_cliente_maria_silva",
  "enterprise": null,
  "cnpj_enterprise": null,
  "freight": 50.00,
  "amount_of_cleaning": 2,
  "cleaning_date": "2023-12-10",
  "cost_of_each_cleanin": 200.00,
  "proposal_doc": "PROP-MS-001.pdf",
  "number_proposal": "PROP-2023-001-MS",
  "proposal_expiration_date": ISODate("2023-11-30T23:59:59Z"),
  "created_proposal_by": "user_id_do_sales_3",
  "address": "Rua das Camélias, 789",
  "city": "São Paulo",
  "state": "SP",
  "zip_code": "02002000",
  "proposal_status": "accepted"
},
{
  "client_id": "id_do_cliente_empresa_solucoes",
  "enterprise": "Soluções Ltda",
  "cnpj_enterprise": "12345678000190",
  "freight": 120.00,
  "amount_of_cleaning": 5,
  "cleaning_date": "2024-01-15",
  "cost_of_each_cleanin": 150.00,
  "proposal_doc": "PROP-ESL-002.pdf",
  "number_proposal": "PROP-2023-002-ESL",
  "proposal_expiration_date": ISODate("2023-12-20T23:59:59Z"),
  "created_proposal_by": "user_id_do_sales_3",
  "address": "Avenida das Palmeiras, 1011",
  "city": "Rio de Janeiro",
  "state": "RJ",
  "zip_code": "22020030",
  "proposal_status": "pending accepted"
},

### 2.4

``` bash
db.client.find(
    { enterprise: { $ne: null } },
    { full_name: 1, cnpj_enterprise: 1, _id: 0 }
);
```

Resposta:

{
  "full_name": "Empresa Soluções Ltda",
  "cnpj_enterprise": "12345678000190",
}

### 2.5

``` bash
db.client_processes.find(
    { class: "Cobrança" }
).sort(
    { valor: -1 }
);

```

Resposta:
{
  "client_id": "id_do_cliente_maria_silva",
  "number": "PROC-2023-001",
  "value": 1500.00,
  "status": "ativo",
  "class": "Cobrança",
  "description": "Processo de cobrança referente a fatura em aberto.",
  "created_at": ISODate("2023-10-26T10:00:00Z")
}

## Exercício 3

### 3.1

``` bash
db.client_processes.updateOne(
    { number: "PROC-2023-001" },
    { $set: { status: "concluído" } } 
);
```

### 3.2

``` bash
db.event.updateOne(
    { nome: "Maria Silva" }, 
    { $set: { note_doc: "OBS-MS-001.txt" } } 
);
```

### 3.3

```bash
db.events.updateOne(
    { empresa: "Soluções Ltda" }, 
    { $inc: { amount_of_cleaning: 1 } }
);
```

## Exercício 4

### 4.1

```bash
db.client_processes.deleteOne(
    { number: "PROC-2023-002" } 
);
```

### 4.2

```bash
db.client.deleteMany(
    { cnpj_enterprise: null }
);
```

## Exercício 5

### 5.1

```bash
db.client.createIndex(
    { full_name: 1 }
);
```

### 5.2

```bash
db.client.getIndexes();

```
