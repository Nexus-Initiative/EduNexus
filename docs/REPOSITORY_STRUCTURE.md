EduNexus/

│

├── README.md

├── LICENSE

├── .gitignore

│

├── docs/

│   ├── SYSTEM_ARCHITECTURE.md

│   ├── DATABASE_SCHEMA.md

│   ├── DATABASE_RELATIONSHIPS.md

│   ├── USER_ROLES.md

│   ├── PERMISSIONS.md


│   ├── MODULES.md

│   ├── API_DESIGN.md

│   ├── ROADMAP.md

│   ├── DATABASE_LAYERS_MAP.md       

│

├── database/

│   ├── edunexus.dbml               

│   ├── schema.sql                   

│   ├── migrations/

│   │   ├── 001_init.sql

│   │   ├── 002_academic_layer.sql

│   │   ├── 003_finance_layer.sql

│   │   ├── ...

│   │   ├── 010_iam_ai_control_plane.sql

│

├── backend/

│   ├── src/

│   │   ├── modules/

│   │   │   ├── auth/

│   │   │   ├── users/

│   │   │   ├── academics/

│   │   │   ├── finance/

│   │   │   ├── library/

│   │   │   ├── hostel/

│   │   │   ├── communication/

│   │   │   ├── clubs/

│   │   │   ├── opportunet/

│   │   │   ├── ai/

│   │   │   ├── iam/                 

│   │   │   ├── feature-flags/       

│   │   │   ├── ui-engine/

│   │   │

│   │   ├── shared/

│   │   │   ├── middleware/

│   │   │   ├── utils/

│   │   │   ├── database/

│   │   │   ├── security/            

│   │   │

│   │   ├── app.js

│   │   ├── server.js

│   │

│   ├── package.json

│   ├── .env

│

├── frontend/

│   ├── mobile-app/

│   │   ├── android/

│   │   ├── ios/

│   │   ├── shared/

│   │

│   ├── desktop-app/

│   │   ├── electron/

│   │

│   ├── web-app/

│

├── ai/

│   ├── opportunet-engine/

│   ├── recommendation-system/

│   ├── student-insights/

│   ├── chatbot/

│   ├── next-action-engine/          

│   ├── ui-personalization-engine/   

│

├── assets/

│   ├── logos/

│   ├── diagrams/

│   │   ├── edunexus-architecture.svg

│   │   ├── edunexus-architecture.png

│   │   ├── database-layers-v10.svg   

│   ├── screenshots/

│

├── tests/

│   ├── unit/

│   ├── integration/

│   ├── e2e/

│

└── scripts/

├── generate-schema.js

├── seed-database.js

├── sync-ai-models.js
