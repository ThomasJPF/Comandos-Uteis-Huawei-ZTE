# 🔷 Guia Completo Switches Datacom - Para Iniciantes

## 🎯 Bem-vindo ao Mundo dos Switches Datacom!

Olá! Se você está aqui, vai trabalhar com **switches Datacom** pela primeira vez. Vamos explicar tudo do zero, com muita calma e exemplos práticos.

### 🤔 O que é um Switch Datacom?

**Datacom** é uma fabricante **brasileira** de equipamentos de rede. Os switches Datacom são muito usados em provedores de internet e empresas no Brasil.

**A boa notícia:** Se você já conhece switches Cisco, vai se sentir em casa! Os comandos Datacom são **muito parecidos** com Cisco.

**Analogia do Switch:**

Imagine uma **estação de trem** com várias plataformas:

- O **switch** é a estação central
- Cada **porta** é uma plataforma
- Os **dispositivos** (computadores, servidores) são os trens
- O switch **direciona** cada trem (dados) para a plataforma correta

---

## 📚 Glossário - Termos que Você Precisa Saber

| Termo               | O que significa?                             | Analogia Simples                                   |
| ------------------- | -------------------------------------------- | -------------------------------------------------- |
| **Switch**          | Equipamento que conecta dispositivos em rede | Estação de trem central                            |
| **Porta/Interface** | Conexão física onde você liga o cabo         | Plataforma do trem                                 |
| **VLAN**            | Rede virtual (separa tráfegos)               | Linhas coloridas do metrô                          |
| **MAC Address**     | Endereço físico único de cada equipamento    | CPF do equipamento                                 |
| **IP Address**      | Endereço lógico na rede                      | Endereço da casa                                   |
| **Gateway**         | Porta de saída para outra rede               | Aeroporto da cidade                                |
| **Trunk**           | Porta que carrega VÁRIAS VLANs               | Rodovia com várias faixas                          |
| **Access**          | Porta que carrega UMA VLAN                   | Rua simples para uma casa                          |
| **Tagged**          | VLAN com "etiqueta" identificadora           | Pacote com etiqueta de endereço                    |
| **Untagged**        | VLAN sem "etiqueta" (transparente)           | Pacote sem etiqueta                                |
| **STP**             | Protocolo anti-loop                          | Sinais de trânsito que evitam rotatórias infinitas |
| **LACP/LAG**        | Agregar portas (aumentar banda)              | Juntar 4 pistas em uma avenida maior               |
| **SFP**             | Módulo óptico para fibra                     | Conversor de cabo para fibra óptica                |
| **Uplink**          | Porta que conecta ao resto da rede           | Rodovia que sai da cidade                          |

---

## 🔑 Como Acessar o Switch Datacom

### Método 1: Telnet (Mais Comum)

**O que você precisa:**

- IP do switch
- Usuário e senha

**Passo a passo:**

1. Abra o CMD (Windows + R, digite `cmd`)

2. Digite:

```cmd
telnet [IP-DO-SWITCH]
```

**Exemplo:**

```cmd
telnet 10.20.30.60
```

3. Vai aparecer:

```
Username: _
```

4. Digite o usuário (geralmente `admin`) e aperte Enter

5. Digite a senha e aperte Enter

6. Você vai ver:

```
DmSwitch>
```

✅ **Parabéns! Você está dentro do switch!**

---

### Método 2: SSH (Mais Seguro)

**Usando PuTTY:**

1. Baixe o PuTTY: https://www.putty.org/
2. Abra o PuTTY
3. Em "Host Name" coloque o IP do switch
4. Em "Connection Type" escolha **SSH**
5. Clique em **Open**
6. Digite usuário e senha

---

### Método 3: Console (Cabo Serial)

**Quando usar?**

- Switch novo (sem IP)
- Perdeu a senha
- Não tem acesso remoto

**O que você precisa:**

- Cabo console (RJ-45 para USB)
- Software: PuTTY, Tera Term, SecureCRT

**Configurações:**

- Baud Rate: 115200
- Data Bits: 8
- Stop Bits: 1
- Parity: None
- Flow Control: None

---

## 🎮 Modos de Operação do Switch Datacom

O switch Datacom tem **3 níveis** de acesso (estilo Cisco):

### 📖 Entendendo os Modos

| Modo             | Prompt                 | O que você pode fazer?          | Como entrar?                    |
| ---------------- | ---------------------- | ------------------------------- | ------------------------------- |
| **Usuário**      | `DmSwitch>`            | Ver informações básicas         | Automático ao logar             |
| **Privilegiado** | `DmSwitch#`            | Ver tudo, mas não configurar    | Digite `enable`                 |
| **Configuração** | `DmSwitch(config)#`    | Mudar configurações             | Digite `configure terminal`     |
| **Interface**    | `DmSwitch(config-if)#` | Configurar uma porta específica | `interface gigabitethernet 1/1` |

**Analogia:**

- **Modo Usuário:** Você está na **recepção** (área pública)
- **Modo Privilegiado:** Você tem **acesso aos andares** (pode ver tudo)
- **Modo Configuração:** Você é o **gerente** (pode mudar as coisas)
- **Modo Interface:** Você está em uma **sala específica** (configura uma porta)

---

### 🎯 Exemplo Prático de Navegação

```bash
# 1. Você loga e está no modo usuário
DmSwitch>

# 2. Entrar no modo privilegiado
DmSwitch> enable
DmSwitch#

# 3. Entrar no modo de configuração
DmSwitch# configure terminal
DmSwitch(config)#

# 4. Entrar em uma interface
DmSwitch(config)# interface gigabitethernet 1/1
DmSwitch(config-if)#

# 5. Voltar um nível
DmSwitch(config-if)# exit
DmSwitch(config)#

# 6. Voltar direto ao modo privilegiado
DmSwitch(config)# end
DmSwitch#

# 7. Sair completamente
DmSwitch# exit
Connection closed by foreign host.
```

> **⚠️ IMPORTANTE NO NOC N1:** Você só deve usar comandos `show` (visualização). NUNCA configure sem autorização!

---

## 📝 Comandos Essenciais - Categoria por Categoria

### 📌 1. Comandos de Navegação Básica

#### Comando: `enable`

**O que faz?**
Entra no modo privilegiado.

**Quando usar?**
Logo após fazer login.

**Exemplo:**

```bash
DmSwitch> enable
Password: ______
DmSwitch#
```

---

#### Comando: `configure terminal`

**O que faz?**
Entra no modo de configuração.

**Quando usar?**
❌ **NUNCA no NOC N1 sem autorização!**

**Exemplo:**

```bash
DmSwitch# configure terminal
DmSwitch(config)#
```

---

#### Comando: `exit`

**O que faz?**
Volta um nível.

**Exemplo:**

```bash
# Saindo de uma interface
DmSwitch(config-if)# exit
DmSwitch(config)#

# Saindo do modo de configuração
DmSwitch(config)# exit
DmSwitch#

# Saindo completamente
DmSwitch# exit
```

---

#### Comando: `end`

**O que faz?**
Volta DIRETO ao modo privilegiado (não precisa dar vários `exit`).

**Exemplo:**

```bash
# Você está em uma interface
DmSwitch(config-if)# end
DmSwitch#
```

---

### 📌 2. Verificação de Interfaces (Portas)

#### Comando: `show interfaces status`

**O que faz?**
Mostra um **resumo** de TODAS as interfaces (status, VLAN, velocidade, duplex).

**Para que serve?**

- Ver rapidamente quais portas estão UP (funcionando) ou DOWN (paradas)
- Ver velocidade e duplex de cada porta
- Ver VLAN de cada porta
- Visão geral do switch

**Sintaxe:**

```bash
show interfaces status
```

**O que você vai ver:**

```
Port      Name                Status       Vlan       Duplex  Speed  Type
Gi1/1     UPLINK-CORE         connected    trunk      full    1000   1000BASE-T
Gi1/2     SERVER-WEB          connected    10         full    1000   1000BASE-T
Gi1/3                         notconnect   1          auto    auto   1000BASE-T
Gi1/4     OLT-ZTE-C300        connected    trunk      full    1000   1000BASE-T
Gi1/5     CAMERA-ENTRADA      connected    20         full    100    100BASE-TX
Gi1/6                         disabled     1          auto    auto   1000BASE-T
```

**Interpretando cada coluna:**

| Coluna     | O que significa?                 | Valores Possíveis                                                            |
| ---------- | -------------------------------- | ---------------------------------------------------------------------------- |
| **Port**   | Nome da porta                    | Gi (GigabitEthernet), Fa (FastEthernet), Te (TenGigabitEthernet)             |
| **Name**   | Descrição/identificação da porta | Texto livre                                                                  |
| **Status** | Estado da porta                  | `connected` (conectada), `notconnect` (desconectada), `disabled` (desligada) |
| **Vlan**   | VLAN da porta                    | Número (1-4094) ou `trunk`                                                   |
| **Duplex** | Modo de transmissão              | `full` (ideal), `half`, `auto`                                               |
| **Speed**  | Velocidade em Mbps               | 10, 100, 1000, 10000, auto                                                   |
| **Type**   | Tipo de interface                | 1000BASE-T (cobre), 1000BASE-SX (fibra), etc                                 |

**Status mais comuns:**

| Status            | O que significa?                               |
| ----------------- | ---------------------------------------------- |
| ✅ `connected`    | Porta funcionando, cabo conectado              |
| ❌ `notconnect`   | Cabo desconectado OU dispositivo desligado     |
| ⚠️ `disabled`     | Porta administrativamente desligada (shutdown) |
| ⚠️ `err-disabled` | Porta bloqueada por erro (loop, segurança)     |

**Análise do exemplo:**

| Porta     | Status             | Análise                                       |
| --------- | ------------------ | --------------------------------------------- |
| **Gi1/1** | connected, trunk   | ✅ Uplink funcionando (carrega várias VLANs)  |
| **Gi1/2** | connected, VLAN 10 | ✅ Servidor conectado na VLAN 10              |
| **Gi1/3** | notconnect         | ❌ Cabo desconectado ou dispositivo desligado |
| **Gi1/4** | connected, trunk   | ✅ OLT conectada (porta trunk)                |
| **Gi1/5** | connected, 100Mbps | ✅ Câmera IP (FastEthernet 100Mbps)           |
| **Gi1/6** | disabled           | ⚠️ Porta desligada manualmente (shutdown)     |

---

#### Comando: `show interfaces description`

**O que faz?**
Mostra TODAS as interfaces com suas **descrições**.

**Para que serve?**

- Identificar rapidamente o que está em cada porta
- Ver qual porta liga para qual equipamento/local

**Sintaxe:**

```bash
show interfaces description
```

**O que você vai ver:**

```
Interface          Status      Protocol    Description
Gi1/1              up          up          UPLINK-CORE-SW01
Gi1/2              up          up          SERVER-WEB-PRINCIPAL
Gi1/3              down        down        LIVRE
Gi1/4              up          up          OLT-ZTE-C300-SLOT1
Gi1/5              up          up          CAMERA-IP-ENTRADA
Gi1/6              admin down  down        PORTA-DESABILITADA
```

**Interpretando:**

| Campo           | O que significa?               |
| --------------- | ------------------------------ |
| **Interface**   | Nome da porta                  |
| **Status**      | Estado físico (camada 1)       |
| **Protocol**    | Estado de protocolo (camada 2) |
| **Description** | Identificação da porta         |

**Status possíveis:**

| Status          | Protocol  | O que significa?                                                |
| --------------- | --------- | --------------------------------------------------------------- |
| ✅ `up`         | ✅ `up`   | Funcionando perfeitamente                                       |
| ❌ `down`       | ❌ `down` | Cabo desconectado ou dispositivo desligado                      |
| ⚠️ `admin down` | ❌ `down` | Desligada manualmente (shutdown)                                |
| ⚠️ `up`         | ❌ `down` | Cabo conectado MAS não comunica (problema de config, VLAN, STP) |

---

#### Comando: `show interfaces [INTERFACE]`

**O que faz?**
Mostra informações **DETALHADAS** de uma interface específica.

**Para que serve?**

- Ver estatísticas completas (pacotes, erros, colisões)
- Ver configuração detalhada
- Diagnosticar problemas

**Sintaxe:**

```bash
show interfaces [TIPO] [NÚMERO]
```

**Exemplo:**

```bash
show interfaces gigabitethernet 1/1
```

**O que você vai ver:**

```
gigabitethernet1/1 is up, line protocol is up (connected)
  Hardware is Gigabit Ethernet, address is 00aa.00bb.00cc
  Description: UPLINK-CORE-SW01
  Internet address is 10.20.30.60/24
  MTU 1500 bytes, BW 1000000 Kbit
  Full-duplex, 1000Mb/s, media type is 1000BASE-T
  Input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last clearing of "show interfaces" counters never
  5 minute input rate 150000 bits/sec, 200 packets/sec
  5 minute output rate 250000 bits/sec, 350 packets/sec

  RX Statistics:
    1234567890 packets input, 987654321098 bytes
    0 broadcasts, 1000 multicasts
    0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
    0 runts, 0 giants, 0 throttles

  TX Statistics:
    987654321 packets output, 123456789098 bytes
    0 broadcasts, 500 multicasts
    0 output errors, 0 collisions, 0 interface resets
    0 babbles, 0 late collisions, 0 deferred
    0 lost carrier, 0 no carrier

  Time since last state change: 150 days, 12:30:00
```

**Interpretando os campos principais:**

| Campo                          | O que significa?             | Ideal               |
| ------------------------------ | ---------------------------- | ------------------- |
| **is up, line protocol is up** | Interface funcionando        | `up/up` ✅          |
| **Hardware address**           | Endereço MAC da porta        | -                   |
| **Internet address**           | IP da porta (se configurado) | -                   |
| **MTU**                        | Tamanho máximo de pacote     | 1500 bytes (padrão) |
| **Full-duplex, 1000Mb/s**      | Velocidade e modo            | Full + 1000 ✅      |
| **RX packets**                 | Pacotes RECEBIDOS            | -                   |
| **TX packets**                 | Pacotes ENVIADOS             | -                   |
| **input errors**               | Erros de entrada             | 0 ✅                |
| **CRC errors**                 | Erros de integridade         | 0 ✅                |
| **output errors**              | Erros de saída               | 0 ✅                |
| **collisions**                 | Colisões de pacotes          | 0 ✅                |

**Análise de problemas:**

| Problema              | O que significa?       | Causa Possível                             |
| --------------------- | ---------------------- | ------------------------------------------ |
| **CRC > 0**           | Pacotes corrompidos    | Cabo ruim, interferência, porta defeituosa |
| **runts > 0**         | Pacotes muito pequenos | Problema de cabo ou colisão                |
| **giants > 0**        | Pacotes muito grandes  | MTU incorreto                              |
| **collisions > 0**    | Colisões na rede       | Duplex errado (half/full mismatch)         |
| **input errors alto** | Muitos erros recebendo | Cabo ruim, porta defeituosa                |

---

### 📌 3. Trabalhando com VLANs

#### O que é VLAN?

**VLAN** (Virtual LAN) separa tráfegos diferentes na mesma rede física.

**Analogia:** Imagine um prédio comercial:

- **VLAN 10:** Andar do RH
- **VLAN 20:** Andar do Financeiro
- **VLAN 30:** Andar da TI

Todos usam o **mesmo elevador** (switch), mas **não se misturam** (segurança, organização).

---

#### Comando: `show vlan`

**O que faz?**
Lista **TODAS** as VLANs configuradas no switch.

**Para que serve?**

- Ver quais VLANs existem
- Ver quais portas pertencem a cada VLAN

**Sintaxe:**

```bash
show vlan
```

**O que você vai ver:**

```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi1/3, Gi1/7, Gi1/8
10   VLAN_ADMIN                       active    Gi1/2, Gi1/9, Gi1/10
20   VLAN_FINANCEIRO                  active    Gi1/5, Gi1/11
30   VLAN_TI                          active    Gi1/6, Gi1/12
100  VLAN_GUEST                       active    Gi1/13, Gi1/14

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        0      0
10   enet  100010     1500  -      -      -        -    -        0      0
20   enet  100020     1500  -      -      -        -    -        0      0
30   enet  100030     1500  -      -      -        -    -        0      0
100  enet  100100     1500  -      -      -        -    -        0      0
```

**Interpretando:**

| Campo              | O que significa?                               |
| ------------------ | ---------------------------------------------- |
| **VLAN**           | Número da VLAN (1-4094)                        |
| **Name**           | Nome/descrição da VLAN                         |
| **Status: active** | VLAN está funcionando                          |
| **Ports**          | Portas que pertencem a essa VLAN (modo access) |

**Nota importante:**

Portas configuradas como **trunk** (que carregam várias VLANs) **NÃO APARECEM** nesta lista de "Ports". Para ver portas trunk, use outro comando.

---

#### Comando: `show vlan id [VLAN-ID]`

**O que faz?**
Mostra detalhes de uma VLAN específica.

**Para que serve?**

- Ver informações de uma VLAN
- Ver quais portas estão nessa VLAN

**Sintaxe:**

```bash
show vlan id [NÚMERO]
```

**Exemplo:**

```bash
show vlan id 10
```

**O que você vai ver:**

```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
10   VLAN_ADMIN                       active    Gi1/2, Gi1/9, Gi1/10

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
10   enet  100010     1500  -      -      -        -    -        0      0
```

✅ A VLAN 10 existe e tem 3 portas em modo access.

---

#### Comando: `show mac address-table vlan [VLAN-ID]`

**O que faz?**
Mostra os **endereços MAC** aprendidos em uma VLAN específica.

**Para que serve?**

- Ver quais dispositivos estão em uma VLAN
- Identificar por qual porta cada dispositivo acessa
- Troubleshooting: verificar se há tráfego na VLAN

**Sintaxe:**

```bash
show mac address-table vlan [NÚMERO]
```

**Exemplo:**

```bash
show mac address-table vlan 10
```

**O que você vai ver:**

```
Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
10      00aa.00bb.00cc    DYNAMIC     Gi1/2
10      00aa.00bb.00dd    DYNAMIC     Gi1/2
10      00aa.00bb.00ee    DYNAMIC     Gi1/9
10      00aa.00bb.00ff    DYNAMIC     Gi1/10
10      00aa.00bb.0011    DYNAMIC     Gi1/1

Total Mac Addresses for this table: 5
```

**Interpretando:**

| Campo             | O que significa?                               |
| ----------------- | ---------------------------------------------- |
| **Vlan**          | Número da VLAN                                 |
| **Mac Address**   | Endereço físico do dispositivo                 |
| **Type: DYNAMIC** | Aprendido automaticamente                      |
| **Ports**         | Por qual porta esse dispositivo está acessando |

**Análise:**

- **4 MACs nas portas Gi1/2, 9, 10:** Dispositivos finais (PCs, impressoras)
- **1 MAC na porta Gi1/1:** Provavelmente outro switch ou roteador (uplink)

**Troubleshooting:**

✅ **Se há MACs:** VLAN está funcionando, há tráfego  
❌ **Se NÃO há MACs:** Problema! VLAN não está passando tráfego ou sem dispositivos

---

#### Comando: `show interfaces trunk`

**O que faz?**
Mostra quais portas estão em modo **trunk** e quais VLANs elas carregam.

**Para que serve?**

- Ver portas de uplink (trunk)
- Ver quais VLANs estão passando em cada trunk
- Troubleshooting de conectividade entre switches

**Sintaxe:**

```bash
show interfaces trunk
```

**O que você vai ver:**

```
Port        Mode         Encapsulation  Status        Native vlan
Gi1/1       on           802.1q         trunking      1
Gi1/4       on           802.1q         trunking      1

Port        Vlans allowed on trunk
Gi1/1       1-4094
Gi1/4       10,20,30,100

Port        Vlans allowed and active in management domain
Gi1/1       1,10,20,30,100
Gi1/4       10,20,30,100

Port        Vlans in spanning tree forwarding state and not pruned
Gi1/1       1,10,20,30,100
Gi1/4       10,20,30,100
```

**Interpretando:**

| Campo                        | O que significa?                        |
| ---------------------------- | --------------------------------------- |
| **Port**                     | Porta em modo trunk                     |
| **Mode: on**                 | Trunk estático (sempre trunk)           |
| **Encapsulation: 802.1q**    | Protocolo de tagging VLAN               |
| **Status: trunking**         | Trunk ativo e funcionando               |
| **Native vlan**              | VLAN sem tag (padrão = VLAN 1)          |
| **Vlans allowed**            | Quais VLANs podem passar                |
| **Vlans allowed and active** | Quais VLANs estão configuradas E ativas |

**Análise:**

- **Gi1/1:** Trunk permitindo TODAS as VLANs (1-4094)
- **Gi1/4:** Trunk permitindo apenas VLANs 10, 20, 30, 100 (OLT)

---

### 📌 4. Diagnóstico e Troubleshooting

#### Comando: `show running-config`

**O que faz?**
Mostra **TODA** a configuração em execução do switch.

**Para que serve?**

- Ver como o switch está configurado
- Fazer backup da configuração
- Auditoria

**Sintaxe:**

```bash
show running-config
```

⚠️ **ATENÇÃO:** Gera MUITO texto!

**Melhor usar com filtros:**

```bash
# Ver apenas VLANs
show running-config | include vlan

# Ver configuração de uma interface
show running-config interface gigabitethernet 1/1
```

---

#### Comando: `show mac address-table`

**O que faz?**
Mostra **TODOS** os endereços MAC aprendidos (todas as VLANs).

**Sintaxe:**

```bash
show mac address-table
```

**O que você vai ver:**

```
Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
1       00aa.00bb.0001    DYNAMIC     Gi1/3
10      00aa.00bb.00cc    DYNAMIC     Gi1/2
10      00aa.00bb.00dd    DYNAMIC     Gi1/9
20      00aa.00bb.00ee    DYNAMIC     Gi1/5
30      00aa.00bb.00ff    DYNAMIC     Gi1/6
...

Total Mac Addresses: 245
```

---

#### Comando: `show arp`

**O que faz?**
Mostra a **tabela ARP** (correspondência entre IPs e MACs).

**Para que serve?**

- Ver qual IP está associado a qual MAC
- Identificar dispositivos por IP

**Sintaxe:**

```bash
show arp
```

**O que você vai ver:**

```
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.20.30.1       25         00aa.00bb.00cc  ARPA   Vlan10
Internet  10.20.30.2       18         00aa.00bb.00dd  ARPA   Vlan10
Internet  10.20.30.10      30         00aa.00bb.00ee  ARPA   Vlan10
Internet  192.168.1.1      15         00aa.00bb.00ff  ARPA   Vlan1
```

**Interpretando:**

| Campo             | O que significa?             |
| ----------------- | ---------------------------- |
| **Address**       | Endereço IP                  |
| **Age**           | Há quantos minutos foi visto |
| **Hardware Addr** | Endereço MAC correspondente  |
| **Interface**     | Interface virtual (VLAN)     |

---

#### Comando: `show interfaces counters`

**O que faz?**
Mostra **contadores de tráfego** de todas as interfaces.

**Sintaxe:**

```bash
show interfaces counters
```

**O que você vai ver:**

```
Port            InOctets    InUcast    InMcast    InBcast    OutOctets   OutUcast
Gi1/1           987654321   654321     1000       500        123456789   456789
Gi1/2           123456789   123000     456        100        987654321   987000
Gi1/3           0           0          0          0          0           0
```

---

#### Comando: `show interfaces counters errors`

**O que faz?**
Mostra **contadores de erros** de todas as interfaces.

**Para que serve?**

- Identificar rapidamente portas com problemas
- Ver CRC, drops, collisions

**Sintaxe:**

```bash
show interfaces counters errors
```

**O que você vai ver:**

```
Port     Align-Err    FCS-Err   Xmit-Err   Rcv-Err   UnderSize  OutDiscards
Gi1/1    0            0         0          0         0          0
Gi1/2    0            0         0          0         0          0
Gi1/3    0            0         0          0         0          0
Gi1/5    5            3         0          2         0          0  ← PROBLEMA!
Gi1/6    150          120       10         80        5          20  ← PROBLEMA SÉRIO!
```

**Interpretando:**

| Coluna          | O que significa?             | Ideal |
| --------------- | ---------------------------- | ----- |
| **Align-Err**   | Erros de alinhamento         | 0     |
| **FCS-Err**     | Erros de FCS (similar a CRC) | 0     |
| **Xmit-Err**    | Erros de transmissão         | 0     |
| **Rcv-Err**     | Erros de recepção            | 0     |
| **UnderSize**   | Pacotes muito pequenos       | 0     |
| **OutDiscards** | Pacotes descartados          | 0     |

**Análise:**

| Porta     | Status | Problema    | Ação                           |
| --------- | ------ | ----------- | ------------------------------ |
| **Gi1/5** | ⚠️     | 5 erros FCS | Verificar cabo                 |
| **Gi1/6** | ❌     | 150+ erros  | Trocar cabo ou verificar porta |

---

### 📌 5. Testes de Conectividade

#### Comando: `ping [IP]`

**O que faz?**
Testa conectividade para um IP.

**Sintaxe:**

```bash
ping [IP]
```

**Exemplo:**

```bash
ping 8.8.8.8
```

**O que você vai ver:**

```
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=117 time=15.2 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=14.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=16.1 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=117 time=15.5 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 14.8/15.4/16.1 ms
```

✅ **0% packet loss** = Conectividade perfeita!

---

#### Comando: `traceroute [IP]`

**O que faz?**
Mostra o **caminho** até o destino.

**Sintaxe:**

```bash
traceroute [IP]
```

**Exemplo:**

```bash
traceroute 8.8.8.8
```

**O que você vai ver:**

```
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 40 byte packets
 1  10.20.30.1 (10.20.30.1)  5.234 ms  4.567 ms  5.123 ms
 2  200.150.100.1 (200.150.100.1)  12.345 ms  11.234 ms  13.456 ms
 3  200.150.100.2 (200.150.100.2)  15.678 ms  14.567 ms  16.789 ms
 4  8.8.8.8 (8.8.8.8)  20.123 ms  19.456 ms  21.234 ms
```

---

### 📌 6. Informações do Sistema

#### Comando: `show version`

**O que faz?**
Mostra versão do software, modelo do switch, uptime.

**Sintaxe:**

```bash
show version
```

**O que você vai ver:**

```
Datacom DmSwitch 3500 Series
Software version: DmOS 11.5.3.2
Compiled: Nov 15 2024 10:30:00
Model: DM3524-V1
Serial Number: DS12345678
Hardware version: 1.0
Uptime: 150 days, 12 hours, 30 minutes

System image file is "dm3500-img-11.5.3.2.bin"
```

---

#### Comando: `show system`

**O que faz?**
Mostra informações do sistema (nome, localização, contato).

**Sintaxe:**

```bash
show system
```

**O que você vai ver:**

```
System Description:  Datacom DmSwitch 3500
System Name:         SWITCH-CORE-01
System Location:     Datacenter Principal
System Contact:      suporte@empresa.com.br
System Up Time:      150 days, 12:30:00
```

---

#### Comando: `show environment`

**O que faz?**
Mostra status de **hardware** (temperatura, ventiladores, fontes).

**Para que serve?**

- Ver se o switch está superaquecendo
- Ver se ventiladores estão funcionando
- Ver se fontes estão OK

**Sintaxe:**

```bash
show environment
```

**O que você vai ver:**

```
Environmental Status:

Temperature:
  System Temperature:       45°C  (Normal)
  Temperature Threshold:    75°C

Fans:
  FAN1:                     Normal  (3000 RPM)
  FAN2:                     Normal  (3000 RPM)

Power Supplies:
  PWR1:                     Normal  (AC, 250W)
  PWR2:                     Not Present
```

**Análise:**

| Item            | Status      | Valores de Referência                                    |
| --------------- | ----------- | -------------------------------------------------------- |
| **Temperatura** | 45°C        | ✅ Normal (até 60°C OK, > 70°C crítico)                  |
| **FAN1/2**      | Normal      | ✅ Funcionando                                           |
| **PWR1**        | Normal      | ✅ Fonte 1 OK                                            |
| **PWR2**        | Not Present | ⚠️ Fonte 2 não instalada (fonte única = sem redundância) |

---

#### Comando: `show logging`

**O que faz?**
Mostra **logs do sistema** (eventos, erros).

**Para que serve?**

- Ver o que aconteceu recentemente
- Investigar problemas

**Sintaxe:**

```bash
show logging
```

**O que você vai ver:**

```
Syslog logging: enabled

System Log Buffer (4096 bytes):

Nov 13 10:10:25: %LINK-3-UPDOWN: Interface GigabitEthernet1/3, changed state to down
Nov 13 10:12:30: %LINK-3-UPDOWN: Interface GigabitEthernet1/3, changed state to up
Nov 13 09:45:10: %STP-2-BLOCK_BPDUGUARD: Received BPDU on port Gi1/5 with BPDU Guard enabled. Port disabled.
```

**Interpretando:**

- **10:10:25:** Porta Gi1/3 caiu
- **10:12:30:** Porta Gi1/3 voltou (ficou 2 minutos offline)
- **09:45:10:** STP bloqueou porta Gi1/5 (detectou BPDU indevido)

---

### 📌 7. Comandos de Roteamento (se Switch Layer 3)

#### Comando: `show ip route`

**O que faz?**
Mostra a **tabela de rotas** (apenas se o switch for Layer 3).

**Sintaxe:**

```bash
show ip route
```

**O que você vai ver:**

```
Codes: C - connected, S - static, R - RIP, O - OSPF, B - BGP
       * - candidate default

Gateway of last resort is 10.20.30.1 to network 0.0.0.0

C       10.20.30.0/24 is directly connected, Vlan10
C       192.168.1.0/24 is directly connected, Vlan1
S*      0.0.0.0/0 [1/0] via 10.20.30.1
```

---

## 🔧 Cenários Práticos do Dia a Dia

### 📞 Cenário 1: Link Down no Switch

**Sintoma:** Alarme: "Link down Gi1/5".

**Passo a passo:**

```bash
# PASSO 1: Ver resumo das portas
show interfaces status

# Procure por Gi1/5:
# Gi1/5    notconnect   ...  ← PROBLEMA!

# PASSO 2: Ver descrição
show interfaces description | include Gi1/5

# OUTPUT:
# Gi1/5   down   down   CAMERA-IP-GARAGEM

# PASSO 3: Ver detalhes da interface
show interfaces gigabitethernet 1/5

# Verificar:
# - Time since last state change: QUANDO caiu?
# - Errors?

# PASSO 4: Ver logs
show logging | include Gi1/5

# PASSO 5: Ver erros
show interfaces counters errors | include Gi1/5
```

**Diagnóstico:**

| Situação                          | Causa                                      | Solução                       |
| --------------------------------- | ------------------------------------------ | ----------------------------- |
| Status: notconnect + 0 erros      | Cabo desconectado ou dispositivo desligado | Verificar cabo e câmera       |
| Status: notconnect + muitos erros | Cabo ruim                                  | Trocar cabo                   |
| Status: disabled                  | Porta desligada manualmente                | Solicitar ativação            |
| Status: err-disabled              | Porta bloqueada (loop, BPDU guard)         | Investigar causa, limpar erro |

---

### 📞 Cenário 2: VLAN Não Funciona

**Sintoma:** Cliente da VLAN 100 sem conectividade.

**Passo a passo:**

```bash
# PASSO 1: Verificar se VLAN existe
show vlan id 100

# Se não aparecer: VLAN não criada! → Escalar

# PASSO 2: Ver portas da VLAN
show vlan id 100

# Verificar:
# - Porta do cliente está na lista?

# PASSO 3: Ver trunks (uplinks)
show interfaces trunk

# Verificar:
# - VLAN 100 está nos trunks?

# PASSO 4: Ver MACs na VLAN
show mac address-table vlan 100

# Se NÃO há MACs: Sem tráfego!

# PASSO 5: Ver config da porta do cliente
show running-config interface gigabitethernet 1/10

# Verificar:
# - switchport mode access
# - switchport access vlan 100
```

**Diagnóstico:**

| Situação          | Causa                   | Solução                              |
| ----------------- | ----------------------- | ------------------------------------ |
| VLAN não existe   | Não criada              | Escalar para criar                   |
| Porta não na VLAN | Config errada           | Escalar para adicionar               |
| VLAN não no trunk | Uplink não carrega VLAN | Escalar para adicionar VLAN ao trunk |
| Porta down        | Problema físico         | Verificar cabo                       |

---

### 📞 Cenário 3: Descobrir Onde um Dispositivo Está Conectado

**Sintoma:** Preciso saber em qual porta o MAC 00aa.00bb.00cc está.

**Passo a passo:**

```bash
# PASSO 1: Buscar o MAC
show mac address-table | include 00aa.00bb.00cc

# OUTPUT:
# 10   00aa.00bb.00cc   DYNAMIC   Gi1/8

# O dispositivo está na porta Gi1/8!

# PASSO 2: Ver descrição dessa porta
show interfaces description | include Gi1/8

# OUTPUT:
# Gi1/8   up   up   SALA-REUNIAO-A

# PASSO 3: Se precisar do IP:
show arp | include 00aa.00bb.00cc

# OUTPUT:
# Internet  10.20.30.50   ...   00aa.00bb.00cc   ARPA   Vlan10
```

✅ **Encontrado!**

- **MAC:** 00aa.00bb.00cc
- **IP:** 10.20.30.50
- **Porta:** Gi1/8
- **Local:** SALA-REUNIAO-A
- **VLAN:** 10

---

### 📞 Cenário 4: Switch Lento - Investigação

**Sintoma:** Rede lenta, equipamentos com perda de pacotes.

**Passo a passo:**

```bash
# PASSO 1: Ver tráfego nas portas
show interfaces status

# Procure por portas com alto uso (InUti/OutUti)

# PASSO 2: Ver erros
show interfaces counters errors

# Procure por FCS-Err, Rcv-Err altos

# PASSO 3: Ver logs
show logging

# Procure por:
# - STP messages repetitivas (loop)
# - err-disabled
# - BPDU Guard

# PASSO 4: Ver quantidade de MACs por porta
show mac address-table

# Se uma porta tem MUITOS MACs (>50): Possível hub ou loop
```

**Possíveis causas:**

1. **Loop de rede:** STP mal configurado
2. **Cabo ruim em porta crítica:** Muitos erros FCS
3. **Broadcast storm:** Dispositivo defeituoso
4. **Porta saturada:** Uplink insuficiente

---

## 📊 Tabela Resumo - Comandos por Situação

| Situação                  | Comandos                                                                                 | O que verificar?                               |
| ------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------- |
| **Link down**             | `show interfaces status`<br>`show interfaces [PORTA]`<br>`show logging`                  | Status: notconnect?<br>Errors?<br>Quando caiu? |
| **VLAN não funciona**     | `show vlan id [VLAN]`<br>`show mac address-table vlan [VLAN]`<br>`show interfaces trunk` | VLAN existe?<br>Há MACs?<br>VLAN no trunk?     |
| **Encontrar dispositivo** | `show mac address-table \| include [MAC]`<br>`show arp \| include [MAC]`                 | Qual porta?<br>Qual IP?                        |
| **Verificar erros**       | `show interfaces counters errors`                                                        | FCS-Err > 0?                                   |
| **Ver config**            | `show running-config`<br>`show running-config interface [PORTA]`                         | Configuração atual                             |
| **Health check**          | `show version`<br>`show system`<br>`show environment`                                    | Versão, uptime<br>Temperatura OK?<br>Fans OK?  |

---

## 📖 Referências e Documentação Oficial

### 📚 Datacom

1. **Portal de Suporte Datacom:**

   - https://www.datacom.com.br/suporte

2. **Manuais DmSwitch:**

   - Documentação oficial dos switches
   - Comandos CLI completos

3. **Base de Conhecimento:**
   - Tutoriais e guias

---

## 💡 Dicas Finais para Iniciantes

### 1️⃣ Use TAB para Autocompletar

```bash
# Digite:
show int[TAB]

# O switch completa:
show interfaces
```

### 2️⃣ Use `?` para Ver Opções

```bash
show ?
# Lista TODOS os comandos "show"

show interfaces ?
# Lista opções de "show interfaces"
```

### 3️⃣ Use `|` (pipe) para Filtrar

```bash
# Filtrar:
show interfaces status | include down

# Buscar:
show mac address-table | include 00aa.00bb
```

### 4️⃣ Comandos Estilo Cisco

Se você conhece Cisco, vai reconhecer:

- `show running-config` = `show run` (aceita abreviação)
- `show interfaces status` = `sh int stat`
- `configure terminal` = `conf t`

### 5️⃣ Não Tenha Medo de Explorar

- Comandos `show` são **seguros**
- Não alteram configuração
- Explore à vontade!

---

## 🎓 Exercícios Práticos

### Exercício 1: Exploração Básica

```bash
# Execute:
show version
show system
show environment
show interfaces status
show vlan
```

### Exercício 2: Investigação de Porta

```bash
# Escolha uma porta (ex: Gi1/1):
show interfaces gigabitethernet 1/1
show interfaces status | include Gi1/1
show interfaces counters errors | include Gi1/1
```

### Exercício 3: Análise de VLAN

```bash
# Escolha uma VLAN:
show vlan id 10
show mac address-table vlan 10
show interfaces trunk
```

### Exercício 4: Busca de Dispositivo

```bash
# Pegue um MAC da tabela:
show mac address-table

# Busque ele:
show mac address-table | include [MAC]
show arp | include [MAC]
```

---

## 🏁 Conclusão

Parabéns! Você agora tem uma base sólida para trabalhar com switches Datacom. Lembre-se:

✅ **show interfaces status** é seu comando mais usado - visão geral  
✅ **show vlan** para entender VLANs  
✅ **show mac address-table** para encontrar dispositivos  
✅ **show environment** para health check  
✅ **Comandos similares ao Cisco** - se você conhece Cisco, vai se adaptar rápido  
✅ **No NOC N1**, use apenas comandos `show` - nunca configure sem autorização

**Continue estudando os outros guias:**

- **GUIA_COMANDOS_WINDOWS_BASICOS.md** - Comandos de rede do Windows
- **GUIA_ZTE_INICIANTE.md** - OLTs ZTE
- **GUIA_HUAWEI_INICIANTE.md** - Switches Huawei

**Boa sorte no NOC! 🚀**

---

**Versão:** 1.0  
**Data:** Novembro 2025  
**Público-Alvo:** Analistas NOC Iniciantes  
**Dificuldade:** Básico a Intermediário  
**Equipamentos:** Datacom DmSwitch series (DM2500, DM3500, DM4100, etc)
