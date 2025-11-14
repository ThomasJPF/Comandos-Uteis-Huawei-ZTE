# 📘 Guia de Comandos Básicos NOC - Troubleshooting

## 🎯 Objetivo

Guia prático de comandos essenciais para troubleshooting em equipamentos OLT ZTE e Switches (Huawei/Datacom).

---

## 🔷 COMANDOS OLT ZTE C300/C320

### 📌 Navegação e Acesso

| Comando              | Descrição                                     |
| -------------------- | --------------------------------------------- |
| `enable`             | Entrar no modo privilegiado                   |
| `configure terminal` | Acessar o terminal de configuração            |
| `exit`               | Sair do modo/interface atual                  |
| `show this`          | Mostrar configurações da interface/modo atual |

---

### 📌 Verificação de VLANs

| Comando                   | Descrição                                                  | Exemplo              |
| ------------------------- | ---------------------------------------------------------- | -------------------- |
| `show vlan [VLAN-ID]`     | Ver onde a VLAN está configurada (portas, interfaces)      | `show vlan 3062`     |
| `show mac vlan [VLAN-ID]` | Ver endereços MAC aprendidos nessa VLAN (verifica tráfego) | `show mac vlan 3062` |

**💡 Uso prático:**

- Se a VLAN está funcionando, você verá MACs da Vport E do SmartGroup
- Se não aparecer MAC, problema pode estar na ONU ou uplink

---

### 📌 Gerenciamento de ONUs

| Comando                                                | Descrição                                              | Exemplo                                       |
| ------------------------------------------------------ | ------------------------------------------------------ | --------------------------------------------- |
| `show gpon onu by sn [SERIAL]`                         | Localizar onde uma ONU está provisionada (slot/pon/id) | `show gpon onu by sn ZTEGD7B31741`            |
| `show gpon onu state gpon-olt_[SLOT]/[PON]`            | Ver status de todas ONUs de uma PON (online/offline)   | `show gpon onu state gpon-olt_1/5/2`          |
| `show gpon onu detail-info gpon-onu_[SLOT]/[PON]:[ID]` | Informações detalhadas de uma ONU específica           | `show gpon onu detail-info gpon-onu_1/5/2:10` |
| `show pon onu uncfg`                                   | Ver ONUs não configuradas aguardando provisionamento   | `show pon onu uncfg`                          |
| `show running-config onu`                              | Ver configuração completa das ONUs                     | -                                             |

---

### 📌 Verificação de Sinal Óptico

| Comando                                                 | Descrição                                           | Exemplo                                        |
| ------------------------------------------------------- | --------------------------------------------------- | ---------------------------------------------- |
| `show pon power onu-rx gpon_olt-[SLOT]/[PON]`           | Ver potência de sinal RX de todas ONUs da PON       | `show pon power onu-rx gpon_olt-1/5/2`         |
| `show pon power attenuation gpon-onu_[SLOT]/[PON]:[ID]` | Ver atenuação de sinal de uma ONU específica        | `show pon power attenuation gpon-onu_1/5/2:10` |
| `show interface gpon-olt_[SLOT]/[PON]`                  | Ver informações da interface PON (TX, status, ONUs) | `show interface gpon-olt_1/5/2`                |

**📊 Valores de Referência RX:**

- ✅ **Normal:** -8 a -25 dBm
- ⚠️ **Atenção:** -25 a -27 dBm
- ❌ **Crítico:** < -27 dBm ou > -8 dBm

---

### 📌 Acesso a Interfaces

| Comando                                  | Descrição                                   | Exemplo                         |
| ---------------------------------------- | ------------------------------------------- | ------------------------------- |
| `interface gpon_olt-[SLOT]/[PON]`        | Acessar uma interface PON para configuração | `interface gpon_olt-1/5/2`      |
| `interface gpon_onu-[SLOT]/[PON]:[ID]`   | Acessar configuração de uma ONU específica  | `interface gpon_onu-1/5/2:10`   |
| `interface vport-[SLOT]/[PON].[ID]:1`    | Acessar a virtual port de uma ONU           | `interface vport-2/5/2.10:1`    |
| `interface smartgroup[ID]`               | Acessar interface de uplink (porta física)  | `interface smartgroup1`         |
| `pon-onu-mng gpon_onu-[SLOT]/[PON]:[ID]` | Acessar gerenciamento avançado da ONU       | `pon-onu-mng gpon_onu-1/5/2:10` |

---

### 📌 Configuração de Uplink/SmartGroup

| Comando                         | Descrição                                      | Exemplo                    |
| ------------------------------- | ---------------------------------------------- | -------------------------- |
| `interface smartgroup[ID]`      | Entrar na interface de uplink                  | `interface smartgroup1`    |
| `switchport vlan [VLAN-ID] tag` | Adicionar VLAN tagged no uplink                | `switchport vlan 3062 tag` |
| `show this`                     | Ver configuração da interface smartgroup atual | -                          |

---

### 📌 Informações do Sistema

| Comando               | Descrição                                      |
| --------------------- | ---------------------------------------------- |
| `show version`        | Ver versão do firmware e modelo do equipamento |
| `show card`           | Ver placas instaladas e status                 |
| `show equipment`      | Ver informações detalhadas de hardware         |
| `show temperature`    | Ver temperatura dos componentes                |
| `show running-config` | Ver toda configuração em execução              |

---

### 📌 Scripts de Provisionamento ONU NBS

#### ✅ COM QinQ (Dupla VLAN)

```bash
# Provisionar ONU na PON
interface gpon_olt-1/4/1
onu 15 type Bridge sn FHTT95D82678
exit

# Configurar ONU
interface gpon_onu-1/4/1:15
name NBS-LMC.10.JIP.2391-3187
sn-bind enable sn
tcont 1 profile PLANO-1G
gemport 1 tcont 1
exit

# Configurar Vport com QinQ (service-port other-all)
interface vport-1/4/1.15:1
service-port 1 other-all tls-vlan 3187
exit

# Configurar serviço na ONU
pon-onu-mng gpon_onu-1/4/1:15
service 1 gemport 1 ethuni eth_0/1
vlan port eth_0/1 mode transparent
exit
```

**📝 Explicação QinQ:**

- `other-all` = Aceita qualquer VLAN do cliente
- `tls-vlan 3187` = Encapsula com VLAN externa 3187
- Cliente → VLAN cliente → OLT adiciona VLAN 3187 → Rede

---

#### ✅ SEM QinQ (VLAN Única)

```bash
# Provisionar ONU na PON
interface gpon_olt-1/4/1
onu 15 type Bridge sn FHTT95D82678
exit

# Configurar ONU
interface gpon_onu-1/4/1:15
name NBS-LMC.10.JIP.2391-3187
sn-bind enable sn
tcont 1 profile PLANO-1G
gemport 1 tcont 1
exit

# Configurar Vport sem QinQ (user-vlan = vlan)
interface vport-1/4/1.15:1
service-port 1 user-vlan 3032 vlan 3032
exit

# Configurar serviço na ONU
pon-onu-mng gpon_onu-1/4/1:15
service 1 gemport 1 ethuni eth_0/1
vlan port eth_0/1 mode transparent
exit
```

**📝 Explicação SEM QinQ:**

- `user-vlan 3032 vlan 3032` = VLAN única (sem encapsulamento)
- Cliente → VLAN 3032 → Rede

---

### ⚠️ IMPORTANTE: Diferenças entre Unidades

**Antes de provisionar, SEMPRE verificar:**

```bash
# 1. Encontrar uma ONU NBS já provisionada na unidade
show gpon onu by sn [SERIAL-CONHECIDA]

# 2. Ver a configuração dela
show running-config onu

# 3. Verificar:
#    - type (Bridge, Router, etc)
#    - profile (PLANO-1G, PLANO-500M, etc)
#    - QinQ (other-all) ou VLAN única (user-vlan)
```

**Cada provedor/unidade pode ter:**

- Profiles diferentes (PLANO-1G, INTERNET-500M, etc)
- Types diferentes (Bridge, Router)
- Com ou sem QinQ

---

## 🔶 COMANDOS SWITCH HUAWEI

### 📌 Navegação e Acesso

| Comando        | Descrição                                     |
| -------------- | --------------------------------------------- |
| `system-view`  | Entrar no modo de configuração                |
| `quit`         | Sair do modo atual                            |
| `return`       | Voltar ao modo de visualização                |
| `display this` | Mostrar configurações da interface/modo atual |

---

### 📌 Verificação de VLANs

| Comando                              | Descrição                                   | Exemplo                         |
| ------------------------------------ | ------------------------------------------- | ------------------------------- |
| `display vlan [VLAN-ID]`             | Ver em quais portas a VLAN está configurada | `display vlan 3062`             |
| `display mac-address vlan [VLAN-ID]` | Ver endereços MAC aprendidos nessa VLAN     | `display mac-address vlan 3062` |
| `display vlan`                       | Listar todas VLANs configuradas             | -                               |

---

### 📌 Verificação de Interfaces

| Comando                                   | Descrição                                                 |
| ----------------------------------------- | --------------------------------------------------------- |
| `display interface description`           | Ver todas interfaces com suas descrições                  |
| `display interface brief`                 | Ver status resumido de todas interfaces (up/down)         |
| `display interface [INTERFACE]`           | Ver detalhes de uma interface específica (erros, tráfego) |
| `display interface GigabitEthernet 0/0/1` | Ver status detalhado da porta GE 0/0/1                    |

---

### 📌 Diagnóstico e Troubleshooting

| Comando                            | Descrição                                   |
| ---------------------------------- | ------------------------------------------- |
| `display current-configuration`    | Ver toda configuração em execução do switch |
| `display mac-address`              | Ver toda tabela MAC do switch               |
| `display arp`                      | Ver tabela ARP (IP x MAC)                   |
| `display interface counters error` | Ver contadores de erros em todas interfaces |
| `display cpu-usage`                | Ver uso de CPU                              |
| `display memory-usage`             | Ver uso de memória                          |

---

### 📌 Testes de Conectividade

| Comando            | Descrição                          | Exemplo               |
| ------------------ | ---------------------------------- | --------------------- |
| `ping [IP]`        | Testar conectividade para um IP    | `ping 10.10.10.1`     |
| `ping -c 100 [IP]` | Ping com 100 pacotes               | `ping -c 100 8.8.8.8` |
| `tracert [IP]`     | Rastreamento de rota até o destino | `tracert 8.8.8.8`     |

---

### 📌 Informações do Sistema

| Comando               | Descrição                             |
| --------------------- | ------------------------------------- |
| `display version`     | Ver versão do firmware e modelo       |
| `display device`      | Ver placas e módulos instalados       |
| `display temperature` | Ver temperatura do equipamento        |
| `display power`       | Ver status de fontes de alimentação   |
| `display fan`         | Ver status dos ventiladores           |
| `display transceiver` | Ver informações de SFPs/transceptores |

---

### 📌 Logs e Histórico

| Comando             | Descrição           |
| ------------------- | ------------------- |
| `display logbuffer` | Ver logs do sistema |
| `display alarm`     | Ver alarmes ativos  |
| `display trap`      | Ver traps SNMP      |

---

## 🔷 COMANDOS SWITCH DATACOM

### 📌 Navegação e Acesso

| Comando              | Descrição                      |
| -------------------- | ------------------------------ |
| `enable`             | Entrar no modo privilegiado    |
| `configure terminal` | Entrar no modo de configuração |
| `exit`               | Sair do modo atual             |
| `end`                | Voltar ao modo privilegiado    |

---

### 📌 Verificação de VLANs

| Comando                                 | Descrição                              | Exemplo                            |
| --------------------------------------- | -------------------------------------- | ---------------------------------- |
| `show vlan id [VLAN-ID]`                | Ver informações de uma VLAN específica | `show vlan id 3062`                |
| `show vlan`                             | Listar todas VLANs configuradas        | -                                  |
| `show mac address-table vlan [VLAN-ID]` | Ver endereços MAC de uma VLAN          | `show mac address-table vlan 3062` |

---

### 📌 Verificação de Interfaces

| Comando                               | Descrição                                               |
| ------------------------------------- | ------------------------------------------------------- |
| `show interfaces status`              | Ver status de todas interfaces (up/down, speed, duplex) |
| `show interfaces description`         | Ver descrições de todas interfaces                      |
| `show interfaces [INTERFACE]`         | Ver detalhes de uma interface específica                |
| `show interfaces gigabitethernet 1/1` | Ver status da porta GE 1/1                              |
| `show interfaces counters`            | Ver contadores de tráfego                               |
| `show interfaces counters errors`     | Ver contadores de erros                                 |

---

### 📌 Diagnóstico e Troubleshooting

| Comando                  | Descrição                    |
| ------------------------ | ---------------------------- |
| `show running-config`    | Ver configuração em execução |
| `show startup-config`    | Ver configuração salva       |
| `show mac address-table` | Ver toda tabela MAC          |
| `show arp`               | Ver tabela ARP               |
| `show ip route`          | Ver tabela de rotas          |

---

### 📌 Testes de Conectividade

| Comando           | Descrição            | Exemplo              |
| ----------------- | -------------------- | -------------------- |
| `ping [IP]`       | Testar conectividade | `ping 10.10.10.1`    |
| `traceroute [IP]` | Rastreamento de rota | `traceroute 8.8.8.8` |

---

### 📌 Informações do Sistema

| Comando            | Descrição                       |
| ------------------ | ------------------------------- |
| `show version`     | Ver versão do firmware e modelo |
| `show system`      | Ver informações do sistema      |
| `show environment` | Ver temperatura, fans, fontes   |
| `show logging`     | Ver logs do sistema             |

---

## 🎯 FLUXOGRAMA DE TROUBLESHOOTING

### Cenário 1: Cliente sem Internet

```
1. Verificar alarme no Zabbix
   ↓
2. OLT ZTE:
   show gpon onu by sn [SERIAL]        # Localizar ONU
   ↓
3. Verificar sinal:
   show pon power onu-rx gpon_olt-X/Y/Z
   ↓
4. Se sinal OK, verificar VLAN:
   show vlan [VLAN-ID]
   show mac vlan [VLAN-ID]
   ↓
5. Switch:
   display vlan [VLAN-ID]              # Huawei
   show vlan id [VLAN-ID]              # Datacom
   ↓
6. Verificar MAC no switch:
   display mac-address vlan [VLAN-ID]  # Huawei
   show mac address-table vlan [ID]    # Datacom
```

---

### Cenário 2: Link Down no Switch

```
1. Identificar porta no Zabbix
   ↓
2. Verificar status:
   display interface brief              # Huawei
   show interfaces status               # Datacom
   ↓
3. Ver detalhes da interface:
   display interface GigabitEthernet X  # Huawei
   show interfaces gigabitethernet X    # Datacom
   ↓
4. Verificar erros:
   display interface counters error     # Huawei
   show interfaces counters errors      # Datacom
   ↓
5. Verificar SFP (se fibra):
   display transceiver                  # Huawei
   show environment                     # Datacom
```

---

### Cenário 3: ONU Offline

```
1. Localizar ONU:
   show gpon onu by sn [SERIAL]
   ↓
2. Verificar status:
   show gpon onu state gpon-olt_X/Y/Z
   ↓
3. Verificar sinal:
   show pon power onu-rx gpon_olt-X/Y/Z
   ↓
4. Se sinal ruim (< -27 dBm):
   → Problema óptico (fibra, conector, ONU)
   ↓
5. Se sem sinal:
   → ONU desligada ou fibra rompida
   ↓
6. Ver ONUs não configuradas:
   show pon onu uncfg
   (verifica se ONU está tentando autenticar)
```

---

## 📋 CHECKLIST DE COMANDOS POR SITUAÇÃO

### ✅ VLAN não está funcionando

**OLT ZTE:**

```bash
show vlan [VLAN-ID]           # Ver onde está configurada
show mac vlan [VLAN-ID]       # Ver se tem tráfego (MACs)
interface smartgroup1
show this                      # Ver se VLAN está no uplink
```

**Switch Huawei:**

```bash
display vlan [VLAN-ID]
display mac-address vlan [VLAN-ID]
display interface brief       # Ver se porta trunk está up
```

**Switch Datacom:**

```bash
show vlan id [VLAN-ID]
show mac address-table vlan [VLAN-ID]
show interfaces status
```

---

### ✅ ONU com sinal fraco

```bash
show gpon onu by sn [SERIAL]
show pon power onu-rx gpon_olt-X/Y/Z
show pon power attenuation gpon-onu_X/Y/Z:ID
show gpon onu detail-info gpon-onu_X/Y/Z:ID
```

**Análise:**

- RX > -8 dBm: Muito forte (possível problema de saturação)
- RX -8 a -25 dBm: ✅ Normal
- RX -25 a -27 dBm: ⚠️ Limiar (monitorar)
- RX < -27 dBm: ❌ Fraco (problema na fibra)

---

### ✅ Provisionar ONU Nova

```bash
# 1. PRIMEIRO: Verificar perfil usado na unidade
show running-config onu | include [PROVEDOR]

# 2. Ver ONU não configurada
show pon onu uncfg

# 3. Usar script apropriado (COM ou SEM QinQ)
# Ver seção "Scripts de Provisionamento ONU NBS" acima
```

---

### ✅ Interface com erros

**Huawei:**

```bash
display interface counters error
display interface GigabitEthernet X/X/X
display transceiver interface GigabitEthernet X/X/X
```

**Datacom:**

```bash
show interfaces counters errors
show interfaces gigabitethernet X/X
show environment
```

---

## 🔍 COMANDOS DE DIAGNÓSTICO RÁPIDO

### OLT ZTE - Health Check Rápido

```bash
show card                     # Status das placas
show temperature             # Temperatura
show version                 # Versão do firmware
show pon onu uncfg           # ONUs aguardando provisão
show running-config | include alarm  # Verificar alarmes
```

### Switch Huawei - Health Check Rápido

```bash
display device               # Status do hardware
display interface brief      # Status portas
display cpu-usage            # Uso de CPU
display memory-usage         # Uso de memória
display alarm                # Alarmes ativos
```

### Switch Datacom - Health Check Rápido

```bash
show system                  # Info do sistema
show interfaces status       # Status portas
show environment            # Hardware (temp, fan, power)
show logging                # Logs recentes
```

---

## 💡 DICAS IMPORTANTES

### 1️⃣ Sempre documente

- Anote o comando executado
- Copie a saída relevante
- Registre horário e equipamento

### 2️⃣ Use | include para filtrar

```bash
# ZTE/Datacom
show running-config | include vlan

# Huawei
display current-configuration | include vlan
```

### 3️⃣ Cuidado ao entrar em modo de configuração

- `configure terminal` (ZTE/Datacom)
- `system-view` (Huawei)
- **Sempre use `exit` para sair, NUNCA desconecte no meio**

### 4️⃣ Perfis variam por unidade

- Sempre consultar ONU similar antes de provisionar
- Types: Bridge, Router, HGU
- Profiles: PLANO-1G, PLANO-500M, etc (variam!)

### 5️⃣ QinQ vs VLAN única

- **QinQ (other-all)**: VLAN do cliente + VLAN externa
- **VLAN única**: Apenas uma VLAN fixa
- Verificar padrão da unidade antes!

---

## 📞 ESCALAÇÃO

Se após usar os comandos básicos não resolver:

1. **Documentar tudo:**

   - Comandos executados
   - Saídas obtidas
   - Horário do problema
   - Equipamentos envolvidos

2. **Escalar para N2/N3** com:
   - Sintoma do problema
   - Verificações já realizadas
   - Logs e outputs relevantes

---

## 📚 APÊNDICE: Comandos que NÃO devem ser usados no NOC N1

❌ **NUNCA execute sem autorização:**

- Comandos de configuração (add, delete, set, no, undo)
- Reboot de equipamentos
- Alteração de VLANs
- Desprovisionamento de ONUs
- Mudanças em uplinks
- Save/write (salvar configuração)

✅ **Apenas comandos de visualização (show/display)**

---

**Versão:** 1.0  
**Data:** Outubro 2025  
**Autor:** ThomasJPF  
**Revisão:** Analista NOC + Documentação Técnica
