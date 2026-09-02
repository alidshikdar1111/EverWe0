# EverWe stability fixes

- Removed the custom Supabase `safeFetch` workaround and restored Supabase's native fetch handling.
- Deferred profile queries triggered by `onAuthStateChange` so they do not run inside the auth callback/lock.
- Made realtime channel cleanup asynchronous and ordered (`unsubscribe` -> `removeChannel`) to avoid teardown races.
- Removed React development StrictMode double-effect execution, which could create duplicate realtime subscribe/cleanup cycles during development.
- Added `.env.example` documenting the two required Vite/Supabase variables without including secrets.

The actual Supabase URL/key must still be supplied by the deployment environment.
