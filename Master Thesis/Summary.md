This is the folder the papers about Artificial Intelligence.

```dataview
LIST Abstract
FROM "Master Thesis/VLM Benchmark Construction"
```
```dataviewjs
const folderPath = "Master Thesis/VLM Benchmark Construction";
const pages = dv.pages(`"${folderPath}"`);

async function extractAbstract(file) {
  const raw = await app.vault.read(file);

  // Match everything after **Abstract**:: until the next bold field or heading
  const regex = /\*\*Abstract\*\*::\s*([\s\S]*?)(?=\n\s*\*\*|#+\s|$)/;
  const match = raw.match(regex);
  return match ? match[1].trim() : null;
}

for (const page of pages) {
  const abstract = await extractAbstract(page.file);
  if (abstract) {
    dv.header(3, page.file.link);     // show note title as link
    dv.paragraph(abstract);           // show multi-paragraph abstract
    dv.el("hr");                      // separator
  }
}
```
