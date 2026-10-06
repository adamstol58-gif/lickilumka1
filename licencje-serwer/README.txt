SERWER LICENCJI AUTORYNEK  (bot Discord + API dla moda)

WYMAGANIA: Node.js 22 LTS (min. 20.12) - https://nodejs.org
Serwer musi dzialac caly czas (najlepiej tani VPS albo Twoj komputer z przekierowanym portem),
bo mod pyta go o licencje.

1. BOT NA DISCORDZIE
   - https://discord.com/developers/applications -> New Application -> zakladka Bot -> Reset Token (skopiuj)
   - OAuth2 -> URL Generator: zaznacz "bot" + "applications.commands", uprawnienia: Send Messages, Embed Links
     -> otworz wygenerowany link i dodaj bota na swoj serwer.
   - Bot musi widziec kanal licencji i miec na nim prawo pisania.

2. KONFIGURACJA
   - w tym folderze:   npm install
   - skopiuj .env.example na .env i uzupelnij: DISCORD_TOKEN, GUILD_ID, LICENSE_CHANNEL_ID
     (ID kopiujesz prawym klikiem po wlaczeniu Trybu dewelopera w ustawieniach Discorda)
   - wygeneruj klucze:   npm run keys
       * linijke SIGNING_PRIVATE_KEY=... wklej do .env  (TAJNE, nikomu nie pokazuj)
       * klucz PUBLICZNY wklej w modzie: License.java -> PUBLIC_KEY_B64
   - w License.java ustaw tez SERVER_URL, np. http://123.45.67.89:8787/api/validate
     (port z .env, na VPS otworz ten port w firewallu)

3. START:   npm start
   Powinno pokazac "Bot zalogowany" i "Komenda /licencja zarejestrowana".

4. UZYCIE NA DISCORDZIE
   /licencja nick:Steve discord:@kupujacy jednostka:Dni ilosc:30
   /licencja nick:Steve discord:@kupujacy jednostka:Permanentna
   - kod XXXX-XXXX-XXXX-XXXX widzisz od razu (tylko Ty), dostaje go kupujacy w DM,
     a na kanale licencji pojawia sie wiadomosc: nick, kod, kiedy wygasa + przyciski
     [Przedluz licencje] (zielony - wpisujesz np. 7d, 12h, 90m, 30s albo perm)
     [Uniewaznij licencje] (czerwony).
   - Komenda i przyciski dzialaja tylko dla osob z uprawnieniem "Zarzadzanie serwerem"
     (albo dla ID z ADMIN_IDS w .env).

5. W GRZE (kupujacy):   /autorynek licencja XXXX-XXXX-XXXX-XXXX
   Pierwsze uzycie przypisuje kod do jego komputera i nicku. Na innym komputerze - odmowa.
   Gdy kupujacy zmieni komputer: uniewaznij stara licencje i wystaw nowa.

BAZA: data/licenses.json (rob kopie zapasowe).
