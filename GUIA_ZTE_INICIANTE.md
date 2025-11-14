# 🔷 Guia Completo OLT ZTE C300/C320 - Para Iniciantes

## 🎯 Bem-vindo ao Mundo das OLTs!

Olá! Se você está aqui, provavelmente vai trabalhar com **OLTs ZTE** pela primeira vez. Não se preocupe, vamos explicar **TUDO** do zero, com muita calma e exemplos práticos.

### 🤔 O que é uma OLT?

**OLT** significa **Optical Line Terminal** (Terminal de Linha Óptica). Mas o que isso significa na prática?

**Analogia simples:** 

Imagine que a internet é como o sistema de água da sua cidade:
- A **estação de tratamento** de água distribui água para as casas
- A **OLT** é como essa estação - ela distribui internet via fibra óptica
- Cada **casa** tem uma caixa d'água (a **ONU**)
- Os **canos** são as fibras ópticas

**Em resumo:**
- **OLT (ZTE C300/C320)** = Central que distribui internet via fibra
- **ONU/ONT** = Equipamento na casa do cliente que recebe a fibra
- **PON** = A "rua" de fibra onde várias ONUs estão conectadas
- **Fibra Óptica** = O "cano" que leva os dados

---

## 📚 Glossário - Termos que Você Precisa Saber

Antes de começar, vamos entender os termos que você vai ouvir TODO DIA:

| Termo | O que significa? | Analogia Simples |
|-------|------------------|------------------|
| **OLT** | Equipamento central que distribui internet | Estação de tratamento de água |
| **ONU/ONT** | Equipamento na casa do cliente | Caixa d'água de cada casa |
| **PON** | Interface/porta da OLT (uma "rua" de fibra) | Uma rua com várias casas |
| **Slot** | "Gaveta" onde fica a placa PON na OLT | Andar de um prédio |
| **Serial (SN)** | "RG" da ONU (identifica cada uma) | CPF da ONU |
| **VLAN** | "Etiqueta colorida" que separa tráfegos | Envelope colorido do correio |
| **MAC Address** | Endereço único de um equipamento na rede | Chassi de um carro |
| **dBm** | Medida de potência do sinal óptico | "Pressão da água no cano" |
| **RX** | Sinal que CHEGA na OLT (receive) | Água chegando na estação |
| **TX** | Sinal que SAI da OLT (transmit) | Água saindo da estação |
| **Gemport** | Canal de comunicação dentro da PON | Faixa de uma rodovia |
| **Tcont** | Container de tráfego (agrupa gemports) | Caminhão que leva vários pacotes |
| **Vport** | Porta virtual da ONU | Porta USB virtual |
| **QinQ** | Dupla VLAN (VLAN dentro de VLAN) | Envelope dentro de envelope |
| **Uplink** | Porta que conecta OLT ao resto da rede | Rodovia que sai da cidade |
| **SmartGroup** | Grupo de portas de uplink (ZTE) | Conjunto de rodovias |
| **Profile** | Configuração de velocidade da ONU | Plano de internet (500M, 1G, etc) |

---

## 🔑 Como Acessar a OLT ZTE

### Método 1: Telnet (Mais Comum)

**O que você precisa:**
- IP da OLT
- Usuário e senha

**Passo a passo:**

1. Abra o CMD (Windows + R, digite `cmd`)

2. Digite:
```cmd
telnet [IP-DA-OLT]
```

**Exemplo:**
```cmd
telnet 10.20.30.100
```

3. Vai aparecer:
```
Login: _
```

4. Digite o usuário (geralmente `admin`) e aperte Enter

5. Digite a senha e aperte Enter

6. Você vai ver:
```
OLT-NOME#
```

✅ **Parabéns! Você está dentro da OLT!**

---

### Método 2: SSH (Mais Seguro)

**Usando PuTTY:**

1. Baixe o PuTTY: https://www.putty.org/
2. Abra o PuTTY
3. Em "Host Name" coloque o IP da OLT
4. Em "Connection Type" escolha **SSH**
5. Clique em **Open**
6. Digite usuário e senha

---

## 🎮 Modos de Operação da OLT ZTE

A OLT ZTE tem **3 níveis** de acesso, como níveis de um prédio:

### 📖 Entendendo os Modos

| Modo | Prompt | O que você pode fazer? | Como entrar? |
|------|--------|------------------------|--------------|
| **Usuário** | `OLT-NOME>` | Apenas ver informações básicas | Automático ao logar |
| **Privilegiado** | `OLT-NOME#` | Ver tudo, mas não mudar | Digite `enable` |
| **Configuração** | `OLT-NOME(config)#` | Mudar configurações | Digite `configure terminal` |

**Analogia:**
- **Modo Usuário:** Você está na **recepção** do prédio (área pública)
- **Modo Privilegiado:** Você tem **acesso aos andares** (pode ver tudo)
- **Modo Configuração:** Você é o **síndico** (pode mudar as coisas)

---

### 🎯 Exemplo Prático de Navegação

```bash
# 1. Você loga e está no modo usuário
OLT-NOME>

# 2. Entrar no modo privilegiado
OLT-NOME> enable
OLT-NOME#

# 3. Entrar no modo de configuração
OLT-NOME# configure terminal
OLT-NOME(config)#

# 4. Voltar um nível
OLT-NOME(config)# exit
OLT-NOME#

# 5. Sair completamente
OLT-NOME# exit
Connection closed by foreign host.
```

> **⚠️ IMPORTANTE NO NOC N1:** Você só deve usar comandos de **visualização** (show). NUNCA entre no modo de configuração sem autorização!

---

## 📝 Comandos Essenciais - Categoria por Categoria

### 📌 1. Comandos de Navegação Básica

#### Comando: `enable`

**O que faz?**
Entra no modo privilegiado (você precisa disso para ver informações detalhadas).

**Quando usar?**
Logo após fazer login.

**Exemplo:**
```bash
OLT-NOME> enable
OLT-NOME#
```

---

#### Comando: `configure terminal`

**O que faz?**
Entra no modo de configuração.

**Quando usar?**
❌ **NUNCA no NOC N1 sem autorização!** Este modo permite MUDAR configurações!

---

#### Comando: `exit`

**O que faz?**
Volta um nível ou sai da OLT.

**Exemplo:**
```bash
# Saindo do modo de configuração
OLT-NOME(config)# exit
OLT-NOME#

# Saindo completamente
OLT-NOME# exit
```

> **💡 Dica:** SEMPRE use `exit` para sair. NUNCA feche a janela no meio de uma sessão!

---

#### Comando: `show this`

**O que faz?**
Mostra a configuração da interface/modo onde você está.

**Quando usar?**
Quando você está dentro de uma interface e quer ver suas configurações.

**Exemplo:**
```bash
OLT-NOME(config)# interface gpon_olt-1/5/2
OLT-NOME(config-if)# show this
```

**O que você vai ver:**
```
interface gpon_olt-1/5/2
  description "PON para Bairro X"
  onu auto-discover enable
  no shutdown
```

✅ Mostra todas as configurações dessa PON específica!

---

### 📌 2. Localizando ONUs

#### Comando: `show gpon onu by sn [SERIAL]`

**O que faz?**
Localiza onde uma ONU está provisionada usando o número de série (SN).

**Para que serve?**
- Encontrar em qual PON uma ONU específica está
- Ver o ID da ONU
- Descobrir slot/PON/ID

**Anatomia do Serial:**
- Formato: **4 letras + 8 dígitos**
- Exemplo: `ZTEG12345678`
- `ZTEG` = Fabricante (ZTE Gpon)
- `12345678` = Número único

**Sintaxe:**
```bash
show gpon onu by sn [SERIAL]
```

**Exemplo:**
```bash
show gpon onu by sn ZTEGD7B31741
```

**O que você vai ver:**
```
Number of ONUs: 1
gpon_onu-1/5/2:10
```

**Interpretando:**
```
gpon_onu-1/5/2:10
         │ │ │ └─ ONU ID = 10
         │ │ └─── PON = 2
         │ └───── Card = 5
         └─────── Slot (Frame) = 1
```

**Leitura:** "A ONU está no Slot 1, Card 5, PON 2, com ID 10"

**Analogia:**
- **Slot 1** = Prédio 1
- **Card 5** = Andar 5
- **PON 2** = Apartamento 2
- **ID 10** = Morador 10

---

#### Comando: `show pon onu uncfg`

**O que faz?**
Mostra ONUs **não configuradas** (descobertas automaticamente pela OLT mas não provisionadas ainda).

**Para que serve?**
- Ver ONUs novas esperando para serem ativadas
- Pegar o serial de uma ONU que acabou de ser conectada

**Sintaxe:**
```bash
show pon onu uncfg
```

**O que você vai ver:**
```
OnuIndex     Sn          State       LastDownCause     Reason
1/5/2:2      ZTEG12345678 Enable      NA                Auto-find success
1/5/3:1      FHTT87654321 Enable      NA                Auto-find success
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **OnuIndex (1/5/2:2)** | Onde a ONU foi detectada (Slot/Card/PON:ID) |
| **Sn (ZTEG12345678)** | Número de série da ONU |
| **State (Enable)** | ONU está online e detectada |
| **LastDownCause** | Última causa de queda (NA = não aplicável) |
| **Reason** | Motivo (Auto-find = descoberta automaticamente) |

✅ Essas ONUs estão PRONTAS para serem provisionadas!

---

#### Comando: `show gpon onu state gpon-olt_[SLOT]/[PON]`

**O que faz?**
Mostra o **status** (online/offline) de TODAS as ONUs de uma PON específica.

**Para que serve?**
- Ver quantas ONUs estão online em uma PON
- Identificar ONUs offline
- Ter uma visão geral da PON

**Sintaxe:**
```bash
show gpon onu state gpon-olt_[SLOT]/[CARD]/[PON]
```

**Exemplo:**
```bash
show gpon onu state gpon-olt_1/5/2
```

**O que você vai ver:**
```
OnuIndex  State       Phase           ConfigState
1/5/2:1   online      working         success
1/5/2:2   online      working         success
1/5/2:3   offline     LOS             success
1/5/2:4   online      working         success
1/5/2:5   online      working         success
```

**Interpretando:**

| Campo | O que significa? | Valores Possíveis |
|-------|------------------|-------------------|
| **OnuIndex** | ID da ONU | Slot/Card/PON:ID |
| **State** | Status atual | `online`, `offline` |
| **Phase** | Fase de operação | `working` (funcionando), `LOS` (sem sinal), `dying-gasp` (desligando) |
| **ConfigState** | Estado da configuração | `success` (OK), `failed` (falhou) |

**Status mais comuns:**

| State | Phase | O que significa? |
|-------|-------|------------------|
| ✅ `online` | `working` | ONU funcionando normalmente |
| ❌ `offline` | `LOS` | ONU sem sinal (Loss of Signal) - fibra desconectada ou ONU desligada |
| ⚠️ `offline` | `dying-gasp` | ONU acabou de desligar |
| ❌ `offline` | `power-off` | ONU sem energia |

---

#### Comando: `show gpon onu detail-info gpon-onu_[SLOT]/[PON]:[ID]`

**O que faz?**
Mostra **TODAS** as informações detalhadas de uma ONU específica.

**Para que serve?**
- Ver tipo, modelo, versão, uptime, sinal, etc.
- Diagnóstico completo de uma ONU

**Sintaxe:**
```bash
show gpon onu detail-info gpon-onu_[SLOT]/[CARD]/[PON]:[ID]
```

**Exemplo:**
```bash
show gpon onu detail-info gpon-onu_1/5/2:10
```

**O que você vai ver:**
```
ONU interface:         gpon-onu_1/5/2:10
Name:                  NBS-Cliente-1234
Description:           Cliente Exemplo Ltda
SN:                    ZTEGD7B31741
Password:              0x00000000
Status:                online
Cause of last going offline: LOS
Time since last went offline: 2 days 5 hour(s) 30 minute(s) 15 second(s)
ONU type:              Bridge
Equipment ID:          F601
Software version:      V6.0.10
Firmware version:      V6.0.10
IP address:            10.10.10.100
FEC state:             disabled
ONU distance:          2544 m
ONU RX/TX power:       -21.25 dBm / 2.31 dBm
Uplink interface:      vport-1/5/2.10:1
```

**Interpretando os campos mais importantes:**

| Campo | O que significa? | Exemplo |
|-------|------------------|---------|
| **Name** | Nome dado à ONU | Geralmente identifica o cliente |
| **SN** | Serial da ONU | ZTEGD7B31741 |
| **Status** | Online ou offline | `online` ✅ |
| **Cause of last going offline** | Por que caiu da última vez | `LOS` (perda de sinal) |
| **Time since last went offline** | Há quanto tempo caiu | 2 dias atrás |
| **ONU type** | Tipo de ONU | `Bridge` (mais comum), `Router`, `HGU` |
| **Equipment ID** | Modelo da ONU | F601, F670, etc |
| **Software version** | Versão do firmware | V6.0.10 |
| **ONU distance** | Distância da OLT | 2544 metros (2.5 km) |
| **ONU RX/TX power** | Potência de sinal | RX: -21.25 dBm (recebe), TX: 2.31 dBm (envia) |

**📊 Valores de Referência RX (Sinal que CHEGA na ONU):**

| RX (dBm) | Qualidade | O que fazer? |
|----------|-----------|--------------|
| **-8 a -25 dBm** | ✅ Excelente/Bom | Nada, está perfeito! |
| **-25 a -27 dBm** | ⚠️ Limiar | Monitorar, pode piorar |
| **< -27 dBm** | ❌ Ruim | Problema na fibra, limpar, verificar emendas |
| **> -8 dBm** | ❌ Muito forte | Excesso de sinal pode danificar a ONU |

**No exemplo acima:**
- RX = **-21.25 dBm** ✅ **ÓTIMO SINAL!**

---

### 📌 3. Verificando Sinal Óptico

#### Comando: `show pon power onu-rx gpon_olt-[SLOT]/[PON]`

**O que faz?**
Mostra a **potência de sinal RX** (recebido) de **TODAS** as ONUs de uma PON.

**Para que serve?**
- Ver de uma vez só quais ONUs estão com sinal fraco
- Identificar problemas de fibra rapidamente

**Sintaxe:**
```bash
show pon power onu-rx gpon_olt-[SLOT]/[CARD]/[PON]
```

**Exemplo:**
```bash
show pon power onu-rx gpon_olt-1/5/2
```

**O que você vai ver:**
```
OnuIndex       RxOltPower(dBm)
-----------------------------
gpon-onu_1/5/2:1    -19.50
gpon-onu_1/5/2:2    -21.25
gpon-onu_1/5/2:3    -28.10  ← PROBLEMA!
gpon-onu_1/5/2:4    -18.75
gpon-onu_1/5/2:5    -22.30
gpon-onu_1/5/2:10   -21.25
```

**Interpretando:**

✅ **ONUs 1, 2, 4, 5, 10:** Sinal bom (-18 a -22 dBm)  
❌ **ONU 3:** Sinal crítico (-28.10 dBm) - Problema na fibra!

**Ação:** Cliente da ONU 3 provavelmente está com internet lenta ou caindo. Verificar fibra, conectores, emendas.

---

#### Comando: `show pon power attenuation gpon-onu_[SLOT]/[PON]:[ID]`

**O que faz?**
Mostra a **atenuação** (perda de sinal) entre OLT e ONU.

**Para que serve?**
- Ver quanta "força" o sinal está perdendo no caminho
- Diagnosticar qualidade da fibra

**Sintaxe:**
```bash
show pon power attenuation gpon-onu_[SLOT]/[CARD]/[PON]:[ID]
```

**Exemplo:**
```bash
show pon power attenuation gpon-onu_1/5/2:10
```

**O que você vai ver:**
```
ONU                     attenuation(dB)
gpon-onu_1/5/2:10       23.56
```

**Interpretando:**

| Atenuação | Qualidade | O que significa? |
|-----------|-----------|------------------|
| **15-25 dB** | ✅ Normal | Perda esperada em instalações típicas |
| **25-28 dB** | ⚠️ Alto | Muitas emendas ou fibra longa |
| **> 28 dB** | ❌ Crítico | Problema sério: conector sujo, emenda ruim, dobra na fibra |

**No exemplo:** 23.56 dB = ✅ **Normal**

---

#### Comando: `show interface gpon-olt_[SLOT]/[PON]`

**O que faz?**
Mostra informações gerais da interface PON (TX, status, ONUs conectadas).

**Para que serve?**
- Ver potência TX da PON (sinal que a OLT ENVIA)
- Ver quantas ONUs estão conectadas
- Status da PON (up/down)

**Sintaxe:**
```bash
show interface gpon-olt_[SLOT]/[CARD]/[PON]
```

**Exemplo:**
```bash
show interface gpon-olt_1/5/2
```

**O que você vai ver:**
```
Interface: gpon-olt_1/5/2
Status:    up
TX Power:  2.50 dBm
ONUs:      15 online, 2 offline
Description: PON Bairro Centro
```

**Interpretando TX Power:**

| TX (dBm) | Status |
|----------|--------|
| **2 a 5 dBm** | ✅ Normal |
| **< 2 dBm** | ❌ Sinal baixo - problema no SFP/módulo óptico |
| **> 5 dBm** | ⚠️ Sinal muito forte (raro) |

---

### 📌 4. Trabalhando com VLANs

#### O que é VLAN?

**VLAN** (Virtual LAN) é como uma "etiqueta colorida" que separa tráfegos diferentes na mesma rede física.

**Analogia:** Imagine um correio:
- Cartas com envelope **vermelho** = Urgente (VLAN 10)
- Cartas com envelope **azul** = Normal (VLAN 20)
- Cartas com envelope **verde** = Propaganda (VLAN 30)

Todos passam pelo mesmo caminhão (cabo de rede), mas são separados pela "cor" (VLAN).

---

#### Comando: `show vlan [VLAN-ID]`

**O que faz?**
Mostra onde uma VLAN específica está configurada (em quais portas/interfaces).

**Para que serve?**
- Ver se uma VLAN existe
- Ver em quais portas ela está
- Ver se está tagged (marcada) ou untagged (sem marca)

**Sintaxe:**
```bash
show vlan [VLAN-ID]
```

**Exemplo:**
```bash
show vlan 3062
```

**O que você vai ver:**
```
VLAN ID:       3062
VLAN Name:     VLAN_3062
VLAN Type:     Static
Status:        Active

Ports:
  smartgroup1          tagged
  vport-1/5/2.10:1     untagged
  vport-1/5/2.11:1     untagged
  vport-1/5/3.5:1      untagged
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **VLAN ID** | Número da VLAN |
| **Status: Active** | VLAN está funcionando |
| **smartgroup1 - tagged** | No uplink (saída para rede), a VLAN vai COM etiqueta |
| **vport - untagged** | Na ONU, a VLAN vai SEM etiqueta (transparente para o cliente) |

**Entendendo Tagged vs Untagged:**

- **Tagged:** A "etiqueta" (número da VLAN) vai junto com os dados
  - Usado em **troncos** (uplinks) entre equipamentos
  - Como enviar uma carta COM envelope

- **Untagged:** A "etiqueta" é removida
  - Usado em portas de **acesso** (clientes)
  - Como tirar a carta do envelope antes de entregar

---

#### Comando: `show mac vlan [VLAN-ID]`

**O que faz?**
Mostra os **endereços MAC** aprendidos em uma VLAN.

**Para que serve?**
- Ver se há tráfego na VLAN (se há MACs, há tráfego)
- Identificar qual porta/ONU está usando a VLAN
- Troubleshooting de conectividade

**Sintaxe:**
```bash
show mac vlan [VLAN-ID]
```

**Exemplo:**
```bash
show mac vlan 3062
```

**O que você vai ver:**
```
MAC Address        VLAN    Port                Type
-------------------------------------------------
00:11:22:33:44:55  3062    vport-1/5/2.10:1    dynamic
AA:BB:CC:DD:EE:FF  3062    vport-1/5/2.10:1    dynamic
11:22:33:44:55:66  3062    smartgroup1         dynamic
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **MAC Address** | Endereço físico de um equipamento |
| **VLAN** | Em qual VLAN esse MAC foi visto |
| **Port** | Por onde esse MAC está acessando |
| **Type: dynamic** | Aprendido automaticamente (não configurado manualmente) |

**Análise:**

✅ **Há MACs na vport E no smartgroup** = VLAN funcionando!
- MACs na **vport** = Equipamentos do cliente (roteador, computador)
- MACs no **smartgroup** = Equipamentos do core da rede

❌ **Não há MACs** = Problema! VLAN não está passando tráfego.

---

### 📌 5. Informações do Sistema

#### Comando: `show version`

**O que faz?**
Mostra versão do firmware, modelo da OLT, uptime.

**Sintaxe:**
```bash
show version
```

**O que você vai ver:**
```
System Description: ZTE ZXA10 C300 OLT
System Software Version: V2.1.0
System Uptime: 150 days, 12 hours, 30 minutes
```

---

#### Comando: `show card`

**O que faz?**
Mostra as **placas instaladas** na OLT e seus status.

**Sintaxe:**
```bash
show card
```

**O que você vai ver:**
```
SlotNo  CardType        Status     Detail
1/1     SCXN            active     OK
1/2     SCXN            active     OK
1/5     GTGH            active     OK (PON Card - 16 PONs)
1/6     GTGH            active     OK (PON Card - 16 PONs)
```

**Interpretando:**

- **SCXN:** Placa de controle/uplink
- **GTGH:** Placa PON (tem as portas GPON)
- **Status: active:** Placa funcionando

---

#### Comando: `show temperature`

**O que faz?**
Mostra temperatura dos componentes da OLT.

**Sintaxe:**
```bash
show temperature
```

**Valores normais:** 40-60°C  
⚠️ **Atenção:** > 70°C  
❌ **Crítico:** > 80°C

---

#### Comando: `show running-config`

**O que faz?**
Mostra **TODA** a configuração em execução da OLT.

**Sintaxe:**
```bash
show running-config
```

⚠️ **ATENÇÃO:** Este comando gera MUITO texto (milhares de linhas)!

**Melhor usar com filtros:**

```bash
# Ver apenas ONUs
show running-config | include onu

# Ver apenas VLANs
show running-config | include vlan

# Ver configuração de uma interface específica
show running-config interface gpon_olt-1/5/2
```

---

## 🛠️ Acessando Interfaces

### 🤔 O que são Interfaces?

**Interface** é uma "porta" ou "conexão" na OLT. Para configurar algo, você precisa "entrar" na interface.

**Analogia:** É como entrar em um cômodo específico da casa para arrumar algo.

---

### Tipos de Interfaces na ZTE

| Tipo | O que é? | Sintaxe | Exemplo |
|------|----------|---------|---------|
| **gpon_olt** | Interface PON (porta física) | `interface gpon_olt-[S]/[C]/[P]` | `interface gpon_olt-1/5/2` |
| **gpon_onu** | Interface da ONU específica | `interface gpon_onu-[S]/[C]/[P]:[ID]` | `interface gpon_onu-1/5/2:10` |
| **vport** | Porta virtual da ONU | `interface vport-[S]/[C]/[P].[ID]:1` | `interface vport-1/5/2.10:1` |
| **smartgroup** | Grupo de uplink | `interface smartgroup[N]` | `interface smartgroup1` |

---

### 🎯 Exemplo: Entrando em uma Interface PON

```bash
OLT-NOME# configure terminal
OLT-NOME(config)# interface gpon_olt-1/5/2
OLT-NOME(config-if)#
```

Agora você está "dentro" da PON 1/5/2 e pode:
- Ver configurações: `show this`
- Adicionar ONUs (se autorizado)
- Voltar: `exit`

---

### 🎯 Exemplo: Acessando Gerenciamento da ONU

```bash
OLT-NOME# configure terminal
OLT-NOME(config)# pon-onu-mng gpon_onu-1/5/2:10
OLT-NOME(config-gpon-onu-mng)#
```

Agora você está no gerenciamento avançado da ONU 10 e pode ver serviços, VLANs, etc.

> **⚠️ LEMBRE-SE:** No NOC N1, você raramente precisa entrar em interfaces. Use apenas comandos `show`!

---

## 🔧 Cenários Práticos do Dia a Dia

### 📞 Cenário 1: Cliente Sem Internet - Checklist Completo

**Sintoma:** Cliente liga dizendo que não tem internet.

**Passo a passo:**

```bash
# PASSO 1: Pegar o serial da ONU do ticket
# Exemplo: ZTEGD7B31741

# PASSO 2: Localizar a ONU
show gpon onu by sn ZTEGD7B31741

# OUTPUT esperado:
# gpon_onu-1/5/2:10

# PASSO 3: Ver se a ONU está online
show gpon onu state gpon-olt_1/5/2

# Procure pela linha da ONU 10:
# 1/5/2:10   online   working   success  ← OK!
# 1/5/2:10   offline  LOS       success  ← PROBLEMA!

# PASSO 4: Ver detalhes da ONU
show gpon onu detail-info gpon-onu_1/5/2:10

# Olhe:
# - Status: online ou offline?
# - Cause of last going offline: LOS? power-off?
# - ONU RX/TX power: Valores bons?

# PASSO 5: Ver sinal
show pon power onu-rx gpon_olt-1/5/2

# Procure pela ONU 10:
# gpon-onu_1/5/2:10    -21.25  ← BOM!
# gpon-onu_1/5/2:10    -28.50  ← RUIM!

# PASSO 6: Ver se VLAN está passando tráfego
# (Pegue a VLAN do cliente no sistema)
show mac vlan 3062

# Deve aparecer MAC da vport da ONU E do smartgroup
```

**Diagnóstico:**

| Situação | Causa | Solução |
|----------|-------|---------|
| ONU offline + LOS + sem sinal | Fibra desconectada ou ONU desligada | Solicitar visita técnica |
| ONU online + sinal bom + sem MAC na VLAN | Problema de VLAN/configuração | Escalar para N2 |
| ONU online + sinal fraco (-27 dBm ou pior) | Fibra com problema | Solicitar limpeza/reparo de fibra |
| ONU offline + power-off | ONU sem energia | Cliente verificar tomada |

---

### 📞 Cenário 2: ONU Não Aparece no Sistema

**Sintoma:** Técnico instalou fibra na casa do cliente, mas ONU não autentica.

**Passo a passo:**

```bash
# PASSO 1: Ver ONUs não configuradas (descobertas mas não provisionadas)
show pon onu uncfg

# Se a ONU aparecer aqui:
# 1/5/2:15   ZTEG12345678   Enable   NA   Auto-find success

# → ONU foi descoberta! Apenas não está provisionada.
# → Solicitar provisionamento para N2

# Se NÃO aparecer:
# → ONU não está sendo "vista" pela OLT
# → Possíveis causas:
#    1. Fibra desconectada
#    2. ONU desligada
#    3. ONU com defeito
#    4. PON da OLT com problema
```

---

### 📞 Cenário 3: Internet Lenta - Verificando Sinal

**Sintoma:** Cliente reclama que internet está lenta.

**Passo a passo:**

```bash
# PASSO 1: Localizar ONU
show gpon onu by sn ZTEGD7B31741
# gpon_onu-1/5/2:10

# PASSO 2: Ver sinal
show pon power onu-rx gpon_olt-1/5/2
# gpon-onu_1/5/2:10    -26.80  ← NO LIMIAR!

# PASSO 3: Ver atenuação
show pon power attenuation gpon-onu_1/5/2:10
# attenuation(dB): 27.50  ← ALTO!

# PASSO 4: Ver detalhes da ONU
show gpon onu detail-info gpon-onu_1/5/2:10
# ONU RX/TX power: -26.80 dBm / 2.31 dBm
# ONU distance: 5200 m  ← Distante
```

**Análise:**
- Sinal no limite (-26.80 dBm)
- Atenuação alta (27.50 dB)
- Distância grande (5.2 km)

**Possíveis causas:**
1. Fibra com muitas emendas
2. Conectores sujos
3. Dobras na fibra

**Solução:** Solicitar visita técnica para:
- Limpar conectores
- Verificar emendas
- Medir link com power meter

---

### 📞 Cenário 4: Vários Clientes Offline na Mesma PON

**Sintoma:** Alarmes de múltiplas ONUs offline na mesma PON.

**Passo a passo:**

```bash
# PASSO 1: Ver status geral da PON
show gpon onu state gpon-olt_1/5/2

# Se TODAS as ONUs estão offline:
# → Problema na PON!
# → Possíveis causas:
#    1. Splitter com defeito
#    2. Fibra de alimentação rompida
#    3. SFP da OLT com defeito

# PASSO 2: Ver interface da PON
show interface gpon-olt_1/5/2

# Se TX Power = 0 ou muito baixo:
# → SFP com problema
# → Escalar para N2 substituir SFP

# Se TX Power = Normal mas ONUs offline:
# → Problema no campo (splitter, fibra)
# → Escalar para supervisão de campo
```

---

### 📞 Cenário 5: Provisionar ONU Nova (COM AUTORIZAÇÃO)

**⚠️ IMPORTANTE:** Apenas execute se você tem autorização e treinamento!

**Antes de começar:**

1. **SEMPRE** verifique como outras ONUs estão provisionadas na mesma unidade:

```bash
# Ver configuração de uma ONU similar
show running-config onu | include [PROVEDOR]
```

2. Identifique:
   - Type: Bridge, Router ou HGU?
   - Profile: PLANO-1G, PLANO-500M, etc?
   - QinQ ou VLAN única?

---

**Script EXEMPLO (pode variar por unidade):**

```bash
# 1. Ver a ONU não configurada e pegar o serial
show pon onu uncfg
# 1/5/2:15   FHTT12345678   Enable   NA   Auto-find success

# 2. Provisionar na PON
configure terminal
interface gpon_olt-1/5/2
onu 15 type Bridge sn FHTT12345678
exit

# 3. Configurar a ONU
interface gpon_onu-1/5/2:15
name CLIENTE-NOME-1234
sn-bind enable sn
tcont 1 profile PLANO-1G
gemport 1 tcont 1
exit

# 4. Configurar Vport (VLAN)
# SEM QinQ (VLAN única):
interface vport-1/5/2.15:1
service-port 1 user-vlan 3062 vlan 3062
exit

# COM QinQ (Dupla VLAN):
interface vport-1/5/2.15:1
service-port 1 other-all tls-vlan 3187
exit

# 5. Configurar serviço na ONU
pon-onu-mng gpon_onu-1/5/2:15
service 1 gemport 1 ethuni eth_0/1
vlan port eth_0/1 mode transparent
exit

# 6. TESTAR
show gpon onu state gpon-olt_1/5/2
# 1/5/2:15  online  working  success  ← SUCESSO!

show pon power onu-rx gpon_olt-1/5/2
# gpon-onu_1/5/2:15  -20.50  ← SINAL BOM!
```

---

## ⚠️ Diferenças Entre Unidades - MUITO IMPORTANTE!

**❌ ERRO COMUM:** Copiar script de provisionamento de uma unidade e usar em outra!

**Por quê?** Cada provedor/unidade pode ter:

### 1️⃣ Profiles Diferentes

**Unidade A:**
- `PLANO-1G`
- `PLANO-500M`
- `PLANO-200M`

**Unidade B:**
- `INTERNET-1000M`
- `INTERNET-500M`
- `BASICO-100M`

### 2️⃣ Types Diferentes

**Unidade A:** Usa `type Bridge`  
**Unidade B:** Usa `type Router`

### 3️⃣ QinQ vs VLAN Única

**Unidade A:** Usa QinQ (`other-all tls-vlan 3187`)  
**Unidade B:** Usa VLAN única (`user-vlan 3062 vlan 3062`)

### 4️⃣ Nomenclatura de VLANs

**Unidade A:** VLANs 3000-3100  
**Unidade B:** VLANs 100-200

---

**✅ REGRA DE OURO:**

**SEMPRE** verifique como as ONUs existentes estão configuradas na unidade antes de provisionar uma nova:

```bash
show running-config onu | include [NOME-PROVEDOR]
```

Copie a estrutura e adapte apenas:
- Serial (SN)
- Nome (name)
- ID da ONU

---

## 📊 Tabela Resumo - Comandos por Situação

| Situação | Comandos | O que verificar? |
|----------|----------|------------------|
| **Localizar ONU** | `show gpon onu by sn [SN]` | Slot/PON/ID |
| **ONU offline** | `show gpon onu state gpon-olt_X/Y/Z`<br>`show pon power onu-rx gpon_olt-X/Y/Z`<br>`show gpon onu detail-info gpon-onu_X/Y/Z:ID` | State: offline?<br>RX < -27 dBm?<br>Last cause: LOS? |
| **ONU não autentica** | `show pon onu uncfg` | Aparece na lista? |
| **VLAN não funciona** | `show vlan [VLAN]`<br>`show mac vlan [VLAN]` | VLAN existe?<br>Há MACs? |
| **Sinal fraco** | `show pon power onu-rx gpon_olt-X/Y/Z`<br>`show pon power attenuation gpon-onu_X/Y/Z:ID` | RX < -27 dBm?<br>Attenuation > 28 dB? |
| **Ver config geral** | `show running-config` | Toda configuração |
| **Health check PON** | `show interface gpon-olt_X/Y/Z`<br>`show gpon onu state gpon-olt_X/Y/Z` | TX OK?<br>Quantas ONUs online? |

---

## 📖 Referências e Documentação Oficial

### 📚 Manuais ZTE

1. **ZTE C300 User Manual:**
   - Documentação oficial do fabricante
   - Comandos CLI completos
   - Disponível no suporte ZTE

2. **ZTE GPON OLT CLI Reference:**
   - Guia de comandos detalhado
   - Sintaxe e exemplos

3. **ZTE ONU Configuration Guide:**
   - Guias de provisionamento
   - Perfis e tipos de ONU

### 📚 Artigos e Recursos

1. **Fiber Optic Association (FOA):**
   - https://www.thefoa.org
   - Tutoriais sobre fibra óptica

2. **GPON Explained:**
   - https://www.fiber-optic-solutions.com/what-is-gpon.html

3. **dBm e Potência Óptica:**
   - https://www.thefoa.org/tech/ref/testing/test/dBm.html

---

## 💡 Dicas Finais para Iniciantes

### 1️⃣ Use TAB para Autocompletar

```bash
# Digite:
show gp[TAB]

# A OLT completa automaticamente:
show gpon
```

### 2️⃣ Use `?` para Ver Opções

```bash
show ?
# Lista TODOS os comandos "show" disponíveis

show gpon ?
# Lista todas as opções de "show gpon"
```

### 3️⃣ Use `| include` para Filtrar

```bash
# Ao invés de ver milhares de linhas:
show running-config

# Filtre apenas o que interessa:
show running-config | include vlan
show running-config | include onu
```

### 4️⃣ Crie um Caderno de ONUs Importantes

Anote:
- Seriais de ONUs de teste
- ONUs de clientes VIP
- ONUs que costumam dar problema

### 5️⃣ Sempre Documente

Após cada atendimento, anote:
- Comandos usados
- Resultados obtidos
- Ações tomadas

### 6️⃣ Não Tenha Medo de Explorar

- Comandos `show` são **seguros** - apenas mostram informações
- Não quebram nada, não alteram configuração
- Explore, teste, aprenda!

---

## 🎓 Exercícios Práticos

### Exercício 1: Exploração Básica

```bash
# Execute e entenda cada output:
show version
show card
show temperature
show gpon onu state gpon-olt_1/5/1
show interface gpon-olt_1/5/1
```

### Exercício 2: Localizando uma ONU

```bash
# Pegue um serial de uma ONU online:
show gpon onu state gpon-olt_1/5/1

# Localize ela:
show gpon onu by sn [SERIAL-OBTIDO]

# Veja detalhes:
show gpon onu detail-info gpon-onu_[LOCALIZACAO]
```

### Exercício 3: Investigação de VLAN

```bash
# Escolha uma VLAN da sua rede (ex: 3062):
show vlan 3062
show mac vlan 3062

# Interprete:
# - Quais portas têm essa VLAN?
# - Quantos MACs foram aprendidos?
# - A VLAN está ativa?
```

### Exercício 4: Análise de Sinal de uma PON

```bash
# Escolha uma PON:
show pon power onu-rx gpon_olt-1/5/1

# Identifique:
# - Qual ONU tem melhor sinal?
# - Qual tem pior sinal?
# - Há alguma com sinal crítico (< -27 dBm)?
```

---

## 🏁 Conclusão

Parabéns por chegar até aqui! Você agora tem uma base sólida para trabalhar com OLTs ZTE. Lembre-se:

✅ **Serial (SN)** é o "RG" da ONU - você vai usar TODO DIA  
✅ **Sinal RX** é a saúde da fibra - valores bons = -8 a -25 dBm  
✅ **show gpon onu by sn** é seu comando mais usado - decore ele  
✅ **Sempre verifique** como outras ONUs estão configuradas antes de provisionar  
✅ **No NOC N1**, use apenas comandos `show` - nunca mude configurações sem autorização  

**Continue estudando os outros guias:**
- **GUIA_COMANDOS_WINDOWS_BASICOS.md** - Comandos de rede do Windows
- **GUIA_HUAWEI_INICIANTE.md** - Switches Huawei
- **GUIA_DATACOM_INICIANTE.md** - Switches Datacom

**Boa sorte no NOC! 🚀**

---

**Versão:** 1.0  
**Data:** Novembro 2025  
**Público-Alvo:** Analistas NOC Iniciantes  
**Dificuldade:** Básico a Intermediário  
**Equipamentos:** ZTE C300, ZTE C320

