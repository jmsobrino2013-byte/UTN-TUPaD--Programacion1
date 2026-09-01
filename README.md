# Subo ejercicios de Unidad 3

#__________________Ejercicio 1: Caja de kiosco___________________

#Pedir nombre del cliente
nombre = input("Ingrese el nombre del cliente: ").strip()
while not nombre.isalpha():
    print("Error: El nombre solo debe contener letras y no puede estar vacío.")
    nombre = input("Ingrese el nombre del cliente: ").strip()

#Pedir cantidad de productos
cantidad_str = input("Ingrese la cantidad de productos a comprar: ").strip()
while not cantidad_str.isdigit() or int(cantidad_str) <= 0:
    print("Error: Debe ingresar un número entero mayor a 0.")
    cantidad_str = input("Ingrese la cantidad de productos a comprar: ").strip()

cantidad = int(cantidad_str)

# Totales
total_sin_descuento = 0.0
total_con_descuento = 0.0

# 3. Iterar por cada producto
for i in range(1, cantidad + 1):
    # Pedir precio del producto
    precio_str = input(f"Ingrese el precio del producto {i} (entero): ").strip()
    while not precio_str.isdigit():
        print("Error: El precio debe ser un número entero válido.")
        precio_str = input(f"Ingrese el precio del producto {i} (entero): ").strip()
    
    precio = float(precio_str) #se pasa de str a float
    total_sin_descuento += precio

    # Pedir si tiene descuento S/N
    descuento_opcion = input(f"¿El producto {i} tiene descuento? (S/N): ").strip().lower()
    while descuento_opcion != 's' and descuento_opcion != 'n':
        print("Error: Debe ingresar 'S' o 'N'.")
        descuento_opcion = input(f"¿El producto {i} tiene descuento? (S/N): ").strip().lower()

    # Aplicar descuento si corresponde (10%)
    if descuento_opcion == 's':
        precio_con_desc = precio * 0.90
    else:
        precio_con_desc = precio
        
    total_con_descuento += precio_con_desc

#Se calculan los totales y el promedio
ahorro_total = total_sin_descuento - total_con_descuento
promedio_producto = total_con_descuento / cantidad

# Resultados
print("\n--- RESUMEN DE COMPRA ---")
print(f"Cliente: {nombre}")
print(f"Total sin descuentos: ${total_sin_descuento:.2f}")
print(f"Total con descuentos: ${total_con_descuento:.2f}")
print(f"Ahorro total: ${ahorro_total:.2f}")
print(f"Promedio por producto: ${promedio_producto:.2f}")


#__________________Ejercicio 2: Acceso al campus y menu seguro__________________

# Variables fijas
USUARIO_CORRECTO = "alumno"
CLAVE_CORRECTA = "python123"

# Intentos disponibles para entrar.
intentos_restantes = 3
login_exitoso = False

print("--- BIENVENIDO AL CAMPUS VIRTUAL ---")

while intentos_restantes > 0 and not login_exitoso:
    usuario_ingresado = input("Ingrese su usuario: ")
    clave_ingresada = input("Ingrese su clave: ")

    if usuario_ingresado == USUARIO_CORRECTO and clave_ingresada == CLAVE_CORRECTA:
        login_exitoso = True
        print("¡Ingreso exitoso al sistema!")
    else:
        intentos_restantes -= 1
        if intentos_restantes > 0:
            print(f"Credenciales invalidas. Le quedan {intentos_restantes} intentos.")
        else:
            print("\n¡ALERTA! Cuenta bloqueada por seguridad.")

# Menu de acciones, en caso de que el usuario sea correcto
while login_exitoso:
    print("\n==============================")
    print("        MENÚ PRINCIPAL        ")
    print("==============================")
    print("1. Ver estado de inscripción")
    print("2. Cambiar clave")
    print("3. Mostrar mensaje motivacional")
    print("4. Salir")
    print("==============================")

    opcion = input("Seleccione una de las opciones anteriores: ")

    # Validación de las opciones del menu.
    while not opcion.isdigit() or not ("1" <= opcion <= "4"):
        print("Error: Opción fuera de rango. Ingrese un número del 1 al 4.")
        opcion = input("Seleccione una opción (1-4): ")
    
    # Ejecución de las opciones.
    if opcion == "1":
        print("\n[ESTADO]: Inscripto")
    
    elif opcion == "2":
        print("\n--- CAMBIO DE CLAVE ---")
        nueva_clave = input("Ingrese su nueva clave (mínimo 6 caracteres): ")
    
        # Validar largo de la clave
        while len(nueva_clave) < 6:
            print("Error: La clave es muy corta. Debe tener al menos 6 caracteres.")
            nueva_clave = input("Ingrese su nueva clave: ")
        
        confirmacion = input("Confirme su nueva clave: ")
    
        # Validacion para que coincidan las contraseñas.
        if nueva_clave == confirmacion:
            CLAVE_CORRECTA = nueva_clave  # Se actualiza la clave en memoria
            print("¡Clave cambiada con éxito!")
        else:
            print("Error: Las claves no coinciden. No se realizó el cambio.")
        
    elif opcion == "3":
        print("[MOTIVACIÓN]: 'La practica hace al maestro. ¡Seguí adelante!'")
    
    elif opcion == "4":
        print("Gracias por usar el Campus. ¡Hasta luego!")
        break # Se termina el programa.


#_____________EJERCICIO 3 - AGENDA DE TURNOS_____________

# Datos y variales iniciales
nombre_operador = input("Ingrese el nombre del operador: ")
while not nombre_operador.isalpha():
    print("Error: El nombre debe contener solo letras.")
    nombre_operador = input("Ingrese el nombre del operador: ")

# Turnos de Lunes (4 cupos y vacíos al inicio)
lunes1, lunes2, lunes3, lunes4 = "", "", "", ""
# Turnos de Martes (3 cupos, vacíos al inicio)
martes1, martes2, martes3 = "", "", ""

# Bucle principal del sistema
while True:
    print("\n========================================")
    print(f"  SISTEMA DE TURNOS - OPERADOR: {nombre_operador.upper()}")
    print("========================================")
    print("1. Reservar turno")
    print("2. Cancelar turno")
    print("3. Ver agenda del día")
    print("4. Ver resumen general")
    print("5. Cerrar sistema")
    print("========================================")
    
    opcion = input("Seleccione una de las opciónes anteriores: ")
    while not opcion.isdigit() or not ("1" <= opcion <= "5"):
        print("Error: Opción inválida.")
        opcion = input("Seleccione una de las opciónes anteriores: ")

    # Cerrar sistema
    if opcion == "5":
        print("\nCerrando el sistema de turnos. ¡Buen día!")
        break

    # Reserva de turnos
    elif opcion == "1":
        print("\n--- RESERVAR TURNO ---")
        dia = input("Seleccione día (1=Lunes, 2=Martes): ")
        while dia != "1" and dia != "2":
            print("Error: Ingrese 1 o 2.")
            dia = input("Seleccione día (1=Lunes, 2=Martes): ")

        paciente = input("Nombre del paciente: ")
        while not paciente.isalpha():
            print("Error: Solo letras.")
            paciente = input("Nombre del paciente: ")

        if dia == "1":
        # Verificar repetido en Lunes
            if paciente in (lunes1, lunes2, lunes3, lunes4):
                print(f"Error: El paciente {paciente} ya tiene un turno asignado el Lunes.")
        # Asignar en el primer espacio libre
            elif lunes1 == "": lunes1 = paciente; print("Turno reservado: Lunes - Turno 1.")
            elif lunes2 == "": lunes2 = paciente; print("Turno reservado: Lunes - Turno 2.")
            elif lunes3 == "": lunes3 = paciente; print("Turno reservado: Lunes - Turno 3.")
            elif lunes4 == "": lunes4 = paciente; print("Turno reservado: Lunes - Turno 4.")
            else:
                print("Disculpe, no hay más cupos disponibles para el día Lunes.")
            
        elif dia == "2":
            # Verificar repetido en Martes
            if paciente in (martes1, martes2, martes3):
                print(f"Error: El paciente {paciente} ya tiene un turno asignado el Martes.")
            # Asignar en el primer espacio libre
            elif martes1 == "": martes1 = paciente; print("Turno reservado: Martes - Turno 1.")
            elif martes2 == "": martes2 = paciente; print("Turno reservado: Martes - Turno 2.")
            elif martes3 == "": martes3 = paciente; print("Turno reservado: Martes - Turno 3.")
            else:
                print("Disculpe, no hay más cupos disponibles para el día Martes.")

    # Cancelacion de turnos.
    elif opcion == "2":
        print("\n--- CANCELAR TURNO ---")
        dia = input("Seleccione día (1=Lunes, 2=Martes): ")
        while dia != "1" and dia != "2":
            print("Error: Ingrese 1 o 2.")
            dia = input("Seleccione día (1=Lunes, 2=Martes): ")
        
        paciente = input("Nombre del paciente a cancelar: ")
        encontrado = False
    
        if dia == "1":
            if lunes1 == paciente: lunes1 = ""; encontrado = True
            elif lunes2 == paciente: lunes2 = ""; encontrado = True
            elif lunes3 == paciente: lunes3 = ""; encontrado = True
            elif lunes4 == paciente: lunes4 = ""; encontrado = True
        elif dia == "2":
            if martes1 == paciente: martes1 = ""; encontrado = True
            elif martes2 == paciente: martes2 = ""; encontrado = True
            elif martes3 == paciente: martes3 = ""; encontrado = True
        
        if encontrado:
            print(f"El turno de {paciente} fue cancelado exitosamente.")
        else:
            print(f"No se encontró ningún paciente con el nombre '{paciente}' en ese día.")

    # Ver agenda del dia.
    elif opcion == "3":
        print("\n--- VER AGENDA ---")
        dia = input("Seleccione día (1=Lunes, 2=Martes): ")
        while dia != "1" and dia != "2":
            print("Error: Ingrese 1 o 2.")
            dia = input("Seleccione día (1=Lunes, 2=Martes): ")
        
        if dia == "1":
            print(f"\nAgenda del Lunes:")
            print(f"Turno 1: {lunes1 if lunes1 != '' else '(libre)'}")
            print(f"Turno 2: {lunes2 if lunes2 != '' else '(libre)'}")
            print(f"Turno 3: {lunes3 if lunes3 != '' else '(libre)'}")
            print(f"Turno 4: {lunes4 if lunes4 != '' else '(libre)'}")
        elif dia == "2":
            print(f"\nAgenda del Martes:")
            print(f"Turno 1: {martes1 if martes1 != '' else '(libre)'}")
            print(f"Turno 2: {martes2 if martes2 != '' else '(libre)'}")
            print(f"Turno 3: {martes3 if martes3 != '' else '(libre)'}")

    # Resumen general
    elif opcion == "4":
        print("\n--- RESUMEN GENERAL ---")
        # Contar Lunes
        nodisp_lunes = 0
        if lunes1 != "": nodisp_lunes += 1
        if lunes2 != "": nodisp_lunes += 1
        if lunes3 != "": nodisp_lunes += 1
        if lunes4 != "": nodisp_lunes += 1
        disp_lunes = 4 - nodisp_lunes
    
        # Contar Martes
        nodisp_martes = 0
        if martes1 != "": nodisp_martes += 1
        if martes2 != "": nodisp_martes += 1
        if martes3 != "": nodisp_martes += 1
        disp_mar = 3 - nodisp_martes
        disp_martes = 3 - nodisp_martes
    
        print(f"Lunes: Ocupados: {nodisp_lunes} | Disponibles: {disp_lunes}")
        print(f"Martes: Ocupados: {nodisp_martes} | Disponibles: {disp_martes}")
    
        # Determinar el día con más turnos
        if nodisp_lunes > nodisp_martes:
            print("Día con más turnos ocupados: Lunes")
        elif nodisp_martes > nodisp_lunes:
            print("Día con más turnos ocupados: Martes")
        else:
            print("Día con más turnos ocupados: Empate entre Lunes y Martes")


#_____________________EJERCICIO 4: ESCAPE ROOM: LA BOVEDA____________________

# Variables iniciales
energia = 100
tiempo = 12
cerraduras_abiertas = 0
alarma = False
codigo_parcial = ""

# Contador interno para la regla anti-spam
racha_forzar = 0

print("=== BIENVENIDO A ESCAPE ROOM: LA BÓVEDA ===")

# Validación obligatoria del nombre del agente
nombre_valido = False
while not nombre_valido:
    nombre_agente = input("Ingrese el nombre del agente (solo letras): ")
    if nombre_agente.isalpha():
        nombre_valido = True
    else:
        print("Error: El nombre debe contener únicamente letras.")

print(f"\nAgente {nombre_agente}, la misión ha comenzado. ¡Buena suerte!\n")

# Bucle principal del juego
# Continúa mientras haya recursos, falten cerraduras y no esté bloqueado por alarma
juego_activo = True

while juego_activo:
    # Mostrar estado actual
    print("-" * 50)
    print(f"ESTADO DEL AGENTE: {nombre_agente.upper()}")
    print(f"Energía: {energia} | Tiempo: {tiempo} h | Cerraduras Abiertas: {cerraduras_abiertas}/3")
    print(f"Alarma: {'ACTIVA' if alarma else 'APAGADA'} | Código Parcial: '{codigo_parcial}'")
    print("-" * 50)

    # REGLA DE BLOQUEO POR ALARMA
    # Si la alarma está encendida y queda poco tiempo, el sistema se bloquea de inmediato
    if alarma and tiempo <= 3 and cerraduras_abiertas < 3:
        print("\n ¡EL SISTEMA SE HA BLOQUEADO POR ALARMA! No pudiste abrir la bóveda a tiempo.")
        juego_activo = False
        break

    # Mostrar menú de acciones
    print("MENÚ DE ACCIONES:")
    print("1. Forzar cerradura (Costo: -20 energía, -2 tiempo)")
    print("2. Hackear panel (Costo: -10 energía, -3 tiempo)")
    print("3. Descansar (Costo: +15 energía, -1 tiempo)")
    
    # Validación de la opción elegida
    opcion_valida = False
    opcion = ""
    while not opcion_valida:
        opcion = input("Seleccione una opción (1-3): ")
        if opcion.isdigit():
            if opcion in ["1", "2", "3"]:
                opcion_valida = True
            else:
                print("Error: Opción fuera de rango (debe ser 1, 2 o 3).")
        else:
            print("Error: Debe ingresar un número entero.")

    # --- OPCIÓN 1: FORZAR CERRADURA ---
    if opcion == "1":
        # Descuento normal de recursos
        energia -= 20
        tiempo -= 2
        racha_forzar += 1  # Incrementa la racha anti-spam

        # Verificar regla anti-spam (3 veces seguidas)
        if racha_forzar == 3:
            print("\n¡REGLA ANTI-SPAM! La cerradura se trabó por forzarla repetidamente. Se activó la alarma.")
            alarma = True
            # No abre cerradura por penalización
        else:
            # Riesgo de alarma si la energía previa al coste (o actual) cae por debajo de 40
            if energia < 40:
                print("\n RIESGO DE ALARMA debido a tu baja energía.")
                
                # Pedir y validar número del 1 al 3
                num_valido = False
                num_elegido = ""
                while not num_valido:
                    num_elegido = input("Elija un número de la suerte (1-3): ")
                    if num_elegido.isdigit() and num_elegido in ["1", "2", "3"]:
                        num_valido = True
                    else:
                        print("Error: Debe elegir un número entero entre 1 y 3.")
                
                if num_elegido == "3":
                    print("¡Activaste los sensores! La alarma se ha encendido.")
                    alarma = True

            # Si no saltó la alarma en este turno, se abre la cerradura con éxito
            if not alarma:
                cerraduras_abiertas += 1
                print("\n ¡Éxito! Lograste forzar y abrir una cerradura.")

    # Hackeo del panel
    elif opcion == "2":
        # Descuento de recursos
        energia -= 10
        tiempo -= 3
        racha_forzar = 0  # Rompe la racha de forzar

        print("\nHackeando el sistema...")
        # For de 4 pasos mostrando progreso
        for paso in range(1, 5):
            print(f"Progreso: Paso {paso}/4...")
            codigo_parcial += "A"  # Suma una letra al código parcial

        # Verificar si se completa el código para abrir cerradura
        if len(codigo_parcial) >= 8:
            if cerraduras_abiertas < 3:
                cerraduras_abiertas += 1
                print("¡Código descifrado! Una cerradura se abrió automáticamente.")
            else:
                print("El código está completo, pero todas las cerraduras ya están abiertas.")

    # Descanso
    elif opcion == "3":
        racha_forzar = 0  # Rompe la racha de forzar
        
        # Costo base de tiempo
        tiempo -= 1
        
        # Recuperación de energía (máximo 100)
        energia += 15
        if energia > 100:
            energia = 100
            
        print("\n Te tomás un momento para descansar y recuperar fuerzas.")

        # Penalización extra si la alarma está encendida
        if alarma:
            energia -= 10
            print("¡El estrés de la alarma encendida te cuesta -10 de energía extra!")

    # VERIFICACIÓN DE CONDICIONES DE FIN DE JUEGO
    if cerraduras_abiertas >= 3:
        print("\n¡VICTORIA! Abriste las 3 cerraduras y lograste entrar.")
        juego_activo = False
    elif energia <= 0:
        print("\nDERROTA: Te quedaste sin energía.")
        juego_activo = False
    elif tiempo <= 0:
        print("\nDERROTA: Se te termino el tiempo.")
        juego_activo = False


#_________________EJERCICIO 5: LA ARENA DEL GLADIADOR________________

print("=== BIENVENIDO A LA ARENA DEL GLADIADOR ===")

# 1: CONFIGURACIÓN DEL PERSONAJE

nombre_valido = False
nombre_jugador = ""

while not nombre_valido:
    nombre_jugador = input("Ingrese el nombre de su Gladiador (solo letras): ")
    if nombre_jugador.isalpha():
        nombre_valido = True
    else:
        print("Error: Solo se permiten letras.")

print(f"\n¡El Gladiador {nombre_jugador} ha ingresado a la arena!\n")

# PASO 2: INICIALIZACIÓN DE ESTADÍSTICAS

# Variables tipo INT (Enteros)
vida_jugador = 100
vida_enemigo = 100
pociones_vida = 3
ataque_pesado_base = 15
daño_enemigo_base = 12

# Variable tipo BOOLEAN (Booleano) para control de turnos
turno_gladiador = True

# Variable tipo FLOAT (Decimal) para el cálculo de multiplicador crítico
multiplicador_critico = 1.5

# PASO 3: EL CICLO DE COMBATE

# El juego sigue activo mientras ambos tengan más de 0 puntos de vida
while vida_jugador > 0 and vida_enemigo > 0:
    
    if turno_gladiador:
        # Mostrar estado de la batalla
        print("-" * 50)
        print(f"ESTADO ACTUAL:")
        print(f"Gladiador {nombre_jugador}: HP {vida_jugador} | Pociones: {pociones_vida}")
        print(f"Enemigo: HP {vida_enemigo}")
        print("-" * 50)

        # Mostrar menú de opciones
        print("MENÚ DE ACCIONES:")
        print("1. Ataque Pesado")
        print("2. Ráfaga Veloz (Uso de bucle for)")
        print("3. Curar")

        # Validación del Menú con .isdigit() en un while
        opcion_valida = False
        opcion = ""
        while not opcion_valida:
            opcion = input("Seleccione una opción (1-3): ")
            if opcion.isdigit():
                if opcion in ["1", "2", "3"]:
                    opcion_valida = True
                else:
                    print("Error: El número debe ser 1, 2 o 3.")
            else:
                print("Error: Debe ingresar un número entero.")

        # LÓGICA DE LAS ACCIONES DEL JUGADOR
        
        # Acción A: Ataque Pesado (Opción 1)
        if opcion == "1":
            # Si la vida del enemigo es menor a 20 puntos, se aplica golpe crítico
            if vida_enemigo < 20:
                daño_final = ataque_pesado_base * multiplicador_critico  # Resultado float
                print(f"\n¡GOLPE CRÍTICO! Multiplicador x{multiplicador_critico} activado.")
            else:
                daño_final = float(ataque_pesado_base)  # Forzado a float para consistencia técnica

            # Reducir vida al enemigo
            vida_enemigo -= int(daño_final)
            print(f"¡Atacaste al enemigo por {daño_final} puntos de daño!")

        # Acción B: Ráfaga Veloz (Opción 2)
        elif opcion == "2":
            print("\nLanzando Ráfaga Veloz...")
            # Bucle for obligatorio que se repite 3 veces usando range
            for golpe in range(1, 4):
                vida_enemigo -= 5
                print(" > Golpe conectado por 5 de daño")

        # Acción C: Curar (Opción 3)
        elif opcion == "3":
            if pociones_vida > 0:
                vida_jugador += 30
                # Evitamos que la curación exceda el límite máximo inicial de 100 de HP
                if vida_jugador > 100:
                    vida_jugador = 100
                pociones_vida -= 1
                print(f"\nTe has curado. Tu vida actual es de {vida_jugador} HP.")
            else:
                print("\n¡No quedan pociones!")
                print("¡Perdiste el turno por buscar una poción vacía!")

        # Cambiar el turno al enemigo de inmediato
        turno_gladiador = False

    else:
        # TURNO DEL ENEMIGO (Se ejecuta de forma automática tras el turno del jugador)
        # Solo ataca si no ha muerto por la acción previa del jugador
        if vida_enemigo > 0:
            vida_jugador -= daño_enemigo_base
            print(f"\n¡El enemigo te atacó por {daño_enemigo_base} puntos de daño!")
        
        # Devolver el turno al jugador
        turno_gladiador = True

# PASO 4: FIN DEL JUEGO
print("\n______ FIN DEL COMBATE______")
if vida_jugador > 0:
    print(f"¡VICTORIA! {nombre_jugador} ha ganado la batalla.")
else:
    print("DERROTA. Has caído en combate.")
print("______________________________")