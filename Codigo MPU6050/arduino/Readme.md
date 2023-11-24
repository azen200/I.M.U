Para calcular el ángulo de inclinación utilizando un MPU6050 con Arduino, puedes usar la biblioteca "Wire" para la comunicación I2C y la biblioteca "MPU6050" para facilitar la lectura de datos del sensor. Aquí hay un ejemplo básico de un programa en Arduino para calcular el ángulo de inclinación:

#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;

void setup() {
  Serial.begin(9600);

  // Inicializar el sensor MPU6050
  mpu.initialize();
  
  // Inicializar la comunicación serial
  Serial.println("Iniciando MPU6050...");
  delay(1000);
}

void loop() {
  // Obtener datos del acelerómetro
  int16_t accelerometerX = mpu.getAccelerationX();
  int16_t accelerometerY = mpu.getAccelerationY();
  int16_t accelerometerZ = mpu.getAccelerationZ();
  
  // Calcular el ángulo de inclinación
  float anguloInclinacion = calcularAnguloInclinacion(accelerometerX, accelerometerY, accelerometerZ);

  // Imprimir el ángulo de inclinación
  Serial.print("Ángulo de inclinación: ");
  Serial.print(anguloInclinacion);
  Serial.println(" grados");

  // Esperar un breve periodo de tiempo antes de la siguiente lectura
  delay(100);
}

float calcularAnguloInclinacion(int16_t accelX, int16_t accelY, int16_t accelZ) {
  // Calcular el ángulo de inclinación usando datos de aceleración
  float anguloInclinacionRad = atan2(-accelX, sqrt(accelY * accelY + accelZ * accelZ));
  
  // Convertir el ángulo a grados
  float anguloInclinacionDeg = anguloInclinacionRad * 180.0 / M_PI;
  
  return anguloInclinacionDeg;
}
