# Installér WordPress via cPanel

## Hvad er det

WordPress kan installeres via cPanel enten automatisk med Softaculous (ét-klik installer) eller manuelt. Softaculous er den hurtigste og mest fejlsikre metode.

## Metode 1: Softaculous (anbefalet)

### Trin-for-trin

1. Log ind på cPanel (`https://domæne:2083`)
2. Gå til **Software → Softaculous Apps Installer**
3. Find **WordPress** (typisk øverst eller søg efter det)
4. Klik **Install**
5. Udfyld installationsdetaljer:

#### Software Setup
- **Choose Protocol:** `https://` (kræver SSL — opsæt det først)
- **Choose Domain:** Vælg domænet
- **In Directory:** Lad feltet stå tomt for at installere i roden. Skriv f.eks. `blog` for at installere på `domæne.dk/blog`

#### Site Settings
- **Site Name:** Sidens titel
- **Site Description:** Kort beskrivelse

#### Admin Account
- **Admin Username:** Vælg et unikt brugernavn (ALDRIG `admin`)
- **Admin Password:** Stærkt password
- **Admin Email:** Email til admin-konto og notifikationer

#### Choose Language
- Vælg **Danish** for dansk WordPress

#### Select Theme
- Vælg et tema (kan ændres bagefter i WordPress)

6. Klik **Install**
7. Softaculous viser en bekræftelse med link til site og admin-panel

### Efter installation
- Frontend: `https://domæne.dk`
- Admin: `https://domæne.dk/wp-admin`
- Opdatér WordPress, temaer og plugins med det samme

## Metode 2: Manuel installation

### 1. Download WordPress
- Hent nyeste version fra [wordpress.org](https://wordpress.org/download/)

### 2. Upload filer
- Gå til cPanel → **File Manager**
- Naviger til `public_html` (eller den relevante mappe)
- Klik **Upload** og upload WordPress ZIP-filen
- Højreklik ZIP-filen → **Extract**
- Flyt indholdet af `wordpress/`-mappen til `public_html/` (så `wp-admin` ligger direkte i roden)

### 3. Opret database
1. Gå til cPanel → **Databases → MySQL Databases**
2. **Create New Database:** Angiv et navn (f.eks. `wp_site`)
3. **Add New User:** Angiv brugernavn og password
4. **Add User to Database:** Tildel brugeren til databasen med **ALL PRIVILEGES**

### 4. Kør installationsguiden
1. Åbn `https://domæne.dk` i browseren
2. Vælg sprog
3. Udfyld databaseoplysninger:
   - Database Name, Username, Password
   - Database Host: `localhost`
   - Table Prefix: `wp_` (ændr gerne for sikkerhed, f.eks. `xk2_`)
4. Udfyld site-titel, admin-brugernavn, password og email
5. Klik **Installér WordPress**

## Fil-rettigheder

Korrekte rettigheder efter installation:

| Type | Rettighed |
|------|-----------|
| Mapper | `755` |
| Filer | `644` |
| `wp-config.php` | `640` eller `644` |

Ændr rettigheder i File Manager: Højreklik → **Change Permissions**

## Bemærkninger

- Softaculous kan også automatisk opdatere WordPress (aktivér under **Softaculous → Installations → Edit Details**)
- Ved manuel installation: Slet installationsfilen (`wp-admin/install.php`) efter opsætning
- Installér aldrig WordPress i en mappe der allerede har filer — det kan overskrive eksisterende indhold
- Brug altid HTTPS fra start — det undgår mixed content-problemer senere
