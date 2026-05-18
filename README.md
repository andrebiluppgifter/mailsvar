# Biluppgifter Mailutkast (Email Response Drafter)

Internt verktyg för säljteamet på Biluppgifter. När en kund eller potentiell kund mailar med en fråga, klistrar du in mailet här och får ett varmt, affärsfokuserat svar-utkast som driver konversationen framåt mot test-token eller demo.

## Hur det funkar

1. Klistra in kundens mail i textfältet
2. Botten genererar ett utkast på samma språk som inkomna mailet
3. Klicka **Kopiera** ovanpå svaret för att kopiera till urklipp
4. Klistra in i din mailklient, justera om du vill, och skicka
5. Vill du iterera direkt i appen: skriv "gör det kortare", "mer formellt", "byt CTA till demo", etc.

## Designval

- **Ton:** varm account-manager. Inte säljig, inte vag.
- **Format:** ren brevkropp, ingen markdown, max 2-4 stycken.
- **Signatur:** "Vänliga hälsningar, Biluppgifter-teamet" (på engelska: "Best regards, the Biluppgifter team").
- **CTA-logik:** tekniska frågor → erbjud test-token; affärsfrågor → erbjud 15-30 min demo; otydligt → erbjud båda.
- **Eskalering:** mail om klagomål/juridik/GDPR får en varningstext på toppen så att kollegan vet att en jurist eller chef bör titta innan svar skickas.

## Filer

| Fil | Roll |
|---|---|
| `index.html` | Frontend — chat-UI med klistra-in-fält och "Kopiera"-knapp |
| `api/chat.js` | Edge function med system prompt för mailutkast |
| `plate.svg` | Logo (lägg in samma fil som du har i andra appar) |
| `vercel.json` | Vercel-config (tom) |
| `.env.example` | Mall för miljövariabler |
| `.gitignore` | Skyddar hemligheter från repot |

## Deploy

### Steg 1 — Skapa GitHub-repo

1. [github.com/new](https://github.com/new) → namn t.ex. `biluppgifter-reply`
2. Public eller Private — båda funkar
3. Lämna allt omarkerat → **Create repository**

### Steg 2 — Ladda upp filer

1. På den tomma reposidan: klicka **"uploading an existing file"**
2. I Finder: gå till `~/Documents/Claude/Projects/Bot/reply`
3. **Tryck `Cmd+Shift+.` i Finder** så ser du gömda filer (`.env.example`, `.gitignore`)
4. Markera alla filer + `api/`-mappen, dra till webbläsaren
5. **OBS — lägg också in `plate.svg`** (samma som ligger i biluppgifter-qa-repot)
6. Commit changes

### Steg 3 — Importera till Vercel

1. [vercel.com/new](https://vercel.com/new) → hitta `biluppgifter-reply` → **Import**
2. Innan Deploy: expandera **Environment Variables** och lägg till:
   - **`ANTHROPIC_API_KEY`** = din `sk-ant-...`-nyckel
3. Klicka **Deploy**

### Steg 4 — Testa

Öppna URL:en, klistra in en testmail (gärna en riktig från er inbox) och kolla att utkastet ser bra ut. Iterera i chatten om något skaver — det tränar både dig och botten.

## Iterera

System prompten ligger i `api/chat.js` (`SYSTEM_PROMPT`-konstanten). Vill du ändra ton, lägga till segment, anpassa CTA-logiken eller signaturen — ändra där, commita, Vercel auto-deployar.

## Kontakt

Frågor: info@biluppgifter.se
