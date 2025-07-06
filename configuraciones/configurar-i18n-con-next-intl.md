# 📚 Guía: Configurar `i18n` con `next-intl`

Esta guía describe paso a paso cómo configurar desde cero un entorno multilenguaje utilizando la biblioteca `next-intl` de **Next.js**.

---

## 📘 Documentación oficial de `next-intl`

Puedes consultar la documentación oficial de esta configuración en:

🔗 [https://next-intl.dev/docs/getting-started/app-router/with-i18n-routing](https://next-intl.dev/docs/getting-started/app-router/with-i18n-routing)

---

## 📂 Estructura recomendada para el proyecto (resumen)

```plaintext
├── messages
│   ├── en.json
│   └── ...
├── next.config.ts
└── src
    ├── i18n
    │   ├── routing.ts
    │   ├── navigation.ts
    │   └── request.ts
    ├── middleware.ts
    └── app
        └── [locale]
            ├── layout.tsx
            └── page.tsx
```

---

## 📂 Estructura de archivos

### 1. Crea la carpeta `messages/` en la raíz del proyecto:

```plaintext
/messages
  ├── en.json
  └── es.json
```

### 2. Contenido de los archivos:

`messages/en.json`:

```json
{
  "Home": {
    "text": "Hello world!"
  },
  "Header": {
    "text": "Header in English"
  },
  "Metadata": {
    "title": "Example i18n with Next.js, next-intl and TS",
    "description": "A sample multilingual app using Next.js, next-intl and TypeScript."
  }
}
```

`messages/es.json`:

```json
{
  "Home": {
    "text": "Hola mundo!"
  },
  "Header": {
    "text": "Header en Español"
  },
  "Metadata": {
    "title": "Ejemplo i18n con Next.js, next-intl y TS",
    "description": "Una aplicación de ejemplo multilingüe usando Next.js, next-intl y TypeScript."
  }
}
```

---

## ⚙️ Configuración del proyecto

### 1. Modifica `next.config.ts`:

```ts
import {NextConfig} from 'next';
import createNextIntlPlugin from 'next-intl/plugin';
 
const nextConfig: NextConfig = {};
 
const withNextIntl = createNextIntlPlugin();
export default withNextIntl(nextConfig);
```

---

### 2. Crea `src/i18n/routing.ts`:

```ts
import {defineRouting} from 'next-intl/routing';
 
export const routing = defineRouting({
  // A list of all locales that are supported
  locales: ['en', 'es'],
 
  // Used when no locale matches
  defaultLocale: 'en'
});
```

---

### 3. Crea `src/i18n/navigation.ts`:

```ts
import {createNavigation} from 'next-intl/navigation';
import {routing} from './routing';
 
// Lightweight wrappers around Next.js' navigation
// APIs that consider the routing configuration
export const {Link, redirect, usePathname, useRouter, getPathname} =
  createNavigation(routing);
```

---

### 4. Crea `src/middleware.ts`:

```ts
import createMiddleware from 'next-intl/middleware';
import {routing} from './i18n/routing';
 
export default createMiddleware(routing);
 
export const config = {
  // Match all pathnames except for
  // - … if they start with `/api`, `/trpc`, `/_next` or `/_vercel`
  // - … the ones containing a dot (e.g. `favicon.ico`)
  matcher: '/((?!api|trpc|_next|_vercel|.*\\..*).*)'
};
```

---

### 5. Crea `src/i18n/request.ts`:

```ts
import {getRequestConfig} from 'next-intl/server';
import {hasLocale} from 'next-intl';
import {routing} from './routing';
 
export default getRequestConfig(async ({requestLocale}) => {
  // Typically corresponds to the `[locale]` segment
  const requested = await requestLocale;
  const locale = hasLocale(routing.locales, requested)
    ? requested
    : routing.defaultLocale;
 
  return {
    locale,
    messages: (await import(`../../messages/${locale}.json`)).default
  };
});
```

---

## 📂 Estructura del `app router`

### 1. Crea carpeta `src/app/[locale]/`:

Mueve `layout.tsx` y `page.tsx` dentro de esta nueva carpeta.

### 2. Modifica `layout.tsx`:

```tsx
import {NextIntlClientProvider, hasLocale} from 'next-intl';
import {getTranslations} from 'next-intl/server';
import {notFound} from 'next/navigation';
import {routing} from '@/i18n/routing';
import type {Metadata} from 'next';
import '@/app/globals.css';

export async function generateMetadata({
  params
}: {
   params: Promise<{locale: string}>;
}): Promise<Metadata> {
  // Ensure that the incoming `locale` is valid
  const {locale} = await params;

  if (!hasLocale(routing.locales, locale)) {
    notFound();
  }

  const t = await getTranslations({locale, namespace: 'Metadata'});

  return {
    title: t('title'),
    description: t('description')
  };
}
 
export default async function LocaleLayout({
  children,
  params
}: {
  children: React.ReactNode;
   params: Promise<{locale: string}>;
}) {
  // Ensure that the incoming `locale` is valid
  const {locale} = await params;
  if (!hasLocale(routing.locales, locale)) {
    notFound();
  }
 
  return (
    <html lang={locale}>
      <body className='flex-full'>
        <div className='card'>
          <NextIntlClientProvider>
            {children}
          </NextIntlClientProvider>
        </div>
      </body>
    </html>
  );
}
```

---

### 3. Modifica `page.tsx`:

```tsx
import {useTranslations} from 'next-intl';

export default function Home() {
  const t = useTranslations('Home');

  return (
    <div className="min-h-screen flex justify-center items-center text-2xl">
      <h1>{t('text')}</h1>
    </div>
  );
}
```

---

En el caso de componentes asincrónicos `page.tsx`, puedes utilizar la función getTranslations en espera:

```tsx
import {getTranslations} from 'next-intl/server';
 
export default async function HomePage() {
  const t = await getTranslations('HomePage');
  return <h1>{t('title')}</h1>;
}
```

---

## 🧩 Crear y traducir componentes

### 1. Crea `src/components/Header.tsx`:

```tsx
"use client"
import {useTranslations} from 'next-intl';

const Header = () => {
  const t = useTranslations('Header');
  return (
    <header>
      <nav>
        <ul>
          <li className='text-red-600 pb-4'>
            {t('text')}
          </li>
        </ul>
      </nav>
    </header>
  );
}

export default Header;
```

---

> ⚠️ `useTranslations` sólo funciona si está dentro de un `NextIntlClientProvider`.

---

### 2. Envolver componente con proveedor en `page.tsx`:

```tsx
import {useTranslations, NextIntlClientProvider, useMessages} from 'next-intl';
import Header from '@/components/Header';

export default function Home() {
  const t = useTranslations('Home');
  const messages = useMessages();

  return (
    <div>
      <NextIntlClientProvider messages={messages}>
        <Header />
      </NextIntlClientProvider>
      <h1>{t('text')}</h1>
    </div>
  );
}
```

---

### 🎨 Archivo `globals.css`:

```css
@import "tailwindcss";

:root {
  --background: #ffffff;
  --foreground: #171717;
}

@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
  }
}

body {
  background: var(--background);
  color: var(--foreground);
  font-family: Arial, Helvetica, sans-serif;
}

@layer base {
  h1, h2 {
    @apply text-gray-700;
  }
  .flex-full {
    @apply min-h-screen flex justify-center items-center;
  }
  .card {
    @apply flex justify-between items-center gap-3 max-w-2xl text-lg bg-white px-4 py-10 sm:p-14 rounded-lg shadow-lg shadow-slate-700 text-center border border-red-600 mx-2;
  }
}
```

---

Abre tu navegador y accede a **`http://localhost:3000/es`** o **`/en`** para probar los idiomas.

¡Espero que esta guía te sea útil para aprender e implementar proyectos multilenguaje con Next.js!

---

*Fin del documento*