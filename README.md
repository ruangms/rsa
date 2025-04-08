###Gerado por IA
```markdown
# Sistema de Criptografia RSA

<img src="https://img.shields.io/badge/Linguagem-C-success"> <img src="https://img.shields.io/badge/Status-Completo-brightgreen"> <img src="https://img.shields.io/badge/Versão-1.0-blue">

Um sistema completo de criptografia RSA para fins educacionais, implementando geração de chaves, cifragem e decifragem de mensagens.

## 📌 Índice
- [Visão Geral](#-visão-geral)
- [Funcionalidades](#-funcionalidades)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Uso](#-instalação-e-uso)
- [Arquitetura Técnica](#%EF%B8%8F-arquitetura-técnica)
- [Exemplo Prático](#-exemplo-prático)
- [Limitações](#-limitações)
- [Arquivos Gerados](#-arquivos-gerados)

## 🌐 Visão Geral
Implementação didática do algoritmo RSA com:
- **Geração de chaves**: Usando primos P e Q
- **Cifragem**: Transformação textual → numérica → criptografada
- **Decifragem**: Operação modular reversa com chave privada

![Diagrama RSA](https://upload.wikimedia.org/wikipedia/commons/1/18/RSA_encryption_%28pt%29.svg)

## ✨ Funcionalidades
| Módulo | Descrição |
|--------|-----------|
| `pega_P_Q()` | Valida primos e calcula n = P×Q |
| `escolha_e()` | Seleciona expoente público coprimo com φ(n) |
| `criptografar()` | Codifica: A=2, B=3,... Espaço=28 → C = Mᵉ mod n |
| `descriptografar()` | Decodifica: M = Cᵈ mod n → texto original |
| `power()` | Exponenciação modular eficiente |
| `teste_primo()` | Verificação de primalidade |

## 🛠️ Pré-requisitos
- Compilador C (GCC recomendado)
- Biblioteca matemática (`-lm`):
  ```bash
  sudo apt-get install build-essential
  ```

## 📥 Instalação e Uso

### Compilação
```bash
gcc rsa.c -o rsa -lm
```

### Execução
```bash
./rsa
```

### Fluxo de Trabalho
1. **Gerar Chaves Públicas**
   - Insira primos P e Q (ex: 61 e 53)
   - Sistema calcula automaticamente:
     - n = 61×53 = 3233
     - φ(n) = 60×52 = 3120
     - e = 17 (coprimo com 3120)

2. **Criptografar**
   ```text
   Mensagem: "HELLO"
   Codificação: H(8)→8, E(5)→5, L(12)→12, L(12)→12, O(15)→15
   Criptografia: 8¹⁷ mod 3233 = 3007, ...
   ```

3. **Descriptografar**
   - Forneça P, Q e e originais
   - Cálculo automático de d (inverso modular)
   - Decodificação numérica → alfabética

## ⚙️ Arquitetura Técnica

### Algoritmos-Chave
1. **Teste de Primalidade** (Divisão trial)
2. **Algoritmo Euclidiano** (MDC para e e φ(n))
3. **Exponenciação Rápida** (O(log y) para xʸ mod p)

### Estrutura de Dados
- **Mensagem**: Array de 50 caracteres
- **Criptograma**: Array de long long int
- **Chaves**: Pares (n, e) e d

### Otimizações
- `power()`: Usa bitshifting para cálculo modular eficiente
- Pré-conversão para maiúsculas com `toupper()`

## 📖 Exemplo Prático

### Entrada
```c
P = 61
Q = 53
e = 17
Mensagem = "RS4"
```

### Processamento
1. Codificação: R(18)→18, S(19)→19, Espaço→28, 4→?? (Inválido)
2. Criptografia:
   - 18¹⁷ mod 3233 = 1802
   - 19¹⁷ mod 3233 = 1216
3. Saída: `1802 1216 28`

### Decriptação:
d = 2753 (17⁻¹ mod 3120)
- 1802²⁷⁵³ mod 3233 = 18 → R
- 1216²⁷⁵³ mod 3233 = 19 → S

## ⚠️ Limitações
| Item | Restrição |
|------|-----------|
| Tamanho da Mensagem | Máx. 49 caracteres |
| Caracteres Válidos | A-Z, espaço |
| Tamanho de Primos | Limitado a `long long int` |
| Segurança | **Não adequado para uso real** |

## 📂 Arquivos Gerados
| Arquivo | Formato | Exemplo |
|---------|---------|---------|
| `CHAVE_RSA.txt` | `n = 3233, e = 17` | Chave pública |
| `mensagem_criptografada.txt` | `3017 1216 28` | Valores separados por espaços |

---

**Nota Educacional**: Este projeto demonstra os princípios matemáticos do RSA. Para implementações seguras, use bibliotecas criptográficas profissionais como OpenSSL.
