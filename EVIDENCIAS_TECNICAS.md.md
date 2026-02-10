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

![Ambiente Kali Linux](./00-kali-environment.png)<img width="1280" height="800" alt="Kali print 2" src="https://github.com/user-attachments/assets/9a495d6c-3bd4-4bd4-bbd7-066a00bcf249" />


---

## **📡 1️⃣ VERIFICAÇÃO DE CONECTIVIDADE**

**Comando utilizado:**

`ping <IP_DO_ALVO>`

**Objetivo:**  
Confirmar comunicação entre Kali Linux e Metasploitable 2.

**Resultado:**  
Respostas ICMP recebidas, confirmando conectividade ativa.

### **📸 Evidência**

![Teste de Ping](./01-ping-test.png)<img width="1920" height="936" alt="01_ping_kali_to_metasploitable" src="https://github.com/user-attachments/assets/31c08772-b537-4572-b6ea-161edd1b44cf" />


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

![Enumeração Nmap](./02-nmap-scan.png)<img width="1920" height="936" alt="03_nmap_initial_enumeration" src="https://github.com/user-attachments/assets/67e91537-0ff5-4bd4-bb5f-e88e30aabf61" />


---

## **📁 3️⃣ DESCOBERTA DE DIRETÓRIO**

**Ferramenta:** Gobuster  

**Diretório identificado:**

`/dav`

**Impacto:**  
Diretório com permissões inadequadas permitindo exploração.

### **📸 Evidência**

![Descoberta de Diretório](./04-gobuster.png)<img width="1920" height="936" alt="04_gobuster_directory_enum" src="https://github.com/user-attachments/assets/640db96b-8bac-435d-9adb-57afe973f2d6" />


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

![Execução Remota](./06-rce.png)<img width="1920" height="936" alt="5_webdav_anonymous_access_listing" src="https://github.com/user-attachments/assets/2eb52eab-7c65-4c8b-b99a-7e257bfd9992" />


---

## **🔐 5️⃣ EXTRAÇÃO DE CREDENCIAIS**

**Arquivo identificado:**

`shadow_copy`

**Impacto:**

- Exposição de hashes de senha  
- Risco de escalonamento de privilégios  
- Potencial comprometimento total do sistema  

### **📸 Evidência**

![Extração de Credenciais](./07-shadow.png)<img width="1920" height="936" alt="8_post_exploitation_hash_dump_shadow_copy" src="https://github.com/user-attachments/assets/9567581c-e617-4385-a572-a6f34aa2987e" />



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
