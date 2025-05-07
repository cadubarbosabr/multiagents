Multiagentes: Sistema de Arquitetura de Soluções com CrewAI e Ollama

Visão Geral
O repositório multiagentes implementa um sistema multiagentes para automação de tarefas técnicas, utilizando o framework CrewAI e o modelo de linguagem Phi-3 Mini executado localmente com o Ollama. O sistema é projetado para criar, revisar e relatar arquiteturas de soluções em nuvem, com foco na integração de tenants B2B e B2C usando o EntraID como provedor de identidade (IdP). Ele é otimizado para rodar em hardware modesto, como a NVIDIA GeForce GTX 1050 Ti (4 GB de VRAM), com aceleração por GPU via CUDA.
Três agentes colaboram sequencialmente:
Arquiteto de Soluções: Gera um desenho de solução e um ADR (Architecture Decision Record) para a integração B2B/B2C.
Tech Lead: Revisa a arquitetura, corrigindo erros e sugerindo melhorias técnicas para escalabilidade e viabilidade.
Gerente de Tecnologia: Produz um relatório com estimativas de custo, cronograma e benefícios.
O projeto destaca-se por sua execução offline, eliminando a dependência de APIs externas (ex.: OpenAI), e por logs detalhados que permitem acompanhar o raciocínio dos agentes. Ele é ideal para desenvolvedores, engenheiros de TI e entusiastas de IA que desejam explorar sistemas multiagentes em ambientes com recursos limitados.
Funcionalidades
Sistema Multiagentes: Coordenação de três agentes (Arquiteto, Tech Lead, Gerente) usando CrewAI para tarefas técnicas colaborativas.
Execução Offline: Uso do Ollama com Phi-3 Mini (~3.8B parâmetros, quantizado em 4-bit) para inferência local, garantindo privacidade e zero custo de API.
Aceleração por GPU: Otimizado para a NVIDIA GeForce GTX 1050 Ti, com configuração para forçar o uso da GPU via CUDA.
Logs Detalhados: Logging personalizado e modo verbose=2 do CrewAI para rastrear prompts, respostas e o raciocínio dos agentes.
Integração B2B/B2C: Foco em arquiteturas de nuvem, com suporte para EntraID como IdP principal.
Modularidade: Estrutura extensível para adicionar novos agentes ou tarefas (ex.: Especialista em Segurança, análise de dados).
Arquitetura Técnica
Componentes Principais
CrewAI: Framework Python para orquestração de agentes multiagentes, com suporte a tarefas sequenciais e contexto compartilhado.
Ollama: Servidor de inferência local que executa o Phi-3 Mini, compatível com a API OpenAI e otimizado para GPUs NVIDIA via CUDA.
Phi-3 Mini: Modelo de linguagem leve (~3.8B parâmetros, quantizado em 4-bit), ideal para hardware com 4 GB de VRAM.
litellm: Biblioteca usada pelo CrewAI para gerenciar chamadas ao Ollama, configurada para o endpoint local (http://localhost:11434).
Fluxo de Trabalho
Arquiteto de Soluções:
Recebe o prompt: "Crie um desenho de solução simples para integrar um tenant B2B com um tenant B2C usando EntraID como IdP, e um ADR com Contexto e Decisão."
Gera um desenho textual (ex.: "Tenant B2B -> EntraID -> Tenant B2C") e um ADR estruturado.
Tech Lead:
Usa a saída do Arquiteto como contexto.
Revisa a arquitetura, sugerindo melhorias (ex.: adicionar API Gateway, corrigir protocolos).
Gerente de Tecnologia:
Usa a arquitetura revisada como contexto.
Produz um relatório com custo estimado, cronograma e benefícios (ex.: "$5.000/mês, 4 meses, segurança e escalabilidade").
Logs: Todas as etapas são registradas em reasoning_logs.log e exibidas no terminal com verbose=2.
Diagrama de Fluxo
mermaid
graph TD
    A[Arquiteto: Gera Desenho e ADR] --> B[Tech Lead: Revisa Arquitetura]
    B --> C[Gerente: Produz Relatório]
Requisitos
Hardware
GPU: NVIDIA GeForce GTX 1050 Ti (4 GB VRAM) ou superior.
RAM: 8 GB ou mais.
Armazenamento: ~5 GB para o Ollama e o modelo Phi-3 Mini.
Sistema Operacional: Windows 10/11 (testado), Linux ou macOS (com ajustes).
Software
Python: 3.8 ou superior.
Ollama: Versão mais recente (ollama.ai).
NVIDIA Drivers: Compatíveis com CUDA (ex.: versão 546.12 ou superior).
CUDA Toolkit: 11.8 ou 12.x (developer.nvidia.com/cuda-downloads).
Dependências Python:
bash
pip install crewai litellm openai requests
Instalação
Instale o Ollama:
Baixe e instale o Ollama em ollama.ai.
Baixe o modelo Phi-3 Mini:
bash
ollama pull phi3-mini
Configure a GPU:
Instale os drivers NVIDIA para a GTX 1050 Ti (www.nvidia.com/Download).
Instale o CUDA Toolkit 11.8 (developer.nvidia.com/cuda-downloads).
Forçar o uso da GPU (opcional):
powershell
$env:CUDA_VISIBLE_DEVICES = "0"
Clone o Repositório:
bash
git clone https://github.com/seu-usuario/multiagentes.git
cd multiagentes
Crie um Ambiente Virtual:
bash
python -m venv .venv
.\venv\Scripts\activate
Instale Dependências:
bash
pip install crewai litellm openai requests
Uso
Inicie o Ollama:
Abra um terminal e execute:
bash
ollama serve
Execute o Script:
bash
python agentes_arquitetura_offline.py
Monitore a GPU:
Verifique o uso da GPU durante a execução:
bash
nvidia-smi
Esperado:
Memory-Usage: ~2-3 GB para Phi-3 Mini.
GPU-Util: 50-90%.
Analise os Logs:
Logs detalhados são salvos em reasoning_logs.log e exibidos no terminal.
Exemplo de log:
2025-05-07 10:00:00,123 - INFO - GPU detectada: GeForce GTX 1050 Ti...
2025-05-07 10:00:01,200 - DEBUG - [Arquiteto] Resposta: Desenho: Tenant B2B -> EntraID...
Configuração Técnica
Modelo Phi-3 Mini
Parâmetros: ~3.8 bilhões.
Quantização: 4-bit (Q4_0), usando ~2-3 GB de VRAM.
Desempenho: Otimizado para a GTX 1050 Ti (768 núcleos CUDA, CUDA 6.1).
Limitações: Saídas simplificadas para tarefas complexas devido ao tamanho do modelo.
Aceleração por GPU
CUDA: Configurado para forçar o uso da GTX 1050 Ti via CUDA_VISIBLE_DEVICES=0.
Monitoramento: Uso de nvidia-smi para verificar VRAM e utilização da GPU.
Otimização: Modelos quantizados e prompts curtos (max_tokens=300) para evitar sobrecarga dos 4 GB de VRAM.
Logging
Biblioteca: logging do Python, com saídas em reasoning_logs.log e terminal.
Nível: DEBUG, capturando prompts, respostas e erros.
Verbose: verbose=2 no CrewAI para rastrear o raciocínio dos agentes.
Exemplo de Saída
Arquiteto de Soluções
Desenho de Solução: O tenant B2B autentica via EntraID usando OAuth 2.0, enquanto o tenant B2C usa OpenID Connect. Uma API Gateway gerencia o tráfego.
ADR:
- Contexto: Necessidade de integração segura entre tenants.
- Decisão: Usar EntraID como IdP único.
- Consequências: Simplifica gerenciamento, mas exige configuração inicial.
Tech Lead
Arquitetura Revisada: Adicionado Azure API Management como Gateway para maior controle de tráfego. Corrigido protocolo para OAuth 2.0 em ambos os tenants.
Gerente de Tecnologia
Relatório:
- Custo Estimado: $5.000/mês para infraestrutura Azure.
- Cronograma: 4 meses para implementação.
- Benefícios: Segurança reforçada, escalabilidade e integração simplificada.
Extensibilidade
O sistema é modular e pode ser expandido para:
Novos Agentes: Ex.: Especialista em Segurança para revisar vulnerabilidades.
python
especialista_seguranca = Agent(
    role="Especialista em Segurança",
    goal="Garantir segurança da arquitetura",
    llm="ollama/phi3-mini"
)
Outros Modelos: Suporte a Mistral-7B (4-bit, ~3-4 GB VRAM) com ajustes:
bash
ollama pull mistral --quantize q4_0
Novos Casos: Planejamento de projetos, análise de dados, ou automação de suporte.
Limitações
Hardware: A GTX 1050 Ti (4 GB VRAM) restringe modelos maiores (ex.: LLaMA-3-8B) e múltiplas iterações simultâneas.
Phi-3 Mini: Saídas podem ser simplificadas para tarefas técnicas complexas.
Configuração: Requer instalação manual de drivers NVIDIA, CUDA, e Ollama, o que pode ser desafiador para iniciantes.
Desempenho: Inferência mais lenta (~segundos por tarefa) devido aos 768 núcleos CUDA da GTX 1050 Ti.
Contribuições
Contribuições são bem-vindas! Para contribuir:
Fork o repositório.
Crie uma branch (git checkout -b feature/nova-funcionalidade).
Commit suas alterações (git commit -m "Adiciona nova funcionalidade").
Envie um pull request.
Sugestões de melhorias:
Adicionar novos agentes ou tarefas.
Otimizar prompts para o Phi-3 Mini.
Integrar ferramentas de visualização (ex.: Mermaid, CSV).
Suportar outros modelos ou GPUs.
Licença
MIT License (LICENSE) <!-- Crie um arquivo LICENSE, se desejar -->
Como Citar
Se usar este projeto em seu trabalho ou pesquisa, cite:
Sistema Multiagentes para Arquitetura de Soluções
Autor: [Seu Nome]
Repositório: https://github.com/seu-usuario/multiagentes
Contato
Autor: [Seu Nome]
GitHub: seu-usuario
X: [
@seu
-usuario] <!-- Adicione seu handle, se aplicável -->
Notas de Segurança
Logs: Não inclua reasoning_logs.log no repositório, pois pode conter dados sensíveis.
Offline: O projeto é 100% offline, garantindo privacidade, mas valide os prompts para evitar exposição de informações corporativas.
.gitignore: Inclui .venv/, *.log, e __pycache__/ para proteger arquivos sensíveis.
Passos para Publicação no GitHub
Crie o Repositório:
Acesse github.com e crie um repositório chamado multiagentes.
Escolha Público (ou Privado, se preferir).
Adicione um README.md inicial (substitua pelo conteúdo acima).
Organize os Arquivos:
Crie uma pasta local:
powershell
mkdir multiagentes
cd multiagentes
Adicione:
agentes_arquitetura_offline.py (o script principal).
README.md (com o conteúdo acima).
.gitignore:
.venv/
__pycache__/
*.log
*.pyc
Opcional: LICENSE (ex.: MIT License).
Inicialize o Git:
powershell
git init
git add .
git commit -m "Initial commit: Sistema multiagentes com CrewAI e Ollama"
Conecte ao GitHub:
powershell
git remote add origin https://github.com/seu-usuario/multiagentes.git
git push -u origin main
Valide no GitHub:
Acesse https://github.com/seu-usuario/multiagentes.
Confirme que o README.md está renderizado corretamente.
Teste clonando o repositório em outro diretório:
powershell
git clone https://github.com/seu-usuario/multiagentes.git
Divulgue:
Adicione tags no GitHub: AI, multiagent, CrewAI, Ollama, Phi-3, GPU.
Compartilhe no X com #AI, #Multiagent, #Ollama, #CrewAI.
Considere um post com capturas de tela (ex.: nvidia-smi, logs).
Próximos Passos
Publique o Repositório:
Siga os passos acima e envie o projeto ao GitHub.
Me avise o link do repositório para revisar o README.md.
Adicione Melhorias:
Inclua capturas de tela ou GIFs no README.md (use ShareX).
Adicione um agente extra (ex.: Especialista em Segurança) se quiser expandir.
Crie um arquivo CSV com saídas, como sugerido anteriormente:
python
import csv
outputs = [{"Agente": task.agent.role, "Saída": task.execute_sync()} for task in equipe.tasks]
with open('agent_outputs.csv', 'w', newline='', encoding='utf-8') as f:
    writer = csv.DictWriter(f, fieldnames=["Agente", "Saída"])
    writer.writeheader()
    writer.writerows(outputs)
Teste o Mistral-7B:
Se quiser saídas mais robustas, baixe o Mistral-7B (4-bit, ~3-4 GB VRAM):
bash
ollama pull mistral --quantize q4_0
Atualize o código:
python
llm="ollama/mistral"
os.environ["OLLAMA_MODEL"] = "mistral"
Monitore a VRAM com nvidia-smi para evitar travamentos.
Feedback:
Compartilhe o link do repositório ou trechos das saídas para ajustes.
Se precisar de ajuda com GitHub Actions, imagens, ou outros recursos, posso fornecer instruções.
O README.md está pronto para destacar a potência e a acessibilidade do seu projeto! Se quiser ajustes (ex.: tom mais informal, seções extras, ou suporte para outro modelo), é só avisar! 🚀
