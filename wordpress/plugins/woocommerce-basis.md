# WooCommerce basis-fejlsøgning

## Problem

WooCommerce-webshoppen oplever problemer som:
- Produkter vises ikke korrekt
- Kurv eller checkout virker ikke
- Betalinger fejler
- Ordrer registreres ikke
- Sitet er blevet langsomt efter WooCommerce-installation

## Løsning

### Grundlæggende fejlsøgning

1. **Tjek WooCommerce status:**
   - Gå til **WooCommerce → Status**
   - Fanen **Systemstatus** viser advarsler med rød/gul markering
   - Løs alle kritiske advarsler først

2. **Ryd WooCommerce cache:**
   - Gå til **WooCommerce → Status → Værktøjer**
   - Klik **Ryd transients** og **Ryd kundesesioner**

3. **Opdatér database:**
   - Gå til **WooCommerce → Status → Værktøjer**
   - Klik **Opdatér database** hvis tilgængelig

### Kurv og checkout virker ikke

1. **Tjek sideindstillinger:**
   - Gå til **WooCommerce → Indstillinger → Avanceret**
   - Kontrollér at Kurv, Checkout og Min konto peger på de korrekte sider
2. **Tjek at siderne indeholder de rigtige shortcodes:**
   - Kurv: `[woocommerce_cart]`
   - Checkout: `[woocommerce_checkout]`
   - Min konto: `[woocommerce_my_account]`
3. **Deaktivér cache-plugin midlertidigt** — caching af kurv/checkout giver problemer
4. **Tilføj kurv/checkout som undtagelse** i cache-pluginet

### Betalinger fejler

1. **Tjek betalingsgateway-indstillinger:**
   - Gå til **WooCommerce → Indstillinger → Betalinger**
   - Kontrollér at den ønskede betalingsmetode er aktiveret og korrekt konfigureret
2. **Tjek SSL-certifikat:**
   - Betalingsgateways kræver HTTPS
   - Tjek at sitet kører på `https://` og at certifikatet er gyldigt
3. **Tjek testmodus:**
   - Mange gateways har testmodus — sørg for at den er slået fra i produktion
4. **Tjek logfiler:**
   - Gå til **WooCommerce → Status → Logs**
   - Vælg den relevante gateway-log for fejldetaljer

### Produkter vises ikke

1. **Tjek produktstatus** — er produktet publiceret og ikke i kladde?
2. **Tjek synlighed** — under produktredigering, tjek "Katalogsynlighed"
3. **Tjek lagerstatus** — er produktet på lager?
4. **Flush permalinks** — gå til **Indstillinger → Permalinks** og klik **Gem ændringer**

### Langsomt site med WooCommerce

1. **Brug en cache-plugin** — men ekskludér kurv, checkout og min konto
2. **Optimer billeder** — brug ShortPixel eller lignende
3. **Begræns antal produkter per side** — 12-24 produkter er rigeligt
4. **Deaktivér unødvendige WooCommerce-features:**
   ```php
   // Tilføj i functions.php — deaktivér WooCommerce scripts på ikke-shop-sider
   function fjern_woo_scripts() {
       if (function_exists('is_woocommerce') && !is_woocommerce()
           && !is_cart() && !is_checkout()) {
           wp_dequeue_style('woocommerce-general');
           wp_dequeue_style('woocommerce-layout');
           wp_dequeue_script('wc-cart-fragments');
       }
   }
   add_action('wp_enqueue_scripts', 'fjern_woo_scripts');
   ```

### WooCommerce-mails sendes ikke

1. Gå til **WooCommerce → Indstillinger → E-mails**
2. Tjek at email-skabelonerne er aktiverede
3. Installér et SMTP-plugin (fx **WP Mail SMTP**) for pålidelig mail-levering
4. Test med **WooCommerce → Status → Værktøjer → Send test-email**

## Bemærkninger

- WooCommerce kræver minimum PHP 7.4 (8.0+ anbefales)
- Hold WooCommerce og alle extensions opdaterede — de udgiver ofte sikkerhedsrettelser
- Brug KUN betalingsgateways der er kompatible med din WooCommerce-version
- Test ALTID betalingsflow efter opdateringer (brug testmodus)
- WooCommerce-support-forummet på wordpress.org er en god ressource
