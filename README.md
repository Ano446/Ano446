import time
import board
import busio
import adafruit_pca9685
from adafruit_motor import servo

# Configuração do PCA9685 para controlar os motores
i2c = busio.I2C(board.SCL, board.SDA)
pca = adafruit_pca9685.PCA9685(i2c)
pca.frequency = 60

# Criando objetos para os servos (motores)
motor_esquerdo = servo.Servo(pca.channels[0])
motor_direito = servo.Servo(pca.channels[1])

# Funções para controlar os motores
def mover_para_frente():
    motor_esquerdo.angle = 180  # Ajuste os ângulos de acordo com seus motores
    motor_direito.angle = 0

def mover_para_tras():
    motor_esquerdo.angle = 0
    motor_direito.angle = 180

def girar_esquerda():
    motor_esquerdo.angle = 0
    motor_direito.angle = 90

def girar_direita():
    motor_esquerdo.angle = 90
    motor_direito.angle = 0

# Loop principal
while True:
    # Leitura dos sensores (simulada neste exemplo)
    distancia_frente = 10  # Substitua por uma leitura real do sensor ultrassônico
    
    # Lógica de controle (simplificada)
    if distancia_frente < 15:
        girar_esquerda()
    else:
        mover_para_frente()
    
    time.sleep(0.1)

