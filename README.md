# Golden power: grafici da incorporare

| File | Che cosa contiene |
|---|---|
| `flusso.html` | Diagramma interattivo: come funziona il golden power, con le fasi e gli esiti del 2025 |
| `dashboard.html` | Paesi (blocchi e prescrizioni) e settori, con l'elenco dei casi per ogni barra |
| `index.html` | Pagina di prova che incorpora i due grafici come farebbe il sito |
| `dati.json` | I 182 casi usati dalla dashboard (dati aperti) |

Le pagine non usano librerie esterne. L'unica risorsa esterna è il font Source Serif 4 di Google Fonts.

## 1. Pubblicare su GitHub Pages

1. Accedi a github.com e crea un nuovo repository (pulsante **New**). Chiamalo per esempio `golden-power`, impostalo **Public** e crealo.
2. Nella pagina del repository clicca **Add file → Upload files**, trascina i quattro file di questa cartella e conferma con **Commit changes**.
3. Vai su **Settings → Pages**. In **Build and deployment** scegli **Deploy from a branch**, branch **main** e cartella **/ (root)**, poi **Save**.
4. Dopo uno o due minuti i grafici sono online:
   - `https://cosimofire.github.io/golden-power-/flusso.html`
   - `https://cosimofire.github.io/golden-power-/dashboard.html`
   - `https://cosimofire.github.io/golden-power-/` (pagina di prova)

Per aggiornare un grafico basta modificare o ricaricare il file su GitHub: la versione online si aggiorna in circa un minuto, anche negli articoli dove è già incorporato.

## 2. Incorporare nell'articolo

Nel CMS inserisci un blocco HTML con questo codice, già pronto per l'account CosimoFire:

```html
<iframe src="https://cosimofire.github.io/golden-power-/flusso.html"
        title="Come funziona il golden power"
        style="width:100%;border:0;height:1150px" scrolling="no"></iframe>
```

```html
<iframe src="https://cosimofire.github.io/golden-power-/dashboard.html"
        title="Golden power: paesi e settori"
        style="width:100%;border:0;height:1800px" scrolling="no"></iframe>
```

### Altezza automatica

I grafici comunicano la propria altezza alla pagina che li ospita. Per usarla aggiungi **una sola volta** nella pagina (nel blocco HTML o nel template del sito) questo script:

```html
<script>
window.addEventListener('message', function (e) {
  if (e.origin !== 'https://cosimofire.github.io') return;
  if (!e.data || !e.data.gpEmbed || !e.data.height) return;
  document.querySelectorAll('iframe').forEach(function (f) {
    if (f.contentWindow === e.source) f.style.height = e.data.height + 'px';
  });
});
</script>
```

Se il CMS non permette di inserire script, gli iframe funzionano lo stesso con l'altezza fissa indicata sopra. In quel caso conviene cambiare `scrolling="no"` in `scrolling="auto"`, così il contenuto resta raggiungibile anche quando una lista aperta lo allunga.

## 3. Note

- **Privacy:** il font viene caricato dai server di Google. Se la policy del giornale lo vieta, si possono caricare i file del font nel repository e togliere il link a `fonts.googleapis.com`.
- **Fonte dei dati:** Relazioni al Parlamento sui poteri speciali 2016-2025 (Presidenza del Consiglio dei ministri). La classificazione per settore e l'attribuzione dei paesi sono redazionali.
