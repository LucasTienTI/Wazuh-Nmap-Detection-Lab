# 🛡️ Wazuh-Nmap-Detection-Lab

Laboratório prático focado em **Blue Team** e monitoramento **SOC**, configurado para detectar e alertar sobre atividades de reconhecimento (Network Scans) em tempo real utilizando o ecossistema Wazuh.

## 📋 Visão Geral do Projeto
Este projeto demonstra a integração entre um SIEM (Wazuh) e endpoints Windows para a detecção de ataques cibernéticos. O foco principal foi capturar um scan de portas originado de uma máquina atacante (Kali Linux) e validar a visibilidade dos logs no dashboard centralizado.

## 🛠️ Arquitetura do Laboratório
* **Manager**: Wazuh Server hospedado em Ubuntu (WSL2).
* **Agent**: Windows 11 monitorado com Wazuh Agent.
* **Fontes de Logs**:
    * **Windows Event Channel**: Application, Security e System logs.
    * **Sysmon**: Utilizado para monitoramento detalhado de conexões de rede e criação de processos.
    * **Windows Firewall**: Logs de pacotes bloqueados configurados para leitura direta em `pfirewall.log`.

## ⚔️ Simulação de Ataque
Para testar a eficiência do monitoramento, foi realizado um scan de rede utilizando **Nmap** no Kali Linux contra o IP do agente Windows:

```bash
nmap -Pn -sT -p 135,139,445,3389 <IP_DO_WINDOWS>

📊 Resultados e Detecção
O laboratório foi bem-sucedido na geração de alertas críticos:

Dashboard de Detecção
Total de Eventos: Mais de 600 alertas gerados durante os testes de estresse.

Alertas de Auditoria: Foram detectados múltiplos eventos de Audit Failure (ID 60104), comprovando que as tentativas de conexão não autorizadas foram registradas e enviadas ao Manager.

Detalhes do Alerta (Forense)
Análise de Fluxo: Identificação precisa do IP de origem do atacante e das portas visadas diretamente nos logs detalhados.

📂 Arquivos do Repositório
ossec-windows-agent.conf: Arquivo de configuração customizado para o agente Windows, incluindo a integração com Sysmon e Firewall.
