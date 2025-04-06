# Counter-App-Carrito-de-Compras-
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carrito de Compras</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 20px;
        }
        .productos {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }
        .producto {
            background: white;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .producto img {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 5px;
        }
        .producto h3 {
            margin: 10px 0;
        }
        .producto p {
            color: #666;
        }
        .precio {
            font-weight: bold;
            color: #2a9d8f;
            font-size: 1.2em;
        }
        .agregar-carrito {
            background-color: #2a9d8f;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
        }
        .carrito {
            background: white;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            height: fit-content;
        }
        .carrito h2 {
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }
        .item-carrito {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }
        .item-info {
            flex-grow: 1;
        }
        .item-cantidad {
            display: flex;
            align-items: center;
        }
        .item-cantidad button {
            background: #ddd;
            border: none;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            cursor: pointer;
        }
        .item-cantidad span {
            margin: 0 10px;
        }
        .eliminar-item {
            color: #e76f51;
            cursor: pointer;
            margin-left: 10px;
        }
        .total {
            font-weight: bold;
            font-size: 1.2em;
            text-align: right;
            margin-top: 20px;
        }
        .vaciar-carrito {
            background-color: #e76f51;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>Tienda Online</h1>
    
    <div class="container">
        <div class="productos">
            <div class="producto">
                <img src="https://via.placeholder.com/250x180?text=Producto+1" alt="Producto 1">
                <h3>Zapatillas Deportivas</h3>
                <p>Zapatillas ideales para running y entrenamiento.</p>
                <div class="precio">$59.99</div>
                <button class="agregar-carrito" data-id="1" data-nombre="Zapatillas Deportivas" data-precio="59.99">Agregar al carrito</button>
            </div>
            
            <div class="producto">
                <img src="https://via.placeholder.com/250x180?text=Producto+2" alt="Producto 2">
                <h3>Camiseta Básica</h3>
                <p>Camiseta de algodón 100% en varios colores.</p>
                <div class="precio">$19.99</div>
                <button class="agregar-carrito" data-id="2" data-nombre="Camiseta Básica" data-precio="19.99">Agregar al carrito</button>
            </div>
            
            <div class="producto">
                <img src="https://via.placeholder.com/250x180?text=Producto+3" alt="Producto 3">
                <h3>Pantalón Jeans</h3>
                <p>Jeans clásicos de corte recto.</p>
                <div class="precio">$39.99</div>
                <button class="agregar-carrito" data-id="3" data-nombre="Pantalón Jeans" data-precio="39.99">Agregar al carrito</button>
            </div>
            
            <div class="producto">
                <img src="https://via.placeholder.com/250x180?text=Producto+4" alt="Producto 4">
                <h3>Reloj Inteligente</h3>
                <p>Con monitor de actividad y notificaciones.</p>
                <div class="precio">$129.99</div>
                <button class="agregar-carrito" data-id="4" data-nombre="Reloj Inteligente" data-precio="129.99">Agregar al carrito</button>
            </div>
        </div>
        
        <div class="carrito">
            <h2>Carrito de Compras</h2>
            <div id="items-carrito"></div>
            <div class="total">Total: $<span id="total-carrito">0.00</span></div>
            <button class="vaciar-carrito" id="vaciar-carrito">Vaciar Carrito</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const carrito = [];
            const itemsCarrito = document.getElementById('items-carrito');
            const totalCarrito = document.getElementById('total-carrito');
            const botonesAgregar = document.querySelectorAll('.agregar-carrito');
            const botonVaciar = document.getElementById('vaciar-carrito');

            // Agregar producto al carrito
            botonesAgregar.forEach(boton => {
                boton.addEventListener('click', agregarAlCarrito);
            });

            // Vaciar carrito
            botonVaciar.addEventListener('click', vaciarCarrito);

            function agregarAlCarrito(e) {
                const id = e.target.dataset.id;
                const nombre = e.target.dataset.nombre;
                const precio = parseFloat(e.target.dataset.precio);

                // Verificar si el producto ya está en el carrito
                const productoExistente = carrito.find(item => item.id === id);

                if (productoExistente) {
                    productoExistente.cantidad++;
                } else {
                    carrito.push({
                        id,
                        nombre,
                        precio,
                        cantidad: 1
                    });
                }

                actualizarCarrito();
            }

            function actualizarCarrito() {
                itemsCarrito.innerHTML = '';
                let total = 0;

                carrito.forEach(item => {
                    const itemElemento = document.createElement('div');
                    itemElemento.classList.add('item-carrito');
                    itemElemento.innerHTML = `
                        <div class="item-info">
                            <span>${item.nombre}</span>
                            <span>$${item.precio.toFixed(2)}</span>
                        </div>
                        <div class="item-cantidad">
                            <button class="disminuir" data-id="${item.id}">-</button>
                            <span>${item.cantidad}</span>
                            <button class="aumentar" data-id="${item.id}">+</button>
                            <span class="eliminar-item" data-id="${item.id}">🗑️</span>
                        </div>
                    `;
                    itemsCarrito.appendChild(itemElemento);

                    total += item.precio * item.cantidad;
                });

                totalCarrito.textContent = total.toFixed(2);

                // Agregar eventos a los nuevos botones
                document.querySelectorAll('.disminuir').forEach(boton => {
                    boton.addEventListener('click', disminuirCantidad);
                });

                document.querySelectorAll('.aumentar').forEach(boton => {
                    boton.addEventListener('click', aumentarCantidad);
                });

                document.querySelectorAll('.eliminar-item').forEach(boton => {
                    boton.addEventListener('click', eliminarItem);
                });
            }

            function disminuirCantidad(e) {
                const id = e.target.dataset.id;
                const item = carrito.find(item => item.id === id);

                if (item.cantidad > 1) {
                    item.cantidad--;
                } else {
                    // Si la cantidad es 1, eliminamos el producto
                    const index = carrito.findIndex(item => item.id === id);
                    carrito.splice(index, 1);
                }

                actualizarCarrito();
            }

            function aumentarCantidad(e) {
                const id = e.target.dataset.id;
                const item = carrito.find(item => item.id === id);
                item.cantidad++;
                actualizarCarrito();
            }

            function eliminarItem(e) {
                const id = e.target.dataset.id;
                const index = carrito.findIndex(item => item.id === id);
                carrito.splice(index, 1);
                actualizarCarrito();
            }

            function vaciarCarrito() {
                carrito.length = 0;
                actualizarCarrito();
            }
        });
    </script>
</body>
</html>
