# advanced-math-engine

### High-Precision Mathematical Computing Engine

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Dependencies](https://img.shields.io/badge/Dependencies-None-success)
![Platform](https://img.shields.io/badge/Platform-Termux%20%7C%20AndroidIDE%20%7C%20Linux-lightgrey)

**Math Engine** é um mecanismo computacional desenvolvido em Python para executar operações matemáticas com foco em precisão numérica, confiabilidade e eficiência algorítmica.

O projeto foi concebido para demonstrar como conceitos de matemática computacional, algoritmos numéricos e engenharia de software podem ser combinados em uma aplicação leve, independente e acessível.

Sua arquitetura utiliza recursos nativos do Python, dispensando bibliotecas externas e permitindo sua execução em diferentes ambientes, incluindo dispositivos Android.

---

## 1. Visão geral

O Math Engine reúne três operações matemáticas principais:

- Cálculo de Pi (π) com alta precisão.
- Cálculo de raízes quadradas utilizando aritmética decimal.
- Estimativa de Pi por meio de simulação estatística Monte Carlo.

Cada operação utiliza uma abordagem matemática específica, escolhida de acordo com o tipo de problema que precisa resolver.

O objetivo não é apenas produzir resultados numéricos, mas também manter controle sobre a precisão dos cálculos, validar entradas e reduzir erros decorrentes das limitações da representação numérica convencional.

## 2. Arquitetura e tecnologias

O projeto foi desenvolvido com uma arquitetura modular, separando os algoritmos matemáticos, as validações e a interface de linha de comando.

### Tecnologias utilizadas

| Tecnologia | Aplicação |
|---|---|
| Python | Linguagem principal |
| Decimal | Aritmética decimal de precisão configurável |
| Binary Splitting | Otimização do cálculo de Pi |
| Chudnovsky | Algoritmo para cálculo de Pi |
| Monte Carlo | Estimativa estatística |
| argparse | Interface de linha de comando |
| unittest | Testes automatizados |

Não são necessárias dependências externas.

### Organização lógica

O mecanismo está dividido em cinco componentes:

1. **Validation Layer:** verifica parâmetros e entradas antes da execução dos cálculos.
2. **Mathematical Core:** concentra os algoritmos matemáticos.
3. **Precision Management:** controla a precisão decimal e o arredondamento.
4. **Command Line Interface:** permite executar operações por meio de comandos.
5. **Testing Layer:** verifica o comportamento esperado dos principais recursos.

Essa separação facilita a manutenção, a identificação de falhas e a expansão futura do projeto.

---

## 3. Algoritmos matemáticos

### 3.1. Cálculo de Pi: Chudnovsky + Binary Splitting

O cálculo de Pi utiliza a série de Chudnovsky, conhecida por sua rápida convergência.

Cada termo da série contribui com aproximadamente 14 casas decimais corretas de Pi.

Para melhorar a eficiência computacional, o projeto utiliza a técnica de Binary Splitting.

Em vez de realizar toda a sequência de operações de maneira linear, essa técnica divide o cálculo em intervalos menores e combina seus resultados por meio de operações inteiras.

**Principais benefícios:**

- Redução de operações intermediárias desnecessárias.
- Utilização de aritmética inteira durante a construção da série.
- Melhor escalabilidade em cálculos de alta precisão.
- Menor dependência de arredondamentos intermediários.

O resultado final é convertido para Decimal, permitindo controlar a precisão e o arredondamento da saída.

### 3.2. Raiz quadrada: Decimal

A operação de raiz quadrada utiliza o módulo Decimal do Python.

Diferentemente dos números tradicionais de ponto flutuante (`float`), que possuem precisão binária limitada, Decimal permite configurar a quantidade de dígitos significativos utilizados nos cálculos.

Isso é especialmente útil em operações que exigem maior controle sobre a representação decimal.

O mecanismo também implementa:

- Verificação de entradas numéricas.
- Rejeição de valores negativos.
- Controle de precisão.
- Arredondamento decimal.
- Tratamento de valores inválidos e não finitos.

### 3.3. Estimativa de Pi: Monte Carlo

O método Monte Carlo utiliza simulação aleatória para estimar o valor de Pi.

O algoritmo gera pontos aleatórios dentro de um quadrado e verifica quantos deles estão dentro de um quarto de círculo.

A relação matemática utilizada é:

\[
\pi \approx 4 \times \frac{N_i}{N_t}
\]

Onde:

- \(N_i\): quantidade de pontos dentro do círculo.
- \(N_t\): quantidade total de pontos gerados.

Quanto maior o número de amostras, maior tende a ser a estabilidade da estimativa.

Entretanto, por ser um método estatístico, ele não garante uma quantidade específica de casas decimais corretas.

O projeto também permite definir uma semente aleatória (`seed`), possibilitando reproduzir uma simulação com os mesmos parâmetros.

---

## 4. Instalação

O Math Engine utiliza apenas a biblioteca padrão do Python.

### Requisitos

- Python 3.9 ou superior.
- Terminal ou ambiente compatível.
- Sistema operacional Linux, Windows ou Android com Termux/AndroidIDE.

### Clonar o repositório

```bash
git clone https://github.com/SEU-USUARIO/math-engine.git
```

Entre na pasta:

```bash
cd math-engine
```

Não é necessário instalar pacotes adicionais.

---

## 5. Utilização

O sistema possui uma interface CLI (Command Line Interface), permitindo executar cada operação diretamente pelo terminal.

### Calcular Pi

```bash
python math_engine.py pi -d 100
```

Calcula Pi com 100 casas decimais.

Para aumentar a precisão:

```bash
python math_engine.py pi -d 1000
```

### Calcular raiz quadrada

```bash
python math_engine.py sqrt 2 -d 50
```

Calcula a raiz quadrada de 2 com 50 casas decimais.

Outros exemplos:

```bash
python math_engine.py sqrt 144 -d 20
```

```bash
python math_engine.py sqrt 98765.4321 -d 100
```

### Executar Monte Carlo

```bash
python math_engine.py monte-carlo -s 1000000
```

Executa uma simulação com um milhão de amostras.

Para reproduzir os resultados:

```bash
python math_engine.py monte-carlo -s 1000000 --seed 42
```

### Consultar a versão

```bash
python math_engine.py --version
```

### Consultar os comandos disponíveis

```bash
python math_engine.py --help
```

---

## 6. Qualidade e confiabilidade

O projeto incorpora mecanismos básicos de controle de qualidade para reduzir comportamentos inesperados durante a execução.

### Validação de entradas

Os parâmetros são verificados antes de serem utilizados nos algoritmos.

Exemplos de situações tratadas:

- Precisão decimal negativa.
- Número de amostras igual a zero.
- Valores numéricos inválidos.
- Tentativa de calcular raiz quadrada de números negativos.
- Valores não finitos.

### Gerenciamento de precisão

O uso de `localcontext()` permite isolar as configurações de precisão decimal de cada operação.

Isso reduz interferências entre cálculos diferentes e torna o comportamento numérico mais previsível.

### Testes automatizados

O projeto utiliza `unittest` para verificar operações e condições importantes.

Execute:

```bash
python math_engine.py test
```

Os testes verificam:

- Cálculo de Pi.
- Precisão dos resultados.
- Cálculo de raízes quadradas.
- Arredondamento.
- Rejeição de valores negativos.
- Validação de parâmetros.
- Reprodutibilidade do Monte Carlo.

Os testes representam uma camada de verificação do comportamento esperado, não uma certificação formal de precisão para qualquer entrada.

---

## 7. Desempenho e limitações

O desempenho depende de fatores como:

- Quantidade de casas decimais solicitadas.
- Capacidade de processamento do dispositivo.
- Memória disponível.
- Complexidade da operação matemática.

O Binary Splitting melhora o desempenho do cálculo de Pi em comparação com uma implementação puramente sequencial.

Ainda assim, cálculos com milhões de casas decimais podem exigir recursos computacionais consideráveis.

O Monte Carlo possui uma característica diferente: seu custo cresce proporcionalmente ao número de amostras, enquanto sua precisão estatística melhora relativamente devagar.

Por isso, os métodos devem ser utilizados de acordo com seus objetivos.

---

## 8. Aplicações e possibilidades de expansão

O Math Engine foi desenvolvido como uma base de estudos e experimentação em matemática computacional.

Sua arquitetura permite considerar futuras extensões, como:

- Operações com números extremamente grandes.
- Fatorial e combinações.
- Logaritmos de alta precisão.
- Exponenciação decimal.
- Conversões entre bases numéricas.
- Integração com APIs.
- Interface gráfica.
- Processamento paralelo.
- Benchmark de algoritmos.
- Exportação de resultados para arquivos.

Essas funcionalidades representam possibilidades de evolução, não recursos já implementados.

---

## 9. Objetivo do projeto

O Math Engine busca explorar a aplicação prática de algoritmos matemáticos e técnicas de precisão numérica em software.

Além de resolver operações matemáticas, o projeto permite estudar decisões importantes de engenharia, como escolha de algoritmos, controle de precisão, validação de dados, organização de código e testes automatizados.

A proposta é construir uma base que possa evoluir de uma ferramenta de terminal para um mecanismo matemático mais abrangente.

---

## 10. Licença

Este projeto está disponibilizado sob a licença MIT.

Consulte o arquivo `LICENSE` para conhecer os termos de utilização, modificação e distribuição.

---

## Autor

**Elison dos Santos Araujo**

Desenvolvimento Backend | Engenharia de Software | Java | Kotlin | Python

GitHub: https://github.com/elisondsaraujo

---

*Desenvolvido com Python, matemática computacional e foco em precisão.*
