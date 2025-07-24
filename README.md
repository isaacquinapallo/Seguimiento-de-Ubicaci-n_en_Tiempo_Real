# GPSApp – Seguimiento de Ubicación en Tiempo Real

Esta aplicación Android desarrollada en **Kotlin** obtiene la ubicación GPS del dispositivo y la envía automáticamente cada 10 segundos a una tabla en **Supabase**. Está pensada para recolectar coordenadas de manera eficiente en segundo plano, usando permisos de ubicación avanzados.

## Tecnologías utilizadas

- Kotlin (Android)
- Google FusedLocationProvider (servicio de ubicación)
- Supabase (como backend y base de datos)
- OkHttp (para hacer solicitudes HTTP)
- Row Level Security en Supabase

##  Funcionalidad

-  Obtiene la ubicación GPS automáticamente.
-  Envía los datos cada 10 segundos a Supabase.
-  Maneja permisos en primer y segundo plano.
-  Guarda en Supabase en la tabla `locations`.

## Capturas de pantalla

### 1. Pantalla mostrando coordenadas en tiempo real  

![Imagen de WhatsApp 2025-07-24 a las 15 20 55_0bb42b94](https://github.com/user-attachments/assets/33ae0e2e-ba0b-4735-9dfe-423ec37093e7)


### 2. Inserciones vistas en Supabase  

<img width="1919" height="939" alt="image" src="https://github.com/user-attachments/assets/f3c70e49-dadd-4638-b75a-2b1bf37c0a39" />


## Instalación

1. Clona el repositorio:

git clone https://github.com/isaacquinapallo/Seguimiento-de-Ubicaci-n_en_Tiempo_Real.git
cd gpsapp

2. Configura tus claves en `local.properties`:

SUPABASE_URL=https://xxxx.supabase.co  
SUPABASE_KEY=eyJhbGciOi...

3. Asegúrate de tener permisos de ubicación y background en tu `AndroidManifest.xml`:

<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />

## Configuración en Supabase

### Tabla `locations`

create table locations (
  id uuid primary key default gen_random_uuid(),
  latitude double precision,
  longitude double precision,
  inserted_at timestamp with time zone default timezone('utc'::text, now())
);

### Habilitar RLS y política pública

alter table locations enable row level security;

create policy "Public insert for anon"
on locations
for insert
to anon
with check (true);

## Uso

Una vez instalada la app y concedidos los permisos:

- La app empezará a enviar coordenadas automáticamente.
- Puedes ver los registros en Supabase en tiempo real.

## Desarrollador

- Isaac Quinapallo
- Desarrollador de Software y entusiasta de la geolocalización en EPN
