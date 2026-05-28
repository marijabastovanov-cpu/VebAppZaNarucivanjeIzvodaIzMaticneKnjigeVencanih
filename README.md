# Veb App ZaNarucivanje Izvoda IzMaticne Knjige Vencanih
# Veb aplikacija za naručivanje izvoda iz matične knjige venčanih

## Opis projekta

Veb aplikacija razvijena u okviru seminarskog rada iz predmeta **Razvoj višeslojnog softvera**.
Aplikacija je namenjena digitalizaciji procesa zakazivanja venčanja i naručivanja izvoda iz matične knjige venčanih.

Cilj sistema je da omogući korisnicima jednostavnije podnošenje zahteva putem veb forme, dok matičarima i administratorima omogućava pregled, izmenu, brisanje, filtriranje i štampu podataka iz evidencije.

Sistem je realizovan kao višeslojna aplikacija u Visual Studio okruženju, uz korišćenje ASP.NET Web Forms tehnologije, SQL Server baze podataka, stored procedura i posebnih klasa za rad sa podacima, poslovnom logikom i korisničkim interfejsom.

---

## Glavne funkcionalnosti

Aplikacija podržava više tipova korisnika:

### Neprijavljeni korisnik

* pregled osnovnih informacija,
* pristup početnoj stranici aplikacije.

### Venčani par

* prijava na sistem,
* unos podataka o ženi i mužu,
* izbor mesta zaključenja braka,
* unos datuma venčanja,
* unos datuma naručivanja izvoda,
* slanje zahteva,
* odjava iz sistema.

### Matičar

* prijava na sistem,
* pregled evidencije venčanja,
* filtriranje podataka po prezimenu ili broju izvoda,
* detaljna izmena podataka,
* brisanje zapisa,
* parametarska štampa,
* odjava iz sistema.

### Administrator

* prijava na sistem,
* pregled evidencije,
* unos novog mesta u šifarnik,
* administracija korisnika,
* odjava iz sistema.

---

## Tehnologije korišćene u projektu

* ASP.NET Web Forms
* C#
* SQL Server
* Stored procedure
* ADO.NET
* XML konfiguracija
* SOAP Web servis
* Visual Studio
* PowerDesigner modeli

---

## Arhitektura sistema

Sistem je organizovan u više slojeva, pri čemu svaki sloj ima jasno definisanu odgovornost.

### Korisnički interfejs

Sloj korisničkog interfejsa čine ASP.NET Web Forms stranice:

* `Login.aspx`
* `Zakazivanje.aspx`
* `VencanjeSpisak.aspx`
* `DetaljnaIzmena.aspx`
* `MestoUnos.aspx`
* `ParametarskaStampa.aspx`

Ovaj sloj omogućava korisnicima unos, pregled i obradu podataka putem veb forme.

### Prezentaciona logika

Prezentaciona logika sadrži klase koje povezuju korisnički interfejs sa poslovnom logikom:

* `FormaLoginKlasa`
* `FormaVencanjeUnosKlasa`
* `FormaVencanjeDetaljiEditKlasa`
* `FormaMestoUnosKlasa`
* `FormaVencanjeSpisakKlasa`

Ove klase pripremaju podatke za prikaz, validiraju osnovni unos i prosleđuju podatke ka poslovnom sloju.

### Poslovna logika

Poslovni sloj sadrži klase koje obrađuju pravila sistema:

* `ZakazivanjeVencanjaKlasa`
* `VencanjeStatistikaKlasa`
* `ProveraProtokolaKlasa`

Ovaj sloj proverava ispravnost podataka, kapacitet termina i poslovna pravila vezana za zakazivanje i naručivanje izvoda.

### Klase podataka

Sloj podataka obuhvata entitetske klase i klase za rad sa stored procedurama:

* `VencanjeKlasa`
* `MestoKlasa`
* `SPVencanjeDBKlasa`
* `SPMestoDBKlasa`

Ovaj sloj omogućava komunikaciju sa bazom podataka.

### DBUtils

Generički sloj za rad sa bazom sadrži:

* `KonekcijaKlasa`
* `TabelaKlasa`

Ove klase omogućavaju povezivanje sa bazom i osnovne operacije nad podacima.

### Klase mapiranja

Sloj mapiranja sadrži:

* `MaperKlasa`

Ova klasa služi za transformaciju podataka između slojeva aplikacije.

### Web servis

Projekat koristi SOAP Web servis:

* `ServisVencanja.asmx`

Servis se koristi za proveru kapaciteta mesta i čitanje XML konfiguracije.

---

## Baza podataka

Baza podataka sadrži sledeće glavne tabele:

* `KORISNIK`
* `DRZAVA`
* `MESTO`
* `VENCANJE`

Tabela `VENCANJE` predstavlja centralnu tabelu sistema, jer sadrži podatke o bračnom paru, mestu i datumu venčanja, kao i datumu naručivanja izvoda.

Tabela `MESTO` predstavlja šifarnik mesta i povezana je sa tabelom `DRZAVA`.

Tabela `KORISNIK` čuva podatke o korisnicima sistema i njihovim ulogama.

---

## Stored procedure

U projektu se koriste stored procedure za rad sa bazom podataka, kao što su:

* unos novog venčanja,
* izmena podataka o venčanju,
* brisanje zapisa,
* pregled evidencije,
* filtriranje zapisa,
* unos novog mesta,
* provera kapaciteta mesta.

Korišćenje stored procedura omogućava bolju organizaciju SQL koda i jasnije odvajanje baze podataka od aplikacione logike.

---

## Poslovna pravila

Sistem primenjuje sledeća poslovna pravila:

* obavezna polja moraju biti popunjena,
* JMBG mora imati tačno 13 cifara,
* mesto venčanja mora biti izabrano iz šifarnika,
* sistem proverava kapacitet termina za izabrano mesto,
* ako nema slobodnih termina, korisnik dobija odgovarajuću poruku,
* ako su podaci ispravni, zahtev se snima u bazu podataka.

---

## PowerDesigner modeli

U okviru dokumentacije izrađeni su sledeći modeli:

* Business Process Model – tok poslovnog procesa,
* Business Process Model – tok primene softvera,
* Use Case dijagram,
* Komponentni dijagram,
* Konceptualni model podataka,
* Dijagram klasa,
* Dijagrami sekvenci.

Ovi modeli prikazuju strukturu sistema, tokove podataka, interakciju korisnika sa aplikacijom i organizaciju softverskih slojeva.

---

## Struktura projekta

```text
MaticnaKnjigaVencanih/
│
├── KorisnickiInterfejs/
│   ├── Login.aspx
│   ├── Zakazivanje.aspx
│   ├── VencanjeSpisak.aspx
│   ├── DetaljnaIzmena.aspx
│   ├── MestoUnos.aspx
│   └── ParametarskaStampa.aspx
│
├── PrezentacionaLogika/
│   ├── FormaLoginKlasa.cs
│   ├── FormaVencanjeUnosKlasa.cs
│   ├── FormaVencanjeDetaljiEditKlasa.cs
│   ├── FormaMestoUnosKlasa.cs
│   └── FormaVencanjeSpisakKlasa.cs
│
├── PoslovnaLogika/
│   ├── ZakazivanjeVencanjaKlasa.cs
│   ├── VencanjeStatistikaKlasa.cs
│   └── ProveraProtokolaKlasa.cs
│
├── KlasePodataka/
│   ├── VencanjeKlasa.cs
│   ├── MestoKlasa.cs
│   ├── SPVencanjeDBKlasa.cs
│   └── SPMestoDBKlasa.cs
│
├── DBUtils/
│   ├── KonekcijaKlasa.cs
│   └── TabelaKlasa.cs
│
├── KlaseMapiranja/
│   └── MaperKlasa.cs
│
└── KadrovskiPodaci/
    └── ServisVencanja.asmx
```

---

## Pokretanje projekta

Za pokretanje projekta potrebno je:

1. Otvoriti solution fajl u Visual Studio okruženju.
2. Kreirati SQL Server bazu podataka.
3. Izvršiti SQL skripte za kreiranje tabela i stored procedura.
4. Podesiti connection string za povezivanje aplikacije sa bazom.
5. Pokrenuti aplikaciju iz Visual Studio okruženja.

---

## Autor

Seminarski rad iz predmeta **Razvoj višeslojnog softvera**
Tema: **Veb aplikacija za naručivanje izvoda iz matične knjige venčanih**

Autor: **Marija Baštovanov**
Fakultet: **Tehnički fakultet “Mihajlo Pupin”, Zrenjanin**

---

## Napomena

Projekat je izrađen u edukativne svrhe kao primer višeslojne veb aplikacije.
Aplikacija prikazuje osnovni proces digitalizacije rada matične službe i može se dalje proširivati dodatnim funkcionalnostima, unapređenjem korisničkog interfejsa i dodatnim validacijama.
