# Time-based Conditional Access Policies

---

## 🇧🇷 Português

### Visão Geral

Este repositório contém políticas de **Acesso Condicional Baseadas em Tempo** para Microsoft 365, configuradas via **Microsoft Graph API**. As políticas permitem restringir ou bloquear o acesso a recursos corporativos com base em dias da semana e horários específicos, aumentando significativamente a segurança do ambiente.

---

### 📁 Arquivos

#### `CA-time-week.json`
Política de Acesso Condicional para **dias úteis (segunda a sexta-feira)**.

- **Dias aplicados:** Segunda, Terça, Quarta, Quinta e Sexta-feira
- **Horário:** 08:00 às 12:59 (horário de Brasília — *E. South America Standard Time*)
- **Comportamento:** A política está ativa somente dentro deste intervalo de tempo. Fora dele, o acesso pode ser liberado ou bloqueado conforme a regra configurada na política principal.

```json
{
  "conditions": {
    "times": {
      "includeAllTimes": false,
      "includeDays": {
        "daysOfWeek": ["monday","tuesday","wednesday","thursday","friday"],
        "timeZone": "E. South America Standard Time",
        "startTime": "08:00:00",
        "endTime": "12:59:59"
      }
    }
  }
}
```

#### `CA-time-weekend.json`
Política de Acesso Condicional para **fins de semana (sábado e domingo)**.

- **Dias aplicados:** Sábado e Domingo
- **Horário:** 00:00 às 23:59 (dia inteiro)
- **Comportamento:** Bloqueia ou exige MFA/controles adicionais para qualquer acesso realizado durante o fim de semana, proporcionando proteção total nos dias em que o acesso não é esperado.

```json
{
  "conditions": {
    "times": {
      "includeAllTimes": false,
      "includeDays": {
        "daysOfWeek": ["saturday","sunday"],
        "timeZone": "E. South America Standard Time",
        "startTime": "00:00:00",
        "endTime": "23:59:59"
      }
    }
  }
}
```

#### `comandos.txt`
Referência rápida com os **endpoints da Microsoft Graph API** necessários para listar, consultar e atualizar políticas de Acesso Condicional, além das permissões de aplicação requeridas.

---

### 🔧 Como Aplicar as Políticas

Utilize o **Microsoft Graph API** com o método `PATCH` para aplicar as condições de tempo a uma política existente:

```
PATCH https://graph.microsoft.com/beta/identity/conditionalAccess/policies/{policy_id}
```

Inclua o JSON correspondente no corpo da requisição.

**Permissões necessárias (Application):**
- `Application.Read.All`
- `Policy.Read.All`
- `Policy.ReadWrite.ConditionalAccess`

---

### ✅ Benefícios

| Benefício | Descrição |
|---|---|
| 🔒 **Redução da superfície de ataque** | Limita o acesso a horários de trabalho, bloqueando tentativas fora do horário esperado |
| 🕵️ **Detecção de anomalias** | Acessos fora dos horários configurados se tornam eventos suspeitos e auditáveis |
| 📋 **Conformidade regulatória** | Facilita o atendimento a normas como ISO 27001, LGPD e SOC 2 |
| 🌐 **Proteção contra ataques externos** | Dificulta ataques de força bruta e credential stuffing fora do horário comercial |
| ⚙️ **Flexibilidade via Graph API** | Permite automação e integração com pipelines de DevSecOps |
| 📊 **Auditoria e rastreabilidade** | Todos os eventos de acesso são registrados no Microsoft Entra ID Logs |

---

### 📌 Pré-requisitos

- Microsoft Entra ID (Azure AD) P1 ou P2
- Permissões de administrador de Acesso Condicional
- Token de acesso OAuth 2.0 para o Microsoft Graph API

---

---

## 🇺🇸 English

### Overview

This repository contains **Time-based Conditional Access Policies** for Microsoft 365, configured via the **Microsoft Graph API**. These policies allow organizations to restrict or block access to corporate resources based on specific days of the week and time windows, significantly enhancing the security posture of the environment.

---

### 📁 Files

#### `CA-time-week.json`
Conditional Access policy for **weekdays (Monday through Friday)**.

- **Days applied:** Monday, Tuesday, Wednesday, Thursday, and Friday
- **Time window:** 08:00 to 12:59 (Brasília timezone — *E. South America Standard Time*)
- **Behavior:** The policy is active only within this time window. Outside of it, access can be granted or denied depending on the main policy configuration.

```json
{
  "conditions": {
    "times": {
      "includeAllTimes": false,
      "includeDays": {
        "daysOfWeek": ["monday","tuesday","wednesday","thursday","friday"],
        "timeZone": "E. South America Standard Time",
        "startTime": "08:00:00",
        "endTime": "12:59:59"
      }
    }
  }
}
```

#### `CA-time-weekend.json`
Conditional Access policy for **weekends (Saturday and Sunday)**.

- **Days applied:** Saturday and Sunday
- **Time window:** 00:00 to 23:59 (all day)
- **Behavior:** Blocks or requires additional controls (e.g., MFA) for any access attempted during the weekend, providing full protection on days when access is not expected.

```json
{
  "conditions": {
    "times": {
      "includeAllTimes": false,
      "includeDays": {
        "daysOfWeek": ["saturday","sunday"],
        "timeZone": "E. South America Standard Time",
        "startTime": "00:00:00",
        "endTime": "23:59:59"
      }
    }
  }
}
```

#### `comandos.txt`
Quick reference with the **Microsoft Graph API endpoints** required to list, query, and update Conditional Access policies, along with the required application permissions.

---

### 🔧 How to Apply the Policies

Use the **Microsoft Graph API** with the `PATCH` method to apply time conditions to an existing policy:

```
PATCH https://graph.microsoft.com/beta/identity/conditionalAccess/policies/{policy_id}
```

Include the corresponding JSON in the request body.

**Required permissions (Application):**
- `Application.Read.All`
- `Policy.Read.All`
- `Policy.ReadWrite.ConditionalAccess`

---

### ✅ Benefits

| Benefit | Description |
|---|---|
| 🔒 **Reduced attack surface** | Limits access to business hours, blocking attempts made outside expected windows |
| 🕵️ **Anomaly detection** | Access outside configured hours becomes a suspicious, auditable event |
| 📋 **Regulatory compliance** | Helps meet standards such as ISO 27001, LGPD, SOC 2, and NIST |
| 🌐 **Protection against external attacks** | Mitigates brute-force and credential stuffing attacks outside business hours |
| ⚙️ **Flexibility via Graph API** | Enables automation and integration with DevSecOps pipelines |
| 📊 **Audit and traceability** | All access events are logged in Microsoft Entra ID Audit Logs |

---

### 📌 Prerequisites

- Microsoft Entra ID (Azure AD) P1 or P2
- Conditional Access Administrator permissions
- OAuth 2.0 access token for Microsoft Graph API

---

*Maintained by [Ch1c4n0](https://github.com/Ch1c4n0) — Dual MVP (Security & Azure) | MCT | Docker Captain*
