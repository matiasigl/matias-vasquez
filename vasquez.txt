from os import system
import random
import csv

trabajadores = ["Juan Perez", "Maria Garcia", "Carlos Lopez", "Ana Martinez", "Pedro Rodriguez", "Laura hernandez", "Miguel Sanchez", "Isabel Gomeez", "Francisco Diaz", "Elena Fernadez"]
sueldos = {}

def asignar_sueldos_aleatorio(trabajadores):
    sueldos = {trabajador: random.randint(300000, 2500000) for trabajador in trabajadores}
    print("Sueldos aleatorios asignados: ")
    for trabajador, sueldo in sueldos.items():
        print(f"{trabajador}: {sueldo}")
    return sueldos

def clasificar_sueldos(trabajadores):
    clasificacion = {"menores a $800000": [], "Entre 800000 y 2000000": [], "Superior a $2000000": []}

    for trabajador, sueldo in sueldos.items():
        if sueldo < 8000000:
            clasificacion["menores a $800000"].append((trabajador, sueldo))
        elif sueldo < 2000000:
            clasificacion["Entre 800000 y 2000000"].append((trabajador, sueldo))
        else:
            clasificacion["Superior a $2000000"].append((trabajador, sueldo))

    print("Clasificacion de sueldos: ")
    for categoria, empleados in clasificacion.items():
        print(f"{categoria} - total: {len(empleados)}")
        for trabajador, sueldo in empleados:
            print(f"{trabajador}: {sueldo}")
        print()

    print(f"total sueldos: {sum(sueldos.values())}")

def ver_estadistica(sueldos):
    sueldo_mas_alto = max(sueldos.values())
    print(f"sueldo mas alto: {sueldo_mas_alto}")
    
    sueldo_mas_bajo = min(sueldos.values())
    print(f"sueldo mas bajo: {sueldo_mas_bajo}")

    promedio_sueldos = round(sum(sueldos.values()) / len(sueldos), 2)
    print(f"sueldo mas bajo: {promedio_sueldos}")

    producto_sueldos = 1
    for sueldo in sueldos.values():
        producto_sueldos *= sueldo
    media_geometrica = round(producto_sueldos ** (1.0 / len(sueldos)), 2)
    print(f"media geometrica: {media_geometrica}")

def reporte_sueldos(sueldos):
    with open('sueldso.csv', 'w', newline='')as archivo_csv:
        escritor_csv = csv.writer(archivo_csv, delimiter=";")
        escritor_csv.writerow(['nombre empleado','sueldo base', 'descuento salud', 'descuento afp', 'sueldo liquido'])

        for trabajdor, sueldo in sueldos.items():
            descuento_salud = round(sueldo * 0,7)
            descuento_afp = round(sueldo * 0,12)
            sueldo_liquido = round(sueldo - descuento_salud - descuento_afp)

            escritor_csv.writerow([trabajdor, round(sueldo, 2 ), descuento_salud, descuento_afp, sueldo_liquido])

def menu():
    salir = False
    sueldos = ()

    while not salir:
        print("Menu")
        print("1 asignar sueldso aleatorios")
        print("2 clasificar sueldos")
        print("3 ver estadisticas")
        print("4 reporte de sueldos")
        print("5 Salir")

        opcion = input("ingrese una opcion: ")

        if opcion == "1":
            sueldos = asignar_sueldos_aleatorio(trabajadores)
        elif opcion == "2":
            if sueldos:
                clasificar_sueldos(sueldos)
            else:
                print("Debe asignar sueldos aleatorios primeramente")
        elif opcion == "3":
            if sueldos:
                ver_estadistica(sueldos)
            else:
                print("Debe asignar sueldos aleatorios primeramente")
        elif opcion == "4":
            if sueldos:
                reporte_sueldos(sueldos)
            else:
                print("Debe asignar sueldos aleatorios primeramente")
        elif opcion == "5":
            salir = True
            print("finalizando el programa")
            print("Desarrollado por Matias Vasquez")
            print("Rut 21.846.652-4")
            exit()
        else:
            print("opcion invalida")

menu()