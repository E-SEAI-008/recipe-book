---
  icon: 📖
  title: Project— Recipe Book - NextJS Path
  unit: 
    name: 022 - TypeScript I
    color: pink
  chapter: 
    name: Introduction to TS
    color: red
  type: 
    name: Article
    color: purple
  ft-id: 022.01.001
  pt-id: NA
  objectives: No objectives
  slides: null
  instructorNotes:
    plainText: null
    links: null
---

**Welcome to the NextJS track!** 🎉


This is a 2‑week sprint. Think of us as launching you off a cliff with a jetpack, not holding your hand for every step. You need a rock‑solid foundation from day one to get you blazing fast! 🚀


### Scaffold Your Project


```bash
npx create-next-app@latest
```


This week you are going to learn about TypeScript. If you want to solely focus on the application and framework conventions we recommend using the JavaScript template:


![Screenshot_2025-06-26_at_18.17.06.png](022-typescript-i/introduction-to-ts/images/screenshot2025-06-26at181706-3d79c2a5.png)


When asked about using TypeScript, simply say no.


If you want an extra challenge and integrate TypeScript concepts as you go…say yes.


### If you chose TypeScript


Remember that  JavaScript code is TypeScript compliant you can continue writing your componets as `jsx` files. Once you’re ready to integrate TypeScript gradually (we recommend waiting for the second week of this project), there are some things to consider:

- Your components have to be `.tsx` instead of `.jsx`
- If you are trying to use navigation params in a page, e.g. `/recipes/tacos` or `/recipes/meatballs` you need to type the params as follows:

```typescript
// src/app/[pastaType]/page.tsx
import { notFound } from 'next/navigation';
import pg from 'pg';

const connectionString =  process.env.PG_URI; 

type Pasta = {
  id: number;
  name: string;
  description: string;
};

const PastaType = async ({ params }: { params: Promise<{ pastaType: string }> }) => {
  const { pastaType } = await params;
  const { Pool } = pg;
  const pool = new Pool({
    connectionString
  });
  const { rows } = await pool.query<Pasta>('SELECT * FROM pasta_types WHERE name = $1', [
    pastaType
  ]);
  if (!rows.length) notFound();
  const result = rows[0];

  return (
    <main className='p-4 space-y-4'>
      <h1 className='text-2xl font-bold'>{result.name}</h1>
      <p>{result.description}</p>
    </main>
  );
};
export default PastaType;
```


The reason for the `params` to be typed as a Promise that returns your list of params is because in [NextJS Dynamic APIs are asynchronous](https://nextjs.org/docs/messages/sync-dynamic-apis)


### Additional Resources

- Remember you have a section in this LMS on NextJS!
- [NextJS Docs](https://nextjs.org/docs/app/getting-started/installation)
