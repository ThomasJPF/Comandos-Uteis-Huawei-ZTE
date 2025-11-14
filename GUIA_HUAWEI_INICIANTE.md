# 🔶 Guia Completo Switches Huawei - Para Iniciantes

## 🎯 Bem-vindo ao Mundo dos Switches Huawei!

Olá! Se você está aqui, vai trabalhar com **switches Huawei** pela primeira vez. Vamos explicar tudo do zero, com muita calma e exemplos práticos.

### 🤔 O que é um Switch?

**Switch** é um equipamento que **conecta vários dispositivos em uma rede**. Ele é como um "guarda de trânsito" que decide para onde cada pacote de dados deve ir.

**Analogia simples:**

Imagine uma grande **estação de metrô** com várias plataformas:
- O **switch** é a estação central
- Cada **porta** do switch é uma plataforma
- Os **dispositivos** (computadores, servidores, roteadores) são os trens
- O switch **direciona** cada trem (dados) para a plataforma correta

**Diferença entre Switch e Roteador:**

| Equipamento | O que faz? | Analogia |
|-------------|-----------|----------|
| **Switch** | Conecta dispositivos na MESMA REDE (camada 2) | Terminal rodoviário municipal - liga bairros da mesma cidade |
| **Roteador** | Conecta REDES DIFERENTES (camada 3) | Aeroporto - liga cidades diferentes |

---

## 📚 Glossário - Termos que Você Precisa Saber

| Termo | O que significa? | Analogia Simples |
|-------|------------------|------------------|
| **Switch** | Equipamento que conecta dispositivos em rede | Estação de metrô com várias plataformas |
| **Porta/Interface** | Conexão física onde você liga o cabo | Tomada na parede |
| **VLAN** | Rede virtual (separa tráfegos) | Corredores coloridos (vermelho, azul) |
| **MAC Address** | Endereço físico único de cada equipamento | Chassi de um carro (único) |
| **IP Address** | Endereço lógico (pode mudar) | Endereço de uma casa (pode mudar se você se mudar) |
| **Gateway** | Porta de saída para outra rede | Portão do condomínio para a rua |
| **Trunk** | Porta que carrega VÁRIAS VLANs | Rodovia com várias faixas (cada VLAN é uma faixa) |
| **Access** | Porta que carrega UMA VLAN (para usuário final) | Estrada simples para uma casa |
| **Tagged** | VLAN com "etiqueta" (número vai junto) | Carta COM envelope colorido |
| **Untagged** | VLAN sem "etiqueta" (transparente) | Carta SEM envelope (só o papel) |
| **STP** | Protocolo que evita loops (círculos) na rede | Sinais de trânsito que evitam carros ficarem em círculo |
| **LACP** | Agregar várias portas em uma (aumentar velocidade) | Juntar 4 pistas em uma rodovia mais larga |
| **SFP** | Módulo óptico para fibra | Adaptador que transforma tomada em fibra óptica |
| **Uplink** | Porta que conecta o switch ao resto da rede | Saída da cidade para a rodovia principal |

---

## 🔑 Como Acessar o Switch Huawei

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
telnet 10.20.30.50
```

3. Vai aparecer:
```
Login: _
```

4. Digite o usuário (geralmente `admin`) e aperte Enter

5. Digite a senha e aperte Enter

6. Você vai ver:
```
<SWITCH-NOME>
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
- Switch novo (sem IP configurado)
- Perdeu a senha
- Não tem acesso remoto

**O que você precisa:**
- Cabo console (RJ-45 para USB ou Serial)
- Software: PuTTY, Tera Term ou SecureCRT

**Configurações:**
- Baud Rate: 9600
- Data Bits: 8
- Stop Bits: 1
- Parity: None
- Flow Control: None

---

## 🎮 Modos de Operação do Switch Huawei

O switch Huawei tem **NÍVEIS** de acesso, como andares de um prédio:

### 📖 Entendendo os Modos

| Modo | Prompt | O que você pode fazer? | Como entrar? |
|------|--------|------------------------|--------------|
| **Visualização** | `<SWITCH-NOME>` | Ver informações básicas | Automático ao logar |
| **Sistema** | `[SWITCH-NOME]` | Ver tudo e configurar | Digite `system-view` |
| **Interface** | `[SWITCH-NOME-GigabitEthernet0/0/1]` | Configurar uma porta específica | `interface GigabitEthernet 0/0/1` |

**Analogia:**
- **Modo Visualização:** Você está no **lobby** do prédio (pode só olhar)
- **Modo Sistema:** Você tem **chave de todos os andares** (pode configurar tudo)
- **Modo Interface:** Você está dentro de um **apartamento específico** (configura uma porta)

---

### 🎯 Exemplo Prático de Navegação

```bash
# 1. Você loga e está no modo visualização
<SWITCH-NOME>

# 2. Entrar no modo sistema
<SWITCH-NOME> system-view
[SWITCH-NOME]

# 3. Entrar em uma interface específica
[SWITCH-NOME] interface GigabitEthernet 0/0/1
[SWITCH-NOME-GigabitEthernet0/0/1]

# 4. Voltar um nível
[SWITCH-NOME-GigabitEthernet0/0/1] quit
[SWITCH-NOME]

# 5. Voltar ao modo visualização
[SWITCH-NOME] return
<SWITCH-NOME>

# 6. Sair completamente
<SWITCH-NOME> quit
```

> **⚠️ IMPORTANTE NO NOC N1:** Você só deve usar comandos `display` (visualização). NUNCA entre no modo sistema para configurar sem autorização!

---

## 📝 Comandos Essenciais - Categoria por Categoria

### 📌 1. Comandos de Navegação Básica

#### Comando: `system-view`

**O que faz?**
Entra no modo de configuração (sistema).

**Quando usar?**
Quando precisa configurar algo (apenas com autorização).

**Exemplo:**
```bash
<SWITCH-NOME> system-view
[SWITCH-NOME]
```

---

#### Comando: `quit`

**O que faz?**
Sai do modo atual (volta um nível).

**Exemplo:**
```bash
# Saindo do modo de interface
[SWITCH-NOME-GigabitEthernet0/0/1] quit
[SWITCH-NOME]

# Saindo completamente
<SWITCH-NOME> quit
Connection closed.
```

> **💡 Dica:** SEMPRE use `quit` para sair. NUNCA feche a janela no meio!

---

#### Comando: `return`

**O que faz?**
Volta DIRETO ao modo visualização (não precisa dar vários `quit`).

**Exemplo:**
```bash
# Você está dentro de uma interface
[SWITCH-NOME-GigabitEthernet0/0/1] return
<SWITCH-NOME>
```

---

#### Comando: `display this`

**O que faz?**
Mostra a configuração da interface/modo onde você está.

**Quando usar?**
Quando está dentro de uma interface e quer ver suas configurações.

**Exemplo:**
```bash
[SWITCH-NOME] interface GigabitEthernet 0/0/1
[SWITCH-NOME-GigabitEthernet0/0/1] display this
#
interface GigabitEthernet0/0/1
 description UPLINK-CORE
 port link-type trunk
 port trunk allow-pass vlan 10 20 30
#
```

---

### 📌 2. Verificação de Interfaces (Portas)

#### Comando: `display interface brief`

**O que faz?**
Mostra um **resumo** de TODAS as interfaces do switch (status, velocidade, duplex).

**Para que serve?**
- Ver rapidamente quais portas estão UP (funcionando) ou DOWN (desligadas)
- Ver velocidade de cada porta
- Visão geral do switch

**Sintaxe:**
```bash
display interface brief
```

**O que você vai ver:**

```
Interface                   PHY   Protocol  InUti OutUti   inErrors  outErrors
GigabitEthernet0/0/1        up    up        0.01%  0.01%          0          0
GigabitEthernet0/0/2        up    up        15%    20%            0          0
GigabitEthernet0/0/3        down  down      0      0              0          0
GigabitEthernet0/0/4        up    up        0      0              5          2
GigabitEthernet0/0/5        *down down      0      0              0          0
XGigabitEthernet0/0/1       up    up        45%    60%            0          0
```

**Interpretando cada coluna:**

| Coluna | O que significa? | Valores Possíveis |
|--------|------------------|-------------------|
| **Interface** | Nome da porta | GigabitEthernet (1G), XGigabitEthernet (10G) |
| **PHY** | Status físico (camada 1 - cabo) | `up` (cabo conectado), `down` (cabo desconectado ou problema) |
| **Protocol** | Status de protocolo (camada 2 - comunicação) | `up` (funcionando), `down` (não funciona) |
| **InUti** | Utilização de entrada (quanto tráfego está CHEGANDO) | Porcentagem (0% a 100%) |
| **OutUti** | Utilização de saída (quanto tráfego está SAINDO) | Porcentagem (0% a 100%) |
| **inErrors** | Erros de entrada | Número (ideal = 0) |
| **outErrors** | Erros de saída | Número (ideal = 0) |

**Status mais comuns:**

| PHY | Protocol | O que significa? |
|-----|----------|------------------|
| ✅ `up` | ✅ `up` | Porta funcionando perfeitamente |
| ❌ `down` | ❌ `down` | Cabo desconectado OU dispositivo desligado |
| ⚠️ `up` | ❌ `down` | Cabo conectado MAS não comunica (problema de configuração, VLAN, STP) |
| ⚠️ `*down` | ❌ `down` | Porta administrativamente desligada (shutdown) |

**Análise do exemplo:**

| Porta | Status | Análise |
|-------|--------|---------|
| **GE0/0/1** | up/up | ✅ Funcionando, baixo uso (0.01%) |
| **GE0/0/2** | up/up | ✅ Funcionando, uso moderado (15-20%) |
| **GE0/0/3** | down/down | ❌ Cabo desconectado ou dispositivo desligado |
| **GE0/0/4** | up/up | ⚠️ Funcionando MAS com 5 erros de entrada - investigar |
| **GE0/0/5** | *down/down | ⚠️ Desligada administrativamente (shutdown) |
| **XGE0/0/1** | up/up | ✅ Uplink 10G funcionando, uso alto (45-60%) - normal |

---

#### Comando: `display interface description`

**O que faz?**
Mostra TODAS as interfaces com suas **descrições** (apelidos/identificações).

**Para que serve?**
- Identificar rapidamente o que está conectado em cada porta
- Ver qual porta liga para qual equipamento/local

**Sintaxe:**
```bash
display interface description
```

**O que você vai ver:**

```
Interface                   Status   Description
GigabitEthernet0/0/1        up       UPLINK-PARA-CORE-SW01
GigabitEthernet0/0/2        up       SERVER-WEB-01
GigabitEthernet0/0/3        down     LIVRE
GigabitEthernet0/0/4        up       OLT-ZTE-C300-SLOT1
GigabitEthernet0/0/5        down     CAMERA-IP-ENTRADA
XGigabitEthernet0/0/1       up       UPLINK-BACKBONE-10G
```

**Interpretando:**
- **GE0/0/1:** Conecta ao switch principal (Core)
- **GE0/0/2:** Servidor web
- **GE0/0/3:** Porta livre/não usada
- **GE0/0/4:** Conecta a uma OLT ZTE
- **XGE0/0/1:** Uplink de 10 Gbps para o backbone

✅ As descrições facilitam MUITO o troubleshooting!

---

#### Comando: `display interface [INTERFACE]`

**O que faz?**
Mostra informações **DETALHADAS** de uma interface específica.

**Para que serve?**
- Ver estatísticas de tráfego (pacotes, bytes, erros)
- Ver velocidade, duplex, MTU
- Ver última vez que a porta mudou de status
- Diagnosticar problemas em uma porta específica

**Sintaxe:**
```bash
display interface [TIPO] [NÚMERO]
```

**Exemplo:**
```bash
display interface GigabitEthernet 0/0/1
```

**O que você vai ver:**

```
GigabitEthernet0/0/1 current state : UP
Line protocol current state : UP
Description: UPLINK-PARA-CORE-SW01
Route Port,The Maximum Transmit Unit is 1500
Internet Address is 10.20.30.50/24
IP Sending Frames' Format is PKTFMT_ETHNT_2, Hardware address is 00aa-00bb-00cc
Port Mode: COMMON COPPER
Speed : 1000,  Loopback: NONE
Duplex: FULL,  Negotiation: ENABLE
Mdi   : AUTO,  Flow-control: DISABLE
Last physical up time   : 2025-11-01 08:30:00 UTC-03:00
Last physical down time : 2025-10-25 14:20:00 UTC-03:00
Current system time: 2025-11-13 10:15:30

Input bandwidth utilization  : 0.01%
Output bandwidth utilization : 0.02%

Input:  120450 packets, 15234000 bytes
        0 broadcasts, 0 multicasts
        0 errors, 0 drops, 0 overruns, 0 buffer failures
        0 CRC, 0 giants, 0 throttles, 0 runts
        0 aborts, 0 ignored, 0 parity errors

Output: 98320 packets, 12450000 bytes
        0 broadcasts, 0 multicasts
        0 errors, 0 drops, 0 underruns, 0 buffer failures
        0 collisions, 0 interface resets
        0 babbles, 0 late collisions, 0 deferred
```

**Interpretando os campos principais:**

| Campo | O que significa? | Valores |
|-------|------------------|---------|
| **current state: UP** | Interface está funcionando | UP ✅ ou DOWN ❌ |
| **Line protocol: UP** | Protocolo de comunicação OK | UP ✅ ou DOWN ❌ |
| **Description** | Identificação da porta | Texto descritivo |
| **Speed: 1000** | Velocidade em Mbps | 10, 100, 1000, 10000 |
| **Duplex: FULL** | Modo de transmissão | FULL (melhor) ou HALF |
| **Last physical up time** | Última vez que ligou | Data e hora |
| **Last physical down time** | Última vez que desligou | Data e hora |
| **Input: X packets** | Quantos pacotes RECEBEU | Número |
| **Output: X packets** | Quantos pacotes ENVIOU | Número |
| **errors** | Erros detectados | Ideal = 0 |
| **drops** | Pacotes descartados | Ideal = 0 |
| **CRC errors** | Erros de integridade de dados | Ideal = 0 ⚠️ |
| **collisions** | Colisões de pacotes | Ideal = 0 |

**Análise de problemas:**

| Problema | O que significa? | Causa Possível |
|----------|------------------|----------------|
| **CRC errors > 0** | Pacotes corrompidos | Cabo ruim, interferência, porta com defeito |
| **drops alto** | Switch descartando pacotes | Tráfego acima da capacidade, buffer cheio |
| **collisions alto** | Colisões na rede | Duplex errado (half ao invés de full), switch muito carregado |
| **giants** | Pacotes muito grandes | MTU incorreto |
| **runts** | Pacotes muito pequenos | Problema de cabo ou interface |

---

### 📌 3. Trabalhando com VLANs

#### O que é VLAN?

**VLAN** (Virtual LAN) é uma forma de **separar** tráfegos diferentes na mesma rede física.

**Analogia:** Imagine um prédio:
- **VLAN 10:** Apartamentos do 1º andar (Administrativo)
- **VLAN 20:** Apartamentos do 2º andar (Financeiro)
- **VLAN 30:** Apartamentos do 3º andar (TI)

Todos usam o **mesmo elevador** (switch), mas **não se misturam** (VLANs diferentes).

---

#### Comando: `display vlan`

**O que faz?**
Lista **TODAS** as VLANs configuradas no switch.

**Para que serve?**
- Ver quais VLANs existem
- Ver quantas portas cada VLAN tem

**Sintaxe:**
```bash
display vlan
```

**O que você vai ver:**

```
VLAN ID: 1
VLAN Type: common
Route Interface: not configured
Description: VLAN 0001
Tagged   Ports: none
Untagged Ports: GE0/0/10 GE0/0/11 GE0/0/12

VLAN ID: 10
VLAN Type: common
Route Interface: not configured
Description: VLAN_ADMIN
Tagged   Ports: GE0/0/1 GE0/0/2
Untagged Ports: GE0/0/3 GE0/0/4 GE0/0/5

VLAN ID: 20
VLAN Type: common
Route Interface: not configured
Description: VLAN_FINANCEIRO
Tagged   Ports: GE0/0/1 GE0/0/2
Untagged Ports: GE0/0/6 GE0/0/7
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **VLAN ID** | Número identificador da VLAN (1-4094) |
| **VLAN Type: common** | VLAN normal/comum |
| **Description** | Nome/descrição da VLAN |
| **Tagged Ports** | Portas que carregam a VLAN COM etiqueta (trunks) |
| **Untagged Ports** | Portas que carregam a VLAN SEM etiqueta (access) |

**Entendendo Tagged vs Untagged:**

- **Tagged (Trunk):** Usado em portas que conectam **switches entre si** ou **switches com roteadores**
  - A "etiqueta" (número da VLAN) vai junto com os dados
  - Uma porta trunk pode carregar **VÁRIAS VLANs** ao mesmo tempo
  - Analogia: Caminhão que leva caixas de várias cores (cada cor = uma VLAN)

- **Untagged (Access):** Usado em portas que conectam **usuários finais** (computadores, telefones, impressoras)
  - A "etiqueta" é removida
  - Uma porta access carrega **APENAS UMA VLAN**
  - Analogia: Entregador que tira a caixa colorida e entrega só o produto

---

#### Comando: `display vlan [VLAN-ID]`

**O que faz?**
Mostra detalhes de uma VLAN específica.

**Para que serve?**
- Ver em quais portas uma VLAN está configurada
- Verificar se uma VLAN existe
- Ver quantos MACs foram aprendidos nessa VLAN

**Sintaxe:**
```bash
display vlan [NÚMERO]
```

**Exemplo:**
```bash
display vlan 10
```

**O que você vai ver:**

```
VLAN ID: 10
VLAN Type: common
Route Interface: not configured
Description: VLAN_ADMIN
Tagged   Ports:
  GigabitEthernet0/0/1
  GigabitEthernet0/0/2
Untagged Ports:
  GigabitEthernet0/0/3
  GigabitEthernet0/0/4
  GigabitEthernet0/0/5

MAC Address Learning: Enable
MAC Addresses: 15
```

**Interpretando:**

- **GE0/0/1 e GE0/0/2 (Tagged):** Provavelmente são uplinks/trunks para outros switches
- **GE0/0/3, 4, 5 (Untagged):** Portas de acesso para usuários
- **MAC Addresses: 15:** Há 15 dispositivos nesta VLAN

---

#### Comando: `display mac-address vlan [VLAN-ID]`

**O que faz?**
Mostra os **endereços MAC** aprendidos em uma VLAN específica.

**Para que serve?**
- Ver quais dispositivos estão em uma VLAN
- Identificar por qual porta cada dispositivo está acessando
- Troubleshooting: ver se um dispositivo está sendo "visto" pelo switch

**Sintaxe:**
```bash
display mac-address vlan [NÚMERO]
```

**Exemplo:**
```bash
display mac-address vlan 10
```

**O que você vai ver:**

```
MAC Address    VLAN    Port                Type      Last-updated
-----------------------------------------------------------------
00aa-00bb-00cc 10      GE0/0/3             dynamic   2025-11-13 10:10:25
00aa-00bb-00dd 10      GE0/0/3             dynamic   2025-11-13 10:05:10
00aa-00bb-00ee 10      GE0/0/4             dynamic   2025-11-13 10:12:50
00aa-00bb-00ff 10      GE0/0/5             dynamic   2025-11-13 10:08:30
00aa-00bb-0011 10      GE0/0/1             dynamic   2025-11-13 10:15:00
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **MAC Address** | Endereço físico único do dispositivo |
| **VLAN** | Em qual VLAN esse dispositivo está |
| **Port** | Por qual porta ele está conectado |
| **Type: dynamic** | Aprendido automaticamente (não configurado manualmente) |
| **Last-updated** | Última vez que o switch viu esse MAC |

**Análise:**

- **4 MACs nas portas GE0/0/3, 4, 5:** Dispositivos finais (PCs, impressoras)
- **1 MAC na porta GE0/0/1:** Provavelmente de outro switch ou roteador (uplink)

**Troubleshooting:**

✅ **Se o MAC do cliente APARECE:** O switch está vendo o dispositivo
❌ **Se o MAC NÃO APARECE:** Problema de conectividade (cabo, porta, VLAN errada)

---

### 📌 4. Diagnóstico e Troubleshooting

#### Comando: `display current-configuration`

**O que faz?**
Mostra **TODA** a configuração em execução do switch.

**Para que serve?**
- Backup da configuração
- Ver como o switch está configurado
- Auditoria

**Sintaxe:**
```bash
display current-configuration
```

⚠️ **ATENÇÃO:** Este comando gera MUITO texto (centenas ou milhares de linhas)!

**Melhor usar com filtros:**

```bash
# Ver apenas VLANs
display current-configuration | include vlan

# Ver apenas interfaces GigabitEthernet
display current-configuration | include GigabitEthernet

# Ver configuração de uma interface específica
display current-configuration interface GigabitEthernet 0/0/1
```

---

#### Comando: `display mac-address`

**O que faz?**
Mostra **TODOS** os endereços MAC aprendidos pelo switch (em todas as VLANs).

**Para que serve?**
- Ver quantos dispositivos estão conectados
- Identificar endereços MAC específicos

**Sintaxe:**
```bash
display mac-address
```

**O que você vai ver:**

```
MAC Address    VLAN    Port                Type      Last-updated
-----------------------------------------------------------------
00aa-00bb-00cc 10      GE0/0/3             dynamic   2025-11-13 10:10:25
00aa-00bb-00dd 10      GE0/0/3             dynamic   2025-11-13 10:05:10
00aa-00bb-00ee 20      GE0/0/6             dynamic   2025-11-13 10:12:50
00aa-00bb-00ff 30      GE0/0/8             dynamic   2025-11-13 10:08:30
...
Total: 245 MAC addresses
```

---

#### Comando: `display arp`

**O que faz?**
Mostra a **tabela ARP** (correspondência entre IPs e MACs).

**Para que serve?**
- Ver qual IP está associado a qual MAC
- Identificar dispositivos por IP
- Troubleshooting de conectividade de camada 3

**Sintaxe:**
```bash
display arp
```

**O que você vai ver:**

```
IP Address      MAC Address     VLAN    Interface         Aging Type
--------------------------------------------------------------------
10.20.30.1      00aa-00bb-00cc  10      GE0/0/3           20    D
10.20.30.2      00aa-00bb-00dd  10      GE0/0/3           18    D
10.20.30.10     00aa-00bb-00ee  10      GE0/0/4           25    D
192.168.1.1     00aa-00bb-00ff  1       GE0/0/10          30    D
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **IP Address** | Endereço IP do dispositivo |
| **MAC Address** | Endereço físico correspondente |
| **VLAN** | Em qual VLAN está |
| **Interface** | Por qual porta está conectado |
| **Aging** | Tempo restante antes de expirar (minutos) |
| **Type: D** | Dinâmico (aprendido automaticamente) |

**Uso prático:**

Se você sabe o IP do cliente mas não sabe o MAC:
```bash
display arp | include 10.20.30.10
```

Se você sabe o MAC mas não sabe o IP:
```bash
display arp | include 00aa-00bb-00ee
```

---

#### Comando: `display interface counters error`

**O que faz?**
Mostra **contadores de erros** de TODAS as interfaces.

**Para que serve?**
- Identificar rapidamente portas com problemas
- Ver se há erros de CRC, drops, collisions
- Diagnóstico de qualidade de links

**Sintaxe:**
```bash
display interface counters error
```

**O que você vai ver:**

```
Interface            InErrors  InCRC  InDiscards  OutErrors  OutDiscards  Collisions
-----------------------------------------------------------------------------------
GE0/0/1                     0      0           0          0            0           0
GE0/0/2                     0      0           0          0            0           0
GE0/0/3                     5      2           3          0            0           0  ← PROBLEMA!
GE0/0/4                     0      0           0          0            0           0
GE0/0/5                   120     80          40          5            0          15  ← PROBLEMA SÉRIO!
```

**Interpretando:**

| Coluna | O que significa? | Ideal |
|--------|------------------|-------|
| **InErrors** | Erros totais de entrada | 0 |
| **InCRC** | Erros de CRC (corrupção de dados) | 0 |
| **InDiscards** | Pacotes descartados na entrada | 0 |
| **OutErrors** | Erros de saída | 0 |
| **OutDiscards** | Pacotes descartados na saída | 0 |
| **Collisions** | Colisões de pacotes | 0 |

**Análise:**

| Porta | Status | Problema | Causa Possível |
|-------|--------|----------|----------------|
| **GE0/0/3** | ⚠️ | 5 erros (2 CRC) | Cabo ruim, começando a degradar |
| **GE0/0/5** | ❌ | 120 erros (80 CRC) + 15 colisões | Cabo muito ruim, duplex errado, ou porta com defeito |

---

#### Comando: `display cpu-usage`

**O que faz?**
Mostra o **uso de CPU** do switch.

**Para que serve?**
- Ver se o switch está sobrecarregado
- Diagnosticar lentidão

**Sintaxe:**
```bash
display cpu-usage
```

**O que você vai ver:**

```
CPU Usage Statistics at 2025-11-13 10:15:30 UTC-03:00
CPU usage:
  5 seconds: 8%
  1 minute:  6%
  5 minutes: 5%
```

**Valores de referência:**

| CPU | Status | Ação |
|-----|--------|------|
| **0-30%** | ✅ Normal | Nenhuma |
| **30-50%** | ⚠️ Moderado | Monitorar |
| **50-80%** | ❌ Alto | Investigar (loops, broadcast storm, ataque) |
| **80-100%** | ❌ Crítico | Ação imediata! |

---

#### Comando: `display memory-usage`

**O que faz?**
Mostra o **uso de memória** do switch.

**Sintaxe:**
```bash
display memory-usage
```

**O que você vai ver:**

```
Memory Statistics:
Total memory: 2048 MB
Used memory:  512 MB (25%)
Free memory:  1536 MB (75%)
```

**Valores de referência:**

| Memória Usada | Status |
|---------------|--------|
| **0-70%** | ✅ Normal |
| **70-85%** | ⚠️ Alto |
| **85-100%** | ❌ Crítico |

---

### 📌 5. Testes de Conectividade

#### Comando: `ping [IP]`

**O que faz?**
Testa conectividade para um IP (igual no Windows).

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
PING 8.8.8.8: 56 data bytes, press CTRL+C to break
Reply from 8.8.8.8: bytes=56 Sequence=1 ttl=117 time=15 ms
Reply from 8.8.8.8: bytes=56 Sequence=2 ttl=117 time=14 ms
Reply from 8.8.8.8: bytes=56 Sequence=3 ttl=117 time=16 ms
Reply from 8.8.8.8: bytes=56 Sequence=4 ttl=117 time=15 ms

--- 8.8.8.8 ping statistics ---
4 packet(s) transmitted
4 packet(s) received
0.00% packet loss
round-trip min/avg/max = 14/15/16 ms
```

✅ **0% packet loss** = Conectividade perfeita!

---

#### Comando: `ping -c [NÚMERO] [IP]`

**O que faz?**
Envia uma quantidade específica de pings.

**Exemplo:**
```bash
ping -c 100 8.8.8.8
```

Envia 100 pings e para.

---

#### Comando: `tracert [IP]`

**O que faz?**
Mostra o **caminho** até o destino (igual tracert do Windows).

**Sintaxe:**
```bash
tracert [IP]
```

**Exemplo:**
```bash
tracert 8.8.8.8
```

**O que você vai ver:**

```
traceroute to 8.8.8.8 (8.8.8.8), max hops: 30, packet size: 40
 1  10.20.30.1     5 ms    4 ms    5 ms
 2  200.150.100.1  12 ms   11 ms   13 ms
 3  200.150.100.2  15 ms   14 ms   16 ms
 4  8.8.8.8        20 ms   19 ms   21 ms
```

---

### 📌 6. Informações do Sistema

#### Comando: `display version`

**O que faz?**
Mostra versão do software, modelo do switch, uptime.

**Sintaxe:**
```bash
display version
```

**O que você vai ver:**

```
Huawei Versatile Routing Platform Software
VRP (R) software, Version 8.180 (S5720 V200R011C10SPC600)
Huawei S5720-28X-SI-AC

System uptime is 150 days, 12 hours, 30 minutes
```

---

#### Comando: `display device`

**O que faz?**
Mostra **placas e módulos** instalados no switch.

**Sintaxe:**
```bash
display device
```

**O que você vai ver:**

```
Slot  Card-Type                Status     
0     S5720-28X-SI-AC          Normal     
1     SFP-10G-LR              Normal     
2     SFP-10G-LR              Normal     
3     Empty                   -          
```

---

#### Comando: `display temperature`

**O que faz?**
Mostra **temperatura** do switch.

**Sintaxe:**
```bash
display temperature
```

**Valores normais:** 35-55°C  
⚠️ **Atenção:** > 60°C  
❌ **Crítico:** > 70°C

---

#### Comando: `display power`

**O que faz?**
Mostra status das **fontes de alimentação**.

**Sintaxe:**
```bash
display power
```

**O que você vai ver:**

```
Power  Status     Mode
PWR1   Normal     AC
PWR2   Absent     -
```

✅ **Normal:** Fonte funcionando  
❌ **Absent:** Fonte não instalada  
❌ **Fault:** Fonte com defeito

---

#### Comando: `display fan`

**O que faz?**
Mostra status dos **ventiladores** (coolers).

**Sintaxe:**
```bash
display fan
```

**O que você vai ver:**

```
Fan  Status     Speed
FAN1 Normal     50%
FAN2 Normal     50%
```

✅ **Normal:** Ventilador funcionando  
❌ **Fault:** Ventilador com defeito (switch vai superaquecer!)

---

#### Comando: `display transceiver`

**O que faz?**
Mostra informações de **SFPs** (módulos ópticos para fibra).

**Para que serve?**
- Ver se SFP está instalado e reconhecido
- Ver potência TX e RX do sinal óptico
- Diagnosticar problemas de fibra

**Sintaxe:**
```bash
display transceiver
```

**O que você vai ver:**

```
Interface          Type              Status    TxPower(dBm)  RxPower(dBm)
GE0/0/1            SFP-1000-LX       Normal    -2.5          -10.2
GE0/0/2            SFP-1000-LX       Normal    -3.1          -25.8
XGE0/0/1           SFP-10G-LR        Normal    -1.2          -8.5
XGE0/0/2           Empty             -         -             -
```

**Interpretando:**

| Campo | O que significa? |
|-------|------------------|
| **Type** | Modelo do SFP (1G, 10G, LX, SR, LR) |
| **Status: Normal** | SFP reconhecido e funcionando |
| **TxPower** | Potência de sinal que SAI (transmit) |
| **RxPower** | Potência de sinal que CHEGA (receive) |

**Valores de referência RX (fibra monomodo):**

| RX (dBm) | Status |
|----------|--------|
| **-3 a -20 dBm** | ✅ Ótimo |
| **-20 a -25 dBm** | ✅ Bom |
| **-25 a -28 dBm** | ⚠️ Limiar |
| **< -28 dBm** | ❌ Fraco (problema na fibra) |

**No exemplo:**

| Porta | RX | Status |
|-------|----|--------|
| **GE0/0/1** | -10.2 dBm | ✅ Ótimo |
| **GE0/0/2** | -25.8 dBm | ⚠️ No limiar - monitorar |
| **XGE0/0/1** | -8.5 dBm | ✅ Ótimo |

---

### 📌 7. Logs e Histórico

#### Comando: `display logbuffer`

**O que faz?**
Mostra os **logs do sistema** (eventos, erros, mudanças).

**Para que serve?**
- Ver o que aconteceu recentemente no switch
- Investigar quando uma porta caiu
- Ver erros e avisos

**Sintaxe:**
```bash
display logbuffer
```

**O que você vai ver:**

```
Nov 13 2025 10:10:25 SWITCH-NOME %%01IFNET/4/LINK_STATE(l)[0]:The line protocol on the interface GigabitEthernet0/0/3 has entered the DOWN state.

Nov 13 2025 10:12:30 SWITCH-NOME %%01IFNET/4/LINK_STATE(l)[1]:The line protocol on the interface GigabitEthernet0/0/3 has entered the UP state.

Nov 13 2025 09:45:10 SWITCH-NOME %%01STP/4/PORT_DISCARDING(l)[2]:Instance 0's port GigabitEthernet0/0/5 has been set to discarding state.
```

**Interpretando:**

- **10:10:25:** Porta GE0/0/3 caiu (DOWN)
- **10:12:30:** Porta GE0/0/3 voltou (UP) - ficou 2 minutos fora
- **09:45:10:** STP bloqueou porta GE0/0/5 (evitando loop)

---

#### Comando: `display alarm`

**O que faz?**
Mostra **alarmes ativos** no switch.

**Sintaxe:**
```bash
display alarm
```

**O que você pode ver:**

```
Active Alarms:
- Temperature high on slot 0 (Level: Minor)
- Fan fault on FAN2 (Level: Major)
- Interface GigabitEthernet0/0/5 down (Level: Warning)
```

---

## 🔧 Cenários Práticos do Dia a Dia

### 📞 Cenário 1: Link Down no Switch

**Sintoma:** Alarme no Zabbix: "Link down GE0/0/5".

**Passo a passo:**

```bash
# PASSO 1: Ver resumo das portas
display interface brief

# Procure pela GE0/0/5:
# GigabitEthernet0/0/5   down   down   ...

# PASSO 2: Ver descrição para saber o que está conectado
display interface description | include GE0/0/5

# OUTPUT:
# GE0/0/5   down   OLT-ZTE-UNIDADE-X

# PASSO 3: Ver detalhes da interface
display interface GigabitEthernet 0/0/5

# Verificar:
# - Last physical down time: QUANDO caiu?
# - Errors: Há muitos erros?

# PASSO 4: Ver logs
display logbuffer | include GigabitEthernet0/0/5

# Procure por:
# - LINK_STATE DOWN
# - Errors
# - STP messages

# PASSO 5: Verificar erros
display interface counters error | include GE0/0/5
```

**Diagnóstico:**

| Situação | Causa | Solução |
|----------|-------|---------|
| PHY down + sem erros | Cabo desconectado ou dispositivo desligado | Verificar cabo e dispositivo |
| PHY up + Protocol down | Problema de camada 2 (VLAN, STP) | Verificar configuração |
| Muitos CRC errors | Cabo ruim | Trocar cabo |
| STP bloqueando | Loop detection | Normal se há redundância |

---

### 📞 Cenário 2: VLAN Não Funciona

**Sintoma:** Cliente não acessa a rede da VLAN 100.

**Passo a passo:**

```bash
# PASSO 1: Verificar se a VLAN existe
display vlan 100

# Se aparecer: VLAN exists
# Se NÃO aparecer: VLAN não criada! → Escalar para N2

# PASSO 2: Ver em quais portas a VLAN está
display vlan 100

# Verificar:
# - A porta do cliente está na lista (untagged)?
# - O uplink está na lista (tagged)?

# PASSO 3: Ver se há tráfego (MACs) nessa VLAN
display mac-address vlan 100

# Se NÃO houver MACs: Sem tráfego → Problema!

# PASSO 4: Verificar porta do cliente
# (Descobrir qual porta pela descrição ou pela localização física)
display interface GigabitEthernet 0/0/10

# Status up ou down?

# PASSO 5: Ver configuração da porta
display current-configuration interface GigabitEthernet 0/0/10

# Verificar:
# - port link-type access (ou trunk?)
# - port default vlan 100 (está configurado?)
```

**Diagnóstico:**

| Situação | Causa | Solução |
|----------|-------|---------|
| VLAN não existe | Não foi criada | Escalar para N2 criar VLAN |
| Porta não está na VLAN | Configuração errada | Escalar para N2 adicionar porta na VLAN |
| Uplink não tem VLAN tagged | VLAN não sai do switch | Escalar para N2 adicionar VLAN no trunk |
| Porta down | Cabo ou dispositivo problema | Verificar físico |

---

### 📞 Cenário 3: Switch Lento - CPU Alta

**Sintoma:** Equipamentos conectados ao switch estão lentos.

**Passo a passo:**

```bash
# PASSO 1: Verificar CPU
display cpu-usage

# Se > 50%: PROBLEMA!

# PASSO 2: Verificar memória
display memory-usage

# Se > 80%: PROBLEMA!

# PASSO 3: Ver logs recentes
display logbuffer

# Procure por:
# - Loops (mensagens STP repetitivas)
# - Broadcast storms
# - Erros

# PASSO 4: Ver portas com mais tráfego
display interface brief

# Procure por InUti ou OutUti > 80%

# PASSO 5: Ver MACs aprendidos por porta
display mac-address

# Se uma porta tem MUITOS MACs (>100): Possível loop ou hub antigo conectado
```

**Possíveis causas:**

1. **Loop de rede:** STP desabilitado ou mal configurado
2. **Broadcast storm:** Dispositivo defeituoso enviando broadcasts
3. **Ataque:** DoS, flood
4. **Hub antigo conectado:** Muitos dispositivos em uma porta

**Ação:** Escalar para N2/N3 com evidências (CPU, logs, porta problemática).

---

### 📞 Cenário 4: Fibra com Problema - Sinal Fraco

**Sintoma:** Link intermitente ou lento em porta com SFP.

**Passo a passo:**

```bash
# PASSO 1: Ver status dos SFPs
display transceiver

# Procure pela porta com problema:
# GE0/0/1   SFP-1000-LX   Normal   -2.5   -28.5  ← RX FRACO!

# PASSO 2: Ver detalhes da interface
display interface GigabitEthernet 0/0/1

# Verificar:
# - Errors? CRC?
# - Input/Output errors?

# PASSO 3: Ver logs
display logbuffer | include GigabitEthernet0/0/1

# Procure por:
# - LINK_STATE flapping (UP e DOWN repetitivo)
# - "Optical module is abnormal"

# PASSO 4: Ver erros
display interface counters error | include GE0/0/1
```

**Valores de referência RX:**

| RX | Status | Ação |
|----|--------|------|
| **-3 a -25 dBm** | ✅ Bom | Nenhuma |
| **-25 a -28 dBm** | ⚠️ Limiar | Monitorar |
| **< -28 dBm** | ❌ Ruim | Limpar conector, verificar fibra |

**Se RX < -28 dBm:**

1. **Limpar conectores** (com álcool isopropílico e pano específico)
2. **Verificar patch cord** (trocar por um novo)
3. **Verificar SFP** (trocar de porta ou usar outro SFP de teste)
4. **Se nada resolver:** Problema na fibra (emenda ruim, cabo cortado)

---

### 📞 Cenário 5: Descobrir Onde um Dispositivo Está Conectado

**Sintoma:** Preciso saber em qual porta um dispositivo (MAC conhecido) está.

**Passo a passo:**

```bash
# PASSO 1: Buscar o MAC na tabela
display mac-address | include [MAC]

# Exemplo:
display mac-address | include 00aa-00bb-00cc

# OUTPUT:
# 00aa-00bb-00cc  10  GE0/0/8  dynamic  ...

# O dispositivo está na porta GE0/0/8!

# PASSO 2: Ver descrição dessa porta
display interface description | include GE0/0/8

# OUTPUT:
# GE0/0/8   up   SWITCH-SALA-A

# PASSO 3: Se precisar do IP:
display arp | include 00aa-00bb-00cc

# OUTPUT:
# 10.20.30.25  00aa-00bb-00cc  10  GE0/0/8  ...
```

✅ **Encontrado!**
- **Dispositivo:** MAC 00aa-00bb-00cc
- **IP:** 10.20.30.25
- **Porta:** GE0/0/8
- **Localização:** SWITCH-SALA-A
- **VLAN:** 10

---

## 📊 Tabela Resumo - Comandos por Situação

| Situação | Comandos | O que verificar? |
|----------|----------|------------------|
| **Link down** | `display interface brief`<br>`display interface [PORTA]`<br>`display logbuffer` | PHY/Protocol status<br>Last down time<br>Errors |
| **VLAN não funciona** | `display vlan [VLAN]`<br>`display mac-address vlan [VLAN]`<br>`display current-configuration interface [PORTA]` | VLAN existe?<br>Há MACs?<br>Porta está na VLAN? |
| **Switch lento** | `display cpu-usage`<br>`display memory-usage`<br>`display interface brief` | CPU > 50%?<br>Memória > 80%?<br>Porta saturada? |
| **Fibra com problema** | `display transceiver`<br>`display interface counters error` | RX < -28 dBm?<br>CRC errors? |
| **Encontrar dispositivo** | `display mac-address \| include [MAC]`<br>`display arp \| include [MAC ou IP]` | Qual porta?<br>Qual IP? |
| **Ver config geral** | `display current-configuration` | Toda configuração |
| **Health check** | `display version`<br>`display device`<br>`display temperature`<br>`display power`<br>`display fan` | Versão, uptime<br>Placas OK?<br>Temperatura OK?<br>Fontes OK?<br>Ventiladores OK? |

---

## 📖 Referências e Documentação Oficial

### 📚 Huawei Documentation Center

1. **Huawei Support:**
   - https://support.huawei.com/enterprise/

2. **S5700 Series Command Reference:**
   - https://support.huawei.com/enterprise/en/doc/

3. **VRP Command Reference:**
   - Documentação completa de comandos CLI

### 📚 Artigos e Tutoriais

1. **Huawei Learning:**
   - https://e.huawei.com/

2. **Configuração de VLANs:**
   - Tutoriais oficiais Huawei

3. **Troubleshooting Guides:**
   - Documentação oficial de resolução de problemas

---

## 💡 Dicas Finais para Iniciantes

### 1️⃣ Use TAB para Autocompletar

```bash
# Digite:
display int[TAB]

# O switch completa:
display interface
```

### 2️⃣ Use `?` para Ver Opções

```bash
display ?
# Lista TODOS os comandos "display"

display interface ?
# Lista todas as opções de "display interface"
```

### 3️⃣ Use `|` (pipe) para Filtrar

```bash
# Filtrar por palavra-chave:
display interface brief | include down

# Buscar apenas GigabitEthernet:
display interface brief | include GigabitEthernet
```

### 4️⃣ Comandos Úteis de Filtro

| Filtro | O que faz? | Exemplo |
|--------|-----------|---------|
| `\| include [texto]` | Mostra apenas linhas com esse texto | `display vlan \| include 100` |
| `\| exclude [texto]` | Remove linhas com esse texto | `display interface brief \| exclude down` |
| `\| begin [texto]` | Mostra a partir dessa linha | `display current-config \| begin vlan` |

### 5️⃣ Não Tenha Medo de Explorar

- Comandos `display` são **seguros** - apenas visualizam
- Não mudam configuração
- Explore à vontade!

### 6️⃣ Sempre Documente

Crie um caderno com:
- IPs dos switches
- Descrições das portas importantes
- VLANs usadas
- Procedimentos comuns

---

## 🎓 Exercícios Práticos

### Exercício 1: Exploração Básica

```bash
# Execute e entenda cada output:
display version
display device
display interface brief
display vlan
display mac-address
```

### Exercício 2: Investigação de Porta

```bash
# Escolha uma porta (ex: GE0/0/1):
display interface GigabitEthernet 0/0/1
display current-configuration interface GigabitEthernet 0/0/1
display interface counters error | include GE0/0/1
```

### Exercício 3: Análise de VLAN

```bash
# Escolha uma VLAN:
display vlan 10
display mac-address vlan 10
display current-configuration | include vlan 10
```

### Exercício 4: Busca de Dispositivo

```bash
# Pegue um MAC da tabela:
display mac-address

# Busque-o:
display mac-address | include [MAC-OBTIDO]
display arp | include [MAC-OBTIDO]
```

---

## 🏁 Conclusão

Parabéns por chegar até aqui! Você agora tem uma base sólida para trabalhar com switches Huawei. Lembre-se:

✅ **display interface brief** é seu comando mais usado - visão geral das portas  
✅ **display vlan** para entender VLANs  
✅ **display mac-address** para encontrar dispositivos  
✅ **display transceiver** para diagnosticar fibras  
✅ **No NOC N1**, use apenas comandos `display` - nunca configure sem autorização  

**Continue estudando os outros guias:**
- **GUIA_COMANDOS_WINDOWS_BASICOS.md** - Comandos de rede do Windows
- **GUIA_ZTE_INICIANTE.md** - OLTs ZTE
- **GUIA_DATACOM_INICIANTE.md** - Switches Datacom

**Boa sorte no NOC! 🚀**

---

**Versão:** 1.0  
**Data:** Novembro 2025  
**Público-Alvo:** Analistas NOC Iniciantes  
**Dificuldade:** Básico a Intermediário  
**Equipamentos:** Huawei S5700, S5720, S6720 series

