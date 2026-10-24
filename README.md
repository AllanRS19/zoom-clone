# Zoom Clone — Aplicación de videollamadas

Aplicación full stack de videollamadas en tiempo real con grabación integrada y autenticación de usuarios, construida con Next.js 14, Stream y Clerk.

**Demo:** https://zoom-clone-lyart.vercel.app

![Captura de la aplicación](./public/screenshot.png)
<!-- Agrega aquí una captura de la pantalla principal y, si puedes, un GIF de una llamada -->

## Funcionalidades

- Videollamadas en tiempo real con baja latencia.
- Grabación integrada: captura, almacenamiento y reproducción de sesiones anteriores.
- Autenticación y manejo de sesiones con Clerk; rutas protegidas con middleware.
- [Reuniones instantáneas y programadas con selector de fecha y hora.]
- [Sala personal y enlaces para invitar a otros participantes.]
- [Listas de reuniones próximas y anteriores.]
- Interfaz responsive con Tailwind CSS y componentes de shadcn/ui.

## Tecnologías

| Área | Herramientas |
| --- | --- |
| Framework | Next.js 14 (App Router), React 18, TypeScript |
| Video en tiempo real | Stream Video React SDK, Stream Node SDK |
| Autenticación | Clerk |
| Estilos y UI | Tailwind CSS, shadcn/ui, Radix UI, lucide-react |
| Despliegue | Vercel |

## Cómo funciona

1. Clerk autentica al usuario y protege las rutas desde `middleware.ts`.
2. Una acción de servidor genera el token de Stream para el usuario autenticado, usando el SDK de Node de Stream. [confirmar nombre y ubicación en `actions/`]
3. El cliente se conecta a Stream con el SDK de React y crea o se une a la llamada.
4. Las grabaciones se guardan en Stream y se listan para reproducirlas después.

## Estructura del proyecto

```
actions/      Acciones de servidor (por ejemplo, generación de tokens)
app/          Rutas y páginas (App Router)
components/   Componentes de interfaz y de reuniones
constants/    Constantes y datos de navegación
hooks/        Hooks personalizados
lib/          Utilidades
providers/    Proveedores de contexto (cliente de Stream)
middleware.ts Protección de rutas con Clerk
```

## Cómo ejecutarlo en local

**Requisitos:** Node.js 18 o superior, y cuentas gratuitas en [Clerk](https://clerk.com) y [Stream](https://getstream.io).

```bash
git clone https://github.com/AllanRS19/zoom-clone.git
cd zoom-clone
npm install
```

Crea un archivo `.env.local` en la raíz:

```env
# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up

# Stream
NEXT_PUBLIC_STREAM_API_KEY=
STREAM_SECRET_KEY=

# URL base de la app
NEXT_PUBLIC_BASE_URL=http://localhost:3000
```
<!-- Confirma estos nombres buscando "process.env" en tu código -->

Inicia el servidor de desarrollo:

```bash
npm run dev
```

Abre [http://localhost:3000](http://localhost:3000).

## Scripts

| Comando | Descripción |
| --- | --- |
| `npm run dev` | Servidor de desarrollo |
| `npm run build` | Build de producción |
| `npm run start` | Ejecuta el build de producción |
| `npm run lint` | Revisa el código con ESLint |

## Despliegue

Desplegado en Vercel. Para desplegar tu propia copia, importa el repo en Vercel y agrega las variables de entorno de arriba.
