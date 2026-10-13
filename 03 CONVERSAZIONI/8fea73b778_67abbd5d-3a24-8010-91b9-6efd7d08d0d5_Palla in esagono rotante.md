# Palla in esagono rotante

Fonte: ChatGPT, conversazione 67abbd5d-3a24-8010-91b9-6efd7d08d0d5.

Copertura: passaggi pertinenti al tema; conversazione integrale nel deposito locale.

## Assistente AI, messaggio 5, ramo attivo

😆 Ecco una versione ulteriormente "assurda" della simulazione. In questo codice, oltre al portale inaspettato già presente, quando la palla collide con il bordo dell'esagono c'è una probabilità di generare cloni colorati della palla stessa che si comportano in modo indipendente per un tempo limitato, creando una situazione surreale e caotica!

```python
import pygame
import math
import sys
import random

# Inizializzazione di Pygame
pygame.init()

# Impostazioni della finestra
LARGHEZZA, ALTEZZA = 800, 600
schermo = pygame.display.set_mode((LARGHEZZA, ALTEZZA))
pygame.display.set_caption("Simulazione: Palla in un Esagono Rotante con Effetti Assurdi")
clock = pygame.time.Clock()

# Parametri dell'esagono
centro_esagono = (LARGHEZZA // 2, ALTEZZA // 2)
raggio_esagono = 200
angolo_rotazione = 0
velocita_rotazione = 0.01  # in radianti per frame

# Parametri della palla
raggio_palla = 10

# Lista delle palle: partiamo con una palla principale
balls = [{
    "pos": [LARGHEZZA // 2, ALTEZZA // 2],
    "vel": [3, -2],
    "lifetime": None,       # None indica la palla principale senza scadenza
    "color": (255, 0, 0)
}]

# Parametri del portale inaspettato
portal_active = False
portal_position = (0, 0)
portal_radius = 20
portal_duration = 180  # durata in frame (circa 3 secondi a 60 FPS)
portal_timer = 0
portal_color = (255, 255, 0)

def calcola_vertici_esagono(centro, raggio, angolo):
    """
    Calcola i vertici di un esagono regolare centrato in 'centro',
    con un dato 'raggio' e ruotato di 'angolo' radianti.
    """
    vertici = []
    for i in range(6):
        theta = angolo + i * (2 * math.pi / 6)
        x = centro[0] + raggio * math.cos(theta)
        y = centro[1] + raggio * math.sin(theta)
        vertici.append((x, y))
    return vertici

def distanza_punto_retta(P, A, B):
    """
    Calcola la distanza dal punto P al segmento di linea definito da A e B,
    restituendo anche il punto di proiezione.
    """
    AP = (P[0] - A[0], P[1] - A[1])
    AB = (B[0] - A[0], B[1] - A[1])
    lunghezza_AB2 = AB[0]**2 + AB[1]**2
    if lunghezza_AB2 == 0:
        return math.hypot(AP[0], AP[1]), A
    t = (AP[0]*AB[0] + AP[1]*AB[1]) / lunghezza_AB2
    t = max(0, min(1, t))
    proiezione = (A[0] + t * AB[0], A[1] + t * AB[1])
    distanza = math.hypot(P[0] - proiezione[0], P[1] - proiezione[1])
    return distanza, proiezione

def spawn_clone(ball):
    """
    Genera un numero casuale (1-3) di cloni della palla corrente.
    I cloni hanno velocità e colore random, e una durata limitata.
    """
    clones = []
    num_clones = random.randint(1, 3)
    for _ in range(num_clones):
        clone = {
            "pos": ball["pos"].copy(),
            "vel": [
                ball["vel"][0] * random.uniform(0.5, 1.5) + random.uniform(-2, 2),
                ball["vel"][1] * random.uniform(0.5, 1.5) + random.uniform(-2, 2)
            ],
            "lifetime": random.randint(300, 600),  # durata in frame per il clone
            "color": (random.randint(0,255), random.randint(0,255), random.randint(0,255))
        }
        clones.append(clone)
    return clones

# Loop principale della simulazione
while True:
    # Gestione degli eventi
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    
    # Aggiorna la rotazione dell'esagono
    angolo_rotazione += velocita_rotazione
    vertici_esagono = calcola_vertici_esagono(centro_esagono, raggio_esagono, angolo_rotazione)
    
    # Gestione del portale inaspettato: appare casualmente lungo un lato dell'esagono
    if not portal_active and random.random() < 0.001:
        portal_active = True
        random_edge_index = random.randint(0, 5)
        A = vertici_esagono[random_edge_index]
        B = vertici_esagono[(random_edge_index + 1) % 6]
        t_random = random.random()
        portal_position = (A[0] + t_random * (B[0] - A[0]), A[1] + t_random * (B[1] - A[1]))
        portal_color = (random.randint(0,255), random.randint(0,255), random.randint(0,255))
        portal_timer = portal_duration
    
    if portal_active:
        portal_timer -= 1
        if portal_timer <= 0:
            portal_active = False

    # Lista per raccogliere nuovi cloni (elemento assurdo!)
    new_balls = []
    
    # Aggiornamento e gestione collisioni per ogni palla
    for ball in balls:
        # Aggiorna la posizione della palla
        ball["pos"][0] += ball["vel"][0]
        ball["pos"][1] += ball["vel"][1]
        
        # Controlla collisioni con ciascun lato dell'esagono
        for i in range(6):
            A = vertici_esagono[i]
            B = vertici_esagono[(i + 1) % 6]
            distanza, proiezione = distanza_punto_retta(ball["pos"], A, B)
            if distanza < raggio_palla:
                # Calcola il vettore normale per riflettere la velocità
                n_x = ball["pos"][0] - proiezione[0]
                n_y = ball["pos"][1] - proiezione[1]
                norma = math.hypot(n_x, n_y)
                if norma != 0:
                    n_x /= norma
                    n_y /= norma
                    prodotto_scalare = ball["vel"][0] * n_x + ball["vel"][1] * n_y
                    ball["vel"][0] = ball["vel"][0] - 2 * prodotto_scalare * n_x
                    ball["vel"][1] = ball["vel"][1] - 2 * prodotto_scalare * n_y
                    # Sposta la palla per evitare collisioni continue
                    overlap = raggio_palla - distanza
                    ball["pos"][0] += n_x * overlap
                    ball["pos"][1] += n_y * overlap
                    
                    # Elemento assurdo: possibilità di generare cloni della palla durante la collisione
                    if random.random() < 0.02:  # probabilità aumentata per effetto surreale
                        clones = spawn_clone(ball)
                        new_balls.extend(clones)
        
        # Gestione della collisione con il portale inaspettato
        if portal_active:
            distanza_portal = math.hypot(ball["pos"][0] - portal_position[0],
                                         ball["pos"][1] - portal_position[1])
            if distanza_portal < (raggio_palla + portal_radius):
                # Teletrasporta la palla in una posizione casuale all'interno dell'esagono
                theta = random.uniform(0, 2 * math.pi)
                r = math.sqrt(random.uniform(0, 1)) * (raggio_esagono - raggio_palla - 5)
                ball["pos"][0] = centro_esagono[0] + r * math.cos(theta)
                ball["pos"][1] = centro_esagono[1] + r * math.sin(theta)
                # Cambia il colore in modo assurdo
                ball["color"] = (random.randint(0,255), random.randint(0,255), random.randint(0,255))
                portal_active = False
        
        # Aggiornamento della durata di vita dei cloni: la palla principale non ha scadenza (lifetime=None)
        if ball["lifetime"] is not None:
            ball["lifetime"] -= 1

    # Aggiungi i nuovi cloni alla lista delle palle
    balls.extend(new_balls)
    # Rimuovi i cloni che hanno esaurito la loro durata
    balls = [ball for ball in balls if ball["lifetime"] is None or ball["lifetime"] > 0]
    
    # Pulizia dello schermo
    schermo.fill((0, 0, 0))
    
    # Disegna l'esagono
    pygame.draw.polygon(schermo, (255, 255, 255), vertici_esagono, 2)
    
    # Disegna il portale se attivo
    if portal_active:
        pygame.draw.circle(schermo, portal_color, (int(portal_position[0]), int(portal_position[1])), portal_radius, 2)
    
    # Disegna tutte le palle (palla principale e cloni assurdi)
    for ball in balls:
        pygame.draw.circle(schermo, ball["color"], (int(ball["pos"][0]), int(ball["pos"][1])), raggio_palla)
    
    pygame.display.flip()
    clock.tick(60)
```

👉 **Domande per approfondire:**
1. Ti interessa sperimentare ulteriori meccanismi assurdi, ad esempio effetti audio o variazioni improvvise nei parametri fisici?
2. Vorresti aggiungere ulteriori comportamenti "quantistici" ai cloni, come la fusione automatica dopo un certo tempo?
3. Ti piacerebbe analizzare in dettaglio come funziona il meccanismo di generazione dei cloni e personalizzarne la probabilità o la durata?

