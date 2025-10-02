🤖 Secretária Virtual AI para WhatsApp (n8n + Chatwoot/Evolution)
Este repositório contém os workflows e scripts necessários para implementar uma Secretária Virtual com Inteligência Artificial robusta, capaz de gerenciar agendas, responder a clientes, lidar com áudios e integrar-se a plataformas de comunicação.


🌟 Funcionalidades Principais
Funcionalidade	Descrição
Atendimento Humanizado	Reage a mensagens, mostra que está digitando/gravando áudio e aguarda o cliente terminar de falar (mensagens "encavaladas").
Resposta em Áudio	Capaz de ouvir áudios dos clientes, transcrever e responder com voz natural via Eleven Labs.
Gestão de Agendas	Agenda, remarca e cancela consultas/reuniões em múltiplas agendas do Google Calendar (multi-ID).
Follow-up Automático	Envia mensagens automáticas de confirmação de presença (follow-up) usando um Agente de Follow-up com memória compartilhada.
Escalonamento para Humano	Em casos de dúvida ou solicitação específica (ex: falar com o financeiro), escala o atendimento para um humano e envia alerta via Telegram.
Envio de Arquivos	Lista arquivos de uma pasta específica no Google Drive e envia o documento solicitado ao cliente (ex: catálogos, pedidos de exame).
Assistente Interno (Telegram)	Permite interações internas via Telegram (ex: "Desmarca todas as consultas do Dr. João amanhã", "Leia meus principais e-mails").


🛠️ Tecnologias Utilizadas
O workflow é construído sobre uma VPS (Máquina Virtual) e utiliza os seguintes serviços:

Categoria	Tecnologia	Uso no Projeto
Automação	n8n	Orquestração de todos os fluxos e lógica de negócio.
IA	Gemini 2.5 Pro	Modelo de linguagem para o Agente de Secretária e de Follow-up (LLM e Agente de Pensamento Thinking).
Comunicação (Opção 1)	Chatwoot + Baileys (Fork Fazeraí)	Plataforma Omnichannel para gestão de conversas e conexão com WhatsApp (via QR Code).
Comunicação (Opção 2)	Evolution API	Alternativa para conexão direta e gerenciamento de instâncias WhatsApp.
Voz/Áudio	Eleven Labs	Geração de respostas de voz com alta qualidade e naturalidade.
Banco de Dados/Memória	Supabase (PostgreSQL)	Armazenamento do histórico de conversas (memória) e gerenciamento de filas de mensagens.
Agendamento	Google Calendar	Gestão de agendas dos profissionais/equipes.
Alertas Internos	Telegram	Canal para alertas e para o Agente de Assistente Interno.
Arquivos	Google Drive	Repositório para os arquivos que a assistente pode enviar aos clientes.



📂 Estrutura do Repositório (Workflows n8n)
O projeto é composto por um Workflow Principal e vários Sub-Workflows, listados por ordem de criação/configuração sugerida no vídeo:

1_secretaria_principal_chatwoot.json ou 1_secretaria_principal_evolution.json - Workflow principal de atendimento.

2_servidor_mcp_google_calendar.json - (Sub-Workflow) Ferramentas para manipulação do Google Calendar.

3_baixar_e_enviar_arquivos.json - (Sub-Workflow) Ferramenta para baixar e enviar arquivos do Google Drive.

4_escalar_para_humano_telegram.json - (Sub-Workflow) Ferramenta para atribuir etiqueta "agente off" no Chatwoot e notificar no Telegram.

5_enviar_mensagem_para_conversa.json - (Sub-Workflow) Ferramenta para o Agente de Follow-up salvar mensagens no histórico da secretária.

6_assistente_interno_telegram.json - (Sub-Workflow) Atendimento a comandos internos via Telegram.

script_supa_base.sql - Script SQL para criação das tabelas de memória e fila no Supabase.

⚙️ Configuração (Passos Chave)
Siga o tutorial do vídeo para obter a explicação completa ([02:00:07]), mas os passos críticos de configuração são:

Configuração da VPS: Instalação do n8n e do Chatwoot (versão com Baileys) ou Evolution API na sua Máquina Virtual.

Conexões/Credenciais: Crie e configure todas as credenciais no n8n para:

Chatwoot/Evolution: URL da instância e Token de Acesso.

Supabase: Host, Database, User e Password (para o banco de dados PostgreSQL).

Eleven Labs: Chave API para geração de voz.

Google: Credenciais OAuth para Google Calendar e Google Drive.

Telegram: BotFather para obter o token e o User Info Bot para obter o ID do seu chat.

Supabase: Execute o script_supa_base.sql no Editor SQL do seu projeto Supabase para criar as tabelas necessárias (fila_mensagens e historico_mensagens).

Webhooks (Chatwoot): Cadastre as URLs de Teste e Produção do Workflow Principal (Webhook node do n8n) como Webhooks no Chatwoot (menu Configurações > Integrações), selecionando o evento "Mensagem Criada".

Sub-Workflows: Copie, cole e salve todos os Sub-Workflows. No Workflow Principal, referencie e selecione os Sub-Workflows criados nos seus respectivos nós (ex: Ferramenta "Escalar para Humano" deve referenciar o 4_escalar_para_humano_telegram).

System Prompt: Revise e personalize o System Prompt do Agente Principal, inserindo as informações da sua empresa (horário de funcionamento, profissionais, IDs das agendas do Google Calendar, etc.).

🚀 Download 



