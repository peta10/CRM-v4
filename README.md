# CRM-v4
Real-Time CRM Dashboard
This repository contains an enterprise-grade, production-ready internal tool example named “Real-Time CRM Dashboard.” It is built using React, TypeScript, Ant Design, GraphQL, Supabase, and other modern libraries. The structure is designed to be easily extended and customized, offering a strong foundation for B2B applications, internal tools, admin panels, dashboards, or any sort of CRUD application.

Directory Structure
pgsql
Copy
Test-CRM-v2-main
└─ Test-CRM-v2-main
   ├─ app
   │  ├─ contracts
   │  │  ├─ loading.tsx
   │  │  ├─ page.tsx
   │  │  └─ [id]
   │  │     ├─ loading.tsx
   │  │     └─ page.tsx
   │  ├─ customers
   │  │  ├─ loading.tsx
   │  │  ├─ page.tsx
   │  │  └─ [id]
   │  │     ├─ loading.tsx
   │  │     └─ page.tsx
   │  ├─ expenses
   │  │  ├─ loading.tsx
   │  │  └─ page.tsx
   │  ├─ globals.css
   │  ├─ layout.tsx
   │  ├─ page.tsx
   │  ├─ reminders
   │  │  ├─ loading.tsx
   │  │  └─ page.tsx
   │  └─ statistics
   │     └─ page.tsx
   ├─ components
   │  ├─ sidebar.tsx
   │  ├─ theme-provider.tsx
   │  └─ ui
   │     ├─ accordion.tsx
   │     ├─ alert-dialog.tsx
   │     ├─ alert.tsx
   │     ├─ aspect-ratio.tsx
   │     ├─ avatar.tsx
   │     ├─ badge.tsx
   │     ├─ breadcrumb.tsx
   │     ├─ button.tsx
   │     ├─ calendar.tsx
   │     ├─ card.tsx
   │     ├─ carousel.tsx
   │     ├─ chart.tsx
   │     ├─ checkbox.tsx
   │     ├─ collapsible.tsx
   │     ├─ command.tsx
   │     ├─ context-menu.tsx
   │     ├─ dialog.tsx
   │     ├─ drawer.tsx
   │     ├─ dropdown-menu.tsx
   │     ├─ form.tsx
   │     ├─ hover-card.tsx
   │     ├─ input-otp.tsx
   │     ├─ input.tsx
   │     ├─ label.tsx
   │     ├─ menubar.tsx
   │     ├─ navigation-menu.tsx
   │     ├─ pagination.tsx
   │     ├─ popover.tsx
   │     ├─ progress.tsx
   │     ├─ radio-group.tsx
   │     ├─ resizable.tsx
   │     ├─ scroll-area.tsx
   │     ├─ select.tsx
   │     ├─ separator.tsx
   │     ├─ sheet.tsx
   │     ├─ sidebar.tsx
   │     ├─ skeleton.tsx
   │     ├─ slider.tsx
   │     ├─ sonner.tsx
   │     ├─ switch.tsx
   │     ├─ table.tsx
   │     ├─ tabs.tsx
   │     ├─ textarea.tsx
   │     ├─ toast.tsx
   │     ├─ toaster.tsx
   │     ├─ toggle-group.tsx
   │     ├─ toggle.tsx
   │     ├─ tooltip.tsx
   │     ├─ use-mobile.tsx
   │     └─ use-toast.ts
   ├─ components.json
   ├─ hooks
   │  ├─ use-mobile.tsx
   │  └─ use-toast.ts
   ├─ lib
   │  ├─ supabaseClient.ts
   │  └─ utils.ts
   ├─ next-env.d.ts
   ├─ next.config.mjs
   ├─ package-lock.json
   ├─ package.json
   ├─ postcss.config.mjs
   ├─ public
   │  ├─ placeholder-logo.png
   │  ├─ placeholder-logo.svg
   │  ├─ placeholder-user.jpg
   │  ├─ placeholder.jpg
   │  └─ placeholder.svg
   ├─ README.md
   ├─ styles
   │  └─ globals.css
   ├─ supabase
   │  └─ migrations
   │     ├─ 20240324_initial_schema.sql
   │     └─ 20250321225113_fancy_peak.sql
   ├─ tailwind.config.js
   └─ tsconfig.json
About
This CRM example demonstrates a Real-Time CRM Dashboard complete with:

Supabase as the backend (authentication, database, and other services)

Secure login/sign-up flows and optional password recovery

GraphQL integration for flexible, efficient data fetching

CRUD operations (companies, contacts, deals, etc.)

Analytics & Charts for high-level overviews of pipelines

A Kanban board for collaborative task management

Responsive design for all devices

Features
Authentication: Secure login, signup, password recovery

Authorization: Granular access control for your data

Dashboard & Charts: Quick metrics and pipeline insights

CRM Modules: Create, read, update, and delete companies, contacts, deals

Task Management: A Kanban-style board for tasks with due dates, multi-assignees, and stage grouping

User Settings: Edit profile information, manage avatars, etc.

Responsive UI: Consistent experience from desktop to mobile

Getting Started (in Cursor or any environment)
Clone the repository:


npm i -D @graphql-codegen/cli \
          @graphql-codegen/typescript \
          @graphql-codegen/typescript-operations \
          @graphql-codegen/import-types-preset \
          prettier \
          vite-tsconfig-paths
<details> <summary><code>graphql.config.ts</code></summary>
ts
Copy
import type { IGraphQLConfig } from "graphql-config";

const config: IGraphQLConfig = {
  // Provide your custom GraphQL endpoint or local schema
  schema: "https://api.your-project.com/graphql",
  extensions: {
    codegen: {
      hooks: {
        afterOneFileWrite: ["eslint --fix", "prettier --write"],
      },
      generates: {
        "src/graphql/schema.types.ts": {
          plugins: ["typescript"],
          config: {
            skipTypename: true,
            enumsAsTypes: true,
            scalars: {
              DateTime: {
                input: "string",
                output: "string",
                format: "date-time",
              },
            },
          },
        },
        "src/graphql/types.ts": {
          preset: "import-types",
          documents: ["src/**/*.{ts,tsx}"],
          plugins: ["typescript-operations"],
          config: {
            skipTypename: true,
            enumsAsTypes: true,
            preResolveTypes: false,
            useTypeImports: true,
          },
          presetConfig: {
            typesPath: "./schema.types",
          },
        },
      },
    },
  },
};

export default config;
</details>
Example Code Snippets
Below are a few brief examples illustrating how certain parts of the CRM might be structured. Feel free to adapt them for your specific needs.

<details> <summary><code>auth.ts</code></summary>
ts
Copy
import { createClient } from "@supabase/supabase-js";

// Example: Initialization of Supabase
const supabase = createClient(
  "https://<YOUR-PROJECT>.supabase.co",
  "<YOUR-ANON-PUBLIC-KEY>"
);

export async function signInWithEmail(email: string, password: string) {
  const { data, error } = await supabase.auth.signInWithPassword({
    email,
    password,
  });
  if (error) {
    throw new Error(error.message);
  }
  return data;
}
</details> <details> <summary><code>graphql/mutations.ts</code></summary>
ts
Copy
import gql from "graphql-tag";

// Example: Update user mutation
export const UPDATE_USER_MUTATION = gql`
  mutation UpdateUser($input: UpdateOneUserInput!) {
    updateOneUser(input: $input) {
      id
      name
      avatarUrl
      email
      phone
      jobTitle
    }
  }
`;

// Example: Create company
export const CREATE_COMPANY_MUTATION = gql`
  mutation CreateCompany($input: CreateOneCompanyInput!) {
    createOneCompany(input: $input) {
      id
      salesOwner {
        id
      }
    }
  }
`;
</details>
Contributing
If you find bugs or want to expand the project, feel free to open pull requests or issues. This codebase can serve as a strong, Supabase-backed CRM foundation.
