# Laboratório Prático: Mapeamento de Ativos e Análise de Superfície de Ataque com Nmap

## 1. Objetivo do Projeto
Demonstrar a aplicação prática de ferramentas de reconhecimento de rede (Nmap) em um ambiente controlado (Lab Doméstico) para identificar portas lógicas abertas, serviços ativos e analisar potenciais riscos de segurança na perspectiva de um Analista de SOC (Blue Team).

## 2. Cenário de Teste
* **Máquina Atacante/Auditora:** Kali Linux v2026 (Configurada em Modo Bridge no VirtualBox para interagir com a rede local).
* **Alvo:** Roteador Gateway Doméstico (`192.168.0.1`).

## 3. Execução Técnica e Comandos Utilizados
Para mapear as portas mais comuns abertas no dispositivo alvo, foi executado o escaneamento rápido via terminal do Kali Linux:

## 4. Identificação
Identifiquei 3 portas abertas no dispositivo:
- Porta 80/TCP (HTTP): Aberta (Gerenciamento WEB padrão)
- Porta 443/TCP (HTTPS): Aberta (Gerenciamento WEB seguro)
- Porta 5000/TCP (UPnP/Mitigado): Aberta
  
Como analista, realizei a validação manual da porta 5000 através do navegador web do Kali Linux para identificar o serviço oculto. A requisição retornou um código HTTP 404 Not Found, confirmando a existência de uma aplicação web de segundo plano (provavelmente UPnP ou API do fabricante) ativa, porém sem indexação de página inicial pública.

## 4. Execução Técnica e Comandos Utilizados
Para mapear as portas mais comuns abertas no dispositivo alvo, foi executado o escaneamento rápido via terminal do Kali Linux:

```bash
sudo nmap -F 192.168.0.1
