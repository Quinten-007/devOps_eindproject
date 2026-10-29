# logboek DevOps eindproject

## 2026-10-29: Git-repository opgezet en gekoppeld aan mijn GitHub 
### Doel
voor ik officieel start aan het project al een versiebeheer omgeving klaarzetten, zodanig dat wanneer ik echt start er geen problemen kunnen opduiken.
### Uitgevoerde stappen
1. Lokale map aangemaakt op host
2. Repository aangemaakt op mijn GitHub
3. Lokale map gekoppeld:
   ```bash
    git init
    git branch -M main
    git remote add origin git@github.com:[user-name]/[repository-name]
   ```
### Resultaat
Repository is bereikbaar op https://github.com/Quinten-007/devOps\_eindproject en de branch `main` volgt `origin/main`. wanneer ik dus vervolgets werk kan ik telkens mijn werk veilig opslaan.

## 2026-10-29: .gitignore toegevoegd

### Doel
Voorkomen dat gevoelige of onnodige bestanden (secrets, sleutels, Terraform-state) per ongeluk in de Git-history terechtkomen.

### Uitgevoerde stappen
1. Gecontroleerd met `ls -a` of er al een `.gitignore` bestond (dat was niet zo).
2. `.gitignore` aangemaakt met regels voor:
   - secrets: `.env`, `.env.*`, `*.key`, `*.pem`, `secrets/`, `*.secret`
   - Terraform: `*.tfstate`, `*.tfstate.*`, `.terraform/`
   - editor- en OS-bestanden: `.vscode/`, `.idea/`, `.DS_Store`, `Thumbs.db`
3. Bestand gecommit en gepusht:
   ```bash
   git add .gitignore
   git commit -m ".gitignore toegevoegd"
   git push
   ```

### Probleem en oplossing
- **Probleem:** `git push` werd geweigerd met `! [rejected] main -> main (fetch first)` omdat ik aanpassingen heb gemaakt in de webiterface van github en niet lokaal eerst een pull heb gedaan.
- **Oorzaak:** `README.md` en `docs/logboek.md` waren rechtstreeks op GitHub aangepast, waardoor de remote een commit bevatte die lokaal ontbrak.
- **Oplossing:** eerst `git pull --no-rebase` uitgevoerd, de merge bevestigd in Vim (`:wq`) en daarna opnieuw `git push`.
- **Les:** altijd eerst `git pull` doen voor het werken, zeker als er ook via de GitHub-webinterface wordt bewerkt.
- **hulpmidel** claude AI voor me te begeleiden de error optelossen.
### Beveiligingsmaatregelen
- `.gitignore` houdt secrets, sleutels en Terraform-state uit versiebeheer.
- Beperking: `.gitignore` werkt enkel voor bestanden die Git nog niet volgt. Een secret die al gecommit is, blijft in de history en moet als gelekt beschouwd en vervangen worden.

### Resultaat
`.gitignore` staat in de repository op `main`, en lokale en remote branch zijn weer gelijk.
