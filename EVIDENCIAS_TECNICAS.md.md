# **📂 EVIDÊNCIAS TÉCNICAS**
**Credential Dump & Webshell Attack Lab**

---

## **🖥️ 0️⃣ AMBIENTE DO ATACANTE – KALI LINUX**

**Sistema:** Kali Linux  
**Virtualização:** VirtualBox  
**Rede:** Host-Only (isolada)  

**Objetivo:**  
Validar que o ambiente está corretamente configurado antes do início da exploração.

### **📸 Evidência**

<img width="1280" height="800" alt="00_kali_environment png" 

---

## **📡 1️⃣ VERIFICAÇÃO DE CONECTIVIDADE**

**Comando utilizado:**

`ping <IP_DO_ALVO>`

**Objetivo:**  
Confirmar comunicação entre Kali Linux e Metasploitable 2.

**Resultado:**  
Respostas ICMP recebidas, confirmando conectividade ativa.

### **📸 Evidência**

<img width="1920" height="936" alt="01_ping_kali_to_metasploitable png" 

---

## **🔎 2️⃣ ENUMERAÇÃO DE PORTAS**

**Ferramenta:** Nmap  

**Objetivo:**  
Identificar portas abertas e serviços expostos.

**Resultado identificado:**

- Múltiplas portas abertas  
- Serviço HTTP ativo  
- Indícios de WebDAV habilitado  

### **📸 Evidência**

<img width="1920" height="936" alt="02_nmap_initial_scan png" 

---

## **📁 3️⃣ DESCOBERTA DE DIRETÓRIO**

**Ferramenta:** Gobuster  

**Diretório identificado:**

`/dav`

**Impacto:**  
Diretório com permissões inadequadas permitindo exploração.

### **📸 Evidência**

<img width="1920" height="936" alt="03_gobuster_directory_enum png" 

---

## **💻 4️⃣ EXECUÇÃO REMOTA DE COMANDOS (RCE)**

Após o upload da WebShell foi possível executar comandos remotamente no servidor.

**Testes realizados:**

`whoami`  

- Navegação em diretórios  
- Enumeração básica do sistema  

**Impacto:**  
Comprometimento do servidor.

### **📸 Evidência**

<img width="1920" height="936" alt="04_webdav_access png" 

---

## **🔐 5️⃣ EXTRAÇÃO DE CREDENCIAIS**

**Arquivo identificado:**

`shadow_copy`

**Impacto:**

- Exposição de hashes de senha  
- Risco de escalonamento de privilégios  
- Potencial comprometimento total do sistema  

### **📸 Evidência**

<img width="1920" height="936" alt="7_shadow_dump png" 

---

## 🚨 ANÁLISE FINAL

A exploração evidenciou falhas críticas na configuração do serviço WebDAV, permitindo:

- Upload não autenticado de arquivo malicioso  
- Execução remota de comandos (RCE)  
- Acesso a arquivos sensíveis do sistema  
- Exposição de hashes de senha  

**Se explorado em ambiente real, o impacto poderia resultar em comprometimento total do servidor.**

---

🔒 **Laboratório executado exclusivamente em ambiente isolado para fins educacionais.**
