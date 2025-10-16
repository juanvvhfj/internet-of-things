# internet-of-things
🌡️ Proyecto: Sensor de Temperatura con LCD, LED y Motor (Arduino UNO)
🧩 Descripción del Proyecto

Este proyecto utiliza un sensor de temperatura TMP36 conectado a un Arduino UNO para medir la temperatura ambiente.
El valor obtenido se muestra en una pantalla LCD 16x2, y se controlan un LED y un motor (ventilador) dependiendo de la temperatura detectada.

⚙️ Componentes Utilizados

Arduino UNO

Sensor de temperatura TMP36

Pantalla LCD 16x2 (modo 4 bits)

Potenciómetro (para ajustar contraste del LCD)

LED con resistencia de 220 Ω

Motor DC o ventilador

Transistor y diodo de protección (para el motor)

Protoboard y cables jumper

🔌 Conexiones Principales
Componente	Pin Arduino	Descripción
TMP36	A0	Entrada analógica de temperatura
LED	D8	Indica temperatura baja/alta
Motor	D9	Activado con señal digital
LCD RS	D7	Control LCD
LCD EN	D6	Control LCD
LCD D4	D5	Datos LCD
LCD D5	D4	Datos LCD
LCD D6	D3	Datos LCD
LCD D7	D2	Datos LCD
Potenciómetro	VCC / GND / VO	Ajuste de contraste
🧠 Lógica del Programa

El programa lee la temperatura del TMP36, la convierte a grados Celsius y ejecuta validaciones según el rango:

Temperatura ≤ 10 °C:

LED parpadea cada 0.5 segundos.

Motor apagado.

Temperatura entre 11 °C y 25 °C:

LED apagado.

Motor apagado.

Temperatura ≥ 26 °C:

LED encendido fijo.

Motor encendido.

💻 Fragmento del Código Principal (void loop())
void loop() {
  int lectura = analogRead(A0);
  float voltaje = lectura * (5.0 / 1023.0);
  float temperatura = (voltaje - 0.5) * 100; // Conversión TMP36

  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperatura);
  lcd.print((char)223);
  lcd.print("C");

  if (temperatura <= 10) {
    digitalWrite(9, LOW); // Motor OFF
    digitalWrite(8, HIGH);
    delay(500);
    digitalWrite(8, LOW);
    delay(500);
    lcd.setCursor(0, 1);
    lcd.print("FRIO: Motor OFF  ");
  } 
  else if (temperatura >= 11 && temperatura <= 25) {
    digitalWrite(8, LOW);
    digitalWrite(9, LOW);
    lcd.setCursor(0, 1);
    lcd.print("NORMAL: Motor OFF");
  } 
  else if (temperatura >= 26) {
    digitalWrite(8, HIGH);
    digitalWrite(9, HIGH);
    lcd.setCursor(0, 1);
    lcd.print("CALOR: Motor ON  ");
  }
}

🧾 Archivos del Proyecto

temp_lcd.ino → Código fuente principal.

README.md → Documento informativo del proyecto.

Captura_circuito.png → Diagrama de conexión (ver imagen adjunta).

🚀 Instrucciones para Subir el Proyecto a GitHub

Abre la carpeta del proyecto en VSCode o Arduino IDE.

Crea el repositorio local:

git init
git add .
git commit -m "Versión inicial del proyecto temp_lcd"


Crea el repositorio en GitHub llamado temp_lcd.

Conecta el repositorio local con el remoto:

git remote add origin https://github.com/tuusuario/temp_lcd.git
git push -u origin main

👨‍💻 Autor

Juan Fernando
Curso de Electrónica / Arduino – 2025
