# Concurrently

Run two CLI commands at the same time! 

```bash
npm i concurrently --save-dev
```

## Usage

```json 
  "scripts": {
    "dev": "concurrently \"cd moderator-dashboard && npm run dev\" \"cd main-server && npm run dev\""
  },
```
