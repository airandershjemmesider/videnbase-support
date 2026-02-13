# Permalinks giver 404 fejl

## Problem

Indlæg og sider giver "404 Ikke fundet"-fejl, selvom de eksisterer i WordPress. Forsiden virker muligvis, men alle undersider giver 404. Problemet skyldes næsten altid ødelagte permalinks eller en manglende/korrupt `.htaccess`-fil.

## Løsning

### Trin 1: Gem permalinks igen

Den nemmeste løsning — virker i de fleste tilfælde:

1. Log ind i WordPress admin
2. Gå til **Indstillinger → Permalinks**
3. Du behøver IKKE ændre noget — klik bare **Gem ændringer**
4. WordPress regenererer `.htaccess`-filen automatisk
5. Test at dine sider virker

### Trin 2: Tjek .htaccess manuelt

Hvis trin 1 ikke virker:

1. Forbind via FTP og åbn `.htaccess` i WordPress-roden
2. Filen bør indeholde:
   ```apache
   # BEGIN WordPress
   <IfModule mod_rewrite.c>
   RewriteEngine On
   RewriteBase /
   RewriteRule ^index\.php$ - [L]
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule . /index.php [L]
   </IfModule>
   # END WordPress
   ```
3. Hvis filen er tom, beskadiget eller mangler — opret den med indholdet ovenfor
4. Gem filen og test

### Trin 3: Tjek at mod_rewrite er aktiveret

Permalinks kræver Apache's `mod_rewrite` modul:

1. Kontakt din hostingudbyder og bed dem bekræfte at `mod_rewrite` er aktiveret
2. De fleste hosts har det aktiveret som standard
3. Hvis du bruger Nginx (ikke Apache) — se trin 5

### Trin 4: Tjek filrettigheder på .htaccess

`.htaccess` skal have rettigheder **644**:

1. Via FTP — højreklik på `.htaccess`
2. Vælg **Rettigheder** (Permissions/Properties)
3. Sæt til **644**
4. Gem

Hvis WordPress ikke kan skrive til `.htaccess` (read-only), kan den ikke opdatere permalinks. Sæt midlertidigt rettigheder til **666**, gem permalinks, og sæt tilbage til **644**.

### Trin 5: Nginx-servere (ikke Apache)

Nginx bruger ikke `.htaccess`. Du skal tilføje rewrite-regler i Nginx-konfigurationen:

```nginx
location / {
    try_files $uri $uri/ /index.php?$args;
}
```

Kontakt din hostingudbyder for at tilføje dette — det kræver typisk serveradgang.

### Trin 6: WordPress i undermappe

Hvis WordPress er installeret i en undermappe (fx `ditsite.dk/blog/`):

1. Tjek at `RewriteBase` matcher:
   ```apache
   RewriteBase /blog/
   ```
2. Tjek at **Indstillinger → Generelt** har den korrekte WordPress-adresse og site-adresse

### Trin 7: Custom post types giver 404

Hvis kun brugerdefinerede indholdstyper giver 404:

1. Gem permalinks igen (Indstillinger → Permalinks → Gem)
2. Problemet opstår ofte efter aktivering af et nyt plugin der registrerer custom post types
3. WordPress skal genopbygge rewrite-reglerne

### Trin 8: Tjek for plugin-konflikter

Nogle plugins overskriver permalink-regler:

1. Deaktivér alle plugins
2. Gem permalinks
3. Test om 404-fejlen er væk
4. Aktivér plugins én ad gangen og test

## Bemærkninger

- "Gem permalinks" er den universelle løsning — gør det ALTID som første trin
- Hvis du ændrer permalink-struktur (fx fra "Almindelig" til "Indlægsnavn"), ændres alle URL'er
- Gamle links til den gamle struktur vil give 404 — opsæt redirects med et plugin (fx Redirection)
- Undgå at redigere `.htaccess` manuelt medmindre det er nødvendigt
- Backup `.htaccess` før du ændrer i den
- LiteSpeed-servere bruger `.htaccess` ligesom Apache
