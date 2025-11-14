# 📚 Guias de Comandos para NOC - Documentação Completa

## 🎯 Visão Geral

Este repositório contém guias **super detalhados** e **didáticos** de comandos para analistas de NOC (Network Operations Center), especialmente **iniciantes**. Toda documentação foi escrita pensando em explicar **como se fosse para uma criança de 5 anos**, com analogias, exemplos práticos e cenários reais.

---

## 📖 Estrutura da Documentação

### 🗂️ Guias Disponíveis

| Guia | Descrição | Para quem? | Dificuldade |
|------|-----------|------------|-------------|
| **[GUIA_COMANDOS_WINDOWS_BASICOS.md](GUIA_COMANDOS_WINDOWS_BASICOS.md)** | Comandos de rede do Windows (ping, tracert, ipconfig, throughput) | Todos os analistas NOC | ⭐ Básico |
| **[GUIA_ZTE_INICIANTE.md](GUIA_ZTE_INICIANTE.md)** | Comandos para OLT ZTE C300/C320 | Quem trabalha com GPON/Fibra | ⭐⭐ Básico-Intermediário |
| **[GUIA_HUAWEI_INICIANTE.md](GUIA_HUAWEI_INICIANTE.md)** | Comandos para Switches Huawei | Quem trabalha com switches Huawei | ⭐⭐ Básico-Intermediário |
| **[GUIA_DATACOM_INICIANTE.md](GUIA_DATACOM_INICIANTE.md)** | Comandos para Switches Datacom | Quem trabalha com switches Datacom | ⭐⭐ Básico-Intermediário |
| **[GUIA_COMANDOS_NOC_BASICO.md](GUIA_COMANDOS_NOC_BASICO.md)** | Guia consolidado original (referência rápida) | Analistas experientes | ⭐⭐⭐ Intermediário |

---

## 🚀 Como Usar Esta Documentação

### 👶 Se você é INICIANTE (primeiro dia/semana no NOC):

**Comece por aqui:**

1. **[GUIA_COMANDOS_WINDOWS_BASICOS.md](GUIA_COMANDOS_WINDOWS_BASICOS.md)**
   - Aprenda ping, tracert, ipconfig
   - Essenciais para QUALQUER profissional de rede
   - ⏱️ Tempo de leitura: 1-2 horas

2. **Depois, vá para o guia do equipamento que você vai trabalhar:**
   - Trabalha com fibra/GPON? → **[GUIA_ZTE_INICIANTE.md](GUIA_ZTE_INICIANTE.md)**
   - Trabalha com switches Huawei? → **[GUIA_HUAWEI_INICIANTE.md](GUIA_HUAWEI_INICIANTE.md)**
   - Trabalha com switches Datacom? → **[GUIA_DATACOM_INICIANTE.md](GUIA_DATACOM_INICIANTE.md)**

3. **Pratique os exercícios** no final de cada guia

---

### 🧑‍💼 Se você é EXPERIENTE (já trabalha há meses/anos):

**Use como referência rápida:**

- **[GUIA_COMANDOS_NOC_BASICO.md](GUIA_COMANDOS_NOC_BASICO.md)** - Consulta rápida, sem explicações longas
- Use os guias específicos quando precisar relembrar algo ou ensinar um colega

---

## 🎓 O que Cada Guia Contém

### ✅ Todos os guias incluem:

📚 **Glossário de Termos**
- Explicação de CADA termo técnico
- Analogias simples do dia a dia

🔑 **Como Acessar**
- Passo a passo de como logar nos equipamentos
- Telnet, SSH, Console

🎮 **Modos de Operação**
- Explicação dos níveis de acesso
- Quando usar cada um

📝 **Comandos Detalhados**
- O QUE o comando faz
- QUANDO usar
- EXEMPLOS reais
- OUTPUT esperado
- Como INTERPRETAR os resultados

🔧 **Cenários Práticos**
- Situações reais do dia a dia
- Passo a passo de troubleshooting
- O que cada resultado significa

⚠️ **Erros Comuns**
- Problemas frequentes
- Como resolver

📊 **Tabelas Resumo**
- Comandos por situação
- Valores de referência

📖 **Referências Oficiais**
- Links para documentação dos fabricantes
- Materiais de estudo

💡 **Dicas para Iniciantes**
- Atalhos
- Boas práticas
- O que NUNCA fazer

🎓 **Exercícios Práticos**
- Para você praticar
- Aprende fazendo!

---

## 🔍 Como Encontrar Comandos Rapidamente

### Método 1: Pesquisa por Situação

**Você está enfrentando:**

| Situação | Abra o Guia | Vá para Seção |
|----------|-------------|---------------|
| Cliente sem internet | GUIA_ZTE_INICIANTE.md | "Cenário 1: Cliente Sem Internet" |
| Link down no switch | GUIA_HUAWEI_INICIANTE.md ou GUIA_DATACOM_INICIANTE.md | "Cenário 1: Link Down" |
| VLAN não funciona | Qualquer guia de switch | "Cenário 2: VLAN Não Funciona" |
| Sinal óptico fraco | GUIA_ZTE_INICIANTE.md | "Cenário 3: Internet Lenta" |
| Testar conectividade | GUIA_COMANDOS_WINDOWS_BASICOS.md | "Comando 1: PING" |

---

### Método 2: Pesquisa por Comando

Use **Ctrl+F** (buscar) no arquivo e digite o comando que procura.

**Exemplos:**
- Busque `show gpon onu` no **GUIA_ZTE_INICIANTE.md**
- Busque `display interface` no **GUIA_HUAWEI_INICIANTE.md**
- Busque `show interfaces` no **GUIA_DATACOM_INICIANTE.md**
- Busque `ping` no **GUIA_COMANDOS_WINDOWS_BASICOS.md**

---

## 📱 Recomendações de Uso

### 💻 No Computador:

1. **Baixe os guias** para ter acesso offline
2. **Use um leitor Markdown** (VS Code, Typora, ou simplesmente o navegador)
3. **Mantenha os guias abertos** em uma janela enquanto trabalha em outra

---

### 📱 No Celular/Tablet:

1. Acesse via **GitHub** (os arquivos .md são renderizados automaticamente)
2. Ou use apps de leitura Markdown:
   - **Android:** Markor, Markdown Reader
   - **iOS:** iA Writer, Markdown Pro

---

## 🎯 Diferenciais Destes Guias

### ✅ O que torna estes guias especiais:

1. **Linguagem SUPER simples**
   - Explicações como se fosse para uma criança
   - Sem jargões desnecessários
   - Analogias do dia a dia

2. **Analogias que fazem SENTIDO**
   - OLT = Estação de tratamento de água
   - VLAN = Envelopes coloridos
   - Switch = Estação de metrô
   - Ping = Bater palmas e ouvir eco

3. **Exemplos REAIS com outputs**
   - Não apenas "execute X"
   - Mostra O QUE você vai ver
   - Ensina a INTERPRETAR o resultado

4. **Valores de referência claros**
   - ✅ Verde = Bom
   - ⚠️ Amarelo = Atenção
   - ❌ Vermelho = Problema

5. **Cenários práticos do dia a dia**
   - "Cliente sem internet - o que fazer?"
   - Passo a passo completo
   - Como diagnosticar

6. **Baseado em documentação oficial**
   - Referências verificadas
   - Comandos testados
   - Boas práticas da indústria

---

## ⚠️ Avisos Importantes

### 🔒 Segurança

- **NO NOC N1:** Use APENAS comandos de visualização (show/display)
- **NUNCA configure** sem autorização do supervisor/N2
- **NUNCA execute** comandos destrutivos (delete, clear, restart)
- **SEMPRE documente** o que você fez

### 📋 Boas Práticas

1. **Sempre documente suas ações:**
   - Anote comandos executados
   - Copie outputs relevantes
   - Registre horários

2. **Verifique antes de executar:**
   - Tem certeza do comando?
   - Está no equipamento correto?
   - Vai apenas visualizar, não alterar?

3. **Quando em dúvida:**
   - Pergunte ao supervisor
   - Não invente
   - Melhor perguntar 10 vezes que quebrar uma vez

4. **Aprenda com cada atendimento:**
   - Faça anotações pessoais
   - Crie seu próprio "caderno de comandos"
   - Revise periodicamente

---

## 🤝 Contribuições

Este material foi criado com base em:

- ✅ **Documentação oficial** dos fabricantes (ZTE, Huawei, Datacom, Microsoft)
- ✅ **Experiência prática** de analistas NOC
- ✅ **Feedback** de iniciantes aprendendo os comandos
- ✅ **Boas práticas** da indústria de telecomunicações

---

## 📞 Estrutura de Escalação

Lembre-se da hierarquia:

```
┌─────────────────────────────────────────┐
│  N1 - VOCÊ (Analista Júnior)           │
│  - Comandos de visualização (show)     │
│  - Diagnóstico básico                  │
│  - Documentação                        │
└─────────────────┬───────────────────────┘
                  │
                  │ Escala se não resolver
                  ↓
┌─────────────────────────────────────────┐
│  N2 (Analista Pleno/Sênior)            │
│  - Configurações simples               │
│  - Troubleshooting avançado            │
│  - Provisionamento                     │
└─────────────────┬───────────────────────┘
                  │
                  │ Escala se não resolver
                  ↓
┌─────────────────────────────────────────┐
│  N3 (Especialista/Arquiteto)           │
│  - Configurações complexas             │
│  - Problemas críticos                  │
│  - Mudanças estruturais                │
└─────────────────────────────────────────┘
```

**NUNCA tenha vergonha de escalar!** É melhor escalar cedo do que causar um problema maior.

---

## 🎓 Plano de Estudos Sugerido (Primeira Semana)

### 📅 Dia 1-2: Fundamentos Windows

- ✅ Leia **GUIA_COMANDOS_WINDOWS_BASICOS.md** (completo)
- ✅ Pratique ping, tracert, ipconfig
- ✅ Faça os exercícios do final

### 📅 Dia 3-4: Seu Equipamento Principal

**Se trabalha com fibra:**
- ✅ Leia **GUIA_ZTE_INICIANTE.md** (até "Comandos Essenciais")
- ✅ Familiarize-se com os termos (OLT, ONU, PON)
- ✅ Entenda o conceito de sinal óptico (RX/TX)

**Se trabalha com switches:**
- ✅ Leia **GUIA_HUAWEI_INICIANTE.md** OU **GUIA_DATACOM_INICIANTE.md**
- ✅ Familiarize-se com VLANs
- ✅ Entenda trunk vs access

### 📅 Dia 5: Cenários Práticos

- ✅ Leia TODOS os "Cenários Práticos" do seu guia
- ✅ Imagine-se executando os comandos
- ✅ Anote dúvidas para tirar com supervisor

---

## 🏆 Meta de Aprendizado

### ✅ Após 1 semana você deve conseguir:

- [ ] Fazer ping e interpretar resultados
- [ ] Fazer tracert e identificar onde está o problema
- [ ] Verificar configurações de rede do PC (ipconfig)
- [ ] Acessar um equipamento via telnet/SSH
- [ ] Executar comandos básicos de visualização
- [ ] Identificar se uma ONU está online/offline (ZTE)
- [ ] Verificar sinal óptico (ZTE)
- [ ] Verificar se uma VLAN existe (Switches)
- [ ] Encontrar um dispositivo pelo MAC (Switches)
- [ ] **Documentar** tudo que você faz

### ✅ Após 1 mês você deve conseguir:

- [ ] Diagnosticar 80% dos problemas de "cliente sem internet"
- [ ] Identificar problemas de sinal óptico
- [ ] Identificar problemas de VLAN
- [ ] Encontrar qualquer dispositivo na rede
- [ ] Escalar corretamente (com todas as informações necessárias)
- [ ] Usar os guias como consulta rápida (sem precisar ler tudo)

---

## 📈 Evolução Contínua

### 💪 Para continuar evoluindo:

1. **Crie seu próprio caderno**
   - Anote comandos que você mais usa
   - Adicione notas pessoais
   - Desenhe diagramas da sua rede

2. **Peça feedback**
   - Pergunte ao supervisor como você está indo
   - Peça para revisar suas documentações
   - Aprenda com analistas mais experientes

3. **Estude a fundo**
   - Leia documentação oficial dos fabricantes
   - Faça cursos online (Udemy, Alura, etc)
   - Tire certificações (CCNA, HCIA, etc)

4. **Pratique, pratique, pratique**
   - Use cada ticket como oportunidade de aprender
   - Não tenha medo de errar (em ambiente de teste)
   - Quanto mais você faz, mais natural fica

---

## 🎯 Objetivo Final

**O objetivo destes guias é fazer você:**

1. ✅ Se sentir **confiante** ao usar os comandos
2. ✅ **Entender** o que cada comando faz (não apenas decorar)
3. ✅ **Diagnosticar** problemas de forma eficiente
4. ✅ **Escalar** corretamente quando necessário
5. ✅ **Crescer** na carreira de NOC/Redes

---

## 💬 Mensagem Final

### 🌟 Para você, analista iniciante:

**Bem-vindo ao mundo das redes!** 🚀

Este é um campo **incrível**, cheio de desafios e aprendizados diários. No começo pode parecer muita informação, mas **não desista**!

**Lembre-se:**
- 🧠 **Ninguém nasce sabendo** - todos os especialistas já foram iniciantes um dia
- 📈 **Você vai melhorar a cada dia** - a curva de aprendizado é íngreme no início, mas compensa
- 🤝 **Perguntar não é fraqueza** - é demonstração de vontade de aprender
- 💪 **Você é capaz** - se outros conseguiram, você também consegue!

**Estes guias foram feitos especialmente para VOCÊ**. Use-os, abuse deles, faça anotações neles, volte quantas vezes precisar.

**Boa sorte na sua jornada! Você vai longe! 🎯**

---

## 📝 Controle de Versão

| Versão | Data | Alterações |
|--------|------|------------|
| 1.0 | Nov/2025 | Criação dos guias iniciais (Windows, ZTE, Huawei, Datacom) |

---

## 📧 Precisa de Ajuda?

- 💬 Pergunte ao seu **supervisor** ou **mentor**
- 📚 Consulte a **documentação oficial** dos fabricantes
- 🔍 Use os **exercícios práticos** dos guias
- 📝 Revise os **cenários práticos** constantemente

---

**Bons estudos e bom trabalho no NOC!** 🎯🚀

---

## 📑 Índice Rápido de Comandos

### Windows
- `ping` - Testar conectividade
- `tracert` - Ver caminho até destino
- `ipconfig` - Ver configurações de rede
- `pathping` - Teste completo (ping + tracert)
- `nslookup` - Testar DNS

### ZTE (OLT)
- `show gpon onu by sn` - Localizar ONU
- `show pon power onu-rx` - Ver sinal óptico
- `show gpon onu state` - Ver status ONUs
- `show vlan` - Ver VLANs
- `show mac vlan` - Ver MACs em VLAN

### Huawei (Switch)
- `display interface brief` - Status de portas
- `display vlan` - Ver VLANs
- `display mac-address` - Ver MACs aprendidos
- `display arp` - Ver tabela ARP
- `display transceiver` - Ver SFPs

### Datacom (Switch)
- `show interfaces status` - Status de portas
- `show vlan` - Ver VLANs
- `show mac address-table` - Ver MACs
- `show arp` - Ver tabela ARP
- `show environment` - Status hardware

---

**Última atualização:** Novembro de 2025  
**Versão:** 1.0  
**Autor:** ThomasJPF  
**Público-alvo:** Analistas NOC Iniciantes a Intermediários

