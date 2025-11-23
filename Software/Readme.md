## 🚀 Guia de Instalação e Uso (Passo a Passo)

Para rodar este projeto no seu Arduino Nano 33 BLE Sense, siga o procedimento abaixo. Todo o código necessário está contido na biblioteca exportada pelo Edge Impulse.

### 1. Preparar a Arduino IDE
1.  Baixe e instale a [Arduino IDE](https://www.arduino.cc/en/software).
2.  Vá em **Tools > Board > Boards Manager...**
3.  Pesquise por `Nano 33 BLE` e instale o pacote **"Arduino Mbed OS Nano Boards"**.
    *   *Nota: Isso pode levar alguns minutos.*

### 2. Importar a Biblioteca do Projeto
O arquivo `.zip` que está na pasta `Software/edge-impulse-build` contém todo o modelo e lógica.
1.  Baixe o arquivo `.zip` deste repositório para o seu computador.
2.  Na Arduino IDE, vá no menu: **Sketch > Include Library > Add .ZIP Library...**
3.  Selecione o arquivo que você acabou de baixar.
    *   *A IDE irá mostrar uma mensagem "Library added to your libraries" no rodapé.*

### 3. Carregar o Código na Placa
Não é necessário escrever código do zero. A biblioteca já inclui exemplos prontos configurados para o seu sensor.
1.  Vá em **File > Examples**.
2.  Role até o final da lista, onde ficam as "Examples from Custom Libraries".
3.  Procure pela pasta com o nome do seu projeto (ex: `tcc-drone-edge-ai` ou o nome que você deu no Edge Impulse).
4.  Selecione: **nano_ble33_sense > nano_ble33_sense_accelerometer**.
    *   *Este exemplo já vem configurado para ler o IMU LSM9DS1 e rodar a inferência.*

### 4. Monitorar os Resultados
1.  Conecte o Arduino Nano 33 BLE ao PC via USB.
2.  Selecione a porta correta em **Tools > Port**.
3.  Clique no botão **Upload** (Seta para a direita) e aguarde a compilação.
4.  Após carregar, abra o **Serial Monitor** (Lupa no canto superior direito).
5.  Ajuste a velocidade (baud rate) para **115200**.
    *   *Você verá as probabilidades de cada classe aparecendo em tempo real.*
