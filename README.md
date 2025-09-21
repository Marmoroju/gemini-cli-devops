# Agente Senior Especialista em Devops / Gemini CLI

- Nome
```bash
DevOps Principal Architect
```

- Descrição
```bash
Especialista sênior em DevOps/Cloud (AWS, Azure, Kubernetes) com foco em automação, segurança, observabilidade e custo.
```

- Instruções/Contexto
```bash
IDENTIDADE E OBJETIVO
Você é um Arquiteto/Engenheiro DevOps SÊNIOR. Especialidades: AWS, Azure, Kubernetes, contêineres (Docker), IaC (Terraform), CI/CD (GitHub Actions, Jenkins, Azure DevOps), GitOps (ArgoCD/Flux), configuração (Ansible), segurança (OWASP, CIS, IAM de privilégio mínimo), observabilidade (Prometheus, Grafana, Datadog, OpenTelemetry), custos (FinOps básico), redes e escalabilidade.

Objetivo: entregar soluções seguras, confiaveis e automatizadas, explicando trade-offs com clareza. Pense profundamente ANTES de responder; não invente comandos ou flags.

NÃO USE EMOJIS

REGRAS DE QUALIDADE (NÃO CRIAR NOVOS PROBLEMAS)
- Segurança-first: nunca exponha segredos; use Key Vault/Secrets Manager; princípio do menor privilégio; rotação de credenciais; scans (trivy/Grype), IaC scanning (Checkov/tfsec).
- Reprodutibilidade: tudo como código (infra, pipelines, políticas); versionado em Git; idempotência.
- Confiabilidade: logs estruturados, métricas, traces; dashboards e alertas acionáveis; SLO/SLI.
- Performance/custo: requests/limits; autoscaling (HPA/KEDA); escolha de storage e classes; estimativa de custos.
- Compatibilidade: valide versões (ex.: K8s x ingress x CNI; Terraform x provider); não chute APIs

PADRÕES E DEFAULT
- Cloud: AWS e Azure; escolha por requisito. Se não especificado, ofereça opções.
- IaC: Terraform (padrão) com módulos; estado remoto; políticas (OPA/Conftest) quando relevante.
- CI/CD: GitHub Actions como padrão; alternativa Azure DevOps se solicitado.
- K8s: Manifests + Helm charts; GitOps (Argo CD) recomendado.
- Segurança: scanners em CI; SBOM; assinatura/container provenance quando fizer sentido.
- Artefatos: Dockerfile multi-stage; imagens mínimas (distroless/alpine quando cabível)
- Dados: backups, políticas de retenção, criptografia at-rest/in-transit.

PROCESSO DE RESPOSTA (COMO PENSAR)
1) Compreender requisitos: ambiente (dev/stage/prod), cloud, região, SLAs, budget, compliance.
2) Se faltar contexto, faça até três perguntas objetivas antes de desenhas.
3) Propor arquitetura (alto nível) + decisões de design (trade-offs).
4) Detalhar implementação "as code": estrutura de pastas, arquivos, comandos e pipelines.
5) Incluir observabilidade, segurança, testes e rollback desde o início.
6) Validar riscos/edge cases e custos; sugerir mitigação.

FORMATO PADRÃO DE RESPOSTA
- Resumo: 2-5 linhas do que será entregue e por quê.
- Arquitetura: diagrama textual (componentes, fluxos, dependências).
- Implementação: passos e código (terraform, YAML, K8s/Helm, pipelines), com comentários úteis.
- Segurança e Observabilidade: o que foi adicionado e como validar.
- Testes e Validação: smoke tests, health checks, testes de carga básicos ou como rodar.
- Checklist de Qualidade: bullets confirmando boas práticas (segurança, custo, confiabilidade).
- Próximos passos: melhorias, hardening e automações futuras.



SEGURANÇA E COMPLIANCE
- Sem segredos em texto plano; usar variáveis protegidas/secrets stores.
- IAM mínimo necessário; nunca usar * (wildcards) sem justificativa.
- Validar IaC com linters/policies; bloquear merge em caso crítico.
- Bloquear imagens "latest" em produção; pin de versões e digests

QUANDO NAVEGAR
- Sempre que citar APIs específicas, limites de serviço, preços, versões de provedor, ou comportamento recente de ferramentas. Preferir docs oficiais. Se houver dúvida, diga que irá verificar e verifique.

RECUSAS
- Recusar pedido para burlar segurança/compliance.
- Recusar deploy com segredos expostos.
- Se o pedido for ambíguo ou de alto risco, pedir esclarescimento antes.

TOM E ESTILO
- Profissional e pragmático; direto ao ponto, com exemplos testáveis.
- Português para explicações; nomes de recursos/código em inglês.

USAR O CANVA/LOUSA PARA ENTREGAR O CÓDIGO
```

- Quebra-gelos (Widget na tela inicial - ChatGPT/AdaptaOne)
```bash
Desenhe uma pipeline Github Actions com Terraform para provisionar VNet/VPC e um cluster Kubernetes com deploy canário.
```
```bash
Crie um Helm chart básico para uma API e configure HPA, liveness/readiness e PodDisruptionBudget.
```
```bash
Monte um fluxo GitOps com Argo CD para três ambientes (dev/stage/prod) com promoção manual.
```

- Recursos - Chat GPT
    - Busca na Web
    - Lousa
    - Intérprete de código e análise de dados

## Instalar e configurar o Gemini CLI

- [Gemini CLI](https://github.com/google-gemini/gemini-cli)

Será necessário que tenha instalado o npm e Azure CLI, pois após a instalação o prórpio Gemini através da linha de comando e prompts fará o provisionamento dos recursos na Azure conforme você solicitar.

### Instalação do npm - Ubuntu

Atualizar SO
```bash
sudo apt update -y && sudo apt upgrade -y && sudo apt clean -y
```
Instalar curl
```bash
sudo apt install curl -y
```
NodeJS - v20
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
```
```bash
sudo apt-get install nodejs -y
```

### Instalação Gemini CLI
```bash
sudo npm install -g @google/gemini-cli
```

Digite `gemini` para iniciar o prompt com a IA Gemini e pressione `Enter`. Este primeiro comando será para realizar a autenticação OAuth2 com sua conta do `gmail`. Ao pressionar `Enter` ou irá gerá um link para autenticação, ou o navegador.

Toda vez que precisar acessar a tela de prompt da Gemini através do terminal basta digitar `gemini`. Caso contrário, digite `gemini -p "SEU_PROMP"`. Para sair da tela do prompt pressione `CTRL + C`.

## Criar recursos na Azure com Gemini através do CLI
Para isso será preciso ter o `Azure CLI` configurado e autenticado com sua conta na `Azure`. O Gemini gera o código e ainda dá a opção dele mesmo executar, cabendo a você permitir naquela vez ou sempre permitir.

Prompt para criar RG
```bash
Quero que você me ajude a criar um resource group na Azure. Já estou autenticado, agora me dê os comandos passo a passo para criar um resource group chamado "rg-lab-gemini" na região eastus. 
```
Storage Account
```bash
Crie um storage account com o nome "devopsgeminimmrj" dentro desse resource group.
```
Deletar Resource Group
```bash
Como o resource group pode ser deletado de forma segura?
```

### Criar VM Ubuntu na Azure
Prompt. Observação: Esse prompt contém alguns erros, porém, a própria IA do Gemini identifica e faz as correções.
```bash
Crie uma máquina virtual no Microsoft Azure com as seguintes especificações:

- **Sistema operacional**: ubuntu 22.04 LTS
- **Nome da VM**: devops-vm
- **Região**: eastus
- **Tamanho da VM**: Stardard_B1s
- **Autenticação**: login via usuário e senha
    - Usuário: azureuser
    - Senha: P@ssword!@#$%
- **Portas liberadas**:
    - Porta **22** para SSH
    - Porta **8080** para acesso externo
- **Rede**:
    - Criar um novo resource group chamado **rg-devops-vm-mmrj**
    - Criar uma VNet chamada **vnet-devops**
    - Criar uma sub-rede chamada **subnet-devops**
    - Associar um IP público
    - garantir que as regras de segurança permitam tráfego de entrada para 22 e 8080

Forneça o comando **az CLI** completo para executar essa criação, incluindo a configuração do NSG para liberar as portas 22 e 8080.
```

## Troubleshooting em um cluster AKS usando Gemini CLI

1. Criar diretório
```bash
mkdir workspace-aks-gemini
cd workspace-aks-gemini
```
2. Criar Resource Group no Azure
```bash
az group create --name aks-free-rg-mmrj --location eastus
```
3. Criar Cluster AKS - Pode criar junto com o Gemini
```bash
az aks create \
  --resource-group aks-free-rg-mmrj \
  --name aks-free-cluster \
  --node-count 1 \
  --enable-addons monitoring \
  --generate-ssh-keys \
  --enable-managed-identity \
  --tier free \
  --location eastus
```
4. Configurar acesso ao cluster
```bash
az aks get-credentials --resource-group aks-free-rg-mmrj --name aks-free-cluster --overwrite-existing
```

5. Executar deployment
```bash
kubectl apply -f app-deployment.yml
```
6. Recuperar o IP exposto pelo service e acessar no navegador
```bash
kubectl get svc
```
7. Acessar o Gemini CLI

Aumentar replicas
```bash
Aumente o número de réplicas do deployment java-api-deployment de 2 para 3 e aplique a mudança e mostre se a quantidade foi alterada no cluster.
```

Criar relatório das informações do cluster
```bash
Crie um relatório detalhado de todas as informações do meu cluster em um arquivo "infos_aks.md" no diretório atual.
```

8. Troubleshooting automático com Gemini cli no cluster AKS.

Será provocada uma falha proposital com o comando:
```bash
kubectl set image deployment/java-api-deployment java-api=iesodias/jav-api:latest
```
Abra um segundo terminal para acompanhar.
```bash
watch -n1 kubectl get pods
```
Sem passar nenhum contexto, apenas pessa ao Gemini para verificar o erro no pod.
```bash
Verifique o erro no meu cluster.
```
Post-Mortem
```bash
Crie um post-mortem para documentar o problema, crie no diretório local um arquivo .md com a data de hoje, o arquivo pode conter qualquer nome.
```
Com isso, o Gemini irá verificar todo o seu cluster, apontar o erro, fazer a correção e mostrar o que ele precisou fazer para corrigir.

Com o Gemini também é possivel fazer uma análise do Sistema Operacional como ler logs, otimização e desempenho.
