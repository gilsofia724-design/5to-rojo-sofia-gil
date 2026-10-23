# 5to-rojo-sofia-gil
pensamiento computacional
https://teams.cloud.microsoft/l/message/19:193019a4-bce8-49a8-aae2-fa73b39a351f_b5d10735-0142-4ec7-9118-7ec8b0d324a4@unq.gbl.spaces/1792166653320?context=%7B%22contextType%22%3A%22chat%22%7D
https://teams.cloud.microsoft/l/message/19:193019a4-bce8-49a8-aae2-fa73b39a351f_b5d10735-0142-4ec7-9118-7ec8b0d324a4@unq.gbl.spaces/1792166673873?context=%7B%22contextType%22%3A%22chat%22%7D
1. Descomposición en subproblemas 

Llegada de estudiantes: Recepción física o digital del estudiante al ingresar al centro, registrando su hora de llegada exacta. 

Registro y clasificación: Identificación del trámite requerido (entrega de documentos, solicitud de constancia, consulta general) y etiquetado de casos prioritarios. 

Gestión de prioridades y cola: Ordenamiento dinámico de los turnos en una estructura de datos que combine el orden estricto de llegada (FIFO) con excepciones de prioridad. 

Atención en ventanilla: Asignación del turno actual a la única ventanilla disponible, procesamiento del trámite y registro del tiempo de atención. 

Cierre y estadísticas: Finalización de la jornada, cálculo de tiempos promedio de espera y generación de reportes de eficiencia. 

2. Datos para representar a un estudiante 

idEstudiante: Identificador único (cédula, pasaporte o código de matrícula). 

nombre: Nombre y apellido del estudiante. 

tipoTramite: Categoría del trámite (1: Entrega de documentos, 2: Solicitud de constancia, 3: Consulta general). 

horaLlegada: Marca de tiempo (timestamp) que registra el momento exacto en que obtuvo su turno. 

esPrioritario: Variable booleana (Verdadero / Falso) para casos especiales (embarazadas, adultos mayores, urgencias institucionales). 

estado: Estado actual en el sistema (Esperando, En atención, Atendido). 

3. Algoritmo en pseudocódigo 

Plaintext 

Inicio 
    Definir Cola_Espera como Cola con Prioridad 
    Mientras la jornada esté activa Hacer 
        Si llega un nuevo estudiante Entonces 
            Leer nombre, idEstudiante, tipoTramite, esPrioritario 
            horaLlegada = ObtenerHoraActual() 
            Crear objeto Estudiante 
             
            Si esPrioritario == Verdadero Entonces 
                Insertar en Cola_Espera con Prioridad Alta 
            Sino 
                Insertar en Cola_Espera con Prioridad Normal (orden FIFO) 
            FinSi 
        FinSi 
 
        Si Ventanilla_Libre Y Cola_Espera no esté vacía Entonces 
            Estudiante_Actual = Siguiente de Cola_Espera 
            Marcar Estudiante_Actual.estado = "En atención" 
            Llamar a Ventanilla(Estudiante_Actual) 
            AtenderTrámite(Estudiante_Actual.tipoTramite) 
            Marcar Estudiante_Actual.estado = "Atendido" 
            RegistrarTiempoDeEspera(Estudiante_Actual) 
        FinSi 
    FinMientras 
    GenerarReporteDeTiempos() 
Fin 
4. Criterio de prioridad 

Criterio elegido: Prioridad mixta (Orden de llegada + Casos especiales + SJF optimizado para trámites rápidos). 

Por qué: Respetar estrictamente el orden de llegada garantiza justicia, pero ante una sola ventanilla, atender primero las consultas generales rápidas (siempre que no desplacen a los prioritarios legales) reduce el tiempo promedio global de espera sin vulnerar el orden general. Los casos prioritarios (salud, discapacidad, urgencias) siempre tienen precedencia absoluta por normativa institucional. 

Problema 2  

1.Representacion de paradas y distancia 

 

Considerando 6 paradas: 

Desde / Hacia 

P1 (Escuela) 

P2  

P3  

P4  

P5  

P6  

P1(Escuela) 

0 

2 km 

5 km 

7 km 

10 km 

12 km 

P3 

2 km 

0 

3 km 

6 km 

8 km 

10 km 

P3 

5 km 

3 km 

0 

2 km 

5 km 

7 km 

P4 

7 km 

6 km 

2 km 

0 

4 km 

6 km 

P5 

10 km 

8 km 

5 km 

4 km 

0 

3 km 

P6 

12 km 

10 km 

7 km 

6 km 

3 km 

0 

2. Algoritmo paso a paso (Vecino más cercano) 

Inicio: Partir de la Escuela y marcarla como visitada. 

Búsqueda: Desde la parada actual, identificar la parada no visitada que se encuentre a menor distancia. 

Desplazamiento: Moverse a dicha parada, registrarla en la secuencia y sumar la distancia. 

Iteración: Repetir los pasos 2 y 3 hasta que todas las paradas hayan sido recorridas. 

Retorno: Volver desde la última parada visitada hacia la Escuela ($P_1$). 

3. Aplicación del algoritmo (Ruta propuesta) 

Salida desde p1 p2(2 km) 

Desde p2 p3(3 km) 

Desde p3 p4(2 km) 

Desde p4 p5(4 km) 

Desde p5 p6(3 km) 

Retorno p6 p1(12 km) 

Distancia total: $2 + 3 + 2 + 4 + 3 + 12 = 26Km 

4. Comparación con otra alternativa 

Alternativa B (Ruta periférica directa): p1 p6 p5  p4 p3 p2 p1(12+3+4+2+3+2=26Km) 

Criterio de elección: Menor tiempo de espera acumulado para los primeros estudiantes. 

Por qué es mejor la Ruta Propuesta: Aunque la distancia total sea la misma, comenzar recogiendo a las paradas más cercanas a la escuela  evita que los estudiantes de esas paradas pasen demasiado tiempo arriba del autobús dando vueltas por toda la ciudad antes de llegar a clases. 

Problema 3 

1. Errores o limitaciones identificados 

Falta de cálculo real del promedio: El pseudocódigo suma las notas (nota1 + nota2 + nota3), pero nunca divide entre 3. Al evaluar una suma directa contra 60, el resultado es incorrecto. 

Ausencia de validación de entradas: No verifica si las notas ingresadas son válidas (pueden introducir números negativos o valores mayores a 100). 

Falta de retroactividad numérica: No muestra al usuario cuál fue el promedio obtenido ni contempla estados intermedios como la recuperación. 
2 y 3. Pseudocódigo corregido con validación de notas (0 a 100) 

Plaintext 

Inicio 
    Definir nota1, nota2, nota3, promedio como Real 
     
    // Validación de nota 1 
    Hacer 
        Escribir "Ingrese la nota 1 (0 a 100): " 
        Leer nota1 
        Si nota1 < 0 O nota1 > 100 Entonces 
            Escribir "Error: La nota debe estar entre 0 y 100." 
        FinSi 
    Mientras nota1 < 0 O nota1 > 100 
 
    // Validación de nota 2 
    Hacer 
        Escribir "Ingrese la nota 2 (0 a 100): " 
        Leer nota2 
        Si nota2 < 0 O nota2 > 100 Entonces 
            Escribir "Error: La nota debe estar entre 0 y 100." 
        FinSi 
    Mientras nota2 < 0 O nota2 > 100 
 
    // Validación de nota 3 
    Hacer 
        Escribir "Ingrese la nota 3 (0 a 100): " 
        Leer nota3 
        Si nota3 < 0 O nota3 > 100 Entonces 
            Escribir "Error: La nota debe estar entre 0 y 100." 
        FinSi 
  Mientras nota3 < 0 O nota3 > 100 
 
    // Cálculo correcto del promedio 
    promedio = (nota1 + nota2 + nota3) / 3 
 
    Escribir "El promedio final es: ", promedio 
 
    // Evaluación con estado de recuperación adicional 
    Si promedio >= 60 Entonces 
        Escribir "Estado: Aprueba" 
    Sino 
        Si promedio >= 40 Entonces 
            Escribir "Estado: Debe ir a recuperación" 
        Sino 
            Escribir "Estado: No aprueba" 
        FinSi 
    FinSi 
Fin 
 

4. Mejora adicional implementada 

Se añadió la opción de indicación de recuperación (para promedios entre 40 y 59.9) junto con la impresión en pantalla del valor numérico exacto del promedio obtenido, mejorando la experiencia de usuario y la utilidad del algoritmo. 

 
