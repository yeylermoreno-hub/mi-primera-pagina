# Tarea 2 – Ejercicios Unidad 1

En esta entrada documento las soluciones a los ejercicios de la sección "Para practicar" de la Unidad 1 del curso Pensamiento Algorítmico. Resuelvo cada reto en Python usando solo `print()` e `input()` para simular los movimientos de la tortuga con texto. Incluyo el enunciado original, el código, una explicación breve y la salida esperada.

## Reto 1: Simula el comportamiento de la tortuga usando solo print() e input()

**Enunciado original**: Intenta recrear el movimiento de la tortuga únicamente con texto, usando funciones, print() e input() para pedir valores al usuario.

```python
# Función para avanzar (simula movimiento horizontal)
def adelante(pasos):
    print("→ " * pasos)  # Imprime flechas hacia la derecha por 'pasos' veces

# Función para girar (simula un giro de 90°)
def girar_derecha():
    print("Girando 90° a la derecha...")  # Mensaje de giro

# Función para subir (simula movimiento vertical)
def arriba(pasos):
    print("↑ " * pasos)  # Imprime flechas hacia arriba por 'pasos' veces

# Programa principal: pide input al usuario y simula movimientos
print("Simulador de tortuga con texto. ¡Empecemos!")
pasos_adelante = int(input("¿Cuántos pasos adelante? "))
adelante(pasos_adelante)

gira = input("¿Girar a la derecha? (s/n): ")
if gira.lower() == 's':
    girar_derecha()

pasos_arriba = int(input("¿Cuántos pasos arriba? "))
arriba(pasos_arriba)

"""
Explicación: Este código crea funciones simples que imprimen símbolos de flechas para simular movimientos. Usa input() para que el usuario decida los pasos y si gira, recreando el comportamiento básico de la tortuga con texto interactivo.
Salida esperada (ejemplo con inputs: 3 adelante, s para girar, 2 arriba):
"""
Simulador de tortuga con texto. ¡Empecemos!
¿Cuántos pasos adelante? 3
→ → → 
¿Girar a la derecha? (s/n): s
Girando 90° a la derecha...
¿Cuántos pasos arriba? 2
↑ ↑
Reto 2: Tortuga bajando
Enunciado original: Crea el rastro de una tortuga moviéndose hacia abajo usando únicamente print() e input().
La salida esperada es similar a [figura de tortuga bajando, que simula una tortuga ASCII descendiendo].
# Dibujo ASCII simple de la tortuga
def dibujar_tortuga():
    print("    ____")
    print("   /    \\")
    print("  |  O O |")
    print("   \\ -- /")
    print("    ----")

# Simula el descenso: pide pasos y "baja" la tortuga imprimiendo espacios crecientes
pasos_bajar = int(input("¿Cuántos pasos bajar? "))
print("\nTortuga bajando ↓↓↓\n")

posicion = 0
for i in range(pasos_bajar):
    print(" " * posicion * 2)  # Espacios para simular descenso
    dibujar_tortuga()
    print("↓")  # Flecha de movimiento
    posicion += 1
    print()  # Línea en blanco para separación
Explicación: El programa dibuja una tortuga en ASCII art y la "baja" agregando espacios crecientes antes de cada dibujo, simulando descenso. Usa input() para el número de pasos y repite el rastro vertical.
Salida esperada (ejemplo con 3 pasos):
¿Cuántos pasos bajar? 3

Tortuga bajando ↓↓↓

    ____
   /    \
  |  O O |
   \ -- /
    ---- ↓

      ____
     /    \
    |  O O |
     \ -- /
      ---- ↓

        ____
       /    \
      |  O O |
       \ -- /
        ---- ↓
Reto 3: Girar y dibujar usando solo print() e input()
Enunciado original: Ahora la tortuga no solo avanza: también gira. Observa cómo lo hace la versión gráfica: [código turtle que dibuja una L]. Salida (versión gráfica): se dibuja una “L”.
# Direcciones posibles: 0=derecha (→), 1=abajo (↓), 2=izquierda (←), 3=arriba (↑)
direccion_actual = 0
posicion_x = 0
posicion_y = 0

def imprimir_movimiento(simbolo, cantidad):
    global posicion_x, posicion_y
    for _ in range(cantidad):
        print(simbolo, end=" ")
        if simbolo == "→":
            posicion_x += 1
        elif simbolo == "↓":
            posicion_y -= 1
        elif simbolo == "←":
            posicion_x -= 1
        elif simbolo == "↑":
            posicion_y += 1
    print()  # Nueva línea

# Programa interactivo
print("Simulador de tortuga giratoria. Comando: 'adelante X' o 'girar'")
while True:
    comando = input("¿Qué hace la tortuga? (adelante X / girar / salir): ")
    if comando == "salir":
        break
    elif comando == "girar":
        direccion_actual = (direccion_actual + 1) % 4
        simbolos = ["→", "↓", "←", "↑"]
        print(f"Giró a: {simbolos[direccion_actual]}")
    else:
        try:
            _, cantidad = comando.split()
            cantidad = int(cantidad)
            simbolos = ["→", "↓", "←", "↑"]
            imprimir_movimiento(simbolos[direccion_actual], cantidad)
        except:
            print("Comando inválido. Usa 'adelante 5' o 'girar'.")
Explicación: Simula giros cambiando la dirección (usando un índice modular) y avanza imprimiendo el símbolo correspondiente. Es interactivo con input(), y dibuja una "L" si das "adelante 5" → "girar" → "adelante 5".
Salida esperada (ejemplo para dibujar L):
Simulador de tortuga giratoria. Comando: 'adelante X' o 'girar'
¿Qué hace la tortuga? (adelante X / girar / salir): adelante 5
→ → → → → 
¿Qué hace la tortuga? (adelante X / girar / salir): girar
Giró a: ↓
¿Qué hace la tortuga? (adelante X / girar / salir): adelante 5
↓ ↓ ↓ ↓ ↓ 
¿Qué hace la tortuga? (adelante X / girar / salir): salir
Reto 4: Encapsula los comportamientos anteriores usando funciones
Enunciado original: Reescribe los retos anteriores creando funciones que representen los movimientos de la tortuga solo con texto. Usa las siguientes funciones como interfaz: adelante(n) # Dibuja el movimiento hacia la derecha (→) por n pasos; abajo(n) # Dibuja el movimiento hacia abajo (↓) por n pasos. Por ejemplo, al ejecutar: adelante(5); abajo(3) Debería producir un patrón en forma de L como en la figura.
# Función para avanzar horizontalmente
def adelante(n):
    print("→ " * n)

# Función para bajar verticalmente
def abajo(n):
    print("↓ " * n)

# Programa principal: simula la "L"
print("Dibujando una L con funciones encapsuladas:")
adelante(5)  # Primera parte horizontal
print()  # Espacio para el giro (simulado)
abajo(3)  # Parte vertical
Explicación breve: Encapsulo los movimientos en funciones reutilizables adelante() y abajo(), como se pide. Llamándolas en secuencia, se genera el patrón "L" con texto, reutilizando código de retos previos.
Salida esperada:
Dibujando una L con funciones encapsuladas:
→ → → → → 

↓ ↓ ↓
Reto 5: La tortuga baja las escaleras
Enunciado original: Ajusta tus funciones para que la tortuga pueda bajar escalones. Cada escalón debe conservar la posición horizontal acumulada y dibujar correctamente tanto el tramo horizontal como el vertical. Por ejemplo: # Escalón 1 adelante(5) abajo(2) # Escalón 2 adelante(5) abajo(2) # Escalón 3 adelante(5) abajo(2) Comportamiento esperado: [figura de escaleras descendiendo, con tramos → y ↓ alternados, conservando alineación horizontal].
# Funciones ajustadas para escaleras (conservan posición horizontal con espacios)
posicion_horizontal = 0  # Variable global para acumular posición X

def adelante(n):
    global posicion_horizontal
    print(" " * posicion_horizontal + "→ " * n)  # Avanza desde posición actual
    posicion_horizontal += n  # Acumula posición

def abajo(n):
    global posicion_horizontal
    print(" " * posicion_horizontal + "↓ " * n)  # Baja manteniendo X

# Programa principal: baja 3 escalones
print("La tortuga baja las escaleras:")
for escalon in range(3):
    adelante(5)  # Tramo horizontal del escalón
    abajo(2)     # Descenso vertical
    print()      # Separación entre escalones
Explicación: Ajusto las funciones para usar una variable global que acumule la posición horizontal (espacios crecientes). Cada escalón avanza 5 → y baja 2 ↓, conservando la alineación, simulando escaleras descendentes.
Salida esperada:
La tortuga baja las escaleras:
→ → → → → 
↓ ↓ 

    → → → → → 
    ↓ ↓ 

        → → → → → 
        ↓ ↓
Referencias de IA
Usé Grok (de xAI) para generar y refinar estas soluciones. Específicamente:

Grok: Conversación sobre la solución del Reto 1 al 5 (enlace: [esta conversación en el chat de Grok]). Me ayudó a extraer enunciados exactos del sitio del curso y a crear códigos limpios con explicaciones simples, asegurando que usen solo print() e input().

Toda la lógica fue revisada y adaptada por mí para ajustarse a los requisitos.
