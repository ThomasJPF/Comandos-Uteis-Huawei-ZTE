# 🪟 Guia de Comandos Básicos Windows para NOC - Para Iniciantes

## 🎯 Bem-vindo ao Mundo do Troubleshooting!

Olá! Se você está lendo isso, provavelmente é seu primeiro dia no NOC (Network Operations Center - Centro de Operações de Rede) ou está começando a aprender sobre redes. **Não se preocupe!** Vamos explicar tudo do zero, com calma e com muitos exemplos.

### 🤔 O que você vai aprender aqui?

Neste guia, você vai aprender a usar ferramentas do Windows para:

- **Testar se um computador/servidor está ligado e acessível** (ping)
- **Ver o caminho que seus dados percorrem na internet** (tracert)
- **Descobrir sua configuração de rede** (ipconfig)
- **Testar a velocidade da sua conexão** (throughput)
- **Resolver problemas de DNS** (nslookup)
- E muito mais!

---

## 📚 Glossário - Entenda os termos antes de começar

Antes de executar comandos, vamos entender alguns termos que você vai ver muito:

| Termo                      | O que significa?                                            | Analogia Simples                                                    |
| -------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------- |
| **IP (Internet Protocol)** | É como o "endereço" de um computador na rede                | Como o endereço da sua casa: Rua X, Número Y                        |
| **Ping**                   | Enviar um "oi!" para outro computador e ver se ele responde | Como bater palmas em uma caverna e ouvir o eco voltar               |
| **Latência**               | O tempo que leva para sua mensagem chegar e voltar          | Tempo entre você gritar e ouvir o eco                               |
| **Pacote**                 | Um pedacinho de dado enviado pela rede                      | Como uma carta enviada pelo correio                                 |
| **Gateway**                | A "porta de saída" da sua rede local para a internet        | Como a porta da sua casa que te leva para a rua                     |
| **DNS**                    | Tradutor de nomes (google.com) para números (IP)            | Como uma agenda telefônica que transforma "João" em "11-99999-9999" |
| **TTL (Time To Live)**     | Quantos "pulos" um pacote pode dar antes de desistir        | Como uma carta que só pode passar por 10 agências de correio        |
| **Throughput**             | Quantidade de dados que passa pela rede por segundo         | Como a quantidade de água que passa por um cano                     |
| **ms (milissegundos)**     | Unidade de tempo, 1000 ms = 1 segundo                       | Um piscar de olhos = cerca de 300ms                                 |

---

## 🔑 Como Abrir o Prompt de Comando (CMD)

Antes de usar qualquer comando, você precisa abrir o **CMD** (Prompt de Comando):

### Método 1: Atalho Rápido ⚡

1. Pressione **Windows + R**
2. Digite `cmd`
3. Aperte **Enter**

### Método 2: Menu Iniciar 🔍

1. Clique no **Menu Iniciar**
2. Digite `cmd` ou `prompt de comando`
3. Clique no aplicativo **Prompt de Comando**

### Método 3: PowerShell (Alternativa Moderna) 💻

1. Pressione **Windows + X**
2. Escolha **Windows PowerShell** ou **Terminal**

> **💡 Dica:** Todos os comandos deste guia funcionam tanto no CMD quanto no PowerShell!

---

## 📝 Comando 1: PING - Seu Melhor Amigo no NOC

### 🤔 O que é o PING?

O comando `ping` é **O COMANDO MAIS IMPORTANTE** que você vai usar no NOC. Ele envia pequenos pacotes de dados para um computador/servidor e espera uma resposta. É como você gritar "Oi!" e esperar ouvir "Oi!" de volta.

**Para que serve?**

- Testar se um servidor está online
- Medir a velocidade da conexão (latência)
- Verificar se há perda de pacotes (instabilidade)

---

### 📖 Sintaxe Básica

```cmd
ping [endereço IP ou nome do site]
```

---

### 🎯 Exemplo 1: Ping Básico

```cmd
ping 8.8.8.8
```

**O que esse comando faz?**

- Envia 4 pacotes para o servidor DNS do Google (8.8.8.8)
- Mostra quanto tempo cada pacote levou para ir e voltar
- No Windows, por padrão, envia apenas 4 pacotes e para

**O que você vai ver:**

```
Disparando 8.8.8.8 com 32 bytes de dados:
Resposta de 8.8.8.8: bytes=32 tempo=15ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=14ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=16ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=15ms TTL=117

Estatísticas do Ping para 8.8.8.8:
    Pacotes: Enviados = 4, Recebidos = 4, Perdidos = 0 (0% de perda),
Aproximar um número redondo de vezes em milissegundos:
    Mínimo = 14ms, Máximo = 16ms, Média = 15ms
```

**Como interpretar isso?**

| Informação            | O que significa?                        | Está bom?     |
| --------------------- | --------------------------------------- | ------------- |
| `Resposta de 8.8.8.8` | O servidor respondeu! Está online!      | ✅ Sim        |
| `bytes=32`            | Tamanho do pacote enviado               | ✅ Normal     |
| `tempo=15ms`          | Levou 15 milissegundos para ir e voltar | ✅ Excelente! |
| `TTL=117`             | O pacote pode dar mais 117 "pulos"      | ✅ Normal     |
| `Perdidos = 0`        | Nenhum pacote se perdeu                 | ✅ Perfeito!  |

**Valores de Referência (Latência):**

- ✅ **0-50ms:** Excelente (ótimo para jogos, vídeo-chamadas)
- ✅ **50-100ms:** Bom (uso normal da internet)
- ⚠️ **100-200ms:** Razoável (pode ter pequenos atrasos)
- ❌ **200ms+:** Ruim (conexão lenta)

---

### 🎯 Exemplo 2: Ping Contínuo (Não Para)

```cmd
ping 8.8.8.8 -t
```

**O que esse comando faz?**

- O `-t` faz o ping **NÃO PARAR NUNCA**
- Útil para monitorar uma conexão por um longo período
- Você verá pacotes sendo enviados continuamente

**Como parar o ping contínuo?**

- Pressione **Ctrl + C** para parar

**Quando usar?**

- Quando você quer monitorar se uma conexão está estável
- Quando um cliente diz "a internet cai de vez em quando"
- Para testar se o problema é temporário ou constante

**O que você vai ver:**

```
Disparando 8.8.8.8 com 32 bytes de dados:
Resposta de 8.8.8.8: bytes=32 tempo=15ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=14ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=16ms TTL=117
Esgotou o tempo limite do pedido.
Resposta de 8.8.8.8: bytes=32 tempo=15ms TTL=117
Resposta de 8.8.8.8: bytes=32 tempo=15ms TTL=117
... (continua até você apertar Ctrl+C)
```

> **⚠️ Viu o "Esgotou o tempo limite do pedido"?** Isso significa que UM pacote se perdeu! Se isso acontece muito, a conexão está instável.

---

### 🎯 Exemplo 3: Ping com Quantidade Específica

```cmd
ping 8.8.8.8 -n 100
```

**O que esse comando faz?**

- O `-n 100` faz o ping enviar **100 pacotes** e depois parar
- Útil quando você quer testar por mais tempo, mas não infinitamente

**Quando usar?**

- Para fazer um teste mais completo (4 pacotes é muito pouco)
- Para ter estatísticas mais confiáveis

---

### 🎯 Exemplo 4: Ping com Pacotes Maiores

```cmd
ping 8.8.8.8 -l 1000
```

**O que esse comando faz?**

- O `-l 1000` (letra L minúscula) envia pacotes de **1000 bytes** ao invés de 32
- Útil para testar se a rede aguenta pacotes maiores

**Por que fazer isso?**

- Às vezes, uma conexão funciona com pacotes pequenos mas falha com pacotes grandes
- Simula melhor o uso real da internet (vídeos, downloads)

---

### 🎯 Exemplo 5: Combinando Opções

```cmd
ping 8.8.8.8 -t -l 1000
```

**O que esse comando faz?**

- Ping **contínuo** (`-t`) com pacotes de **1000 bytes** (`-l 1000`)
- Teste completo de estresse da conexão!

---

### 🎯 Exemplo 6: Ping para um Site (Nome ao invés de IP)

```cmd
ping www.google.com
```

**O que esse comando faz?**

- Faz ping para o site do Google
- O Windows automaticamente converte "www.google.com" para um IP
- Útil para testar se o DNS está funcionando

**O que você vai ver:**

```
Disparando www.google.com [142.250.185.36] com 32 bytes de dados:
Resposta de 142.250.185.36: bytes=32 tempo=15ms TTL=117
...
```

> **💡 Viu o `[142.250.185.36]`?** Esse é o IP real do servidor do Google! O DNS converteu "www.google.com" para esse número.

**Se você ver:**

```
Não foi possível localizar o host www.google.com. Verifique o nome e tente novamente.
```

❌ **Problema de DNS!** O Windows não conseguiu transformar o nome em IP. Possíveis causas:

- Seu servidor DNS está offline
- Você digitou o nome errado
- Não tem conexão com a internet

---

### 📊 Tabela Resumo - Opções do PING

| Opção         | O que faz?                          | Exemplo                  |
| ------------- | ----------------------------------- | ------------------------ |
| `-t`          | Ping contínuo (não para até Ctrl+C) | `ping 8.8.8.8 -t`        |
| `-n [número]` | Define quantos pacotes enviar       | `ping 8.8.8.8 -n 100`    |
| `-l [bytes]`  | Define tamanho do pacote            | `ping 8.8.8.8 -l 1000`   |
| `-w [ms]`     | Define tempo máximo de espera       | `ping 8.8.8.8 -w 5000`   |
| `-4`          | Força uso de IPv4                   | `ping www.google.com -4` |
| `-6`          | Força uso de IPv6                   | `ping www.google.com -6` |

---

## 📝 Comando 2: TRACERT - Rastreando o Caminho dos Dados

### 🤔 O que é o TRACERT?

O comando `tracert` (trace route = traçar rota) mostra **TODOS OS PONTOS** que seus dados passam até chegar ao destino. É como ver todas as cidades que um ônibus passa entre sua casa e o destino final.

**Para que serve?**

- Ver onde seus dados estão demorando (qual ponto da rota é lento)
- Identificar onde a conexão está falhando
- Entender a estrutura da rede

**Analogia:** Imagine que você quer ir de São Paulo até o Rio de Janeiro de ônibus. O tracert mostra:

1. Sua casa (0ms)
2. Rodoviária de SP (5ms)
3. Pedágio da Régis Bittencourt (20ms)
4. Cidade de Resende (80ms)
5. Rodoviária do Rio (150ms)

---

### 📖 Sintaxe Básica

```cmd
tracert [endereço IP ou nome do site]
```

---

### 🎯 Exemplo 1: Tracert Básico

```cmd
tracert 8.8.8.8
```

**O que esse comando faz?**

- Mostra TODOS os roteadores/switches entre você e o Google DNS
- Para cada ponto, mostra quanto tempo levou (3 tentativas)

**O que você vai ver:**

```
Rastreando a rota para dns.google [8.8.8.8]
com no máximo 30 saltos:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2     5 ms     4 ms     5 ms  10.20.30.1
  3    12 ms    11 ms    13 ms  200.150.100.1
  4    15 ms    14 ms    16 ms  200.150.100.2
  5    20 ms    19 ms    21 ms  8.8.8.8

Rastreamento concluído.
```

**Como interpretar cada linha?**

| Coluna                  | O que significa?                           |
| ----------------------- | ------------------------------------------ |
| **Número (1, 2, 3...)** | O "salto" (hop) - cada roteador no caminho |
| **<1 ms, 5 ms, 12 ms**  | Tempo até esse ponto (3 medições)          |
| **192.168.1.1**         | IP desse ponto da rota                     |

**Interpretando o exemplo acima:**

1. **Salto 1 (192.168.1.1):** Seu roteador de casa - resposta instantânea (<1ms) ✅
2. **Salto 2 (10.20.30.1):** Roteador do seu provedor - 5ms ✅
3. **Salto 3-4:** Roteadores intermediários na internet - 12-15ms ✅
4. **Salto 5 (8.8.8.8):** Servidor do Google - 20ms total ✅

---

### 🎯 Exemplo 2: Identificando Problemas com Tracert

```cmd
tracert 8.8.8.8
```

**Cenário com PROBLEMA:**

```
Rastreando a rota para dns.google [8.8.8.8]
com no máximo 30 saltos:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2     5 ms     4 ms     5 ms  10.20.30.1
  3    12 ms    11 ms    13 ms  200.150.100.1
  4     *        *        *     Esgotado o tempo limite do pedido.
  5     *        *        *     Esgotado o tempo limite do pedido.
  6     *        *        *     Esgotado o tempo limite do pedido.
```

**O que significa o `*` (asterisco)?**

❌ O asterisco significa que aquele ponto **NÃO RESPONDEU** no tempo limite.

**Possíveis causas:**

1. Aquele roteador está configurado para **não responder tracert** (comum em alguns lugares por segurança)
2. Aquele ponto está **offline/com problema**
3. Há um **firewall bloqueando**

**Como saber se é problema real?**

- Se você consegue acessar o site/IP no navegador, provavelmente é apenas bloqueio de tracert
- Se você NÃO consegue acessar, o problema está em um dos pontos com `*`

---

### 🎯 Exemplo 3: Tracert para um Site

```cmd
tracert www.google.com
```

**O que esse comando faz?**

- Igual ao tracert com IP, mas você pode usar nomes
- Útil quando você só sabe o nome do site

---

### 🎯 Exemplo 4: Tracert Mais Rápido

```cmd
tracert -d 8.8.8.8
```

**O que esse comando faz?**

- O `-d` impede que o Windows tente descobrir o NOME de cada IP
- Muito mais rápido!

**Quando usar?**

- Quando você só quer ver os números (IPs)
- Quando o tracert está demorando muito

---

### 📊 Valores de Referência - Tracert

| Situação                                 | O que significa?                                  |
| ---------------------------------------- | ------------------------------------------------- |
| **Saltos 1-3:** < 20ms                   | ✅ Sua rede local e provedor estão ótimos         |
| **Saltos 4-10:** < 50ms                  | ✅ Rota normal pela internet                      |
| **Saltos 4-10:** > 100ms                 | ⚠️ Algum ponto está lento                         |
| **Muitos `*` no meio, mas chega ao fim** | ⚠️ Provavelmente bloqueio de firewall (normal)    |
| **`*` no final e não chega ao destino**  | ❌ Problema! O servidor está offline ou bloqueado |
| **Salto aumenta 200ms+ de repente**      | ❌ Gargalo naquele ponto!                         |

---

## 📝 Comando 3: PATHPING - O Melhor dos Dois Mundos

### 🤔 O que é o PATHPING?

O `pathping` é uma **combinação de ping + tracert**. Ele:

1. Primeiro faz um tracert (mostra o caminho)
2. Depois fica 300 segundos (5 minutos) testando cada ponto
3. Mostra estatísticas detalhadas de perda de pacotes

**Para que serve?**

- Encontrar EXATAMENTE onde está havendo perda de pacotes
- Diagnosticar problemas intermitentes
- Ter um relatório completo da qualidade da rota

---

### 📖 Sintaxe Básica

```cmd
pathping [endereço IP ou nome]
```

---

### 🎯 Exemplo 1: Pathping Básico

```cmd
pathping 8.8.8.8
```

**O que esse comando faz?**

- Faz tracert para 8.8.8.8
- Depois testa CADA ponto por 5 minutos
- Mostra um relatório final

**IMPORTANTE:** ⏰ Este comando **DEMORA 5 MINUTOS!** Seja paciente!

**O que você vai ver:**

```
Rastreando a rota para dns.google [8.8.8.8]
com no máximo 30 saltos:
  0  SEU-PC [192.168.1.100]
  1  192.168.1.1
  2  10.20.30.1
  3  200.150.100.1
  4  8.8.8.8

Computando estatísticas por 125 segundos...
            Origem para Aqui   Este Nó/Link
Salto  RTT    Perdido/Enviado = Pct  Perdido/Enviado = Pct  Endereço
  0                                           SEU-PC [192.168.1.100]
                                0/ 100 =  0%   |
  1    1ms     0/ 100 =  0%     0/ 100 =  0%  192.168.1.1
                                0/ 100 =  0%   |
  2    5ms     0/ 100 =  0%     0/ 100 =  0%  10.20.30.1
                                0/ 100 =  0%   |
  3   12ms     0/ 100 =  0%     0/ 100 =  0%  200.150.100.1
                                0/ 100 =  0%   |
  4   20ms     0/ 100 =  0%     0/ 100 =  0%  8.8.8.8

Rastreamento concluído.
```

**Como interpretar?**

| Coluna              | O que significa?                                      |
| ------------------- | ----------------------------------------------------- |
| **Salto**           | Número do ponto na rota                               |
| **RTT**             | Round Trip Time - Tempo médio de resposta             |
| **Perdido/Enviado** | Quantos pacotes se perderam vs quantos foram enviados |
| **Pct**             | Porcentagem de perda                                  |
| **Endereço**        | IP desse ponto                                        |

**Valores de Referência:**

- ✅ **0% de perda:** Perfeito!
- ⚠️ **1-3% de perda:** Aceitável (pode ter micro-instabilidades)
- ❌ **5%+ de perda:** Problema! Conexão instável
- ❌ **10%+ de perda:** Problema sério!

---

### 🎯 Exemplo 2: Pathping com PROBLEMA

```cmd
pathping 8.8.8.8
```

**Cenário com perda de pacotes:**

```
Salto  RTT    Perdido/Enviado = Pct  Perdido/Enviado = Pct  Endereço
  0                                           SEU-PC
  1    1ms     0/ 100 =  0%     0/ 100 =  0%  192.168.1.1
  2    5ms     15/ 100 = 15%    15/ 100 = 15% 10.20.30.1  ← PROBLEMA!
  3   12ms     15/ 100 = 15%     0/ 100 =  0%  200.150.100.1
  4   20ms     15/ 100 = 15%     0/ 100 =  0%  8.8.8.8
```

**Interpretação:**

❌ **Salto 2 (10.20.30.1) está com 15% de perda!**

Veja que os saltos seguintes (3 e 4) mostram:

- **"Perdido/Enviado = 15%" na coluna "Origem para Aqui"** (herdam a perda do salto 2)
- **MAS "0%" na coluna "Este Nó/Link"** (eles próprios não têm perda)

**Conclusão:** O problema está especificamente no **Salto 2**!

---

### 🎯 Exemplo 3: Pathping Mais Rápido (para testes)

```cmd
pathping -q 10 8.8.8.8
```

**O que esse comando faz?**

- O `-q 10` faz enviar apenas 10 pacotes por salto (ao invés de 100)
- Muito mais rápido (cerca de 30 segundos ao invés de 5 minutos)
- Menos preciso, mas útil para testes rápidos

---

## 📝 Comando 4: IPCONFIG - Descobrindo Sua Configuração de Rede

### 🤔 O que é o IPCONFIG?

O `ipconfig` mostra as **configurações de rede do seu computador**. É como ver seu "RG" na rede: qual seu IP, quem é seu gateway, quem é seu DNS, etc.

**Para que serve?**

- Ver qual seu IP atual
- Descobrir quem é seu gateway (roteador)
- Ver quais servidores DNS você está usando
- Renovar seu IP (quando trava)

---

### 📖 Sintaxe Básica

```cmd
ipconfig
```

---

### 🎯 Exemplo 1: IPCONFIG Básico

```cmd
ipconfig
```

**O que esse comando faz?**

- Mostra informações BÁSICAS de rede

**O que você vai ver:**

```
Configuração de IP do Windows

Adaptador Ethernet Ethernet:

   Sufixo DNS específico de conexão. . . . . . :
   Endereço IPv4. . . . . . . . . . . . . . . : 192.168.1.100
   Máscara de Sub-rede . . . . . . . . . . . . : 255.255.255.0
   Gateway Padrão. . . . . . . . . . . . . . . : 192.168.1.1
```

**Entendendo cada campo:**

| Campo                   | O que significa?                   | Analogia                                  |
| ----------------------- | ---------------------------------- | ----------------------------------------- |
| **Endereço IPv4**       | Seu "endereço" na rede local       | Como o número da sua casa na rua          |
| **Máscara de Sub-rede** | Define o "tamanho do bairro"       | Quantas casas tem na sua rua              |
| **Gateway Padrão**      | A "porta de saída" para a internet | Como a saída do seu condomínio para a rua |

**No exemplo acima:**

- **Seu IP:** 192.168.1.100
- **Seu roteador (gateway):** 192.168.1.1
- Você está na rede **192.168.1.X** (rede local)

---

### 🎯 Exemplo 2: IPCONFIG /ALL - Informações Completas

```cmd
ipconfig /all
```

**O que esse comando faz?**

- Mostra **TODAS** as informações de rede (muito mais detalhado)

**O que você vai ver:**

```
Configuração de IP do Windows

   Nome do Host. . . . . . . . . . . . . : SEU-PC
   Sufixo DNS Primário . . . . . . . . . :
   Tipo de Nó. . . . . . . . . . . . . . : Híbrido
   Roteamento de IP Habilitado . . . . . : Não
   Proxy WINS Habilitado . . . . . . . . : Não

Adaptador Ethernet Ethernet:

   Sufixo DNS específico de conexão. . . :
   Descrição . . . . . . . . . . . . . . : Realtek PCIe GbE Family Controller
   Endereço Físico . . . . . . . . . . . : AA-BB-CC-DD-EE-FF
   DHCP Habilitado . . . . . . . . . . . : Sim
   Configuração Automática Habilitada. . : Sim
   Endereço IPv4. . . . . . . . . . . . . : 192.168.1.100(Preferencial)
   Máscara de Sub-rede . . . . . . . . . : 255.255.255.0
   Concessão Obtida. . . . . . . . . . . : quinta-feira, 13 de novembro de 2025 08:00:00
   Concessão Expira. . . . . . . . . . . : sexta-feira, 14 de novembro de 2025 08:00:00
   Gateway Padrão. . . . . . . . . . . . : 192.168.1.1
   Servidor DHCP . . . . . . . . . . . . : 192.168.1.1
   Servidores DNS. . . . . . . . . . . . : 8.8.8.8
                                           8.8.4.4
```

**Campos importantes:**

| Campo                     | O que significa?                         | Por que importa?                              |
| ------------------------- | ---------------------------------------- | --------------------------------------------- |
| **Endereço Físico (MAC)** | Identificador ÚNICO da sua placa de rede | Como o CHASSI de um carro - nunca muda        |
| **DHCP Habilitado: Sim**  | Seu IP é automático (dado pelo roteador) | Significa que você não configurou IP fixo     |
| **Servidor DHCP**         | Quem te deu o IP                         | Geralmente é seu roteador                     |
| **Servidores DNS**        | Quem traduz nomes (google.com) em IPs    | Se estiver errado, sites não abrem            |
| **Concessão Expira**      | Quando seu IP "vence"                    | Depois disso, o roteador pode te dar outro IP |

---

### 🎯 Exemplo 3: IPCONFIG /RELEASE e /RENEW - Renovando seu IP

**Quando usar?**

- Quando você mudou configurações no roteador
- Quando sua internet travou e não volta
- Quando você quer forçar o computador a pegar um novo IP

**Passo a Passo:**

```cmd
ipconfig /release
```

**O que esse comando faz?**

- **"Devolve" seu IP** para o roteador
- Seu computador fica temporariamente **SEM IP** (sem internet)

**Depois:**

```cmd
ipconfig /renew
```

**O que esse comando faz?**

- **Pede um novo IP** para o roteador
- Seu computador recebe um IP novo (ou o mesmo de antes)

**Sequência completa:**

```cmd
ipconfig /release
ipconfig /renew
```

> **⚠️ AVISO:** Durante o `/release`, você vai ficar **SEM INTERNET** por alguns segundos! Não se assuste!

---

### 🎯 Exemplo 4: IPCONFIG /FLUSHDNS - Limpando Cache de DNS

**Quando usar?**

- Quando você mudou um site de servidor
- Quando um site está abrindo a versão antiga/errada
- Quando você alterou configurações de DNS

```cmd
ipconfig /flushdns
```

**O que esse comando faz?**

- **Apaga a "memória"** de sites que você acessou
- Força o Windows a buscar os IPs dos sites novamente

**O que você vai ver:**

```
Configuração de IP do Windows

Liberação do Cache do DNS Resolver bem-sucedida.
```

---

### 📊 Tabela Resumo - IPCONFIG

| Comando                | O que faz?                        | Quando usar?                          |
| ---------------------- | --------------------------------- | ------------------------------------- |
| `ipconfig`             | Mostra IP, gateway, máscara       | Ver configuração básica               |
| `ipconfig /all`        | Mostra TUDO (MAC, DNS, DHCP, etc) | Diagnóstico completo                  |
| `ipconfig /release`    | Devolve o IP atual                | Antes de renovar                      |
| `ipconfig /renew`      | Pede um novo IP                   | Depois de release ou quando travou    |
| `ipconfig /flushdns`   | Limpa cache de DNS                | Site não abre ou mostra versão antiga |
| `ipconfig /displaydns` | Mostra cache de DNS               | Ver quais sites estão na memória      |

---

## 📝 Comando 5: NSLOOKUP - Testando DNS

### 🤔 O que é o NSLOOKUP?

O `nslookup` (name server lookup) é usado para **testar se o DNS está funcionando**. Ele pergunta ao servidor DNS: "Qual o IP de www.google.com?" e mostra a resposta.

**Para que serve?**

- Ver se o DNS está respondendo
- Descobrir o IP de um site
- Testar se um domínio existe
- Identificar problemas de DNS

**Lembrando:** DNS é como uma agenda telefônica. Transforma "google.com" em "142.250.185.36".

---

### 📖 Sintaxe Básica

```cmd
nslookup [nome do site]
```

---

### 🎯 Exemplo 1: NSLOOKUP Básico

```cmd
nslookup www.google.com
```

**O que esse comando faz?**

- Pergunta ao seu DNS: "Qual o IP de www.google.com?"
- Mostra a resposta

**O que você vai ver:**

```
Servidor:  dns.google
Address:  8.8.8.8

Não autoritativa:
Nome:    www.google.com
Addresses:  142.250.185.36
           2800:3f0:4001:815::2004
```

**Entendendo a resposta:**

| Linha                         | O que significa?                                   |
| ----------------------------- | -------------------------------------------------- |
| **Servidor: dns.google**      | Nome do servidor DNS que respondeu                 |
| **Address: 8.8.8.8**          | IP do servidor DNS                                 |
| **Não autoritativa**          | Essa resposta veio do cache (não direto do Google) |
| **Nome: www.google.com**      | O site que você perguntou                          |
| **Addresses: 142.250.185.36** | O IP do site (IPv4)                                |
| **2800:...**                  | O IP do site em IPv6 (versão nova de IP)           |

**Está funcionando?**
✅ Sim! O DNS conseguiu traduzir "www.google.com" para o IP "142.250.185.36".

---

### 🎯 Exemplo 2: NSLOOKUP com PROBLEMA

```cmd
nslookup www.siteinventado.com.br
```

**O que você pode ver:**

```
Servidor:  dns.google
Address:  8.8.8.8

*** dns.google não encontrou www.siteinventado.com.br: Non-existent domain
```

**O que significa?**
❌ O site **não existe** ou o domínio está incorreto!

---

### 🎯 Exemplo 3: Testando um Servidor DNS Específico

```cmd
nslookup www.google.com 1.1.1.1
```

**O que esse comando faz?**

- Pergunta para o servidor **1.1.1.1** (Cloudflare) ao invés do seu DNS padrão
- Útil para testar se o problema é no seu DNS

**Servidores DNS públicos famosos:**

| DNS        | IP                | Empresa    |
| ---------- | ----------------- | ---------- |
| Google DNS | 8.8.8.8 e 8.8.4.4 | Google     |
| Cloudflare | 1.1.1.1 e 1.0.0.1 | Cloudflare |
| Quad9      | 9.9.9.9           | Quad9      |
| OpenDNS    | 208.67.222.222    | Cisco      |

---

### 🎯 Exemplo 4: NSLOOKUP Reverso (IP para Nome)

```cmd
nslookup 8.8.8.8
```

**O que esse comando faz?**

- Faz o **CONTRÁRIO:** Dado um IP, descobre o nome

**O que você vai ver:**

```
Servidor:  dns.google
Address:  8.8.8.8

Nome:    dns.google
Address:  8.8.8.8
```

✅ O IP "8.8.8.8" pertence a "dns.google".

---

## 📝 Comando 6: NETSTAT - Vendo Conexões Ativas

### 🤔 O que é o NETSTAT?

O `netstat` (network statistics) mostra **todas as conexões de rede ativas** do seu computador. É como ver uma lista de todas as "chamadas telefônicas" que seu computador está fazendo.

**Para que serve?**

- Ver quais programas estão usando a internet
- Identificar portas abertas
- Detectar conexões suspeitas

---

### 📖 Sintaxe Básica

```cmd
netstat
```

---

### 🎯 Exemplo 1: NETSTAT Básico

```cmd
netstat
```

**O que você vai ver:**

```
Conexões Ativas

  Proto  Endereço Local         Endereço Externo      Estado
  TCP    192.168.1.100:49671    142.250.185.36:443    ESTABLISHED
  TCP    192.168.1.100:49672    40.90.189.152:443     ESTABLISHED
```

**Entendendo cada coluna:**

| Coluna               | O que significa?                              |
| -------------------- | --------------------------------------------- |
| **Proto**            | Tipo de conexão (TCP ou UDP)                  |
| **Endereço Local**   | Seu IP + porta que você está usando           |
| **Endereço Externo** | IP + porta do servidor remoto                 |
| **Estado**           | Status da conexão (conectado, esperando, etc) |

**Estados comuns:**

| Estado          | O que significa?                                  |
| --------------- | ------------------------------------------------- |
| **ESTABLISHED** | Conexão ativa e funcionando                       |
| **LISTENING**   | Seu computador está esperando conexões (servidor) |
| **TIME_WAIT**   | Conexão fechando                                  |
| **CLOSE_WAIT**  | Conexão esperando fechar                          |

---

### 🎯 Exemplo 2: NETSTAT com Nome dos Programas

```cmd
netstat -b
```

> **⚠️ IMPORTANTE:** Este comando precisa ser executado como **Administrador**!

**Como executar como administrador:**

1. Clique com botão direito no CMD
2. Escolha "Executar como administrador"

**O que você vai ver:**

```
  TCP    192.168.1.100:49671    142.250.185.36:443    ESTABLISHED
  [chrome.exe]

  TCP    192.168.1.100:49672    40.90.189.152:443     ESTABLISHED
  [Teams.exe]
```

✅ Agora você vê **QUAL PROGRAMA** está fazendo cada conexão!

---

### 🎯 Exemplo 3: NETSTAT Mostrando Portas em LISTENING

```cmd
netstat -a
```

**O que esse comando faz?**

- O `-a` mostra **TODAS** conexões, incluindo portas esperando conexão

---

### 🎯 Exemplo 4: NETSTAT Atualização Contínua

```cmd
netstat -a 5
```

**O que esse comando faz?**

- Atualiza a tela a cada **5 segundos**
- Útil para monitorar em tempo real

---

## 📝 Comando 7: ARP - Tabela de Endereços MAC

### 🤔 O que é o ARP?

O `arp` (Address Resolution Protocol) mostra a **tabela de correspondência entre IPs e MACs** na sua rede local.

**Lembrando:**

- **IP:** Endereço lógico (pode mudar)
- **MAC:** Endereço físico da placa de rede (nunca muda)

---

### 🎯 Exemplo: ARP Básico

```cmd
arp -a
```

**O que você vai ver:**

```
Interface: 192.168.1.100 --- 0xb
  Endereço IP       Endereço Físico      Tipo
  192.168.1.1       aa-bb-cc-dd-ee-01   dinâmico
  192.168.1.50      aa-bb-cc-dd-ee-02   dinâmico
  192.168.1.255     ff-ff-ff-ff-ff-ff   estático
```

**Entendendo:**

- **192.168.1.1 → aa-bb-cc-dd-ee-01:** O roteador (gateway)
- **192.168.1.50 → aa-bb-cc-dd-ee-02:** Outro computador na rede
- **192.168.1.255 → ff-ff-ff-ff-ff-ff:** Endereço de broadcast (para "todos")

---

## 📝 Testes de THROUGHPUT (Velocidade da Internet)

### 🤔 O que é Throughput?

**Throughput** é a **quantidade de dados** que consegue passar pela sua conexão em um determinado tempo. É medido em:

- **Mbps** (Megabits por segundo)
- **MB/s** (Megabytes por segundo)

**Analogia:** Imagine um cano de água:

- Um cano **fino** passa pouca água por segundo (baixo throughput)
- Um cano **grosso** passa muita água por segundo (alto throughput)

---

### 🎯 Método 1: Teste Online (Mais Fácil)

**Sites confiáveis para teste:**

1. **Speedtest by Ookla:** https://www.speedtest.net
2. **Fast.com (Netflix):** https://fast.com
3. **Nperf:** https://www.nperf.com

**Como fazer:**

1. Abra um dos sites acima
2. Clique em "GO" ou "Iniciar Teste"
3. Aguarde o teste completar

**O que você vai ver:**

- **Download:** Velocidade para baixar (receber dados)
- **Upload:** Velocidade para enviar dados
- **Ping:** Latência da sua conexão

---

### 🎯 Método 2: iPerf3 (Profissional)

O **iPerf3** é uma ferramenta profissional para testar throughput entre dois pontos.

#### 📥 Instalando iPerf3

1. Baixe de: https://iperf.fr/iperf-download.php
2. Escolha "Windows" → Baixe o arquivo .zip
3. Extraia em uma pasta (ex: `C:\iperf3`)

#### 🎯 Usando iPerf3

**Você precisa de:**

- Um **servidor** (computador que vai receber)
- Um **cliente** (computador que vai enviar)

**No computador servidor:**

```cmd
cd C:\iperf3
iperf3 -s
```

**O que esse comando faz?**

- `-s` = modo servidor (server)
- Fica esperando conexões na porta 5201

**No computador cliente:**

```cmd
cd C:\iperf3
iperf3 -c [IP-DO-SERVIDOR]
```

**Exemplo:**

```cmd
iperf3 -c 192.168.1.100
```

**O que você vai ver:**

```
Connecting to host 192.168.1.100, port 5201
[  5] local 192.168.1.101 port 49823 connected to 192.168.1.100 port 5201
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec   112 MBytes   941 Mbits/sec
[  5]   1.00-2.00   sec   112 MBytes   940 Mbits/sec
[  5]   2.00-3.00   sec   112 MBytes   941 Mbits/sec
...
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.00  sec  1.09 GBytes   940 Mbits/sec                  sender
[  5]   0.00-10.00  sec  1.09 GBytes   938 Mbits/sec                  receiver
```

**Entendendo o resultado:**

- **Transfer:** Quantidade de dados enviada (1.09 GB em 10 segundos)
- **Bitrate:** Velocidade média (940 Mbps) ✅
- Isso significa uma rede Gigabit funcionando quase no máximo!

---

### 🎯 Método 3: Teste de Download Manual

**Método simples:**

1. Baixe um arquivo grande de um servidor rápido
2. Veja a velocidade de download

**Bons locais para testar:**

- Steam (se tiver): Baixe um jogo e veja a velocidade
- Ubuntu ISO: https://ubuntu.com/download (arquivo grande)

**Como calcular:**

- Se você baixou **100 MB em 10 segundos**:
- Velocidade = 100 MB ÷ 10 s = **10 MB/s**
- Em Mbps: 10 MB/s × 8 = **80 Mbps**

> **📚 Conversão:** 1 Byte = 8 bits, então **1 MB/s = 8 Mbps**

---

## 📝 Comando 8: HOSTNAME e WHOAMI

### 🤔 Para que servem?

Comandos simples para saber **quem você é** na rede.

---

### 🎯 HOSTNAME - Nome do Computador

```cmd
hostname
```

**O que você vai ver:**

```
SEU-PC
```

✅ Esse é o nome do seu computador na rede!

---

### 🎯 WHOAMI - Usuário Logado

```cmd
whoami
```

**O que você vai ver:**

```
desktop-abc123\thomas
```

✅ Você está logado como "thomas" no computador "desktop-abc123".

---

## 🔧 Cenários Práticos do Dia a Dia no NOC

### 📞 Cenário 1: Cliente Reclama "Não Tenho Internet"

**Passo a passo de diagnóstico:**

```cmd
REM 1. Verificar se você tem IP
ipconfig

REM 2. Testar gateway (seu roteador)
ping 192.168.1.1

REM 3. Testar DNS do Google
ping 8.8.8.8

REM 4. Testar resolução de nomes
ping www.google.com

REM 5. Ver o caminho até o Google
tracert 8.8.8.8
```

**Interpretando resultados:**

| O que funciona?  | O que NÃO funciona?    | Problema está em:      |
| ---------------- | ---------------------- | ---------------------- |
| Gateway funciona | Internet não funciona  | Provedor/Roteador      |
| Ping IP funciona | Ping site não funciona | DNS                    |
| Nada funciona    | Tudo falha             | Cabo/WiFi desconectado |

---

### 📞 Cenário 2: Internet Lenta

**Diagnóstico:**

```cmd
REM 1. Ver latência básica
ping 8.8.8.8 -n 100

REM 2. Ver onde está o atraso
tracert 8.8.8.8

REM 3. Teste detalhado de qualidade
pathping 8.8.8.8

REM 4. Teste de velocidade
REM (Use speedtest.net no navegador)
```

**Valores de referência:**

| Ping      | Qualidade    |
| --------- | ------------ |
| 0-50ms    | ✅ Excelente |
| 50-100ms  | ✅ Bom       |
| 100-200ms | ⚠️ Razoável  |
| 200ms+    | ❌ Ruim      |

---

### 📞 Cenário 3: Site Específico Não Abre

**Diagnóstico:**

```cmd
REM 1. Testar se o DNS resolve o site
nslookup www.siteproblema.com

REM 2. Se resolver, testar ping para o IP
ping [IP-RETORNADO]

REM 3. Ver se o problema é no caminho
tracert www.siteproblema.com

REM 4. Limpar cache de DNS e tentar novamente
ipconfig /flushdns
```

---

### 📞 Cenário 4: Conexão Caindo Toda Hora

**Diagnóstico:**

```cmd
REM 1. Ping contínuo para monitorar
ping 8.8.8.8 -t

REM Deixe rodando e observe:
REM - Se aparecer "Esgotou o tempo" = perda de pacote
REM - Se os tempos variam muito = instabilidade
REM - Se para completamente = queda de conexão

REM 2. Após alguns minutos, pare (Ctrl+C) e veja as estatísticas
```

**Estatísticas esperadas:**

```
Pacotes: Enviados = 500, Recebidos = 500, Perdidos = 0 (0% de perda)
```

✅ **0% de perda** = Conexão estável  
❌ **Mais de 1% de perda** = Conexão instável

---

## ⚠️ Erros Comuns e Como Resolver

### ❌ Erro: "Não foi possível localizar o host"

**O que significa?**
O DNS não conseguiu transformar o nome em IP.

**Soluções:**

```cmd
REM 1. Verificar conexão
ping 8.8.8.8

REM 2. Testar DNS diferente
nslookup www.google.com 1.1.1.1

REM 3. Limpar cache DNS
ipconfig /flushdns

REM 4. Renovar IP
ipconfig /release
ipconfig /renew
```

---

### ❌ Erro: "Esgotado o tempo limite do pedido"

**O que significa?**
O pacote não voltou no tempo esperado. Possíveis causas:

- Servidor offline
- Firewall bloqueando
- Conexão muito lenta
- Perda de pacotes

**Soluções:**

```cmd
REM 1. Tentar com mais tempo de espera (5 segundos)
ping 8.8.8.8 -w 5000

REM 2. Ver onde está o problema
tracert 8.8.8.8

REM 3. Teste mais longo
pathping 8.8.8.8
```

---

### ❌ Erro: "Destino inalcançável"

**O que significa?**
Não há caminho para chegar ao destino.

**Soluções:**

```cmd
REM 1. Verificar gateway
ipconfig

REM 2. Testar gateway
ping [IP-DO-GATEWAY]

REM 3. Ver tabela de rotas
route print
```

---

## 📊 Tabela Resumo - Quando Usar Cada Comando

| Situação                             | Comando                        | Por quê?                       |
| ------------------------------------ | ------------------------------ | ------------------------------ |
| **Testar se servidor está online**   | `ping [IP]`                    | Resposta rápida                |
| **Ver caminho até o destino**        | `tracert [IP]`                 | Identificar onde está lento    |
| **Diagnóstico completo de rota**     | `pathping [IP]`                | Ver perda de pacotes por ponto |
| **Ver meu IP e configurações**       | `ipconfig`                     | Dados básicos                  |
| **Ver TODAS configurações**          | `ipconfig /all`                | Diagnóstico completo           |
| **Internet não funciona**            | `ipconfig /release` + `/renew` | Renovar IP                     |
| **Site não abre**                    | `nslookup [site]`              | Testar DNS                     |
| **Testar velocidade**                | Speedtest.net                  | Teste rápido                   |
| **Testar velocidade profissional**   | iPerf3                         | Teste entre dois pontos        |
| **Ver conexões ativas**              | `netstat -a`                   | Ver o que está conectado       |
| **Identificar programa usando rede** | `netstat -b`                   | Ver qual programa              |

---

## 📖 Referências e Documentação Oficial

### 📚 Microsoft Learn (Documentação Oficial Windows)

1. **Ping:**

   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/ping

2. **Tracert:**

   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/tracert

3. **Pathping:**

   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/pathping

4. **Ipconfig:**

   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/ipconfig

5. **Nslookup:**

   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/nslookup

6. **Netstat:**
   - https://learn.microsoft.com/pt-br/windows-server/administration/windows-commands/netstat

### 📚 Ferramentas Externas

1. **iPerf3:**

   - Site oficial: https://iperf.fr
   - Documentação: https://iperf.fr/iperf-doc.php

2. **Speedtest:**
   - https://www.speedtest.net

---

## 💡 Dicas Finais para Iniciantes

### 1️⃣ Pratique Todos os Dias

- Execute os comandos mesmo quando não há problemas
- Familiarize-se com os outputs normais
- Assim você reconhece quando algo está errado

### 2️⃣ Documente Tudo

- Copie e cole os comandos usados
- Salve os outputs
- Anote horário e circunstâncias

### 3️⃣ Não Tenha Medo de Errar

- Comandos de visualização (ping, ipconfig, tracert) são **seguros**
- Eles apenas **mostram** informações, não **mudam** nada
- O Windows não vai quebrar se você testar!

### 4️⃣ Compare com Máquinas Funcionando

- Teste os mesmos comandos em um computador que está funcionando
- Compare os resultados
- Isso ajuda a identificar o que é "normal"

### 5️⃣ Use a Ajuda Integrada

- Todos os comandos têm ajuda: `ping /?`
- Mostra todas as opções disponíveis

### 6️⃣ Crie um Caderno de Comandos

- Anote os comandos que você mais usa
- Crie seu próprio "cheatsheet" (cola)
- Adicione notas pessoais

---

## 🎓 Exercícios Práticos para Você Tentar

### Exercício 1: Diagnóstico Básico

```cmd
REM Execute estes comandos e entenda cada saída:
ipconfig
ping 8.8.8.8
ping www.google.com
tracert 8.8.8.8
nslookup www.google.com
```

### Exercício 2: Teste de Estabilidade

```cmd
REM Deixe este ping rodando por 5 minutos:
ping 8.8.8.8 -t
REM Depois pare (Ctrl+C) e analise as estatísticas
```

### Exercício 3: Exploração de Rede Local

```cmd
REM Descubra sua rede:
ipconfig
REM Veja o IP do gateway e ping nele:
ping [IP-DO-SEU-GATEWAY]
REM Veja a tabela ARP:
arp -a
```

### Exercício 4: Teste de DNS

```cmd
REM Teste diferentes servidores DNS:
nslookup www.google.com 8.8.8.8
nslookup www.google.com 1.1.1.1
nslookup www.google.com
```

---

## 🏁 Conclusão

Parabéns por chegar até aqui! Agora você tem uma base sólida de comandos Windows para troubleshooting. Lembre-se:

✅ **Ping** é seu melhor amigo - use sempre  
✅ **Tracert** mostra o caminho - use quando ping funciona mas internet está lenta  
✅ **Ipconfig** mostra sua identidade na rede - use para ver configurações  
✅ **Nslookup** testa DNS - use quando sites não abrem  
✅ **Pathping** é o teste completo - use quando quer certeza absoluta

**Pratique, pratique, pratique!** A experiência vem com o tempo. Boa sorte no NOC! 🚀

---

**Versão:** 1.0  
**Data:** Novembro 2025  
**Autor:** ThomasJPF  
**Público-Alvo:** Analistas NOC Iniciantes  
**Dificuldade:** Básico

---
