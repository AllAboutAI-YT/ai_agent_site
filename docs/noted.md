Add Structured Data (JSON-LD)
If you want to help crawlers (including LLMs) parse your page contextually, embed JSON-LD for schema markup. In the App Router, you can do one of the following:

Option A: Inline in page.tsx
tsx
Copy code
// app/ai-agent/page.tsx

import React from 'react';

export const metadata = {
  title: 'What is an AI Agent?',
  description: 'Learn about AI Agents, their characteristics, and use cases.'
};

export default function AiAgentPage() {
  const jsonLdData = {
    "@context": "https://schema.org",
    "@type": "Article",
    headline: "What is an AI Agent?",
    description: "An overview of AI Agents and their characteristics.",
    author: "Your Name or Company",
    datePublished: "2024-12-30"
  };

  return (
    <main>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLdData) }}
      />
      <h1>What is an AI Agent?</h1>
      {/* ... rest of your content */}
    </main>
  );
}
Option B: head.tsx
Alternatively, create a head.tsx in the same folder for custom <head> content:

markdown
Copy code
app/
  └── ai-agent/
      ├── page.tsx
      └── head.tsx
tsx
Copy code
// app/ai-agent/head.tsx
export default function Head() {
  const jsonLdData = {
    "@context": "https://schema.org",
    "@type": "Article",
    headline: "What is an AI Agent?",
    description: "An overview of AI Agents and their characteristics.",
    author: "Your Name or Company",
    datePublished: "2024-12-30"
  };

  return (
    <>
      <title>What is an AI Agent?</title>
      <meta
        name="description"
        content="Learn about AI Agents, their characteristics, and use cases."
      />
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLdData) }}
      />
    </>
  );
}
Then, Next.js will automatically merge this into the <head> for the /ai-agent route.

3. Link in Your Layout or Navigation
If you have a global layout at app/layout.tsx, you might include a navigation bar or links:

tsx
Copy code
// app/layout.tsx
import './globals.css';
import Link from 'next/link';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        <nav>
          <Link href="/">Home</Link>
          <Link href="/ai-agent">What is an AI Agent?</Link>
        </nav>
        {children}
      </body>
    </html>
  );
}
Now you have a direct link to your new /ai-agent page from anywhere on the site.