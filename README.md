### Documentation

Node JS, Gemini AI Based RAG Application

## How to setup application ?

```sh
1. Create an API Key using url. (https://aistudio.google.com/app/apikey)
2. Create .env file in the application and add Gemini AI API Key like this:
GEMINI_AI_API_KEY=your api key
3. Execute command in application root 'npm install'
4. Install nodemon package in your machine using command 'npm install -g nodemon'
5. Execute command 'nodemon start'
```

### Search query from C# pdf file added in repository and being used in our RAG application

```sh
1. Open RAG class file added in RAG folder and pass search query provided below in generateOutput method (refer screenshot).
```
![Search Query](https://github.com/user-attachments/assets/2a11e8fb-99dc-490e-81af-a4707a94636d)

### Output

![Search Output](https://github.com/user-attachments/assets/168ceeb9-7ce2-419a-9259-c721aff0f6fa)

## Processing single PDF file (CLI pattern):
```sh
node gemini/RAG.js "How does GC work in C#?" "C#.pdf"
```
# Using the npm script:
```sh
npm run ragrun -- "How does garbage collection work in C#?" "C#.pdf"
```
## Processing multiple PDFs in parallel

```sh
# Example: ask a question, then list files you want to include (absolute or relative paths)
node gemini/Rag-Multiple-Files.js "How does garbage collection work in C#?" "C#.pdf" "Python-Programming.pdf"
```

We can also pass a directory and the script will include all `.pdf` files from that directory:

```sh
node gemini/Rag-Multiple-Files.js "Any relevant info about Python memory management?" ./pdfs
```

If no files are passed as CLI arguments, the script falls back to default sample PDFs located in the repo.

Note: Files will be read in parallel to speed up indexing; errors loading any single file won't stop the whole job — they're logged to the console.

Debugging tip: we can run in "dry-run" mode to verify which chunks are retrieved without calling the AI model:

```sh
# Dry run example (no API key required)
node gemini/Rag-Multiple-Files.js "How does GC work in C#?" "C#.pdf" --dry

# Or using npm script
npm run ragrun-multi -- "How does GC work in C#?" "C#.pdf" -- --dry
```