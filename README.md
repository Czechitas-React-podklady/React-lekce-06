# React - lekce 6

Tento repozitář obsahuje podklady a cvičení pro 6. lekci kurzu React od Czechitas.

Tentokrát jsou příklady připravené v **samostatných repozitářích** - klikni na odkaz a postupuj dle návodu v repozitáři konkrétního cvičení.

## Události

Události jsou základem veškeré interaktivity na webu. V čistém JavaScriptu jsme s událostmi pracovali tak, že jsme prve na stránce vybrali pomocí `document.querySelector('.selector')` a potom na vybraný prvek přidali událost pomocí metody `addEventListener('click', funkce)`. V Reactu se vyhýbáme přímé manipulaci s prvky, takže tímto způsobem to dělat nebudeme.

V Reactu je to ve skutečnosti mnohem jednodušší. Událost nastavíme danému JSX elementu přímo jako atribut. A obslužnou funkci, která se má při výskytu události zavolat, nadefinujeme přímo uvnitř komponenty.

Pokud například chceme reagovat na kliknutí na tlačítko:
```jsx
const Komponenta = () => {
  const handleClick = () => {
    alert('ahoj');
  };

  return (
    <button onClick={handleClick}>
      Řekni ahoj
    </button>
  );
};
```

Všechny události v Reactu začínají na `on` a pak následuje název události (zapsané jako camelcase), takže máme např. `onKeyDown`, `onMouseEnter`, `onSubmit`, `onChange` a další.

Stejně jako v čistém JaVaScriptu může mít obslužná funkce (tzv. posluchač události) jeden parametr, do kterého prohlížeč předá objekt představující nastalou událost. Tento parametr se obvykle nazývá `event` nebo zkáceně jen `e`. Objekt obsahuje spoustu vlastností popisujících událost, např. vlastnost `target`, ve kterém je uložený prvek, na kterém událost nastala.

Takže např. obsah textového pole můžeme přečíst následovně:

```jsx
const Komponenta = () => {
  const handleChange = (event) => {
    console.log(event.target.value);
  };

  return (
    <input type="text" onChange={handleChange} />
  );
};
```

Už jsme říkali, že v Reactu téměř nikdy nepoužíváme přímou manipulaci s obsahem stránky. Zatím tedy neumíme např. jako reakci na kliknutí změnit text nebo CSS styl nějakého jiného prvku. Zatím jsme omezeni na používání výpisu do konzole nebo vyskakovací okénka `alert`. Se změnou obsahu stránky nám pomůže tzv. **stav**, o kterém si řekneme vzápětí.

### Cvičení na události

- [Cvičení 1 - Události](https://github.com/Czechitas-React-podklady/Cviceni-React-udalosti)

---

## Stav

Pochopit stav v Reactu může být občas výzva, ale význam stavu v Reactu je stejný, jako v reálném okolním světě.

Pokud například prodáváte pohovku, zmíníte v inzerátu její **stav**. Stavem pohovky myslíme sadu vlastností, které pohovka má a které se mohou během její životnosti měnit. Některé vlastnosti se nemění, např. váha nebo to, zda je nebo není pohovka rozkládací. Jiné vlastnosti se mění - např. barva může vyblednout, potah se může prodřít.

Podobně si můžeme představit stav auta. Nemění se velikost nádrže, počet kol. Ale během používání auta se mění počet najetých kilometrů, množství benzínu v nádrži, zda jsou nebo nejsou rozsvícená světla, kolik je v autě zrovna osob, apod.

Podobně si lze představit stav ve webové aplikace, stav jejích komponent. Zaškrtávací políčko může být zaškrtnuté nebo ne. Vysouvací menu může být otevřené nebo zavřené. V eshopu se může stavem rozumnět počet zboží v košíku, v emailové aplikaci např. počet emailů ve schránce, jméno přihlášeného uživatele, text zprávy, kterou má uživatel rozepsanou.

Stav v JavaScriptu si můžeme jednoduše představit jako proměnnou. Např. nádrž ve našem virtuálním autě na začátku cesty:

```jsx
let tankLevel = 'full';
```

Po dlouhé cestě:

```jsx
tankLevel = 'almost empty';
```

Když brzo nenatankujeme, tak:

```jsx
tankLevel = 'empty';
```

### Stav v Reactu a useState

React pro práci se stavem nabízí speciální funkci `useState`. Tato funkce vrátí pole o dvou prvcích. První z nich představuje proměnnou obsahující hodnotu našeho stavu. Druhý prvek v poli představuje funkci, kterou použijeme pro změnu našeho stavu.

Do funkce `useState` jde předat jeden parametr, kterým se nastavuje výchozí hodnota stavu.

```jsx
import React, { useState } from 'react';

const Auto = () => {
  const [tankLevel, setTankLevel] = useState('full');

  return <div className="auto">Tank level: {tankLevel}</div>;
};
```

Když bychom chtěli stav změnit, použijeme funkci, kterou jsme získali z `useState`. Je dobrým zvykem, že tyto funkce začínají slovem `set` a pokračují názvem proměnné se stavem. V našem případě tedy `setTankLevel`, protože náš stav jsme si pojmenovali `tankLevel`.

Chceme změnit stav nádrže:

```jsx
setTankLevel('almost empty');
```

Když se změní stav komponenty, dojde k tzv. přerenderování (překreslení) komponenty. Všude, kde jsme v komponentě použili hodnotu stavu, se změna okamžitě projeví.

### Pravidla pro práci se stavem

- Všimněte si, že funkci `useState` musíme na začátku komponenty naimportovat.
- V komponentě můžeme mít stavů samozřejmě více. Prostě použijeme `useState` několikrát.
- Všechny `useState` se ale při každém překreslení komponenty musí volat ve stejném pořadí - nemůžeme tedy `useState` dávat například dovnitř `if` a někdy ho volat a někdy ne. React by pak nebyl schopen vše správně propojit.
- Funkce pro změnu stavu pojmenováváme `setNazevStavu` - takže např. pro stav `age` to bude `setAge`.

### Příklad na změnu stavu

```jsx
import React, { useState } from 'react';

const Pocitadlo = () => {
  const [pocet, setPocet] = useState(0);

  const handleClick = () => {
    setPocet(pocet + 1);
  }

  return (
    <button onClick={handleClick}>
      Počet kliků: {pocet}
    </button>
  );
};
```

### Cvičení na stav

- [Cvičení 2 - Stav](https://github.com/Czechitas-React-podklady/Cviceni-React-stav)
