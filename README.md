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

  <img width="1920" height="920" alt="analiseDeSuperficieNMAP" src="https://github.com/user-attachments/assets/4ac92e53-ed4a-4b28-b7e4-c45efe433764" />
  
Como analista, realizei a validação manual da porta 5000 através do navegador web do Kali Linux para identificar o serviço oculto. A requisição retornou um código HTTP 404 Not Found, confirmando a existência de uma aplicação web de segundo plano (provavelmente UPnP ou API do fabricante) ativa, porém sem indexação de página inicial pública.

## 5.Conclusão e Mitigações Recomendadas
Recomendação de Hardening: Manter o firmware do roteador sempre atualizado para mitigar vulnerabilidades conhecidas nos serviços web das portas 80 e 443.

Desativação de Recursos Desnecessários: Se o serviço da porta 5000 (UPnP) não for estritamente necessário para aplicações internas, recomenda-se desativá-lo diretamente no painel de controle do roteador para reduzir a superfície de ataque da rede.

## 6. Execução Técnica e Comandos Utilizados
Para mapear as portas mais comuns abertas no dispositivo alvo, foi executado o escaneamento rápido via terminal do Kali Linux:

sudo nmap -F 192.168.0.1


Análise Avançada de Impressão Digital (Fingerprinting)

sudo nmap -A -v 192.168.0.1

<img width="650" height="516" alt="FP3" src="https://github.com/user-attachments/assets/3338a2e1-df43-4e86-84fc-82f0925706c9" />
<img width="650" height="516" alt="Fingerprinting1" src="https://github.com/user-attachments/assets/1ac0dfe3-567d-49d7-8b58-88c499125c07" />

O ativo foi identificado como um sistema baseado em Linux 3.2 - 4.14. Na visão de defesa, essa informação é usada para mapear se o firmware atual possui CVEs (Vulnerabilidades e Exposições Conhecidas) ativas que exijam uma atualização imediata.

## 7. Auditoria de Vulnerabilidades Automatizada (Nmap Scripting Engine)
Foi executada uma varredura profunda utilizando o motor de scripts do Nmap focado em falhas conhecidas através do comando técnico:
```bash
sudo nmap --script=vuln 192.168.0.1

