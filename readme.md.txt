Integração e Armazenamento AWS
  Visão Geral

Este projeto demonstra duas arquiteturas distintas de integração e processamento de dados na AWS (Amazon Web Services), envolvendo serviços como S3, Lambda, RDS (PostgreSQL), EC2, EBS e Snapshots.

O objetivo é apresentar dois fluxos de trabalho para o armazenamento, processamento e backup de dados provenientes de um cliente externo, garantindo automação, escalabilidade e segurança.

☁️ Arquitetura 1 — Automação de Processamento com S3 e Lambda
🔹 Descrição

Nesta arquitetura, o cliente envia arquivos para um bucket do S3. Sempre que um novo arquivo é adicionado, um evento (Trigger) é acionado automaticamente, invocando uma função AWS Lambda.
A função Lambda processa o arquivo e insere os dados resultantes em um banco de dados RDS PostgreSQL.

🔹 Fluxo de Dados

O cliente envia arquivos para o S3 Bucket.

O S3 dispara um evento Trigger.

O evento aciona uma função Lambda, responsável pelo processamento.

A função Lambda conecta-se ao RDS PostgreSQL e grava os dados processados.

🔹 Benefícios

Totalmente serverless — não requer servidores dedicados.

Escalabilidade automática através do Lambda.

Baixo custo e manutenção mínima.

Ideal para processamento assíncrono de arquivos.

💻 Arquitetura 2 — Processamento Manual com EC2, EBS e Snapshots
🔹 Descrição

Nesta abordagem, o processamento ocorre em uma instância EC2, onde o cliente também envia os arquivos.
Os dados são manipulados localmente e armazenados em um RDS PostgreSQL.
Os volumes de dados da instância são mantidos em EBS (Elastic Block Store) e backups regulares são feitos como snapshots armazenados no S3.

🔹 Fluxo de Dados

O cliente envia arquivos para a instância EC2.

A instância EC2 processa os arquivos e os envia para o RDS PostgreSQL.

O volume EBS armazena temporariamente os dados durante o processamento.

São criados snapshots periódicos do EBS, salvos em um bucket S3.

🔹 Benefícios

Maior controle sobre o ambiente de execução.

Possibilidade de customização de configurações de hardware e software.

Backup automatizado com snapshots do EBS no S3.

Recomendado para workloads de processamento pesado.

⚙️Serviços AWS Utilizados  | Serviço	Função Principal
Amazon S3                   | Armazenamento de arquivos e snapshots
AWS Lambda                  | Processamento automático via eventos do S3
Amazon RDS                  | Banco de dados relacional
Amazon EC2                  | Computação sob demanda para processamento manual
Amazon EBS                  | Volume de armazenamento persistente para EC2
Amazon CloudWatch           | Monitoramento e logs de execução

🔒 Segurança e Boas Práticas

Utilizar IAM Roles com permissões mínimas necessárias para Lambda e EC2.

Habilitar criptografia (AES-256) nos buckets S3 e volumes EBS.

Configurar backup automatizado no RDS.

Restringir o acesso público aos buckets S3.

Utilizar VPCs privadas para o RDS e EC2.

🚀 Possíveis Extensões Futuras

Adicionar API Gateway para integração RESTful com Lambda.

Implementar SNS/SQS para filas de mensagens assíncronas.

Automatizar snapshots com AWS Backup.

Criar dashboards no CloudWatch para monitoramento em tempo real.

🧠 Conclusão

O projeto apresenta duas abordagens para integrar e processar dados utilizando serviços AWS.
A primeira arquitetura foca em automação e simplicidade (serverless), enquanto a segunda oferece maior controle e persistência de dados.

Ambas seguem boas práticas de segurança, escalabilidade e recuperação de dados, podendo ser aplicadas em diferentes cenários de negócio conforme a necessidade do sistema.essar, e após as validações é feito o drive para a EBS.  