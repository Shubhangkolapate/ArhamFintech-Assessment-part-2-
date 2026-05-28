Realtime chat example using Supabase
This is a full-stack Slack clone example using:

Frontend:
Next.js - a React framework for production.
Supabase.js for user management and realtime data syncing.
Backend:
supabase.com/dashboard: hosted Postgres database with restful API for usage with Supabase.js.
<img width="1536" height="864" alt="slack-clone-demo" src="https://github.com/user-attachments/assets/99c13f4e-b9d3-4a62-a922-a66a0424481e" />
NOTE: The secret key has full access to your data, bypassing any security policies. These keys have to be kept secret and are meant to be used in server environments and never on a client or browser.

Supabase details
Using a Remote Supabase Project
Create or select a project on Supabase Dashboard.
Copy and fill the dotenv template cp .env.production.example .env.production
Link the local project and merge the local configuration with the remote one:
SUPABASE_ENV=production npx supabase@latest link --project-ref <your-project-ref>
Sync the configuration:
SUPABASE_ENV=production npx supabase@latest config push
Sync the database schema:
SUPABASE_ENV=production npx supabase@latest db push
Vercel Preview with Branching
Supabase integrates seamlessly with Vercel's preview branches, giving each branch a dedicated Supabase project. This setup allows testing database migrations or service configurations safely before applying them to production.

Steps
Ensure the Vercel project is linked to a Git repository.

Configure the "Preview" environment variables in Vercel:

NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY
Create a new branch, make changes (e.g., update max_frequency), and push the branch to Git.

Open a pull request to trigger Vercel + Supabase integration.
Upon successful deployment, the preview environment reflects the changes.
Preview Checks

Role-based access control (RBAC)
Use plus addressing to sign up users with the admin & moderator roles. Email addresses including +supaadmin@ will be assigned the admin role, and email addresses including +supamod@ will be assigned the moderator role. For example:

// admin user
email+supaadmin@example.com

// moderator user
email+supamod@example.com
Users with the moderator role can delete all messages. Users with the admin role can delete all messages and channels (note: it's not recommended to delete the public channel).

Postgres Row level security
This project uses very high-level Authorization using Postgres' Row Level Security. When you start a Postgres database on Supabase, we populate it with an auth schema, and some helper functions. When a user logs in, they are issued a JWT with the role authenticated and their UUID. We can use these details to provide fine-grained control over what each user can and cannot do.

For the full schema refer to full-schema.sql.
For documentation on Role-based Access Control, refer to the docs.
