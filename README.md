Sistema multiagentes com CrewAI e Ollama (Phi-3 Mini) para criar e revisar arquiteturas de integração B2B/B2C com EntraID. Otimizado para a NVIDIA GeForce GTX 1050 Ti (4 GB VRAM), roda offline com aceleração por GPU. Três agentes colaboram:
Arquiteto: Gera desenho de solução e ADR.
Tech Lead: Revisa a arquitetura para escalabilidade.
Gerente: Produz relatório de custo e benefícios.
Logs detalhados rastreiam o raciocínio dos agentes.
Funcionalidades
Multiagentes com CrewAI.
Inferência offline com Phi-3 Mini (~2-3 GB VRAM).
Aceleração por GPU (CUDA).
Logs em reasoning_logs.log e terminal (verbose=2).
Foco em integração B2B/B2C com EntraID.
Requisitos
Hardware: GTX 1050 Ti (4 GB VRAM), 8 GB RAM.
OS: Windows 10/11.
Software: Python 3.8+, Ollama, NVIDIA Drivers, CUDA 11.8.
Dependências:
bash
pip install crewai litellm openai requests
Instalação
Ollama:
bash
ollama pull phi3-mini
GPU:
Instale drivers NVIDIA (nvidia.com).
Instale CUDA 11.8 (developer.nvidia.com).
Opcional: $env:CUDA_VISIBLE_DEVICES = "0"
Repositório:
bash
git clone https://github.com/seu-usuario/multiagentes.git
cd multiagentes
Ambiente Virtual:
bash
python -m venv .venv
.\venv\Scripts\activate
pip install crewai litellm openai requests
Uso
Inicie o Ollama:
bash
ollama serve
Execute:
bash
python agentes_arquitetura_offline.py
Monitore GPU:
bash
nvidia-smi
VRAM: ~2-3 GB.
GPU-Util: 50-90%.
Logs: Veja reasoning_logs.log e terminal.
Detalhes Técnicos
CrewAI: Orquestra agentes com tarefas sequenciais.
Ollama: Servidor local (http://localhost:11434) para Phi-3 Mini (4-bit, ~3.8B parâmetros).
litellm: Gerencia chamadas ao Ollama.
GPU: GTX 1050 Ti, CUDA 11.8, CUDA_VISIBLE_DEVICES=0.
Logs: logging.DEBUG e verbose=2.
Exemplo de Saída
Arquiteto: "Desenho: Tenant B2B -> EntraID -> Tenant B2C. ADR: Contexto: Integração segura..."
Tech Lead: "Revisão: Adiciona API Gateway, corrige OAuth 2.0."
Gerente: "Relatório: Custo: $5.000/mês, 4 meses, segurança."
Extensibilidade
Adicione agentes (ex.: Segurança).
Teste Mistral-7B (4-bit, ~3-4 GB VRAM):
bash
ollama pull mistral --quantize q4_0
Novos casos: Planejamento, análise de dados.
Limitações
Phi-3 Mini gera saídas simplificadas.
GTX 1050 Ti limita modelos maiores.
Configuração inicial complexa (drivers, CUDA).
Contribuições
Fork o repositório.
Crie branch: git checkout -b feature/nova-funcionalidade.
Commit: git commit -m "Adiciona funcionalidade".
Pull request.
Licença
MIT License (LICENSE)
Contato
GitHub: seu-usuario
X: [
@seu
-usuario]
Publicação no GitHub
Crie Repositório:
Em github.com, crie multiagentes (Público/Privado).
Organize Arquivos:
Pasta multiagentes:
agentes_arquitetura_offline.py
README.md (este arquivo)
.gitignore:
.venv/
__pycache__/
*.log
*.pyc
Opcional: LICENSE (MIT)
Git:
bash
cd multiagentes
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/seu-usuario/multiagentes.git
git push -u origin main
Valide:
Acesse https://github.com/seu-usuario/multiagentes.
Confirme renderização do README.md.
Divulgue:
Tags: AI, multiagent, CrewAI, Ollama, Phi-3.
Compartilhe no X: #AI #Multiagent #Ollama.
Próximos Passos:
Publique com os passos acima.
Adicione screenshots (use ShareX).
Para extensões (ex.: novo agente), avise para ajustes.
Compartilhe o link do repositório para feedback.
Se precisar de mais concisão, ajustes ou seções específicas, é só pedir! 🚀
