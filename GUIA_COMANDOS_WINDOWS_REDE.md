# 🪟 Guia para Iniciantes: Comandos de Rede do Windows

## 👋 Bem-vindo!

Este guia vai te ensinar comandos básicos de rede do Windows que você usa no **CMD (Prompt de Comando)**. Vou explicar tudo de forma bem simples, como se você nunca tivesse visto isso antes!

> **🎯 Para quem é este guia?**  
> Para você que está começando no NOC e precisa testar conexões de rede, verificar se um servidor está respondendo, ou descobrir por onde os dados estão passando na internet.

---

## 🤔 O que é o CMD?

O **CMD** (Command Prompt) é como uma "caixa de texto mágica" onde você digita comandos e o computador faz coisas. É tipo conversar com o computador usando texto!

**Como abrir o CMD:**
1. Aperte a tecla **Windows** + **R**
2. Digite `cmd` e aperte **Enter**
3. Uma janela preta vai aparecer - é o CMD!

---

## 📚 Comandos Básicos de Rede

### 1. 🏓 PING - Testar se um computador está "vivo"

#### 🤔 O que é?

Imagine que você está em uma caverna e grita "OOOI!". Se você ouvir o eco voltando, significa que tem algo lá na frente refletindo o som. O **ping** faz exatamente isso, mas com a internet!

Ele manda um "grito digital" para um computador/servidor e espera a resposta voltar.

#### 📖 Como funciona?

**Comando básico:**
```
ping 8.8.8.8
```

**O que cada parte significa:**
- `ping` = o comando que você quer executar
- `8.8.8.8` = o endereço IP do Google (um servidor na internet)

#### ✅ Exemplo prático:

```
C:\Users\Thomas> ping 8.8.8.8

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

#### 🔍 Como ler o resultado (linha por linha):

1. **"Resposta de 8.8.8.8"** = O servidor respondeu! Está vivo! 🎉
2. **"bytes=32"** = Tamanho do pacote enviado (como tamanho da carta)
3. **"tempo=15ms"** = Levou 15 milissegundos para ir e voltar (mais rápido que um piscar de olhos!)
4. **"TTL=117"** = "Time To Live" - quantos "pulos" na internet o pacote pode dar antes de morrer
5. **"Perdidos = 0 (0% de perda)"** = Todos os pacotes chegaram! Conexão perfeita! ✅

#### 🎨 Variações úteis:

| Comando | O que faz | Quando usar |
|---------|-----------|-------------|
| `ping google.com` | Testa usando nome ao invés de IP | Quando você não sabe o IP |
| `ping 8.8.8.8 -n 10` | Envia 10 pacotes ao invés de 4 | Para testar por mais tempo |
| `ping 8.8.8.8 -t` | Fica pingando infinitamente (Ctrl+C para parar) | Para monitorar conexão em tempo real |
| `ping 8.8.8.8 -l 1000` | Envia pacotes maiores (1000 bytes) | Para testar com pacotes grandes |
| `ping 192.168.1.1` | Testa seu roteador/modem | Para ver se problema é na sua rede local |

#### 💡 O que significa cada resultado?

**✅ Resposta de [IP]:** = SUCESSO! Está funcionando!

**❌ "Esgotado o tempo limite do pedido":**
- O servidor não respondeu a tempo
- Pode estar offline, muito longe, ou bloqueando ping
- É como gritar e não ouvir eco

**❌ "Host de destino inacessível":**
- Não consegue chegar no servidor
- É como tentar ligar para um número que não existe
- Problema na rota/caminho até o destino

**⚠️ "Tempo limite da solicitação excedido":**
- A requisição demorou demais
- Conexão muito lenta ou instável

#### 🎯 Situações do dia a dia:

**Situação 1: Cliente diz que internet não funciona**
```
ping 8.8.8.8
```
- Se funcionar: Internet OK, problema é no site que ele quer acessar
- Se não funcionar: Problema na conexão da internet

**Situação 2: Testar se computador na rede local está ligado**
```
ping 192.168.1.50
```
- Se responder: Computador está ligado e na rede
- Se não responder: Computador desligado ou problema de rede

---

### 2. 🗺️ TRACERT - Rastreamento de Rota (Mapa do Caminho)

#### 🤔 O que é?

Imagine que você quer ir de ônibus da sua casa até a praia. O ônibus faz várias paradas no caminho: padaria → escola → mercado → shopping → praia.

O **tracert** mostra TODAS as paradas (servidores) que seus dados fazem até chegar no destino final!

#### 📖 Como funciona?

**Comando básico:**
```
tracert google.com
```

#### ✅ Exemplo prático:

```
C:\Users\Thomas> tracert google.com

Rastreando a rota para google.com [142.250.219.46]
com no máximo 30 saltos:

  1    <1 ms    <1 ms    <1 ms  192.168.1.1
  2    10 ms     9 ms    11 ms  10.0.0.1
  3    15 ms    14 ms    16 ms  200.123.45.1
  4    18 ms    17 ms    19 ms  200.123.45.254
  5    25 ms    24 ms    26 ms  142.250.219.46

Rastreamento concluído.
```

#### 🔍 Como ler o resultado:

Cada linha é uma "parada" no caminho:

**Linha 1:** `192.168.1.1` = Seu roteador/modem em casa
**Linha 2:** `10.0.0.1` = Equipamento do provedor de internet (OLT, roteador, etc)
**Linha 3-4:** = Servidores intermediários (backbone da operadora)
**Linha 5:** = Destino final (servidor do Google)

**Os três números de tempo** (ex: `10 ms 9 ms 11 ms`):
- São 3 tentativas diferentes
- Mostram quanto tempo levou em cada tentativa
- Se variar muito = conexão instável

#### ⚠️ Possíveis problemas:

**`* * * Esgotado o tempo limite do pedido`:**
```
  3    15 ms    14 ms    16 ms  200.123.45.1
  4     *        *        *     Esgotado o tempo limite do pedido
  5    25 ms    24 ms    26 ms  142.250.219.46
```
- O servidor na posição 4 não respondeu
- Mas o destino final (linha 5) funcionou
- Normal! Alguns servidores não respondem tracert por segurança

**Tempo muito alto em algum ponto:**
```
  3    15 ms    14 ms    16 ms  200.123.45.1
  4   300 ms   290 ms   310 ms  200.123.45.254  ← PROBLEMA AQUI!
  5   320 ms   315 ms   325 ms  142.250.219.46
```
- Se algum salto tem tempo muito maior que os anteriores
- Significa que ESSE equipamento está com problema
- É onde a "lentidão" está acontecendo

#### 💡 Quando usar:

- Cliente reclama de lentidão
- Ping funciona mas está lento
- Quer descobrir ONDE na internet está o problema
- Ver se problema é na rede local, no provedor, ou no destino

---

### 3. 🔍 IPCONFIG - Ver configurações de rede do seu computador

#### 🤔 O que é?

É como pedir pro seu computador te mostrar a "carteira de identidade" da rede dele. Mostra o endereço IP, máscara, gateway, etc.

#### 📖 Comandos:

**Ver informações básicas:**
```
ipconfig
```

**Ver TODAS as informações (modo detalhado):**
```
ipconfig /all
```

#### ✅ Exemplo prático:

```
C:\Users\Thomas> ipconfig

Configuração de IP do Windows

Adaptador Ethernet Ethernet:

   Sufixo DNS específico de conexão. . . . . . :
   Endereço IPv4. . . . . . . . . . . . . . . : 192.168.1.100
   Máscara de Sub-rede . . . . . . . . . . . . : 255.255.255.0
   Gateway Padrão. . . . . . . . . . . . . . . : 192.168.1.1
```

#### 🔍 Como ler:

- **Endereço IPv4:** = Seu "CPF" na rede local (192.168.1.100)
- **Máscara de Sub-rede:** = Define quem está na mesma rede que você
- **Gateway Padrão:** = O "porteiro" que leva seus dados para fora da rede (geralmente é o roteador)

#### 🎨 Variações úteis:

| Comando | O que faz | Quando usar |
|---------|-----------|-------------|
| `ipconfig /all` | Mostra TUDO (DNS, MAC, DHCP, etc) | Para diagnóstico completo |
| `ipconfig /release` | "Solta" seu IP atual | Quando vai renovar IP |
| `ipconfig /renew` | Pega um novo IP do servidor DHCP | Quando IP não funciona |
| `ipconfig /flushdns` | Limpa cache DNS (memória de sites) | Quando site não abre |
| `ipconfig /displaydns` | Mostra cache DNS | Para ver sites já acessados |

#### 💡 Comando importante para NOC:

**Renovar IP (resolver 80% dos problemas de "não conecta"):**
```
ipconfig /release
ipconfig /renew
```

**Limpar cache DNS (quando site não abre):**
```
ipconfig /flushdns
```

---

### 4. 🔎 NSLOOKUP - Consultar DNS (Tradutor de Nomes)

#### 🤔 O que é?

Você sabe o nome "google.com", mas o computador precisa do endereço IP (números). O DNS é o "tradutor" que transforma nomes em IPs.

É como procurar o telefone de alguém na agenda pelo nome!

**nslookup** = "Name Server Lookup" (Procurar no Servidor de Nomes)

#### 📖 Como funciona:

**Comando básico:**
```
nslookup google.com
```

#### ✅ Exemplo prático:

```
C:\Users\Thomas> nslookup google.com

Servidor:  dns.google
Address:  8.8.8.8

Não autoritativa resposta:
Nome:    google.com
Address:  142.250.219.46
```

#### 🔍 Como ler:

1. **Servidor: dns.google (8.8.8.8)** = Qual servidor DNS você está usando para fazer a consulta
2. **Nome: google.com** = O nome que você procurou
3. **Address: 142.250.219.46** = O IP que corresponde a esse nome!

#### 💡 Quando usar:

**Problema: Site não abre**
```
nslookup sitequeproblema.com
```

**Resultado possível 1 - Funciona:**
```
Nome:    sitequeproblema.com
Address:  200.100.50.25
```
✅ DNS funcionando! Se site não abre, problema é outro

**Resultado possível 2 - Não funciona:**
```
*** dns.google não pode localizar sitequeproblema.com: Non-existent domain
```
❌ Site não existe ou DNS com problema

#### 🎨 Variações úteis:

```
nslookup -type=mx google.com    ← Ver servidores de email
nslookup -type=ns google.com    ← Ver servidores DNS do domínio
nslookup google.com 1.1.1.1     ← Usar DNS específico (Cloudflare)
```

---

### 5. 📊 NETSTAT - Ver conexões ativas (Quem está conectado)

#### 🤔 O que é?

Mostra TODAS as conexões de rede que seu computador tem no momento. É como ver uma lista de "com quem você está conversando agora na internet".

#### 📖 Como funciona:

**Comando básico:**
```
netstat
```

**Comando mais útil (com mais informações):**
```
netstat -ano
```

#### ✅ Exemplo prático:

```
C:\Users\Thomas> netstat -n

Conexões Ativas

  Proto  Endereço local         Endereço remoto         Estado
  TCP    192.168.1.100:50234   142.250.219.46:443      ESTABLISHED
  TCP    192.168.1.100:50235   104.244.42.1:443        ESTABLISHED
  TCP    192.168.1.100:50236   157.240.195.35:443      TIME_WAIT
```

#### 🔍 Como ler cada coluna:

- **Proto:** = Protocolo (TCP ou UDP)
- **Endereço local:** = Seu computador e porta que está usando
- **Endereço remoto:** = Para onde você está conectado
- **Estado:** = Status da conexão

#### 📖 Estados possíveis:

| Estado | O que significa | Analogia |
|--------|-----------------|----------|
| **ESTABLISHED** | Conexão ativa e funcionando | Chamada de telefone em andamento |
| **LISTENING** | Porta aberta esperando conexões | Telefone esperando tocar |
| **TIME_WAIT** | Conexão fechando, aguardando confirmação | Desligando o telefone |
| **CLOSE_WAIT** | Esperando fechar conexão | Outro lado desligou, você ainda não |

#### 🎨 Variações úteis:

| Comando | O que faz |
|---------|-----------|
| `netstat -n` | Mostra IPs (ao invés de nomes) |
| `netstat -a` | Mostra TODAS conexões (ativas e esperando) |
| `netstat -b` | Mostra qual programa está usando cada conexão |
| `netstat -ano` | Mostra tudo + número do processo (PID) |
| `netstat -s` | Mostra estatísticas detalhadas |

#### 💡 Uso prático no NOC:

**Ver se uma porta específica está aberta:**
```
netstat -an | findstr :80
```
(Procura se porta 80 está aberta/sendo usada)

**Ver quantas conexões estão ativas:**
```
netstat -n | find /c "ESTABLISHED"
```

---

### 6. 🛤️ PATHPING - Ping + Tracert Turbinado

#### 🤔 O que é?

É a **UNIÃO** do ping e tracert! Ele faz o traceroute E testa cada parada do caminho por um tempo mais longo para dar estatísticas.

**É tipo o "modo debug" do troubleshooting de rede!**

#### 📖 Como funciona:

**Comando:**
```
pathping google.com
```

⚠️ **ATENÇÃO:** Demora alguns minutos para completar! Seja paciente!

#### ✅ Exemplo prático:

```
C:\Users\Thomas> pathping google.com

Rastreando a rota para google.com [142.250.219.46]
com no máximo 30 saltos:
  0  SEU-PC [192.168.1.100]
  1  192.168.1.1
  2  10.0.0.1
  3  200.123.45.1
  4  142.250.219.46

Calculando estatísticas por 100 segundos...
            Origem para Aqui   Este Nó/Link
Salto  RTT    Perda/Enviados = % Perda/Enviados = %  Endereço
  0                                                    SEU-PC
                                0/ 100 =  0%   |
  1    1ms     0/ 100 =  0%     0/ 100 =  0%   192.168.1.1
                                0/ 100 =  0%   |
  2   10ms     0/ 100 =  0%     0/ 100 =  0%   10.0.0.1
                                0/ 100 =  0%   |
  3   15ms     0/ 100 =  0%     0/ 100 =  0%   200.123.45.1
                                0/ 100 =  0%   |
  4   25ms     0/ 100 =  0%     0/ 100 =  0%   142.250.219.46

Rastreamento concluído.
```

#### 🔍 Como ler:

- **RTT** = Round Trip Time (tempo de ida e volta)
- **Perda/Enviados** = Quantos pacotes se perderam de 100 enviados
- **% Perda** = Porcentagem de perda em cada ponto

**✅ Conexão perfeita:** 0% de perda em todos os pontos
**⚠️ Problema:** Se algum ponto tem % de perda > 0%, TEM PROBLEMA ALI!

#### 💡 Quando usar:

- Conexão instável (hora funciona, hora não)
- Lentidão intermitente
- Quer fazer análise profunda de onde está o problema
- Quando ping e tracert não foram suficientes

#### ⚠️ Cuidado:

- Demora 2-5 minutos para completar
- Use quando tiver tempo
- NÃO use se tiver pressa

---

## 🎯 Fluxo de Troubleshooting

Quando um cliente liga dizendo "internet não funciona", siga esta ordem:

### 1️⃣ Teste básico de conexão
```
ping 8.8.8.8
```
- ✅ Funciona = Internet OK, problema é no site/DNS
- ❌ Não funciona = Prossiga para passo 2

### 2️⃣ Teste o roteador local
```
ping 192.168.1.1
```
- ✅ Funciona = Problema é entre roteador e internet
- ❌ Não funciona = Problema é no computador ou roteador

### 3️⃣ Verifique DNS
```
ping google.com
```
- ✅ Funciona = DNS OK
- ❌ Não funciona = Problema de DNS, tente:
```
ipconfig /flushdns
```

### 4️⃣ Trace a rota
```
tracert 8.8.8.8
```
- Veja onde os pacotes estão parando ou ficando lentos

### 5️⃣ Renove o IP (se necessário)
```
ipconfig /release
ipconfig /renew
```

---

## 🚨 Erros Comuns e Soluções

### Erro 1: "ping não é reconhecido como comando"

**Causa:** CMD não está encontrando o comando
**Solução:** 
- Certifique-se que está no CMD (não PowerShell)
- Ou tente reiniciar o CMD como Administrador

---

### Erro 2: "Geral falha de ping"

**Causa:** Firewall ou driver de rede com problema
**Solução:**
1. Desative temporariamente o firewall
2. Reinicie o adaptador de rede
3. Reinicie o computador

---

### Erro 3: Todos os comandos dão timeout

**Causa:** Sem conexão com internet
**Solução:**
1. Verifique o cabo de rede
2. Verifique se Wi-Fi está conectado
3. Renove o IP: `ipconfig /release` e `ipconfig /renew`

---

## 📋 Tabela Resumo - Quando Usar Cada Comando

| Comando | Quando usar | Tempo |
|---------|-------------|-------|
| `ping` | Testar se algo está vivo/respondendo | 5 segundos |
| `ping -t` | Monitorar conexão em tempo real | Contínuo |
| `tracert` | Ver caminho até o destino | 10-30 segundos |
| `pathping` | Análise profunda de perda de pacotes | 2-5 minutos |
| `ipconfig` | Ver configurações de rede | Instantâneo |
| `ipconfig /renew` | Resolver problema de "sem internet" | 5-10 segundos |
| `nslookup` | Testar se DNS funciona | 2 segundos |
| `netstat` | Ver conexões ativas | Instantâneo |

---

## 🎓 Glossário - Dicionário de Termos

| Termo | Explicação Simples |
|-------|-------------------|
| **IP** | Endereço do computador na rede (como CPF) |
| **DNS** | Tradutor de nomes (google.com) para IPs (142.250.219.46) |
| **Gateway** | Portão de saída da sua rede (geralmente o roteador) |
| **Ping** | Teste se algo responde (como mandar um "oi") |
| **TTL** | Tempo de vida do pacote (quantos pulos pode dar) |
| **Latência** | Tempo de atraso (ms = milissegundos) |
| **Perda de Pacotes** | Quando dados se perdem no caminho (%) |
| **TCP** | Protocolo confiável (garante entrega) |
| **UDP** | Protocolo rápido (não garante entrega) |
| **Porta** | "Porta" específica de um serviço (80=web, 443=https) |
| **Máscara de Sub-rede** | Define quem está na mesma rede |

---

## 🎯 Exercícios Práticos

### Exercício 1: Teste básico
1. Abra o CMD
2. Digite: `ping 8.8.8.8`
3. Anote o tempo médio de resposta
4. Digite: `ping google.com`
5. Compare os resultados

**O que você aprendeu:** Diferença entre pingar IP vs nome

---

### Exercício 2: Rastreamento
1. Digite: `tracert google.com`
2. Conte quantos "saltos" foram necessários
3. Veja qual salto tem o maior tempo

**O que você aprendeu:** Por quantos servidores seus dados passam

---

### Exercício 3: Diagnóstico DNS
1. Digite: `nslookup youtube.com`
2. Anote o IP retornado
3. Digite: `ping [IP_ANOTADO]`
4. Funciona?

**O que você aprendeu:** Como DNS traduz nomes em IPs

---

### Exercício 4: Suas configurações
1. Digite: `ipconfig /all`
2. Encontre e anote:
   - Seu IP
   - Seu Gateway
   - Seu DNS
3. Pingue cada um deles

**O que você aprendeu:** Entender sua configuração de rede

---

## 📚 Referências Oficiais

Este guia foi baseado em documentação oficial e confiável:

### Microsoft Official Documentation:
- [Windows Networking Commands Reference](https://docs.microsoft.com/en-us/windows-server/networking/)
- [Network Troubleshooting Guide - Microsoft TechNet](https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/)
- [Windows Command-Line Reference](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/)

### RFCs (Request for Comments - Padrões da Internet):
- RFC 792 - Internet Control Message Protocol (ICMP) - Base do comando ping
- RFC 791 - Internet Protocol (IP)
- RFC 1035 - Domain Names (DNS)

### Artigos Técnicos Confiáveis:
- Cisco Networking Academy - Network Fundamentals
- CompTIA Network+ Study Materials
- Microsoft Learn - Windows Networking Fundamentals

### Ferramentas Online para Praticar:
- [Ping.eu](https://ping.eu) - Ping online de qualquer lugar do mundo
- [YouGetSignal.com](https://www.yougetsignal.com) - Ferramentas de rede online

---

## 💬 Dicas Finais

### ✅ Boas Práticas:

1. **Sempre documente** o que você testou
2. **Compare** resultados (antes vs depois)
3. **Teste múltiplas vezes** (um erro pode ser aleatório)
4. **Anote horários** quando o problema ocorre
5. **Use `-n` para especificar quantidade de pings** (ex: `ping -n 100 8.8.8.8`)

### ⚠️ Cuidados:

1. **NÃO** faça ping flood (`ping -t` com `-l 65500`) - é ataque DDoS!
2. **NÃO** fique pingando servidores o tempo todo - alguns bloqueiam
3. **Sempre use** esses comandos com responsabilidade
4. Alguns comandos precisam de **privilégios de administrador**

### 🎓 Continue Aprendendo:

- Pratique TODOS os dias
- Teste em situações reais
- Pergunte quando tiver dúvida
- Consulte este guia sempre que precisar

---

**Versão:** 1.0 (Para Iniciantes)  
**Data:** Novembro 2024  
**Autor:** Guia Didático NOC - Comandos Windows  
**Nível:** Iniciante (ELI5 - Explain Like I'm 5)

---

## ❓ Perguntas Frequentes (FAQ)

**P: Por que o ping falha mesmo com internet funcionando?**
R: Alguns servidores bloqueiam ping por segurança. Tente pingar outro servidor.

**P: O que é um "bom" tempo de ping?**
R: 
- Excelente: < 20ms
- Bom: 20-50ms
- Razoável: 50-100ms
- Ruim: > 100ms

**P: Posso danificar algo usando esses comandos?**
R: Não! Esses comandos apenas LEEM informações, não modificam nada.

**P: Preciso ser administrador?**
R: Para ping, tracert, nslookup: NÃO
Para alguns netstat avançados: SIM

**P: Qual a diferença entre CMD e PowerShell?**
R: PowerShell é mais moderno e poderoso. Mas os comandos de rede funcionam em ambos!

---

🎉 **Parabéns!** Agora você sabe os comandos básicos de rede do Windows! Continue praticando e em breve isso será natural para você! 🚀

