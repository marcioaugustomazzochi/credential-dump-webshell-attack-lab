![MIT License](https://img.shields.io/badge/license-MIT-green)

# Credential Dump & Webshell Attack Lab

## 📌 Visão Geral

Projeto de laboratório de Segurança da Informação demonstrando exploração controlada de vulnerabilidades WebDAV, execução remota de comandos e análise de credenciais em ambiente isolado para fins educacionais.

O laboratório evidencia como falhas de configuração e exposição inadequada de serviços podem resultar no comprometimento completo de um servidor.

---

## 🎯 Objetivo

Demonstrar, em ambiente controlado, o ciclo completo de um teste de invasão envolvendo:

- Reconhecimento
- Enumeração de serviços
- Exploração de vulnerabilidade WebDAV
- Upload e utilização de WebShell
- Execução remota de comandos (RCE)
- Enumeração interna do sistema
- Extração de hashes de credenciais

---

## 🖥️ Ambiente Utilizado

- Kali Linux (Máquina atacante)
- Metasploitable 2 (Máquina alvo vulnerável)
- VirtualBox
- Rede Host-Only (Ambiente isolado)

---

## 🔎 Metodologia

### 1️⃣ Verificação de Conectividade
Validação da comunicação entre atacante e alvo via teste de ping.

### 2️⃣ Enumeração de Portas
Utilização do Nmap para identificação de serviços expostos e versões em execução.

### 3️⃣ Enumeração Web
Identificação de tecnologias e serviços web com WhatWeb.

### 4️⃣ Descoberta de Diretórios
Uso do Gobuster para identificação de diretórios sensíveis.

### 5️⃣ Exploração WebDAV
Acesso ao diretório `/dav` via cadaver, validando permissões inadequadas.

### 6️⃣ Execução Remota de Comandos
Utilização de webshell para execução remota de comandos no servidor.

### 7️⃣ Extração de Credenciais
Identificação e leitura de arquivo contendo hashes de senha (`shadow_copy`).

---

## 🚨 Vulnerabilidades Identificadas

- WebDAV habilitado sem controle de acesso adequado
- Permissão de upload de arquivos maliciosos
- Execução remota de comandos via WebShell
- Exposição de hashes de senha
- Armazenamento inseguro de arquivo sensível
- Serviços desatualizados

---

## 🔴 Impacto

A exploração resultou em:

- Comprometimento do servidor web
- Execução remota de comandos no contexto do serviço
- Exposição de credenciais críticas
- Possibilidade de escalonamento de privilégios
- Risco de comprometimento total do host

Severidade estimada: **CRITICAL**

---

## 🛡️ Recomendações

- Desabilitar WebDAV quando não necessário
- Implementar autenticação forte e controle de acesso adequado
- Restringir métodos HTTP (especialmente PUT e DELETE)
- Remover arquivos sensíveis armazenados indevidamente
- Atualizar serviços e aplicações desatualizadas
- Implementar monitoramento e hardening do servidor

---

## 📌 Conclusão

Neste laboratório foi confirmado que uma configuração inadequada de serviços web pode levar ao comprometimento completo do sistema, incluindo execução remota de comandos e exposição de credenciais sensíveis.

A cadeia de exploração evidencia a importância de boas práticas de configuração, atualização de serviços e controle rigoroso de acesso.
