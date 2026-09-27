# CondorTravels · API de reserva de vuelos

Backend desarrollado para el **reto SenaSoft**: búsqueda de vuelos, **selección de asientos**, reservas con pasajeros y **pagos con PayU Latam** (sandbox).

Frontend: [FrontendSenaSoft](https://github.com/CristianGarcia7/FrontendSenaSoft)

## ✨ Funcionalidades

- Autenticación con **JWT**.
- Búsqueda de vuelos por origen y destino, incluidos vuelos con regreso.
- Mapa de asientos por vuelo con su disponibilidad.
- Reservas con varios pasajeros y sus asientos, y consulta de "mis reservas".
- **Pagos con PayU**: creación de la orden, página de respuesta y *webhook* de confirmación. Ver [`PAYU_INTEGRATION.md`](PAYU_INTEGRATION.md).
- Comando `php artisan seats:regenerate` para regenerar los asientos.
- **Dockerfile** para desplegar (incluye drivers de MySQL y PostgreSQL).

## 🧱 Stack

Laravel 12 · PHP 8.2 · JWT Auth · SQLite / MySQL / PostgreSQL · PayU Latam · Docker

## 🚀 Cómo correrlo

```bash
composer install
cp .env.example .env        # SQLite por defecto; variables PAYU_* (ver PAYU_SETUP.md)
php artisan key:generate
php artisan jwt:secret
php artisan migrate
php artisan serve           # http://127.0.0.1:8000
```

## 📡 Endpoints destacados

| Método | Ruta | Descripción |
|---|---|---|
| `POST` | `/api/login` · `/api/addUser` | Autenticación y registro |
| `POST` | `/api/searchFlights` | Buscar vuelos |
| `GET` | `/api/flights/{id}/available-seats` | Asientos disponibles |
| `POST` | `/api/addReservationWithPayment` | Reservar y pagar |
| `GET` | `/api/myReservations` | Reservas del usuario |
| `POST` | `/api/payment/create-order` · `/api/payment/confirmation` | Flujo de pago PayU |

> Las credenciales de PayU que aparecen en la documentación son las **públicas del sandbox** de PayU, solo para pruebas.
