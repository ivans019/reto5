### trabajo programacion reto 5
## diagrama de flujo menu principal 
![imagen](imagenes/menup.png)


## diagrama de flujo de funciones 


# funcion guardado
![imagen](imagenes/grafica.png)

# funcion explorar
![imagen](imagenes/explorar.png)

# funcion analisis texto
![imagen](imagenes/topp.png)

# funcion menu TXT
![imagen](imagenes/txt.png)

# funcion encabezados
![imagen](imagenes/encabezados.png)

# funcion CSV
![imagen](imagenes/csv.png)




### código completo del reto 5


import os
import csv
import matplotlib.pyplot as plt


def guardar(defecto):
    if not os.path.exists("outputs"):
        os.makedirs("outputs")
    nombre = input(f"Nombre imagen (Enter para {defecto}): ")
    if nombre == "":
        nombre = defecto
    if not nombre.endswith(".png") and not nombre.endswith(".jpg"):
        nombre = nombre + ".png"
    ruta = "outputs/" + nombre
    plt.savefig(ruta)
    print(f"Guardado en: {ruta}")
    plt.show()
    plt.close()


def explorar():
    ruta = input("\nCarpeta (Enter para '.'): ")
    if ruta == "":
        ruta = "."
    if os.path.isdir(ruta):
        for nombre in os.listdir(ruta):
            if nombre.endswith(".txt") or nombre.endswith(".csv"):
                print(nombre)
    else:
        print("Carpeta no válida.")


def top_palabras(lineas):
    conectores = ["de", "la", "que", "el", "en", "y", "a", "los", "del", "se", "las", "por", "un", "para", "con", "no", "una", "su", "al", "lo", "es"]
    conteo = {}
    for l in lineas:
        texto = l.lower()
        for p in texto.split():
            limpia = p.strip(".,;:!?\"'()[]-")
            if len(limpia) > 1 and not limpia.isdigit() and limpia not in conectores:
                if limpia in conteo:
                    conteo[limpia] = conteo[limpia] + 1
                else:
                    conteo[limpia] = 1

    palabras = list(conteo.keys())
    cantidades = list(conteo.values())
    top_p = []
    top_c = []
    vueltas = min(5, len(palabras))

    for i in range(vueltas):
        mayor = max(cantidades)
        pos = cantidades.index(mayor)
        top_p.append(palabras[pos])
        top_c.append(mayor)
        cantidades[pos] = -1

    return top_p, top_c
