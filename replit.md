# Smart Terrace Farming System

## Overview

A full-stack web application for sustainable terrace farm management in hilly regions. Helps farmers monitor IoT sensor data and receive smart recommendations for irrigation, fertilizer timing, crop care, and farm management.

## Demo Credentials
- Email: `demo@farm.com`
- Password: `password123`

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + Tailwind CSS
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Auth**: JWT (bcryptjs + jsonwebtoken)
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Charts**: Recharts

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/         # Express API server (JWT auth, all routes)
│   └── smart-terrace/      # React frontend (all 10 pages)
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/                 # Drizzle ORM schema + DB connection
├── scripts/                # Utility scripts (seed.ts)
```

## Features

1. **Authentication** - Register, Login, Logout with JWT
2. **Farm Setup** - Create/edit farm profile (location, soil type, terraces, etc.)
3. **Crop Management** - Add/edit/delete crops with growth stages
4. **Sensor Readings** - Manual entry, demo mode, IoT device endpoint
5. **Dashboard** - Live sensor cards, alerts summary, recommendations
6. **Recommendation Engine** - Rule-based alerts and crop care advice
7. **Alerts** - Severity-based alerts, resolve functionality
8. **Analytics** - Daily/Weekly/Monthly trend charts with Recharts
9. **Device Management** - Register and track IoT devices
10. **Settings/Profile** - View and update user/farm info
11. **Crop Price Analytics** - Manual market price entry, trend detection (rising/falling/stable), SMA-based price prediction (next day + next week), Recharts line chart with forecast overlay, dashboard widget

## IoT Integration

ESP32 devices can POST to `/api/readings/device` with:
```json
{
  "deviceId": "ESP32-001",
  "soilMoisture": 35,
  "temperature": 28,
  "humidity": 62,
  "lightIntensity": 700,
  "waterLevel": 40
}
```

## Database Tables

- `users` - Authentication
- `farms` - Farm profiles
- `crops` - Crop management
- `devices` - IoT devices
- `sensor_readings` - Time-series sensor data
- `alerts` - Generated alerts
- `recommendations` - Smart recommendations

## Root Scripts

- `pnpm run build` — typecheck + build all
- `pnpm run typecheck` — typecheck all packages
- `pnpm --filter @workspace/db run push` — push DB schema changes
- `pnpm --filter @workspace/scripts run seed` — seed demo data
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API client
