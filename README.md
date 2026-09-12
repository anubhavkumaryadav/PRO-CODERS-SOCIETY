# PRO-CODERS-SOCIETY
Production-grade competitive programming championship platform built with Next.js 15, PostgreSQL, Prisma, Auth.js, TailwindCSS, Framer Motion, shadcn-style primitives, Recharts, Zod, and Cloudinary.
Environment
Create .env from .env.example:

DATABASE_URL=
DIRECT_URL=
AUTH_SECRET=
NEXTAUTH_SECRET=
NEXTAUTH_URL=http://localhost:3000
ADMIN_EMAIL=
ADMIN_PASSWORD_HASH=
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
Use PostgreSQL only. In production, set DATABASE_URL to the pooled Neon connection string and DIRECT_URL to the direct connection string used by Prisma migrations.

Local Setup
npm install
npm run db:generate
npm run db:push
npm run dev
Open http://localhost:3000. The private admin route is /controlroomadmin. The first admin user is bootstrapped from ADMIN_EMAIL and ADMIN_PASSWORD_HASH.

Generate the password hash with:

node -e "const bcrypt=require('bcryptjs'); bcrypt.hash('replace-with-admin-password', 12).then(console.log)"
Neon PostgreSQL
Create a Neon project.
Copy the pooled PostgreSQL connection string.
Set pooled DATABASE_URL and direct DIRECT_URL in .env and Vercel.
Run npm run db:push locally or from a deployment job.
Vercel Deployment
Import the repository into Vercel.
Set all required environment variables.
Use the default Next.js build command: npm run build.
Set NEXTAUTH_URL to the production URL.
Keep AUTH_SECRET and NEXTAUTH_SECRET long, random, and private.
Admin Capabilities
Create, edit, and delete contests through protected admin API routes.
Upload invite posters, contest banners, certificates, profile images, logos, and editorials to Cloudinary.
Import standings from CSV, pasted tables, copied HTML table text, and Codeforces public contests.
Correct ranks, scores, penalties, solved counts, first solves, names, usernames, and years.
Scoring
finalScore = (contestPoints - penalty) + bonusPoints
Bonus points:

1st: +500
2nd: +250
3rd: +125
4th: +50
5th: +25
Society ELO is recalculated from placement, solved count, field size, final score, podium pressure, and first solves.
