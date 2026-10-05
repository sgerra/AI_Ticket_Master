# AGENTS.md

## Propósito
AI Ticket Manager centraliza los pedidos de soporte, consultas y desarrollos que hoy se gestionan por mail y reuniones.
Usa IA para sugerir categoría, prioridad y área responsable, detectar información faltante y encontrar tickets similares.
La decisión final sobre cada sugerencia siempre la toma una persona; la IA nunca resuelve ni cierra tickets automáticamente.

## Stack
- Frontend: React + Vite
- Backend / DB / Auth: Supabase (proyecto cloud, sin instancia local)
- Lógica de IA: Supabase Edge Functions (Deno) que llaman a la API de Anthropic (Claude)
- Node.js: 22 LTS
- Gestor de paquetes: npm
- Testing: Vitest

## Cómo correr
```
npm install
npm run dev
npx vitest run
```
Deploy de una Edge Function (requiere Supabase CLI logueada y linkeada al proyecto):
```
supabase functions deploy <nombre-funcion>
```

## Qué NO hacer
- No exponer ni usar la API Key de Anthropic desde el frontend: solo se usa dentro de Supabase Edge Functions (RNF-04).
- No permitir que la IA resuelva, cierre o modifique automáticamente los datos definitivos de un ticket: toda sugerencia debe ser aceptada, modificada o rechazada por un usuario (RN-02).
- No enviar respuestas automáticas a usuarios sin revisión humana (fuera de alcance del PRD).
