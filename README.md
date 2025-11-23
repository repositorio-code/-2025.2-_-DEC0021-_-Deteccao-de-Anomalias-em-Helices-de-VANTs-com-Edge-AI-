# 2025.2 - DEC0021 - Detecção de Anomalias em Hélices de VANTs com Edge AI

> Projeto de Trabalho de Conclusão de Curso (TCC) - UFSC Campus Araranguá

Este repositório contém o código-fonte, esquemas e documentação do sistema embarcado desenvolvido para detectar falhas estruturais e operacionais (desbalanceamento) em sistemas rotativos de drones utilizando Inteligência Artificial na borda (*TinyML*).

**Autor:** [Nikolas Lopes]  
**Orientador:** [Prof. Rodrigo Pereira, DR.]

---

## 📸 Galeria do Projeto

<table>
  <tr>
    <td align="center">
      <img src="docs/Foto_Drone.png" width="400" alt="Configuração da Hélice"/>
      <br />
      <b>Sistema completo</b>
    </td>
    <td align="center">
      <img src="docs/Foto_Montagem.png" width="400" alt="Detalhe do Sensor"/>
      <br />
      <b>Montagem do Sensor Arduino</b>
    </td>
  </tr>
  <tr>
    <td colspan="2" align="center">
      <img src="docs/Foto_Setup.png" width="600" alt="Setup Completo"/>
      <br />
      <b>Montagem Para Coleta</b>
    </td>
  </tr>
</table>

---

## 📖 Introdução

A segurança operacional de Veículos Aéreos Não Tripulados (VANTs) depende criticamente da integridade de seus sistemas de propulsão. Falhas em hélices, como rachaduras ou desbalanceamentos, podem levar a vibrações excessivas e quedas catastróficas.

Este projeto propõe uma solução de baixo custo baseada em **Edge AI** (Inteligência Artificial na Borda). Utilizando um microcontrolador **Arduino Nano 33 BLE Sense** e a plataforma **Edge Impulse**, desenvolvemos um modelo capaz de classificar em tempo real, através da análise de vibração (FFT), os seguintes estados operacionais:

1. **Motor Parado**
2. **Motor Ligando** (Transitório)
3. **Motor Ligado** (Operação Normal)
4. **Anomalia** (Hélice Desbalanceada/Danificada)

A solução elimina a necessidade de telemetria para a nuvem, garantindo latência mínima (<20ms) e maior autonomia.

---

## 📊 Resultados Obtidos

O modelo de TinyML demonstrou alta eficácia na distinção entre estados normais e de falha. Abaixo, os resultados de validação e métricas de desempenho:

### Matriz de Confusão
<div align="center">
  <img src="docs/Matriz_Confusao.PNG" width="600" alt="Matriz de Confusão"/>
  <p><i>Demonstração da precisão na classificação dos estados. Note a clara separação entre "Motor Ligado" e "Anomalia".</i></p>
</div>

### Métricas Detalhadas (F1-Score)
<div align="center">
  <img src="docs/METRICAS.PNG" width="600" alt="Métricas F1 Score"/>
</div>

---

## ⚙️ Pipeline de Machine Learning

O desenvolvimento seguiu o ciclo de vida de Edge AI padrão:
1. **Coleta de Dados:** Acelerômetro 3 eixos a 100Hz.
2. **Processamento (DSP):** Filtro Passa-Alta + FFT (Análise Espectral).
3. **Classificação:** Rede Neural Densa (DNN).

<div align="center">
  <img src="docs/edge-ai-lifecycle-ml-pipeline.png" width="700" alt="Pipeline ML"/>
</div>

> *Distribuição dos dados coletados para treinamento e teste:*
> <img src="docs/Distribuicao_Dados.PNG" width="600" />

---

## 🛠 Hardware Necessário

Lista de materiais utilizados na construção da bancada de testes e do sistema embarcado:

| Componente | Modelo Específico | Função |
| :--- | :--- | :--- |
| **Microcontrolador** | Arduino Nano 33 BLE Sense | Processamento de IA e leitura do sensor IMU (LSM9DS1). |
| **Motor Brushless** | D2836 (Série 2217) - 1000KV | Propulsão principal do sistema de teste ([Ver Manual](docs/Brushless_Motor_Instruction (1).pdf)). |
| **ESC** | Controlador de 40A | Controle de velocidade do motor. |
| **Hélices** | Modelo 1045 (Plástico) | Uma íntegra e outra com fita adesiva para simular desbalanceamento. |
| **Fonte de Bancada** | Ajustável (12V) | Simulação de bateria LiPo 3S. |

---

## 🔌 Esquema de Conexão

A conexão física é simplificada devido aos sensores integrados do Nano 33 BLE Sense.

1. **Fixação do Sensor:** O Arduino deve ser fixado rigidamente à base do motor (usando fita dupla face forte e abraçadeiras) para garantir que o acelerômetro interno capture as vibrações mecânicas.
2. **Alimentação:** O Arduino é alimentado via cabo USB (durante o desenvolvimento/monitoramento serial).
3. **Controle do Motor:** O ESC é conectado ao motor (3 fios) e alimentado pela fonte 12V. O sinal de controle PWM do ESC pode ser gerado por um gerador de sinal externo ou por um pino PWM de outro microcontrolador auxiliar.

---

## 🚀 Guia de Instalação e Uso (Passo a Passo)

Para rodar este projeto no seu Arduino Nano 33 BLE Sense, siga o procedimento abaixo. Todo o código necessário está contido na biblioteca exportada pelo Edge Impulse.

### 1. Preparar a Arduino IDE
1.  Baixe e instale a [Arduino IDE](https://www.arduino.cc/en/software).
2.  Vá em **Tools > Board > Boards Manager...**
3.  Pesquise por `Nano 33 BLE` e instale o pacote **"Arduino Mbed OS Nano Boards"**.
    *   *Nota: Isso pode levar alguns minutos.*

### 2. Importar a Biblioteca do Projeto
O arquivo `.zip` que está na pasta `Software/edge-impulse-build` deste repositório contém todo o modelo e lógica.
1.  Baixe o arquivo `.zip` da pasta `Software` para o seu computador.
2.  Na Arduino IDE, vá no menu: **Sketch > Include Library > Add .ZIP Library...**
3.  Selecione o arquivo que você acabou de baixar.
    *   *A IDE irá mostrar uma mensagem "Library added to your libraries" no rodapé.*

### 3. Carregar o Código na Placa
Não é necessário escrever código do zero. A biblioteca já inclui exemplos prontos configurados para o seu sensor.
1.  Vá em **File > Examples**.
2.  Role até o final da lista, onde ficam as "Examples from Custom Libraries".
3.  Procure pela pasta com o nome da sua biblioteca (ex: `tcc-drone-edge-ai` ou similar).
4.  Selecione: **nano_ble33_sense > nano_ble33_sense_accelerometer**.
    *   *Este exemplo já vem configurado para ler o IMU LSM9DS1 e rodar a inferência.*

### 4. Monitorar os Resultados
1.  Conecte o Arduino Nano 33 BLE ao PC via USB.
2.  Selecione a porta correta em **Tools > Port**.
3.  Clique no botão **Upload** (Seta para a direita) e aguarde a compilação.
4.  Após carregar, abra o **Serial Monitor** (Lupa no canto superior direito).
5.  Ajuste a velocidade (baud rate) para **115200**.

---

## 💻 Funcionamento do Firmware

O código realiza o seguinte fluxo em loop contínuo:

1. **Leitura:** Coleta dados brutos de aceleração (eixos X, Y, Z) do sensor interno.
2. **DSP Integrado:** A biblioteca processa os dados brutos (Filtro + FFT) automaticamente.
3. **Inferência:** Executa a Rede Neural (TFLite Micro) na borda.
4. **Saída:** Imprime no Serial Monitor a classe detectada e sua probabilidade.

---

## 📄 Licença

Este projeto é de código aberto e está licenciado sob a [MIT License](LICENSE).
