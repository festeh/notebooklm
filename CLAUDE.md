# NotebookLM Podcast Generation Workflow

**IMPORTANT:** We generate a SEPARATE podcast for EACH CHAPTER, not one podcast for the entire book.

## PDF Handling

Never use the Read tool for large PDFs. Use the `/pdf` skill instead.

When running PDF skill scripts, use `uv run` to ensure all dependencies are available:
```bash
uv run python .claude/skills/pdf/scripts/<script_name>.py <args>
```

## Stage 1: Book Analysis & Template Generation

1. **User provides book sources** (PDF, URL, or text)

2. **Extract and output chapter list:**
   ```
   Chapters:
   1. Chapter Name
   2. Chapter Name
   ...
   ```

3. **Analyze book** - Understand themes, style, target audience, key concepts

4. **Generate book-specific podcast template** (applies to ALL chapters):
   ```
   Book: <title>
   Podcast Style: <e.g., conversational, deep-dive, beginner-friendly>
   Target Audience: <who this is for>

   Focus Areas:
   - <book-wide theme 1>
   - <book-wide theme 2>

   Content Guidelines:
   - Use insightful analogies to explain complex concepts
   - Discuss tradeoffs and tensions between different approaches
   - Connect ideas to real-world applications

   Core Questions to Address:
   - <recurring question relevant to book's subject>
   - <another key question>

   Episode Structure:
   - <how each chapter podcast should flow>
   ```

5. **Iterate with user** until template is approved

## Stage 2: Automated Podcast Generation

Triggered when user types **START**

**Pre-requisite:** Notebook for the book must already exist on NotebookLM (do not attempt to create it via Chrome extension)

**Podcast Settings:**
- Length: LONG (select "Long" option in NotebookLM)
- Language: English

### Chapter Prompt Construction

**CRITICAL:** Each chapter prompt MUST include BOTH:
1. **Chapter-specific content** - key topics and concepts from that chapter
2. **Template guidelines** - the Content Guidelines from the approved template (analogies, tradeoffs, common mistakes, WHY not just HOW, etc.)

Do NOT just list chapter topics. Always incorporate the stylistic instructions from the template into each prompt.

### Generation Steps

1. For each chapter from the list:
   - Use Claude Chrome extension to interact with NotebookLM
   - In Studio tab, click the **pencil icon** next to "Audio Overview" (not on Audio Overview itself)
   - Set length to LONG, language to English
   - Enter chapter prompt that combines chapter content WITH template guidelines
   - Click Generate
   - Track progress

2. Verify all podcasts generated successfully
