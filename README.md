# Credential Dump & Webshell Attack Lab

## 📌 Visão Geral

Projeto de laboratório de Segurança da Informação demonstrando exploração controlada de vulnerabilidades WebDAV, execução remota de comandos e análise de credenciais em ambiente isolado para fins educacionais.

O objetivo deste laboratório é evidenciar, de forma estruturada, como falhas de configuração e serviços expostos podem resultar no comprometimento completo de um servidor.

---

## 🎯 Objetivo

Demonstrar, em ambiente controlado, o ciclo completo de um teste de invasão envolvendo:

- Reconhecimento
- Enumeração de serviços
- Identificação de vulnerabilidades
- Exploração de WebDAV
- Upload e utilização de WebShell
- Execução remota de comandos (RCE)
- Enumeração interna
- Extração de hashes de credenciais

---

## 🖥️ Ambiente Utilizado

- Kali Linux (Máquina atacante)
- Metasploitable 2 (Máquina alvo vulnerável)
- Oracle VirtualBox
- Rede Host-Only (ambiente isolado e controlado)

---

## 🔎 Metodologia

### 1️⃣ Verificação de Conectividade
Validação da comunicação entre atacante e alvo via teste de ping.

### 2️⃣ Enumeração de Portas
Varredura com Nmap para identificação de serviços expostos e versões em execução.

### 3️⃣ Enumeração de Tecnologias Web
Identificação de servidor web e tecnologias utilizadas por meio de fingerprinting.

### 4️⃣ Descoberta de Diretórios
Enumeração de diretórios sensíveis utilizando wordlists.

### 5️⃣ Exploração do Serviço WebDAV
Identificação de diretório exposto (/dav) permitindo interação e manipulação de arquivos.

### 6️⃣ Upload e Execução de WebShell
Validação de execução remota de comandos através de webshell acessível via navegador/HTTP.

### 7️⃣ Enumeração Interna do Sistema
Coleta de informações do sistema comprometido (usuário, versão do sistema, diretórios).

### 8️⃣ Extração de Credenciais
Identificação e leitura de arquivo contendo hashes de senha (shadow_copy), expondo credenciais locais.

---

## 🚨 Vulnerabilidades Identificadas

- WebDAV habilitado sem autenticação adequada
- Permissão de upload de arquivos maliciosos
- Execução remota de comandos via WebShell
- Exposição de hashes de senha
- Armazenamento inseguro de arquivo sensível contendo credenciais
- Serviços desatualizados

---

## 🔴 Impacto

A exploração resultou em:

- Comprometimento do servidor web
- Execução remota de comandos no contexto do serviço (www-data)
- Exposição de credenciais locais
- Possibilidade de escalonamento de privilégios
- Risco de comprometimento total do host

Severidade estimada: **CRITICAL**

---

## 🛡️ Recomendações

- Desabilitar WebDAV quando não necessário
- Implementar autenticação e controle de acesso adequado
- Restringir métodos HTTP (especialmente PUT e DELETE)
- Remover arquivos sensíveis armazenados indevidamente
- Atualizar serviços e aplicações desatualizadas
- Implementar monitoramento de integridade de arquivos
- Aplicar políticas de hardening no servidor

---

## 📊 Linha do Tempo do Ataque

1. Identificação do host ativo
2. Enumeração de portas e serviços expostos
3. Identificação de serviço WebDAV habilitado
4. Descoberta de diretórios sensíveis
5. Upload/uso de WebShell
6. Execução remota de comandos
7. Enumeração interna
8. Extração de hashes de credenciais

---

## 📌 Conclusão

O laboratório demonstrou como uma cadeia de vulnerabilidades e más configurações pode levar ao comprometimento completo de um sistema. A combinação de serviços desprotegidos, exposição de arquivos sensíveis e ausência de controles adequados resultou em um cenário de risco crítico.

Este projeto foi desenvolvido exclusivamente para fins educacionais, em ambiente isolado e controlado, com o objetivo de estudo e aprimoramento técnico em Segurança da Informação.

---

## ⚠️ Aviso

Este laboratório foi executado em ambiente virtual isolado. Nenhum sistema real foi impactado. As técnicas demonstradas são utilizadas apenas para fins educacionais e de estudo em segurança ofensiva.
