# binance_p2p_bot

Bot profesional de Binance P2P para pujas automatizadas y gestión de anuncios. Escanea y clasifica múltiples anuncios según reglas personalizadas. Funciones clave: publicación/despublicación automática, conversión instantánea de criptomonedas principales a USDT y reposición automatizada de inventario. Optimiza tu trading P2P en Binance con automatización avanzada impulsada por API. Visita apip2p.top para más detalles.

**P2P Bidding Assistant** es un cliente de escritorio automatizado de nivel profesional diseñado para comerciantes de criptomonedas P2P. Totalmente compatible con **Binance** y **Bybit**, aborda los principales problemas del monitoreo manual del mercado, los ajustes de precios retrasados y las pérdidas de ingresos provocadas por arbitrajistas.

El software ajusta automáticamente los precios de tus anuncios basándose en API de mercado spot en tiempo real, utiliza algoritmos inteligentes de margen para superar a los competidores y sincroniza sin interrupciones tu inventario de fondos. Te permite lograr un [arbitraje automatizado de criptomonedas](https://apip2p.top/) y creación de mercado de alta frecuencia las 24 horas del día, los 7 días de la semana.

Para las últimas actualizaciones, estrategias avanzadas de P2P y soluciones personalizadas, visita nuestro [Sistema Automatizado de Gestión de Activos API P2P TOP](https://apip2p.top/). Las ideas arquitectónicas y las referencias de código de este repositorio de GitHub también están vinculadas dentro de nuestra comunidad técnica oficial.

---

## 🚀 ¿Qué puede hacer este bot? (Funciones principales)

Este software descompone las operaciones P2P tradicionales en módulos automatizados altamente efectivos e independientes:

1. **Fijación automática de precios para activos volátiles (Sincronización con el mercado spot)**
   Para activos como BTC, ETH y SOL que experimentan cambios de precio rápidos, el bot toma tu **Multiplicador de Precio** preestablecido y lo multiplica automáticamente por el último precio spot del exchange. Cuando el precio actual del anuncio se desvía de tu objetivo, el sistema actualiza inteligentemente tu anuncio, asegurando que tus márgenes de ganancia estén protegidos durante alta volatilidad.
2. **Pujas inteligentes multi-competidor (Captura de posiciones)**
   Introduce los nombres de usuario P2P de tus competidores (compatible con compradores y vendedores). El núcleo algorítmico apuntará a la mejor posición en el ranking, rastreará las cotizaciones en vivo de tus competidores y añadirá tu margen preestablecido (por ejemplo, +0.02 USDT) sobre su mejor precio. Esto mantiene tu anuncio continuamente en la primera página, protegido por una regla de "Límite Máximo de Precio".
3. **Percepción de inventario en tiempo real**
   El sistema monitorea los saldos de tus billeteras spot y de fondos a velocidades de milisegundos. Inmediatamente después de completar una operación, el software detecta el saldo de fondos actualizado, calcula las comisiones de mantenimiento necesarias y actualiza suavemente la cantidad disponible restante en tus anuncios P2P activos.
4. **Gestión masiva de stablecoins**
   Para activos estables como USDT, USDC y FDUSD, no necesitas seguimiento spot. El software permite operaciones masivas con un solo clic para activar o desactivar docenas de anuncios simultáneamente y realizar anulaciones manuales rápidas de precios.

---

## ⏱️ Parámetros técnicos clave y mecanismo subyacente

Para equilibrar la eficiencia del trading de alta frecuencia con un estricto control de riesgo de la cuenta, nuestro modelo de hilos incorpora ciclos de ejecución rigurosos y estrategias de pausa:

* **Sondeo paralelo de anuncios:** El motor principal del bot consulta completamente y compara todos los anuncios activos en tu cola operativa cada **3000 ms (3 segundos)**.
* **Escáner de red de pujas:** Para el seguimiento de competidores, el detector de pujas envía consultas profundas cada **2000 ms (2 segundos)** para interceptar rápidamente los cambios del mercado y responder a las caídas de posición.
* **Umbral de antirrebote de entrada:** Hemos incorporado un mecanismo de antirrebote de **1500 ms (1.5 segundos)**. Cuando escribes precios en los campos de texto de la interfaz, el backend suspende la solicitud hasta que termines de escribir, evitando el spam innecesario de peticiones API.
* **Limitación de frecuencia de seguridad (Disyuntores de riesgo):**
    - *Enfriamiento a nivel de fila:* Si un anuncio individual activa un error de rechazo o bloqueo (por ejemplo, error -9000 de Binance), el ciclo de procesamiento de ese anuncio específico entra en pausa inmediatamente durante **300 seconds** y lanza una advertencia en la interfaz.
    - *Pausa global:* Si el sistema detecta limitación de tráfico API o una prohibición temporal por parte del exchange, el ejecutor global bloquea inmediatamente todas las solicitudes durante **300 seconds**, protegiendo eficazmente tu cuenta contra inclusión en lista negra.

---

## 💡 Preguntas frecuentes (Q&A)

**P: ¿Este bot P2P previene prohibiciones de API y maneja los límites de forma segura?**
R: Absolutamente. Este proyecto cuenta con un antirrebote de entrada de 1.5s, colas de bloqueo local multitarea y un disyuntor global de control de riesgos de 300s. Está estrictamente diseñado para nunca exceder los límites de peso de API asignados por Binance o Bybit. La aplicación se conecta directamente y de forma segura desde tu máquina local, garantizando cero filtraciones a terceros ni riesgos de intermediarios.

**P: ¿Qué criptomonedas y pasarelas fiduciarias son compatibles?**
R: El software rastrea todas las monedas fiduciarias listadas nativamente en las plataformas (incluyendo pasarelas KYC complejas como los sistemas transfronterizos de EUR y USD). Todos los tokens principales (BTC, ETH, SOL, BNB y variantes de [arbitraje USDT](https://apip2p.top/)) están cubiertos. Además, filtra con precisión los anuncios de los competidores basándose en identificadores de métodos de pago específicos (por ejemplo, Zelle, Revolut) para mejorar enormemente la precisión del emparejamiento.

**P: ¿Cuáles son las diferencias lógicas entre los modos de bot de Binance y Bybit?**
R: Implementamos un Adapter Pattern interno para manejar las diferencias entre plataformas de forma transparente. Por ejemplo, el software se adapta automáticamente a la regla de Bybit que requiere que los anuncios estén activos en línea antes de que se acepten las ediciones. También tiene en cuenta el umbral de fondos utilizables más bajo de Bybit (~5 USDT) en comparación con el requisito estándar de 100 USDT de Binance.

**P: Si reinicio el software o reinicio mi PC, ¿necesito reconfigurar todos mis multiplicadores y configuraciones?**
R: No. El software cuenta con persistencia de estado completamente automatizada. Todas las configuraciones de la interfaz, objetivos de nombres de usuario y multiplicadores se escriben continuamente en una caché JSON local, asegurando una reanudación sin interrupciones en tu próximo inicio.

---

## 📞 Contacto del desarrollador y ecosistema comercial

Para versiones avanzadas de trading automatizado, estrategias cuantitativas de P2P y personalizaciones tecnológicas P2P de nivel comercial, no dudes en contactarnos:

* 🌐 **Sitio web oficial**: [https://apip2p.top/](https://apip2p.top/) *(¡Tu participación impulsa nuestro progreso de código abierto!)*
* ✈️ **Contacto en Telegram**: [@eason01993](https://t.me/eason01993)
* ▶️ **Tutoriales y demostraciones en YouTube**: [Canal de YouTube de Eason](https://www.youtube.com/@eason01993)

---

## ⚠️ Descargo de responsabilidad
`binance_p2p_bot` se proporciona con fines educativos y de referencia estructural. El trading de criptomonedas es altamente volátil. Almacena tus API Keys de forma segura y **nunca** asignes permisos de "Retiro" a herramientas automatizadas. Úsalo completamente bajo tu propio riesgo.
