# move-tech-cloud-application-comp-4

Ponto de partida da **Competência 4 — Gestão de Dados e Persistência**.

Este repositório é um template. Use-o como base para criar o seu próprio repositório e trabalhar na competência.

> Parte do curso **Move Tech** — Magalu × Prósper Digital Skills  
> Formação em Cloud Computing para iniciantes

---

## Etapa anterior

> [move-tech-cloud-application-comp-3](https://github.com/move-tech-cloud-computing/move-tech-cloud-application-comp-3)

---

## O que você vai fazer nesta competência

Ao final da Competência 4, os dados devem **persistir em banco de dados** mesmo quando o container reinicia.

O código de integração com o banco já está pronto neste repositório. Seu trabalho é modelar os dados, provisionar e conectar o banco na Magalu Cloud.

- [ ] Criar o documento de modelagem de dados da aplicação (`docs/data-model.md`)
- [ ] Criar uma instância PostgreSQL no DBaaS da Magalu Cloud
- [ ] Criar o Kubernetes Secret com a string de conexão (`DATABASE_URL`)
- [ ] Fazer o deploy da aplicação
- [ ] Validar que os dados persistem após reiniciar o container

---

## Como rodar localmente

**Pré-requisito:** [Docker Desktop](https://www.docker.com/products/docker-desktop/) instalado (Mac e Windows) ou [Docker Engine](https://docs.docker.com/engine/install/) (Linux).

```bash
docker compose up --build
```

Acesse a documentação interativa em: http://localhost:8000/docs

---

## Secrets necessários no GitHub

Configure estes secrets no seu repositório (Settings → Secrets and variables → Actions):

| Secret | Descrição |
|--------|-----------|
| `MGC_REGISTRY_USER` | Usuário do Container Registry da MGC |
| `MGC_REGISTRY_PASSWORD` | Senha do Container Registry da MGC |
| `MGC_REGISTRY_NAME` | Nome do seu registry na MGC |
| `MGC_KUBECONFIG` | Conteúdo do arquivo `kubeconfig.yaml` (cole o conteúdo diretamente) |
| `DATABASE_URL` | String de conexão do PostgreSQL (`postgresql://user:pass@host/orders`) |
---

## Próxima etapa

Ao concluir esta competência, a solução de referência será publicada em:  
[move-tech-cloud-application-comp-5](https://github.com/move-tech-cloud-computing/move-tech-cloud-application-comp-5)
