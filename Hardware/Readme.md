# 🛠 Especificações de Hardware

Este diretório contém detalhes técnicos e visuais sobre os componentes físicos utilizados na construção da bancada de testes e do sistema embarcado do projeto.

## 📸 Galeria de Componentes


<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="ArduinoNANO.png" width="250" alt="Arduino Nano 33 BLE Sense"/>
        <br /><b>Microcontrolador</b>
      </td>
      <td align="center">
        <img src="MotorBrushless.png" width="250" alt="Motor Brushless D2836"/>
        <br /><b>Motor Brushless D2836</b>
      </td>
      <td align="center">
        <img src="DiagramaCircuito.png" width="400" alt="Esquemático Simplificado"/>
        <br /><b>Diagrama de Conexão</b>
      </td>
    </tr>
  </table>
</div>
<div align="center">
<td align="center">
        <img src="DiagramaCircuito.png" width="400" alt="Esquemático Simplificado"/>
        <br /><b>Diagrama de Conexão</b>
</td>
## 1. Microcontrolador: Arduino Nano 33 BLE Sense
A unidade de processamento central responsável pela coleta de dados e execução do modelo de TinyML.

*   **Processador:** nRF52840 (ARM Cortex-M4F @ 64MHz)
*   **Memória:** 1MB Flash / 256KB RAM
*   **Sensor IMU:** LSM9DS1 (Acelerômetro + Giroscópio de 9 eixos)
*   **Tensão de Operação:** 3.3V
*   **Justificativa:** Escolhido pela integração nativa de sensores de alta precisão e capacidade de processamento DSP (Digital Signal Processing) necessária para a FFT.

## 2. Motor Brushless: D2836 (Série 2217)
Motor responsável pela propulsão do sistema de teste.

*   **Modelo:** D2836-8 (Série 2217)
*   **KV (RPM/V):** 1100KV (ou 1000KV conforme disponibilidade)
*   **Potência Máxima:** ~336 Watts
*   **Corrente Máxima:** ~18A (Eficiência máxima)
*   **Eixo:** 4.0 mm
*   **Peso:** 70g
*   **Empuxo Estimado:** ~1130g (com hélice 11x7 ou similar)
*   **Manual Técnico:** [Ver PDF em ../docs/Brushless_Motor_Instruction (1).pdf](../docs/Brushless_Motor_Instruction%20(1).pdf)

## 3. Controlador de Velocidade (ESC)
*   **Corrente Contínua:** 40A
*   **BEC (Battery Eliminator Circuit):** 5V/3A (Linear)
*   **Bateria Suportada:** 2S a 4S LiPo

## 4. Hélices
Para os testes de indução de falhas, foram utilizados dois conjuntos:
*   **Tipo:** 1045 (10 polegadas x 4.5 de passo), Plástico ABS.
*   **Modificação de Falha:** Aplicação de fita adesiva em uma das pás para alterar o centro de gravidade e induzir vibração por desbalanceamento dinâmico, sem destruição da peça.

