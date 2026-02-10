# Credential Dump & Webshell Attack Lab

## 📌 Visão Geral

Projeto de laboratório de Segurança da Informação demonstrando exploração controlada de vulnerabilidades WebDAV, execução remota de comandos e análise de credenciais em ambiente isolado para fins educacionais.

---

## 🎯 Objetivo

Demonstrar, em ambiente controlado, o ciclo completo de:

- Reconhecimento
- Enumeração de serviços
- Exploração de vulnerabilidade WebDAV
- Upload e utilização de WebShell
- Execução remota de comandos (RCE)
- Extração de hashes de credenciais

---

## 🖥️ Ambiente Utilizado

- Kali Linux (Máquina atacante)
- Metasploitable 2 (Máquina alvo)
- VirtualBox
- Rede Host-Only (Ambiente isolado)

---

## 🔎 Metodologia

### 1️⃣ Verificação de Conectividade
Validação da comunicação entre atacante e alvo via ping.

### 2️⃣ Enumeração de Portas
Utilização do Nmap para identificação de serviços expostos.

### 3️⃣ Enumeração Web
Identificação de tecnologias com WhatWeb.

### 4️⃣ Descoberta de Diretórios
Uso do Gobuster para identificação de diretórios sensíveis.

### 5️⃣ Exploração WebDAV
Acesso ao diretório /dav via cadaver.

### 6️⃣ Execução Remota de Comandos
Utilização de webshell para execução de comandos no servidor.

### 7️⃣ Extração de Credenciais
Identificação e leitura de arquivo contendo hashes de senha (shadow_copy).

---

## 🚨 Vulnerabilidades Identificadas

- WebDAV habilitado sem controle adequado
- Upload de arquivo malicioso permitido
- Execução remota de comandos via WebShell
- Exposição de hashes de senha
- Configuração insegura de armazenamento de credenciais

---

## 🔴 Impacto

- Comprometimento do servidor web
- Execução remota de comandos
- Exposição de credenciais críticas
- Possibilidade de escalonamento de privilégio
- Comprometimento total do host

Severidade: **CRITICAL**

---

## 🛡️ Recomendações

- Desabilitar WebDAV quando não necessário
- Implementar autenticação forte
- Restringir métodos HTTP (PUT/DELETE)
- Remover arquivos sensíveis expostos
- Atualizar serviços desatualizados
- Monitoramento e hardening do servidor

---

## 📌 Conclusão

O laboratório demonstrou como uma configuração inadequada de serviços web pode levar ao comprometimento completo do sistema, incluindo execução remota de comandos e exposição de credenciais sensíveis.

Projeto realizado exclusivamente para fins educacionais em ambiente controlado.
