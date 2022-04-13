**Středoškolská odborná činnost 2022**

#  Fotografický web a administrační systém pro amatérského fotografa

### **Jiří Vala - Student POJFM**

<div style="page-break-after: always;"></div>

### Obsah

1. Vymezení pojmů
2. Úvod a zadání práce
3. Klíčové vlastnosti a požadavky projektu
   1. Serverless architektura
   2. Moderní techstack
      1. Frontend a UI/UX
         1. HTML & CSS a Javascript
         2. React.js
         3. SASS/SCSS

      2. Backend
         1. Node.js
         2. Shell scripty
         3. Firebase

4. Struktura projektu s ohledem na DMP
5. Průběh vývoje
6. Webová prezentace
7. Administrační systém
8. VPS - Virtual Private Server
   1. Operační systém GNU/Linux
      1. Debian 11

   2. Nginx
   3. CI/CD
      1. CI/CD scripty na  VPS

9. Závěr

<div style="page-break-after: always;"></div>

## 1. Vymezení pojmů

1. **DMP** - Dlouhodobá maturitní práce.
2. **CMS** -  Content Management System, v překladu Administrační systém, je systém, který umožňuje manipulaci s daty a obsahem webové stránky či webové (ale i desktopové) aplikace.
3. **Hosting** (webhosting) - Znamená pronájem prostoru na cizím webovém serveru za účelem spuštění webové stránky či aplikace.
4. **Continuous Deployment (CI/CD)** - CI  - Continuous Intergration  a CD - Continuous Delivery je proces, který umožňuje nepřetržité dodávání aktuální verze projektu k testování či produkčnímu spuštění. V praxi to znamená, že pokud tým vývojářů provede změnu a uloží ji do _remote repositáře_ (místo pro ukládání zdrojových kódů v cloudu), tato změna se automaticky projeví (_deployne_) na produkční server (server, na kterém je spuštěna aktuální verze projektu a je poskytována uživatelům z venčí).
5. **Fetching** - Proces během kterého se "_stahují_" data z databáze. Tento anglický výraz doslova znamená "_přinést_".
6. **Backend (server)** - Logická část aplikace nebo webu. Požadavky, které uživatel aplikace provede (například _přejmenování záznamu v databázi_) a data (například _všechny záznamy_), které si vyžádá, tento server nejdříve zpracuje, případně vytáhne z databáze a pak je odešle uživateli aplikace, která je následně zobrazí, či případně upraví v databázi.
6. **Frontend **- Jedná se o grafické uživatelské rozhraní, v rámci webových aplikací a stránek většinou nejčastěji pomocí značkovacího jazyka HTML, stylovacího jazyka CSS a scriptovacího jazyka Javascript.
7. **Cloud Computing Provider** - Poskytovatel cloudových služeb a infrastruktury (serverů).
8. **(Public/Private) API** - API je soubor procedur, funkcí a protokolů zajišťující komunikaci mezi dvěma platformami, které si vzájemně vyměňují data (například dvě rozdílné aplikace). K public API má přístup kdokoliv, k private API jen autentifikovaní uživatele například pomocí unikátního ID tokenu. 
9. **DDOS útok **- Distributed Denial Of Service - je útok jehož cílem je pomocí sítě mnoha virtuálních počítačů, které v jednu chvíli budou provádět požadavky na daný server, vyřadit tento server z provozu, jelikož nezvládne nápor takového počtu požadavků a zhroutí se.
9. **Framework** - Jedná se o podpůrnou softwarovou strukturu, která zjednodušuje vývoj a organizaci projektu v daném jazyce. Může obsahovat další funkce, podpůrné programy nebo vzory a doporučené postupy ve vývoji.
9. **Knihovna** - Jedná se souhrn procedur a funkcí, často avšak také konstant a datových typů, které usnadňují vývojáři práci tím, že může použít již hotový kód. 
9. **Open-source** - Jedná se o projekt s otevřeným zdrojovým kódem, což znamená, že na jeho vývoji se může podílet každý a každý si jej může stáhnout. Popularita open-source projektů v posledních letech velmi roste.
9. **CRUD Operace** - Create, read, update, delete (vytvořit, číst, změnit, smazat) jsou čtyři základní operace se záznamem v databázové tabulce.
9. **Shell** - Jedná se o vrstvu operačního systému, která provádí příkazy a spouští programy.
9. **Pagination** - Jedná se o proces rozdělování obsahu na jednotlivé stránky a podstránky. Nejčastěji ji vidíme ve formě čísel na konci webové stránky.
9. **Dropdown menu** - Jedná se o list záznamů, který se zobrazí až ve chvíli, kdy uživatel nějakým způsobem provede interakci s tímto menu, například kliknutím myši.
9. **Algoritmus** - Proces jednotlivých příkazů za účelem splnění zadaného úkolu.
9. **Push notifikace** - Notifikace, které se zobrazují uživateli na mobilním zařízení v notifikační listě nebo na zamykací obrazovce.

<div style="page-break-after: always;"></div>

## 2. Úvod a zadání práce

Pan Milan Bureš st. (dále jen *fotograf* nebo _zákazník_) je amatérský fotograf, který si již před pár lety nechal na zakázku vytvořit webovou stránku, na které by prezentoval své fotografie, zachycující náhodné okamžiky jeho života. Nicméně postupem času se jeho web i administrační systém stali zastaralými a bylo potřeba celý systém zmodernizovat i vzhledem k faktu, že jeho webová stránka fungovala pomocí Adobe Flash Player, kterému skončila podpora a není již podporovaný moderními prohlížeči.

Proto mě v rámci dlouhodobé maturitní práce zprostředkované mým garantem kontaktoval a požádal, zda-li bych jeho webovou prezentaci nemohl modernizovat. Mým úkolem bylo vytvořit web, který bude sloužit jako virtuální galerie jeho fotografií a bude zobrazitelná a funkční na všech zařízeních, a administrační systém (dále jen _CMS_), který bude umožňovat nahrávání, správu a manipulaci fotografií či alb, ve kterých se jednotlivé fotografie seskupují.

Pro potřeby mé maturitní práce bylo potřeba, aby projekt obsahoval i část jiného předmětu, než jen programování (celý systém jsem naprogramoval) a databáze (data a fotografie, které fotograf nahraje/uloží). Rozhodl jsem se tedy, že si vytvořím vlastní server běžící na operačním systému Linux, na kterém budu _hostovat_ vlastní instanci celého systému a bude obsahovat funkcionalitu tzv. _Continuous Deploymentu_, což přesně kopíruje funkcionality komerční instance projektu určené jen pro účely zákazníka.

<div style="page-break-after: always;"></div>

## 3. Klíčové vlastnosti a požadavky projektu

Během vývoje webové prezentace byl velký důraz kladen na to, aby se co nejvíce podobala stávající verzi. Ne veškeré elementy webu byly replikovatelné a také jsem se chtěl co nejvíce řídit pravidly dobrého webu. Pro porovnání, zde jsou screenshoty jednotlivých webových stránek.

![../](/home/valaj/projects/school/maturita-docs/documents/soc/assets/milanburescz.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.1 -  Fotografova původní webová stránka <br>
    (Zdroj: Autor práce)
</p>
![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/dmp-bures.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.2 -  Mé zpracování webové prezentace<br>
    (Zdroj: Autor práce)
</p>


### 3.1 Serverless architektura

Ačkoliv je samozřejmostí, že je jak webová prezentace tak CMS hostovaná na nějakém fyzickém serveru, k požadavkům jako _fetching_ dat z databáze nepoužívám žádný další (_backend_) server. To znamená, že jsem sice odkázaný kompletně na svého _cloud computing providera_, což je v mém případě Firebase od Google, ale na druhou stranu se nemusím (a ani zákazník) starat o údržbu vlastního serveru a ani jeho prvotní konfiguraci, vše je tzv. _out-of-the-box_ připravené k použití. 

Díky serverless architektuře jsem nemusel vytvářet žádný _backend server_ s _private API_, pomocí kterého bych dostával data z databáze a _cloud storage_ do webové prezentace nebo administračního systému.  

Serverless architektura má mnoho výhod, jedna z těch hlavních a největších je samozřejmě absence potřeby konfigurovat a později spravovat vlastní server, jelikož to kompletně zprostředkovává daný _cloud computing provider_, ale také celková cena _"pronájmu"_ , jelikož ta se počítá podle počtu požadavků na danou službu (napříkad _fetchování_ dat z databáze), bezpečnost, jelikož jsou tyto architektury zabezpečené například proti _DDOS_ útokům, ale také celková škálovatelnost celého systému. _Cloud computing provider_ automaticky škáluje prostředky (úložistě, výpočetní výkon apod.), které jsou k dispozici pro daný systém.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/non-vs-serverless.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.3 -  Graf popisující škálovatelnost jednotlivých architektur<br>
    (Zdroj: Autor práce)
</p>


Na grafu jde vidět, že pokud si zvolíme cestu non-serverless architektury, musíme s narůstajícími požadavky výkon zvyšovat, což ale v praxi znamená dočasné odstavení systému  od provozu a dodatečnou správu hardwaru a tento výpočetní výkon se nemění, pokud se opět nevylepší, zatímco serverless řešení se automaticky škáluje. 

###  3.2 Moderní techstack

Jelikož byla původní webová stránka i administrační systém postavena na poměrně zastaralých technologiích, bylo potřeba modernizovat a během vývoje jsem používal jen ty nejmodernější a mezi vývojáři velmi rozšířené technologie.

#### 3.2.1 Frontend a UI/UX

Jedná se o grafické uživatelské rozhraní, v rámci webových aplikací většinou nejčastěji pomocí značkovacího jazyka HTML, stylovacího jazyka CSS a scriptovacího jazyka Javascript. Nicméně v dnešní době na tyto technologie, které existují delší dobu, existuje mnoho _frameworků_ a _knihoven_, které nejen zjednodušují práci vývojářům, ale také celkově zlepšují _performance_ aplikace či webu, která je díky tomu rychlejší, intuitivnější a použitelnější, což ve výsledku znamená, že například návštěvník webové stránky neztratí zájem, jelikož se stránka nebude dlouze načítat.

UI (user interface - uživatelské prostředí) a UX (user experience - v hrubém překladu uživatelská zkušenost) je sada pravidel a procedur, kterém mají za úkol zjednodušit uživatelskou interakci se systémem tak, aby se uživateli produkt používal co nejsnáze a byl co nejvíce intuitivní. Během vývoje administračního systému jsem se inspiroval návrhem, který jsem našel na designovém webu Dribble.com. 

##### **3.2.1.1 HTML & CSS  a Javascript**

Jedná se o základní technologie, se kterými se dnes vyvíjejí webové stránky či aplikace a všechny ostatní technologie si z nich něco vzaly. 

Základním stavebním kamenem webové stránky i aplikace je HTML dokument, který obsahuje všechny elementy, které má web zobrazovat. 
Tyto elementy nastyluje stylovací jazyk CSS, což znamená, že v CSS dokumentu vybereme jednotlivý HTML element pomocí CSS selektoru a nastavíme mu například jinou barvu, šířku, či například nastavíme animaci, která se spustí po tom, co uživatel přes tento element přejede myší.
Pokud má mít web nějakou funkcionalitu, například po zadaní dvou čísel vypočítat součet, použijeme Javacript. Ten je vlastně logickým mozkem celého webu a stará se o tyto početní operace, získávání dat z databáze a jejich následné vložení do struktury HTML elementu (DOM) nebo interaktivitu s uživatelem .

##### **3.2.1.2 React.js**

React.js je Javascriptový _framework_ vyvíjený firmou Meta (Facebook) a _open-source_ komunitou vývojářů po celém světě a k dnešnímu dni se jedná o nejvíce používaný _framework_ na světě pro jeho jednoduchost a modularitu.

Je optimální pro tvorby _SPA_ (single page aplikací), jako je například administrační systém, protože velmi dobře pracuje s rychle měnícími se daty. Během vývoje react aplikace se celá aplikace rozdělí na jednotlivé komponenty, což má za následek jednoduchý a přehledný zdrojový kód a celou strukturu projektu, což je potřebné u velkého a komplexního projektu a já sám jsem během vývoje pocítil výrazný rozdíl v jednoduchosti vývoje oproti samotného _vanilla_ Javascriptu (bez použití frameworku či knihovny.)

<div style="page-break-after: always;"></div>

```react
// Component -  tento blok kódu mohu použít tolikrát,  kolikrát potřebuji
import React from "react";
import "../style/components/SummaryWidget.css";
class SummaryWidget extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div className="summary-widget">
        <div className="icon">
          <>{this.props.icon}</>
        </div>
        <div className="data">
          <p id="name">{this.props.data_name}</p>
          <p id="value">{this.props.data_value}</p>
        </div>
      </div>
    );
  	 }
}

export default SummaryWidget;
```

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.4 -  Ukázka jednoduché komponenty pomocí frameworku React<br>
    (Zdroj: Autor práce)
</p>



##### **3.2.1.3 SASS/SCSS**

**SASS** je _preprocessor_ stylovacího jazyka CSS, což znamená, že styly psané v SCSS (_sassy css_) zpracuje a  překompiluje to klasického CSS. 
**SCSS** je další z mnoha stylovacích jazyků a jedná se o přímé rozšíření klasického CSS, přidává například proměnné, _nesting_, což znamená, že jednotlivé selektory můžeme psát přímo hierarchicky do sebe a pod sebe, což zlepšuje přehlednost jednotlivých stylů a například tzv. _mixins_, což jsou vlastně bloky stylů, které se dají použít vícekrát, což snižuje počet stylů, které musí vývojář napsat.

<div style="page-break-after: always;"></div>

```scss
.element {
    p {
        color: $mainRed; // Proměnná 
    }
    button  {
        @include submit-btn; // Použítí mixin pomocí jeho unikátního jména
    }
}
```

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.5 -  Ukázka stylování v SCSS<br>
    (Zdroj: Autor práce)
</p>



```css
.element > p  {
    color: #b30e2c
}
.element > button {
    border: solid #b30e2c 1px;
    background-color: #b30e2c;
    color: white;
}
```

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.6 -  Ukázka stylování v CSS<br>
    (Zdroj: Autor práce)
</p>



#### 3.2.2 Backend

Termín _backend_ označuje logickou část aplikace či webu a jeho úkolem je zpracování dat, se kterými uživatel manipuluje na _frontendu_. _Backend_ má většinou na starost správu databází (_CRUD_ operace), správu uživatelů a jejich autentizaci nebo například notifikace například ve formě mailu.  

##### **3.2.2.1 Node.js** 

Node.js je tzv. _runtime_ pro Javascript určený k vytváření vysoce škálovatelných _backend_ aplikací a webových serverů. Toto má společné např. s jazykem PHP, který má stejné zaměření. JavaScript se tedy díky tomuto prostředí dá používat i na serveru a ne jen na druhém konci, u klienta. Avšak na rozdíl např. od zmíněného PHP je v Node.js kladen důraz na vysokou škálovatelnost, tzn. schopnost obsloužit mnoho připojených klientů naráz. Pro tuto vlastnost a vysokou výkonnost je dnes Node.js velmi oblíbený pro tvorbu tzv. API serverů pro klientské single page aplikace rovněž v Javascriptu.  

##### **3.2.2.2 Shell scripty**

Shell scripty jsou sada příkazů, které po spuštění zpracovává a provede _shell_. Význam těchto scriptů v rámci tohoto projektu jsou _CI/CD_ a _DevOps_ Operace, které jsou detailněji popsány v bodu *8.3*.

##### **3.2.2.3 Firebase**

Firebase je _cloud computing provider_ nabízející služby jako hosting webových stránek, hosting databází, ale mnoho dalších jako je například _machine learning_, které však pro mě vzhledem k povaze projektu nejsou důležité. V tomto projektu zajišťuje všechny tyto zmíněné služby a nebýt Firebase, musel bych je všechny řešit sám, například pronájmem dalšího serveru, kde by byly databáze a podobně.
Databáze, které v rámci Firebase využívám, jsou tzv. _Firestore_ a _Cloud Storage_.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/firebaseDash.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.7 -  Nástěnka  projektu ve Firebase Console<br>
    (Zdroj: Autor práce)
</p>


**Firestore** je NO-SQL databáze, což znamená, že jednotlivé záznamy uchovává v datovém typu Objekt, což je _key-value_ datový typ, který slouží pro jednoduché popisování parametru daného předmětu, například člověka. Pro mé účely (ukládání záznamů o jednotlivých albech a fotografiích) je naprosto dostačující, avšak jedinou nevýhodou je, že NO-SQL databáze neumí vytvářet relace mezi jednotlivými tabulkami, tudíž, když jsem chtěl vytvořit relaci mezi albem a jeho fotografiemi, musel jsem v albu vytvořit pole s názvem _connectedImages_ a v něm uchovávat _IDs_ všech těchto fotografií.

<div style="page-break-after: always;"></div>

![image-20220307000221034](/home/valaj/projects/school/maturita-docs/documents/soc/assets/firestore.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.8 -  Firebase Firestore  záznamy jednotlivých alb<br>
    (Zdroj: Autor práce)
</p>


**Cloud Storage** je cloudové úložiště pro všechny typy souborů. Avšak vzhledem k tomu, že by pan fotograf měl nahrávat jen fotografie, ve scriptu, který řídí  nahrávání nových fotografií je implementováno jednoduché ověření, zda li soubor, který se snaží nahrát, doopravdy je typu obrázku/fotky. Nicméně kdyby si to zákazník přál, jsem schopen implementovat i nahrávání souborů jiných, než fotografií.

```js
export const Images = {
  Meta: {
    /**
     * @param {*} File File that is uploaded to `input` element
     * @returns {bool} `true` if the file is type of image
     */
    isImage: (file) => {
      if (file["type"].split("/")[0] === "image") {
        return true;
      } else return false;
    },
  },
    // ... další helper funkce
};

```

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.9  - Ukázka funkce, která zjišťuje, zda je nahraný  soubor typu  image<br>
    (Zdroj: Autor práce)
</p>

<div style="page-break-after: always;"></div>

 ## 4. Struktura projektu s ohledem na DMP

Projekt je rozdělen na dvě částí - komerční a školní (DMP). Co se týče části komerční, všechny služby okolo hostingu a databází bude zprostředkovávat Firebase, jelikož je to v rámci dlouhodobého hlediska nejjednodušší a hlavně nejlevnější řešení. Školní část (DMP) budu zcela spravovat já, tudíž mám pronajatý vlastní server, na kterém budu zprostředkovávat hosting a backend služby, nicméně všechna data budou poskytována a požadována z databází komerční části.

  

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/project_structure.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.10 -  Diagram popisující kompletní strukturu projektu<br>
    (Zdroj: Autor práce)
</p>



<div style="page-break-after: always;"></div>

## 5. Průběh vývoje

Vývoj webové prezentace začal někdy v dubnu roku 2021 a během té doby jsme si se zákazníkem vyměnili nespočet emailů a nespočet telefonních hovorů. A i přesto, že jsem se snažil o co nejvíce _agilní_ vývoj, několikrát se stalo, že po tom co jsme daný _vývojový sprint_ označili za ukončený a já se tak mohl přesunout na další část vývoje nebo další funkcionalitu, zákazník napsal email s tím, že by rád ještě něco změnil, což není až takový problém, nicméně některé z těchto změn byly poměrně velké a znamenaly například přetvoření celého schéma databáze.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/agile_developmnet.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.11 -  Princip agiliního vývoje, který se  odehrává v takzvaných sprintech<br>
    (Zdroj: netmagnet.cz)
</p>



Vývoj obou systémů (webové stránky a adminstračního systému) začal nejprve ve vanilla Javacriptu, což se pro mě jevilo jako nejsnazší řešení, jelikož v té době jsem neuměl ovládat žádný _framework_, který by mi vývoj usnadnil. Čistý Javascript je sám o sobě pro projekt, jako je webová stránka naprosto dostačující a i když bych nyní vývoj začal s _frameworkem_, jako je například Gatsby.js, není to až tak potřeba. Nicméně, jak jsem do administračního systému přidával dál složitější a složitější funkcionality, došel jsem k názoru, že se projekt stává nepřehledným a proto jsem se rozhodl, že celý administrační systém _refaktoruji_ a přepíši pomocí _frameworku_ React.js, který nejen že zvýší celkovou _performance_ a přehlednost nejen struktury projektu, ale i samotného kódu, což se vyplatilo, protože nyní mám přesný přehled o tom, kde co je a jak to funguje.

<div style="page-break-after: always;"></div>

 ## 6. Webová prezentace

Webová prezentace bude panu fotografovi sloužit jako virtuální galerie fotek, aby lidé, které jeho tvorba zajímá, měli všechny jeho fotografie na "dosah ruky" a vzhledem k tehdejší koronavirové situaci je více než vhodné, aby nemuseli chodit přímo na výstavu.

Samotná webová prezentace obsahuje přesně to, co obsahovala ta stávající, tedy, hlavní stránku, na které je jen galerie z alba "Hlavní", jelikož se jedná o fotografie, které se panu fotografovi líbí nejvíce a o kterých si myslí, že by mohly oslovit nejvíce lidí. Po kliknutí náhledovou fotografii se spustí galerie, která avšak nedovoluje rozkliknout informační box s více informacemi o dané fotografii.

Data, které web používá k svému fungování nejsou dynamická, jelikož by to z principu fungování statické webové stránky nemělo smysl. Data se stahují z databáze ve chvíli, kdy uživatel přijde na stránku poprvé. To znamená, že pokud uživatel nahraje novou fotografii, změny na webu se projeví až ve chvíli, kdy uživatel stránku znovu načte. 

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/dmp-bures.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.12 -  Hlavní stránka webové prezentace<br>
    (Zdroj: Autor práce)
</p>



Dále stránku "Úvodem", která slouží jako předmluva pro celý web, který má simulovat umělecké dílo spolu s jeho uměleckými fotografiemi. Tento text je samozřejmě editovatelný v administračním systému.

Odkaz na stránku alba "Nejnovější". Nejedná se o, jak by se mohlo podle názvu zdát, album s fotografiemi, které byly nahrány nedávno, ale o fotografie, které byly nedávno vyfoceny, ostatní alba totiž mohou obsahovat i fotografie, které byly vyfoceny před rokem 2000. To znamená, že se jedná o výběr fotografií, které pan fotograf nedávno vyfotil a rozhodl se, že je bude sdílet. Při vývoji této podstránky jsem musel vymyslet systém, jakým budu fotografie na webu zobrazovat, jelikož si zákazník přál, aby místo galerie, která je použita u všech ostatních alb, byla použita tabulka s náhledy fotografií. Abych tohoto docílil, spolu se správnou _pagination_, musel jsem pole se všemi fotografiemi rozdělit na části po 6 fotografiích a poté je v těchto částech zobrazit na webu. Po kliknutí na náhled fotografie se však otevře galerie, jako u všech ostatních alb.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/album.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.13 -  Galerie po rozkliknutí náhledové fotografie <br>
    (Zdroj: Autor práce)
</p>



_Dropdown menu_ s odkazy na existující alba. Jelikož jsou alba dynamickými prvky v databázi, musel jsem vymyslet způsob, jakým budu vytvářet podstránky jednotlivých alb, nemohl jsem totiž ručně pro každé album vytvořit podstránku pokaždé, co ji uživatel administračního systému vytvoří. Implementoval jsem tedy _algoritmus_, který na základě _id_ obsažené v URL linku alba vytáhne z databáze správný záznam o albu právě pomocí daného _id_.

```js
// This file manipulates with URL query params using which
// we show correct album

// Imports
import { async } from "regenerator-runtime";
import "../css/collections.css";
import { Collections, Images, Storage } from "./core";
import { Gallery } from "../components/gallery";

// Variables
let collectionId = new URL(document.location).searchParams.get("collectionId");
let collectionObject = Storage.getSpecific(collectionId);
const galleryWrapper = document.querySelector("#gallery-wrapper");

document.querySelector(".collectionName").innerText = collectionObject.name;
galleryWrapper.appendChild(new Gallery(collectionObject.images));
```

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.14 -  Ukázka systému  získávání správného alba<br>
    (Zdroj: Autor práce)
</p>



Stránku "Výstavy", která obsahuje seznam všech výstav, na kterých pan fotograf kdy vystavoval své fotografie. Samozřejmě se jedná o editovatelný text.

"Biografie" popisuje dosavadní život pana fotografa společně s jeho fotografií.

V poslední řadě "Kontakt", kde lze najít veškeré kontaktní možnosti. Formulář, který podstránka obsahuje, bude pomocí Firebase Functions posílat email a _push notifikaci_ panu fotografovi vždy, když mu někdo napíše email, aby se nikdy nestalo, že nebude vědět o tom, že mu někdo psal.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/contact.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.15 - Stránka s kontaktním formulářem.<br>
    (Zdroj: Autor práce)
</p>



Jelikož je webová prezentace napsána ve vanilla Javascriptu, v budoucnu mám v plánu ji přepsat pomocí _frameworku_ Gatsby.js, který slouží pro generování statických HTML stránek za použítí React.js, což bude mít za následek nejen mnohonásobně jednodušší budoucí vývoj, ale také rychlejší načítací časy.

<div style="page-break-after: always;"></div>

## 7. Administrační systém

Administrační systém je systém které zprostředkovává manipulaci s daty, které se objevují na dané webové stránce. Jednoduše řečeno, díky administračnímu systému je uživatel schopen své fotografie nahrávat, mazat, upravovat jejich název a popis, stejně tak jako uvidí, která z nich je nejvíce oblíbená na základě _lajků_ a podobně. Dále administrační systém obsahuje funkcionalitu pro manipulaci s alby, do kterých bude uživatel své fotografie rozdělovat. Ty samozřejmě může obdobně vytvářet, mazat a upravovat jejich fotografický obsah. V neposlední řadě systém obsahuje i informační nástěnku, kde je velmi dobře vidět například kolik fotografií je v danou chvíli nahraných na webu a v jakých albech, kolik úložného prostoru jeho fotografie zabírají a nebo třeba seznam posledních nahraných fotografií, aby je nemusel hledat.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/admin.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.16 -  Ukázka nástěnky administračního systému<br>
    (Zdroj: Autor práce)
</p>



Všechny data, se kterými uživatel pracuje, jsou zobrazována v reálném čase, což znamená,  že pokud, například upraví název fotografie, tato změna se ihned projeví jak v samotném administračním systému, tak v databázi a tím pádem i na webové stránce.

Díky Firebase Auth se do systému nedostane uživatel, který **není** autentifikovaný, tedy přihlášený. Prozatím celý autentifikační systém funguje za pomocí emailu a hesla, jelikož web spravuje jeden člověk a není potřeba, abych implementoval například autentifikaci pomocí Google či jiného již existujícího účtu. 
Celá aplikace je "obalená" v auth elemementu, který po úspěšném přihlášení (ověří se, zda uživatel existuje na Firebase Auth serveru) uchovává informace o přihlášeném uživateli a pokud záznam o tomto uživateli existuje, auth element jej pustí dál, jinak bude přesměrován zpět na přihlašovací obrazovku.

Administrační systém obsahuje veškeré nástroje k tomu, aby uživatek mohl manipulovat s fotografiemi a alby, které nahraje a vytvoří. Po nahrání jedné či více fotografií se tyto fotografie objeví na podstránce  "Fotografie" v přehledném seznamu. Kliknutím na jednotlivé fotografie se uživatel dostane na stránku pro manipulaci s jednotlivou fotografií, kde ji může přejmenovat, přidat popis, přiřadit do alba nebo ji z alba odstranit, a nebo fotografii odstranit úplně. Také lze vidět metadata fotografie, jako například kdy byla nahrána, či případně kolikrát ji návštěvníci webové prezentace udělili "lajk".

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/allPhotos.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.17 - Stránka se seznamem všech nahraných fotografií.<br>
    (Zdroj: Autor práce)
</p>



![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/imageManipulator.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.18 - Stránka pro manipulaci  jednotlivé fotografie.<br>
    (Zdroj: Autor práce)
</p>



![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/albums.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.19 - Stránka se všemi aktuálně vytvořenými alby.<br>
    (Zdroj: Autor práce)
</p>

<div style="page-break-after: always;"></div>

## 8. VPS - Virtual Private Server

VPS slouží k realizaci školní části projektu a de facto bude kopírovat veškerou funkcionalitu Firebase. Bude zajišťovat _hosting_ celého projektu pomocí webového serveru nginx, díky kterému bude uživatel moc přistoupit na webovou prezentaci i administrační systém, a _backend služby_, jako například _private API_ pomocí _Node.js_, aby _Github Actions Hook_ mohl provést _HTTP Request_, který spustí _CI/CD_ scripty.

### 8.1 Operační systém GNU/Linux

V dnešní době je jako serverový operační systém nejvíce rozšířený GNU/Linux pro jeho minimalističnost a poměrně jednoduchou konfiguraci. Podle _hostingtribunal.com_ až 96% serverů z 1 milionu celosvětově nejpoužívanějších serverů používá Linux jako svůj operační systém a proto jsem se i já rozhodl použít Linux a nejen z toho důvodu, že jej dennodenně používám.

#### 8.1.1 Debian 11

Jako _cloud computing providera_ pro můj VPS jsem si vybral DigitalOcean, vzhledem k jeho ceně a celkové nabídce se jevil jako nejlepší. Původně jsem na svůj VPS chtěl nainstalovat Arch Linux, jelikož se jedná o Linuxovou distribuci, kterou dennodenně používám, nicméně má jednu velkou nevýhodu - nemá vlastní instalátor (i když nyní již existuje instalační script), což mě osobně při instalaci v domácích lokálních podmínkách vůbec nevadilo, ale v případě instalování Arche na VPS by to znamenalo, že bych musel mít vlastnoručně přizpůsobené _ISO_, které bych použil k instalaci, jelikož DIgitalOcean nenabízí Arch k nainstalování na jejich VPS, které nazývají _Droplets_.

Volba tedy padla na _Debian 11_, jelikož je v jeho minimalistické instalaci poměrně "čistý" a tudíž neobsahuje zbytečné programy a podobně (_bloatware_). Vzhledem k tomu, že tento "počítač" bude sloužit jako server, není potřeba a je až zbytečné instalovat jakékoli desktopové prostředí _GUI_ (Graphical User Interface), jelikož by to mělo nejen za následek zvýšení požadavků na výpočetní výkon serveru, což je nežádoucí, jelikož chceme, aby operační systém serveru zabíral co nejméně prostoru a prostředků, a zároveň celá konfigurace systému je proveditelná jen za pomoci příkazové řádky _CLI_ (Command Line Interface). Na obrázku pod lze vidět, jak _CLI-only_ Debian v _idle_ stavu (stavu, kdy neprovádí žádné operace) zabírá na paměti RAM jen 89MB z dostupných 1GB, tedy necelých 10%.

<div style="page-break-after: always;"></div>

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/VPS.png)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.20 -  Diagnostický  nástroj neofetch zobrazující základní informace o systému po tom, co se na něj připojíme pomocí SSH<br>
    (Zdroj: Autor práce)
</p>



### 8.2 Nginx

Aby hardwarový server mohl poskytovat uživatelům z vnější sítě webové stránky či aplikace, musí na něm běžet softwarový webový server a optimálně _load balancer_, aby nápor uživatelů nepřesáhl výkon serveru. 

Jeho základní výhodou oproti konkurenčnímu webovému serveru Apache je právě zmíněný _load balancing_, díky kterému nginx mnohem lépe zvládá nápor požadavků na server a rovnoměrně rozkládá zátěž.

<div style="page-break-after: always;"></div>

### 8.3 CI/CD

CI (Continuous Integratiaon) a CD (Continuous Delivery) je proces, který umožňuje nepřetržité dodávání aktuální verze projektu k testování či produkčnímu spuštění. V praxi to znamená, že pokud tým vývojářů provede změnu a uloží ji do _remote repositáře_ (místo pro ukládání zdrojových kódů v cloudu), tato změna se automaticky projeví (_deployne_) na produční server (server, na kterém je spuštěna aktuální verze projektu a je poskytována uživatelům z venčí).

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/CICD.jpg)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.21 -  Diagram znázorňující princip fungování CI/CD<br>
    (Zdroj: flagship.io)
</p>



#### 8.3.1 CI/CD scripty na VPS

Po té, co provedu změnu v zdrojovém kódu webové prezentace nebo administračního systému a tuto změnu nahraji pomocí verzovacího systému _git_ do Github repozitáře, je potřeba, aby se tato změna projevila na produkčním serveru. K tomu využiji _shell_ scripty, Github actions hooky a Node.js _API_.  

Celá operace bude probíhat tak, že jakmile _pushnu_ (nahraji) změny do repozitáře, Github Actions zaznamenají, že se snažím o provedení nějaké změny ve zdrojovém kódu a spustí interní script, který provede požadavek (request) na mé Node.js _API_, které zase pro změnu spustí script přímo na VPS, který si _pullne_ (stáhne) nejnovější verzi zdrojového kódu přímo do adresáře s soubory, odkud je poté webový server nginx nabízí uživatelům z vnější sítě.

![](/home/valaj/projects/school/maturita-docs/documents/soc/assets/VPS_clone.svg)

<p style="text-align: center; margin: 0px; line-height: 15px;">
    Obr.22 -  Diagram znázorňující princip stahování poslední změny na lokální úložiště VPS<br>
    (Zdroj: Autor práce)
</p>

<div style="page-break-after: always;"></div>

## 9. Závěr

Během vývoje tohoto projektu jsem se naučil mnoho nových věcí, které věřím, že mě v mém profesionálním životě posunuly dál, a jsem rád, že jsem si jako dlouhodobou maturitní práci vybral právě tento projekt. Mrzí mne však, že jsem začal pozdě s vývojem pomocí _frameworku_ React.js, jelikož bych měl vývoj snazší a neztratil bych čas vyvíjením administračního systému ve vanilla Javascriptu a tím pádem bych se mohl soustředit na důležitější věci, než je opětovné vyvíjení systému, který jsem již jednou vytvořil.
