# 🧮 Calculadora Gráfica - MARIE Assembly

## 📝 Sobre o Projeto
Este é um projeto acadêmico de arquitetura de computadores desenvolvido inteiramente em **Assembly MARIE** (Machine Architecture that is Really Intuitive and Easy). 

Diferente de calculadoras convencionais de terminal, este projeto vai além da lógica matemática e implementa um **motor de renderização gráfica**. O código processa as entradas do usuário, realiza o cálculo, divide o resultado em dígitos unitários e desenha visualmente os números no display do simulador manipulando ponteiros de memória (pixels).

## 🚀 Funcionalidades
* **4 Operações Básicas:** Suporte a Soma, Subtração, Multiplicação e Divisão.
* **Suporte a Números Negativos:** Capacidade de calcular e renderizar o sinal de menos (`-`). Limite de exibição de `-999` a `9999`.
* **Tratamento de Exceções:** Sistema de segurança que impede a divisão por zero. Caso ocorra, a execução é desviada para uma rotina de erro que desenha a palavra **ERRO** no display.
* **Renderização via Sprites:** O código possui "sprites" programados instrução por instrução para desenhar os caracteres mapeando a tela do simulador (16x16).

## ⚙️ Como Utilizar
Para testar a calculadora, você precisará do [Simulador MARIE.js](https://marie.js.org/) ou do simulador em Java.

Ao rodar o arquivo `Calculadora_DEFINITIVA.mas`, o painel (Display) será limpo (cor preta) e o sistema aguardará 3 entradas (Inputs) estritamente na seguinte ordem:

1. **Operador:** Digite o número correspondente à operação desejada:
   * `1` para Soma
   * `2` para Subtração
   * `3` para Multiplicação
   * `4` para Divisão
2. **Primeiro Valor (X):** Insira o primeiro número da operação.
3. **Segundo Valor (Y):** Insira o segundo número da operação.

Após o terceiro input, o resultado será processado e renderizado diretamente no display do simulador.

## 🧠 Arquitetura do Código
Para gerenciar a complexidade, as mais de 600 linhas de código foram estruturadas de forma modular:

* **Módulos 1 e 2 (Setup e I/O):** Responsáveis por limpar o buffer de vídeo (endereços `0F00` em diante) e rotear o operador lógico.
* **Módulo 3 (ALU):** Realiza as operações. Como o MARIE não possui instruções nativas de multiplicação e divisão, estas foram construídas do zero através de loops de somas e subtrações sucessivas.
* **Módulo 4 (Filtro Universal/Parser):** Uma rotina crucial que decompõe o valor final contínuo (ex: 250) em unidades individuais para o display (2, 5 e 0) através de subtrações de base 10 (milhar, centena, dezena, unidade).
* **Módulos 5, 6 e 7 (GPU Lógica):** Contém o motor de passo do cursor (para que os números não sejam desenhados um em cima do outro) e as coordenadas Hexadecimais para desenhar cada segmento gráfico na tela.

## 🛠️ Tecnologias e Conceitos Aplicados
* **Linguagem:** Assembly (Conjunto de Instruções MARIE)
* **Conceitos:** Endereçamento Indireto (`StoreI`), Desvios Condicionais (`Skipcond`), Manipulação de Memória de Vídeo, Loops, Ciclo Busca-Decodifica-Executa.
