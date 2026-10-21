<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Juego 3D: Frontón Neón</title>
    <script src="https://code.playcanvas.com/playcanvas-stable.min.js"></script>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background-color: #000; cursor: crosshair; }
        canvas { display: block; width: 100vw; height: 100vh; }
        #interfaz {
            position: absolute;
            top: 20px;
            left: 20px;
            color: white;
            font-family: system-ui, sans-serif;
            background: rgba(0, 0, 0, 0.8);
            padding: 15px;
            border-radius: 8px;
            border: 2px solid #ff9a77;
            box-shadow: 0 0 15px #ff9a7744;
            pointer-events: none; /* Para que no interfiera con el ratón */
        }
        #puntos { color: #ff9a77; font-size: 24px; font-weight: bold; }
        #mensajeOver {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: system-ui, sans-serif;
            font-size: 32px;
            font-weight: bold;
            color: #ff4757;
            background: rgba(0, 0, 0, 0.9);
            padding: 30px;
            border-radius: 10px;
            border: 3px solid #ff4757;
            display: none;
            text-align: center;
            cursor: pointer;
            pointer-events: auto;
        }
    </style>
</head>
<body>

    <div id="interfaz">
        Rebotes: <span id="puntos">0</span><br>
        <span style="font-size: 14px; color: #a2aec9;">Mueve el ratón para controlar la paleta</span>
    </div>

    <div id="mensajeOver" onclick="location.reload()">
        ¡LA BOLA ESCAPÓ!<br>
        <span style="font-size:16px; color:#fff;">Haz clic para reiniciar</span>
    </div>

    <canvas id="mundo3D"></canvas>

    <script>
        const canvas = document.getElementById('mundo3D');
        const spanPuntos = document.getElementById('puntos');
        const divMensaje = document.getElementById('mensajeOver');
        
        const app = new pc.Application(canvas);
        app.start();
        app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
        app.setCanvasResolution(pc.RESOLUTION_AUTO);
        window.addEventListener('resize', () => app.resizeCanvas());

        // 1. ESCENARIO (El Túnel)
        const camara = new pc.Entity();
        camara.addComponent('camera', { clearColor: new pc.Color(0.05, 0.02, 0.1) });
        camara.setPosition(0, 0, 10);
        camara.lookAt(0, 0, 0);
        app.root.addChild(camara);

        const luz = new pc.Entity();
        luz.addComponent('light', { type: 'directional', color: new pc.Color(1, 1, 1), intensity: 1.5 });
        luz.setEulerAngles(30, 45, 0);
        app.root.addChild(luz);

        // Crear las paredes del túnel (Fondo, Techo, Suelo, Izquierda, Derecha)
        const matPared = new pc.StandardMaterial();
        matPared.diffuse.set(0.1, 0.1, 0.3); // Azul oscuro
        matPared.update();

        const matFondo = new pc.StandardMaterial();
        matFondo.diffuse.set(0.8, 0.2, 0.5); // Rosa/Morado
        matFondo.update();

        function crearPared(x, y, z, sx, sy, sz, material) {
            const pared = new pc.Entity();
            pared.addComponent('render', { type: 'box' });
            pared.setLocalScale(sx, sy, sz);
            pared.setPosition(x, y, z);
            pared.render.material = material;
            app.root.addChild(pared);
        }

        crearPared(0, 0, -20, 20, 14, 1, matFondo); // Fondo
        crearPared(0, -7, -10, 20, 1, 20, matPared); // Suelo
        crearPared(0, 7, -10, 20, 1, 20, matPared); // Techo
        crearPared(-10, 0, -10, 1, 14, 20, matPared); // Izquierda
        crearPared(10, 0, -10, 1, 14, 20, matPared); // Derecha

        // 2. JUGADOR (Paleta transparente controlada por el ratón)
        const matPaleta = new pc.StandardMaterial();
        matPaleta.diffuse.set(0.2, 0.9, 0.7); // Cian Neón
        matPaleta.opacity = 0.6; // Hacerla semi-transparente
        matPaleta.blendType = pc.BLEND_NORMAL;
        matPaleta.update();

        const jugador = new pc.Entity();
        jugador.addComponent('render', { type: 'box' });
        jugador.setLocalScale(4, 3, 0.5);
        jugador.setPosition(0, 0, 5); // Cerca de la cámara
        jugador.render.material = matPaleta;
        app.root.addChild(jugador);

        // 3. LA BOLA
        const matBola = new pc.StandardMaterial();
        matBola.diffuse.set(1, 0.6, 0.4); // Naranja Neón
        matBola.emissive.set(1, 0.6, 0.4);
        matBola.update();

        const bola = new pc.Entity();
        bola.addComponent('render', { type: 'sphere' });
        bola.setLocalScale(1, 1, 1);
        bola.setPosition(0, 0, 0);
        bola.render.material = matBola;
        app.root.addChild(bola);

        // 4. VARIABLES DEL JUEGO
        let juegoActivo = true;
        let puntos = 0;
        
        // Velocidad de la bola en los 3 ejes
        let velX = 8;
        let velY = 6;
        let velZ = -15; // Empieza yendo hacia el fondo

        // Control del ratón
        let ratonX = 0;
        let ratonY = 0;

        window.addEventListener('mousemove', (e) => {
            // Mapear la posición 2D de la pantalla a coordenadas 3D limitadas
            // La pantalla va de 0 a window.innerWidth. Queremos que el espacio 3D vaya de -8 a +8.
            let xPantalla = (e.clientX / window.innerWidth) * 2 - 1; // Rango -1 a 1
            let yPantalla = (e.clientY / window.innerHeight) * 2 - 1; // Rango -1 a 1 (invertido)
            
            ratonX = xPantalla * 8; // Multiplicamos para abarcar el ancho del túnel
            ratonY = -yPantalla * 5.5; // Invertimos Y porque en la pantalla abajo es positivo, en 3D abajo es negativo
        });

        // 5. BUCLE PRINCIPAL
        app.on('update', function (dt) {
            if (!juegoActivo) return;

            // Mover la paleta hacia el ratón suavemente (Interpolación Lineal)
            let posJ = jugador.getPosition();
            jugador.setPosition(
                posJ.x + (ratonX - posJ.x) * 10 * dt,
                posJ.y + (ratonY - posJ.y) * 10 * dt,
                5
            );

            // Mover la bola
            let posB = bola.getPosition();
            bola.setPosition(
                posB.x + (velX * dt),
                posB.y + (velY * dt),
                posB.z + (velZ * dt)
            );

            // ACTUALIZAR POSICIÓN PARA COLISIONES
            posB = bola.getPosition();

            // Colisiones con las paredes laterales (Eje X)
            if (posB.x > 9 || posB.x < -9) {
                velX = -velX;
                bola.setPosition(posB.x > 0 ? 9 : -9, posB.y, posB.z); // Evitar que se pegue
            }

            // Colisiones con el techo y suelo (Eje Y)
            if (posB.y > 6 || posB.y < -6) {
                velY = -velY;
                bola.setPosition(posB.x, posB.y > 0 ? 6 : -6, posB.z);
            }

            // Colisión con la pared del fondo (Eje Z)
            if (posB.z < -19) {
                velZ = -velZ;
                bola.setPosition(posB.x, posB.y, -19);
            }

            // Colisión con la Paleta del Jugador (Eje Z positivo)
            if (velZ > 0 && posB.z > 4 && posB.z < 6) {
                // Comprobar si la bola está dentro del área de la paleta (Ejes X e Y)
                // La paleta mide 4 de ancho (mitad 2) y 3 de alto (mitad 1.5)
                if (posB.x > posJ.x - 2.5 && posB.x < posJ.x + 2.5 &&
                    posB.y > posJ.y - 2 && posB.y < posJ.y + 2) {
                    
                    velZ = -velZ; // Rebotar hacia el fondo
                    
                    // Añadir un poco de la inercia/posición de la paleta a la bola
                    velX += (posB.x - posJ.x) * 2;
                    velY += (posB.y - posJ.y) * 2;
                    
                    puntos++;
                    spanPuntos.textContent = puntos;

                    // Aumentar velocidad (Dificultad)
                    velZ -= 1;
                }
            }

            // GAME OVER: La bola pasó la paleta (z > 7)
            if (posB.z > 7) {
                juegoActivo = false;
                divMensaje.style.display = 'block';
            }
        });
    </script>
</body>
</html>