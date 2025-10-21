---
title: Introduction to Invisible AI
---

So far you've learned how to call an LLM programmatically and how to iterate on your prompt to perform different tasks (text extraction and summarization). Now let's move from basic scripts to features that create genuine value for users so you'll understand Invisible AI techniques - what they are, why users appreciate them, and how to build them with AI SDK + v0.

Let's set aside chatbots for a moment. Some of the most impactful AI features happen when users don't even realize it's there. Smart categorization. Instant summaries. Forms with intelligent assistance. These are the features we're building next.

**Invisible AI** is thoughtful enhancements that make your app easier to use.

## Beyond Chatbots: Subtle Superpowers

Chatbots get much of the attention (we'll build one later!), but AI's real impact often comes from features users don't explicitly notice.

Invisible AI integrates helpful assistance and automation throughout your app and processes.

These features don't advertise themselves; they just work.

The goal is a seamless experience the user simply appreciates.

### Further Reading: Ethics of Subtle AI

When AI is invisible, it raises important ethical considerations about transparency and user agency.

*   [The Ethics of Invisible AI](https://uxdesign.cc/the-ethics-of-invisible-ai-470732142ee5) — Exploring transparency concerns when AI operates behind the scenes
*   [Transparent AI and User Trust](https://www.research.ibm.com/blog/ai-transparency-trust) — Research on balancing seamless UX with appropriate transparency
*   [Designing Ethical AI Experiences](https://pair.withgoogle.com/guidebook/patterns) — Google's People + AI Research guidebook on ethical AI design patterns

## Activation Energy: The Science Behind Great UX

You can think about UX as activation energy. Every form field, every click, every search = friction. It adds up over time sapping users of precious energy and attention.

Invisible AI done well actively reduces that friction. It automates repetitive tasks and makes complex flows feel intuitive. The needs of the user are **anticipated** without directly asking.

For product developers, this approach offers several benefits: less friction = more sign-ups, better conversion rates, fewer support tickets.

## Advancing: From Basic Text to Structured Data

In the last lesson, you used `generateText` for basic text generation. For most invisible AI features you'll be using `generateObject` to generate structured data instead. This approach is powerful and allows you to turn prompts into data that your applications can use.

### Build Your Own Comparison

Now let's build this ourselves. Your template already has starter files with imports and sample data ready.

#### Step 1: Implement Text Extraction

Open `app/(2-invisible-ai)/test-structured.ts`. Inside the `compareOutputs` function, replace the first TODO with a `generateText` example:

```typescript
  // Replace the first TODO with this:
  console.log('\n=== Using generateText (Plain Text) ===\n');
  const { text } = await generateText({
    model: 'openai/gpt-4.1',
    prompt: `Extract all names from this text: ${namesText}`,
  });
  console.log('Raw text output:', text);
  console.log('Output type:', typeof text);
  console.log('Need to parse string to get individual names');
```

#### Step 2: Implement Structured Extraction

Now replace the second TODO with `generateObject`:

```typescript
  // Replace the second TODO with this:
  console.log('\n=== Using generateObject (Structured Data) ===\n');

  const appointmentSchema = z.object({
    title: z.string().describe('The meeting title or subject'),
    date: z.string().describe('The date of the meeting'),
    time: z.string().nullable().describe('The time of the event'),
    location: z.string().nullable().describe('Where the event will take place'),
    attendees: z.array(z.string()).nullable().describe('People attending'),
  });

  const { object } = await generateObject({
    model: 'openai/gpt-4.1',
    prompt: `Parse appointment details from: ${appointmentText}`,
    schema: appointmentSchema,
  });

  console.log('Structured output:', JSON.stringify(object, null, 2));
  console.log('Output type:', typeof object);
  console.log('\nDirect property access:');
  console.log('- Title:', object.title);
  console.log('- Date:', object.date);
  console.log('- Time:', object.time);
  console.log('- Location:', object.location);
  console.log('- Attendees:', object.attendees?.join(', '));
```

#### Step 3: Test Your Implementation

Run your script to see the difference:

```bash
pnpm invisible-ai:compare
```

You'll see:

*   **generateText** returns: "Guillermo, Lee, Sarah" - just a string
*   **generateObject** returns: A typed object with properties you can use directly!

### Build Real Invisible AI Examples

Now let's create practical examples. Open `app/(2-invisible-ai)/invisible-ai-demo.ts`. This file has two functions with TODOs for you to implement.

#### Step 1: Implement Smart Form Filling

In the `smartFormFill` function, replace the TODOs:

```typescript
// Replace the TODOs in smartFormFill with:

// Define the structure we want
const eventSchema = z.object({
  eventTitle: z.string().describe('The title or purpose of the event'),
  date: z.string().describe('The date of the event'),
  time: z.string().nullable().describe('The time of the event'),
  duration: z.string().nullable().describe('How long the event will last'),
  location: z.string().nullable().describe('Where the event will take place'),
  attendees: z.array(z.string()).nullable().describe('People attending'),
  notes: z.string().nullable().describe('Additional notes or agenda items'),
});

// Extract structured data from natural language
const { object: eventDetails } = await generateObject({
  model: 'openai/gpt-4.1',
  prompt: `Extract calendar event details from: "${userInput}"`,
  schema: eventSchema,
});

// Display as if it's a form being auto-filled
console.log('✨ AI automatically fills your form:\n');
console.log(`📅 Event: ${eventDetails.eventTitle}`);
console.log(`📆 Date: ${eventDetails.date}`);
if (eventDetails.time) console.log(`⏰ Time: ${eventDetails.time}`);
if (eventDetails.location) console.log(`📍 Location: ${eventDetails.location}`);
if (eventDetails.attendees) console.log(`👥 Attendees: ${eventDetails.attendees.join(', ')}`);
if (eventDetails.notes) console.log(`📝 Notes: ${eventDetails.notes}`);

console.log('\n✅ Form ready to save - no manual input needed!');
```

#### Step 2: Implement Email Triage (Optional Challenge)

Try implementing the `smartEmailTriage` function on your own! Use a similar pattern with `generateObject` and a Zod schema for email categorization.

>💡 Learning with AI Assistance
>> **New to these prompts?** Throughout this course, you'll find structured prompts you can copy and use with ChatGPT, Claude, or other AI assistants. These help you explore design decisions (like schema choices, error handling strategies) without just giving you the answer. Think of them as guided discovery tools that model good prompt engineering while helping you learn.
>> **For this challenge:** If you're unsure about when to use `.optional()` vs `.nullable()` in your email triage schema, try this prompt:

Prompt: Understanding Zod Optional vs Nullable

```
<context>
I'm building an email triage feature using the Vercel AI SDK with generateObject and Zod schemas.
I need to extract fields like priority, category, and suggested response from user emails.
</context>

<current-schema>
const emailSchema = z.object({
  category: z.string(),
  priority: z.string(),
  suggestedResponse: z.string(), // Should this be optional or nullable?
});
</current-schema>

<question>
What's the difference between `.optional()` and `.nullable()` in Zod schemas?

When should I use each for fields that might not have a value?

Specifically for my email triage case:
- If an email is too complex for auto-response, I want no suggestedResponse field
- Should I use `.optional()` or `.nullable()`?
- How does this affect the AI's output from generateObject?

Explain the difference with code examples showing when each should be used.
</question>
```

This will help you understand the semantic difference and make your schema more robust!

### Test Your Work

Once you've implemented both scripts, run them to see Invisible AI in action:

```
# First, run your comparison to understand the difference
pnpm invisible-ai:compare

# Then see your practical examples
pnpm invisible-ai:demo
```

What You've Built

You've just implemented two key Invisible AI patterns:

1.  **Text vs Structured Output** - You saw how `generateObject` gives you typed, ready-to-use data instead of strings you need to parse
2.  **Smart Form Filling** - Natural language input automatically populates form fields
3.  **Email Triage** (if you did the challenge) - Automatic categorization and prioritization

These patterns are the foundation for countless Invisible AI features!

## You're Already Using Invisible AI. It's Everywhere.

Invisible AI is everywhere:

*   Linear suggesting issue titles? AI.
*   Figma search understanding "blue button"? AI.
*   Gmail smart replies? AI.
*   GitHub Copilot? AI.
*   Analytics showing anomalies? AI.

These features don't scream "AI" - they just feel like good UX enhancing, but not interrupting, your workflows.

## A Quick Review

*   **Invisible AI** = subtle features that make your app easier to use
*   Reduces UX friction (activation energy) and delights users
*   Powered by `generateObject` + Zod schemas for structured data generation

Reflection Prompt

Spotting Invisible AI

What apps do you use with hidden AI features? Identify 1-2 examples. How do they improve UX? How could you build something similar with the AI SDK?

Save Reflection

## Next Up: Building a Classification Engine

Ready to build something practical with Invisible AI? You'll start with auto-classification - automatically routing support tickets, content, and user messages into predefined categories. This pattern applies to countless workflows: customer support, content moderation, email triage, feedback analysis. You'll build a system that takes unstructured user text, organizes it into clear categories using Zod schemas for type safety, and significantly improves support workflow efficiency.

Let's put `generateObject` to work!