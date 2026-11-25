---
layout: default
title: Aplicación de Búsqueda de Caminos al Grafo del Metro
parent: Tareas
grand_parent: Lógica Matemática y Matemáticas Discretas
nav_order: 8
---

# Aplicación de Búsqueda de Caminos al Grafo del Metro

```python
import matplotlib.pyplot as plt
import networkx as nx


# ============================================================
# DATOS DE LA RED DEL METRO
# ============================================================

metro_cdmx = {
    "Línea 1": [
        "Pantitlán", "Zaragoza", "Gómez Farías", "Boulevard Puerto Aéreo",
        "Balbuena", "Moctezuma", "San Lázaro", "Candelaria", "Merced",
        "Pino Suárez", "Isabel la Católica", "Salto del Agua", "Balderas",
        "Cuauhtémoc", "Insurgentes", "Sevilla", "Chapultepec", "Juanacatlán",
        "Tacubaya", "Observatorio"
    ],

    "Línea 2": [
        "Cuatro Caminos", "Panteones", "Tacuba", "Cuitláhuac", "Popotla",
        "Colegio Militar", "Normal", "San Cosme", "Revolución", "Hidalgo",
        "Bellas Artes", "Allende", "Zócalo/Tenochtitlan", "Pino Suárez",
        "San Antonio Abad", "Chabacano", "Viaducto", "Xola",
        "Villa de Cortés", "Nativitas", "Portales", "Ermita",
        "General Anaya", "Tasqueña"
    ],

    "Línea 3": [
        "Indios Verdes", "Deportivo 18 de Marzo", "Potrero", "La Raza",
        "Tlatelolco", "Guerrero", "Hidalgo", "Juárez", "Balderas",
        "Niños Héroes", "Hospital General", "Centro Médico",
        "Etiopía/Plaza de la Transparencia", "Eugenia",
        "División del Norte", "Zapata", "Coyoacán",
        "Viveros/Derechos Humanos", "Miguel Ángel de Quevedo",
        "Copilco", "Universidad"
    ],

    "Línea 4": [
        "Martín Carrera", "Talismán", "Bondojito", "Consulado",
        "Canal del Norte", "Morelos", "Candelaria", "Fray Servando",
        "Jamaica", "Santa Anita"
    ],

    "Línea 5": [
        "Pantitlán", "Hangares", "Terminal Aérea", "Oceanía", "Aragón",
        "Eduardo Molina", "Consulado", "Valle Gómez", "Misterios",
        "La Raza", "Autobuses del Norte", "Instituto del Petróleo",
        "Politécnico"
    ],

    "Línea 6": [
        "El Rosario", "Tezozómoc", "UAM-Azcapotzalco",
        "Ferrería/Arena Ciudad de México", "Norte 45", "Vallejo",
        "Instituto del Petróleo", "Lindavista",
        "Deportivo 18 de Marzo", "La Villa-Basílica",
        "Martín Carrera"
    ],

    "Línea 7": [
        "El Rosario", "Aquiles Serdán", "Camarones", "Refinería",
        "Tacuba", "San Joaquín", "Polanco", "Auditorio",
        "Constituyentes", "Tacubaya", "San Pedro de los Pinos",
        "San Antonio", "Mixcoac", "Barranca del Muerto"
    ],

    "Línea 8": [
        "Garibaldi/Lagunilla", "Bellas Artes", "San Juan de Letrán",
        "Salto del Agua", "Doctores", "Obrera", "Chabacano",
        "La Viga", "Santa Anita", "Coyuya", "Iztacalco", "Apatlaco",
        "Aculco", "Escuadrón 201", "Atlalilco", "Iztapalapa",
        "Cerro de la Estrella", "UAM-I", "Constitución de 1917"
    ],

    "Línea 9": [
        "Tacubaya", "Patriotismo", "Chilpancingo", "Centro Médico",
        "Lázaro Cárdenas", "Chabacano", "Jamaica", "Mixiuhca",
        "Velódromo", "Ciudad Deportiva", "Puebla", "Pantitlán"
    ],

    "Línea A": [
        "Pantitlán", "Agrícola Oriental", "Canal de San Juan",
        "Tepalcates", "Guelatao", "Peñón Viejo", "Acatitla",
        "Santa Marta", "Los Reyes", "La Paz"
    ],

    "Línea B": [
        "Buenavista", "Guerrero", "Garibaldi/Lagunilla", "Lagunilla",
        "Tepito", "Morelos", "San Lázaro", "Ricardo Flores Magón",
        "Romero Rubio", "Oceanía", "Deportivo Oceanía",
        "Bosque de Aragón", "Villa de Aragón", "Nezahualcóyotl",
        "Impulsora", "Río de los Remedios", "Múzquiz", "Ecatepec",
        "Olímpica", "Plaza Aragón", "Ciudad Azteca"
    ],

    "Línea 12": [
        "Mixcoac", "Insurgentes Sur", "Hospital 20 de Noviembre",
        "Zapata", "Parque de los Venados", "Eje Central", "Ermita",
        "Mexicaltzingo", "Atlalilco", "Culhuacán",
        "San Andrés Tomatlán", "Lomas Estrella", "Calle 11",
        "Periférico Oriente", "Tezonco", "Olivos", "Nopalera",
        "Zapotitlán", "Tlaltenco", "Tláhuac"
    ]
}


# ============================================================
# CREACIÓN DEL GRAFO
# ============================================================

# El grafo representa la red del Metro.
# Las estaciones son los nodos y las conexiones son las aristas.
G = nx.Graph()

# Conecta cada estación con la siguiente dentro de su línea.
for linea, estaciones in metro_cdmx.items():
    for i in range(len(estaciones) - 1):
        G.add_edge(
            estaciones[i],
            estaciones[i + 1],
            linea=linea,
            peso=1
        )


# ============================================================
# ENTRADA DE DATOS
# ============================================================

print("======================================")
print("   BUSCADOR DE RUTAS DEL METRO CDMX")
print("======================================")

origen = input("\nEstación de origen: ").strip()
destino = input("Estación de destino: ").strip()


# ============================================================
# BÚSQUEDA DEL CAMINO MÁS CORTO
# ============================================================

# Se verifica que las estaciones existan en el grafo.
if origen not in G:
    print(f'\nLa estación "{origen}" no existe.')

elif destino not in G:
    print(f'\nLa estación "{destino}" no existe.')

else:
    try:
        # Dijkstra encuentra la ruta con el menor número de tramos.
        ruta = nx.dijkstra_path(
            G,
            source=origen,
            target=destino,
            weight="peso"
        )

        print("\n========== MEJOR RUTA ==========")
        print(f"Origen: {origen}")
        print(f"Destino: {destino}")
        print(f"Estaciones recorridas: {len(ruta)}")
        print(f"Tramos recorridos: {len(ruta) - 1}")

        # Muestra el recorrido y la línea utilizada.
        print("\nRecorrido:")

        linea_anterior = None
        transbordos = 0

        for i in range(len(ruta) - 1):
            actual = ruta[i]
            siguiente = ruta[i + 1]
            linea_actual = G[actual][siguiente]["linea"]

            # Hay transbordo cuando cambia la línea.
            if linea_anterior is not None and linea_actual != linea_anterior:
                transbordos += 1
                print(f"\n--- Transbordo a {linea_actual} ---")

            print(f"{actual} -> {siguiente} ({linea_actual})")
            linea_anterior = linea_actual

        print(f"\nTransbordos: {transbordos}")


        # ====================================================
        # DIBUJO DE TODA LA RED Y LA RUTA ENCONTRADA
        # ====================================================

        # Colores de las líneas del Metro.
        colores_metro = {
            "Línea 1": "#F04E98",
            "Línea 2": "#005EB8",
            "Línea 3": "#AF9800",
            "Línea 4": "#6BBBAE",
            "Línea 5": "#FFD100",
            "Línea 6": "#DA291C",
            "Línea 7": "#E87722",
            "Línea 8": "#009A44",
            "Línea 9": "#512F2E",
            "Línea A": "#981D97",
            "Línea B": "#B1B3B3",
            "Línea 12": "#C99700"
        }

        # NetworkX acomoda automáticamente todas las estaciones.
        posiciones = nx.spring_layout(
            G,
            seed=15,
            k=0.35,
            iterations=200
        )

        # Conexiones pertenecientes a la ruta calculada.
        aristas_ruta = list(zip(ruta, ruta[1:]))

        # Color de cada tramo de la ruta según su línea.
        colores_ruta = [
            colores_metro.get(
                G[actual][siguiente]["linea"],
                "red"
            )
            for actual, siguiente in aristas_ruta
        ]

        plt.figure(figsize=(24, 18))

        # Dibuja toda la red en gris y con poca intensidad.
        nx.draw_networkx_edges(
            G,
            posiciones,
            edge_color="lightgray",
            width=1.5,
            alpha=0.5
        )

        # Dibuja todas las estaciones.
        nx.draw_networkx_nodes(
            G,
            posiciones,
            node_size=45,
            node_color="white",
            edgecolors="gray",
            linewidths=0.7
        )

        # Nombres de todas las estaciones.
        nx.draw_networkx_labels(
            G,
            posiciones,
            font_size=5,
            font_color="gray"
        )

        # Resalta las conexiones de la ruta.
        nx.draw_networkx_edges(
            G,
            posiciones,
            edgelist=aristas_ruta,
            edge_color=colores_ruta,
            width=6,
            alpha=1
        )

        # Resalta las estaciones que forman parte de la ruta.
        nx.draw_networkx_nodes(
            G,
            posiciones,
            nodelist=ruta,
            node_size=150,
            node_color="yellow",
            edgecolors="black",
            linewidths=1.5
        )

        # Resalta el origen en verde.
        nx.draw_networkx_nodes(
            G,
            posiciones,
            nodelist=[origen],
            node_size=300,
            node_color="limegreen",
            edgecolors="black",
            linewidths=2
        )

        # Resalta el destino en rojo.
        nx.draw_networkx_nodes(
            G,
            posiciones,
            nodelist=[destino],
            node_size=300,
            node_color="tomato",
            edgecolors="black",
            linewidths=2
        )

        # Vuelve a escribir únicamente las estaciones de la ruta
        # para que sus nombres sean más visibles.
        etiquetas_ruta = {
            estacion: estacion
            for estacion in ruta
        }

        nx.draw_networkx_labels(
            G,
            posiciones,
            labels=etiquetas_ruta,
            font_size=8,
            font_weight="bold",
            font_color="black"
        )

        plt.title(
            f"Ruta más corta: {origen} → {destino}",
            fontsize=18
        )

        plt.axis("off")
        plt.tight_layout()
        plt.show()

    except nx.NetworkXNoPath:
        print("\nNo existe una ruta entre esas estaciones.")
```
# Ejemplo de Búsqueda 1
## Pantitlán -> Buenavista

![Gráfica de concentración]({{ '/assets/img/Logica/datos1.png' | relative_url }})
![Gráfica de concentración]({{ '/assets/img/Logica/busqueda1.png' | relative_url }})

# Ejemplo de Búsqueda 2
## Instituto del Petróleo -> Tacubaya

![Gráfica de concentración]({{ '/assets/img/Logica/datos2.png' | relative_url }})
![Gráfica de concentración]({{ '/assets/img/Logica/busqueda2.png' | relative_url }})
