````markdown
# Multiagentes: Sistema de Arquitetura de Soluções com CrewAI e Ollama

## 📌 Visão Geral

Este repositório implementa um sistema **multiagentes** para automação de tarefas técnicas usando o framework **CrewAI** e o modelo de linguagem **Phi-3 Mini** via **Ollama**, com execução 100% offline e suporte a **GPU NVIDIA GTX 1050 Ti**.

Três agentes atuam sequencialmente:
- **Arquiteto de Soluções:** Cria o desenho de arquitetura e um ADR.
- **Tech Lead:** Revisa a arquitetura, sugerindo melhorias.
- **Gerente de Tecnologia:** Gera um relatório com custo, cronograma e benefícios.

### ⚙️ Funcionalidades
- ✅ Execução offline com **Ollama + Phi-3 Mini**
- ✅ Coordenação multiagente via **CrewAI**
- ✅ Suporte a **GPU modesta (GTX 1050 Ti, 4GB VRAM)**
- ✅ Logs detalhados com raciocínio dos agentes
- ✅ Foco em **integração B2B/B2C com EntraID**
- ✅ Estrutura modular para novos agentes/tarefas

---

## 🧠 Arquitetura Técnica

### 🧩 Componentes
- **CrewAI:** Framework de agentes coordenados
- **Ollama:** Servidor local compatível com API OpenAI
- **Phi-3 Mini:** Modelo quantizado de ~3.8B parâmetros (4-bit)
- **litellm:** Gerencia chamadas ao Ollama local

### 🔁 Fluxo de Trabalho
```mermaid
graph TD
    A[Arquiteto: Gera Desenho e ADR] --> B[Tech Lead: Revisa Arquitetura]
    B --> C[Gerente: Produz Relatório]
````

---

## 🖥️ Requisitos

### 🔧 Hardware

* GPU: NVIDIA GTX 1050 Ti (4 GB) ou superior
* RAM: 8 GB+
* Armazenamento: 5 GB livres
* SO: Windows 10/11 (testado), Linux/macOS (com ajustes)

### 📦 Software

* Python 3.8+
* Ollama (última versão)
* Drivers NVIDIA com CUDA
* CUDA Toolkit 11.8 ou 12.x

```bash
pip install crewai litellm openai requests
```

---

## 🚀 Instalação

### 1. Instale o Ollama

```bash
ollama pull phi3-mini
```

### 2. Configure a GPU

* Instale drivers e CUDA Toolkit 11.8+
* (Opcional) Forçar uso da GPU:

```powershell
$env:CUDA_VISIBLE_DEVICES = "0"
```

### 3. Clone o repositório

```bash
git clone https://github.com/seu-usuario/multiagentes.git
cd multiagentes
```

### 4. Crie o ambiente virtual

```bash
python -m venv .venv
.\.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Linux/macOS
pip install crewai litellm openai requests
```

---

## ▶️ Uso

### 1. Inicie o Ollama

```bash
ollama serve
```

### 2. Execute o sistema

```bash
python agentes_arquitetura_offline.py
```

### 3. Monitore a GPU (opcional)

```bash
nvidia-smi
```

**Uso esperado:** \~2-3 GB de VRAM, 50-90% de utilização

---

## 📝 Exemplo de Saída

**Arquiteto de Soluções**

```text
Desenho: Tenant B2B -> EntraID -> Tenant B2C
ADR:
- Contexto: Integração segura entre tenants
- Decisão: Usar EntraID como IdP único
- Consequências: Simplifica gestão, exige configuração inicial
```

**Tech Lead**

```text
Adicionado Azure API Management como Gateway
Corrigido para OAuth 2.0 em ambos os tenants
```

**Gerente de Tecnologia**

```text
- Custo: $5.000/mês
- Prazo: 4 meses
- Benefícios: Segurança, escalabilidade, integração simplificada
```

---

## 🧩 Extensibilidade

### ➕ Novos Agentes

```python
especialista_seguranca = Agent(
    role="Especialista em Segurança",
    goal="Garantir segurança da arquitetura",
    llm="ollama/phi3-mini"
)
```

### 🔄 Outros Modelos

```bash
ollama pull mistral --quantize q4_0
```

---

## ⚠️ Limitações

* **GPU**: 4 GB de VRAM limita modelos maiores e múltiplas iterações simultâneas
* **Phi-3 Mini**: Respostas simplificadas para tarefas complexas
* **Configuração**: Exige instalação manual de Ollama, drivers e CUDA

---

## 🤝 Contribuições

Contribuições são bem-vindas!

```bash
git checkout -b feature/nova-funcionalidade
git commit -m "Adiciona nova funcionalidade"
git push origin feature/nova-funcionalidade
```

Sugestões:

* Novos agentes (ex.: Especialista em Segurança)
* Otimização de prompts
* Suporte a novos modelos ou GPUs

---

## 📄 Licença

MIT License – veja o arquivo [LICENSE](LICENSE)

---

## 📚 Citação

```text
Sistema Multiagentes para Arquitetura de Soluções  
Autor: [Seu Nome]  
Repositório: https://github.com/seu-usuario/multiagentes
```

---

## 📬 Contato

**Autor:** \CaduBarbosa
**GitHub:** \CaduBarbosaBR
**X (Twitter):** \CaduBarbosaBR

---

## 🔐 Notas de Segurança

* Não envie arquivos `.log` para o repositório (via `.gitignore`)
* Valide os prompts antes de uso em ambiente corporativo
* O projeto roda 100% offline (sem chamadas externas)

---

## 📁 .gitignore

```
.venv/
__pycache__/
*.log
*.pyc
```

---

## ✅ Publicação no GitHub

1. Crie o repositório: `multiagentes`
2. Adicione `README.md`, `LICENSE`, `.gitignore`, e `agentes_arquitetura_offline.py`
3. Inicialize o Git:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/seu-usuario/multiagentes.git
git push -u origin main
```

---

## 📌 Próximos Passos

* Adicione capturas de tela (ex.: `nvidia-smi`, logs)
* Expanda com agentes adicionais
* Exporte saídas para CSV:

```python
import csv
outputs = [{"Agente": task.agent.role, "Saída": task.execute_sync()} for task in equipe.tasks]
with open('agent_outputs.csv', 'w', encoding='utf-8') as f:
    writer = csv.DictWriter(f, fieldnames=["Agente", "Saída"])
    writer.writeheader()
    writer.writerows(outputs)
```

---

Explore o poder dos **sistemas multiagentes offline** com CrewAI + Ollama!

```
