# 🐞 Perché i Vostri Bug sono Teoremi Fallaci

Sapete che una ricetta ben scritta può essere perfetta ma non garantisce che il pollo al curry che descrive verrà esattamente come lo presenta la foto nel ricettario? Eppure una ricetta è un algoritmo, dice come fare il piatto passo per passo. Ma c'è una differenza, la ricetta non ha un sistema di tipi abbastanza espressivo. Se la ricetta lo avesse e se il dominio degli oggetti su cui lavora fosse rigoroso allora il piatto verrebbe sempre bene e identico alla foto, in cucina non accade così (per fortuna credo) ma in informatica accade qualcosa di più interessante. E questo qualcosa è una verità cosmica ingiusta che nessuno vi dice e che ...forse... capirete 20 anni dopo aver lasciato l'università. Vi ricordate l'esame di logica? E quello di programmazione? In realtà, ma shhhhh è un segreto... i due professori stanno parlando proprio della stessa cosa, solo che in lingue diverse e con una comunicazione che nella maggior parte dei casi farebbe impallidire la Torre di Babele. Mentre voi freneticamente modificate interi moduli cercando quel maledetto `NullPointerException`, da qualche parte un logico matematico sta tranquillamente scrivendo simboli incomprensibili su una lavagna e fondamentalmente... sta scrivendo il vostro codice. Anzi, sta *dimostrando* il vostro codice.

Questa celebre osservazione, formalmente enunciata nella cosiddetta **Corrispondenza di Curry-Howard** afferma che esiste un isomorfismo perfetto tra:

1. **Programmi tipizzati** (il vostro codice, con i suoi tipi, funzioni e ricorsioni angosciate)
2. **Prove costruttive di teoremi** (quello che Euclide e i suoi epigoni facevano, solo con più rigore e meno "intuitivamente è ovvio")

Quindi quando scrivete un programma **con un sistema di tipi sufficientemente espressivo** state fornendo una costruzione esplicita della dimostrazione di un teorema anche se non semra a prima vista. E non è neanche una di quelle cose che insegnanti entusiasti dicono per rendere la lezione più interessante, ma è un fatto matematico reale e completamente rigoroso.


## Chi Erano Questi Curry e Howard?

Il primo dei duem **Haskell Curry**, fu un logico e matematico americano che, a quanto pare, aveva così tanto tempo libero che decise di studiar come i combinatori logici potessero essere utilizzati in logica proposizionale. Nel suo sistema di combinatori, scoprì una struttura alquanto strana, i combinatori (funzioni particolari) avevano una struttura che assomigliava maledettamente ai tipi di un sistema logico. Era come se il codice e la logica stessero avendo una relazione segreta.

Il secondo ma secondo solo per citazione, è **William Alvin Howard**, un ricercatore che nel 1969 disse essenzialmente: "Ehi, avete notato che i sistemi di tipi del lambda-calcolo (cioè i fondamenti della programmazione funzionale) sono sistemi di deduzione naturale in logica intuizionista?" Non è il tipo di osservazione che vi farebbe guadagnare molti like su Instagram, ma vi cambia completamente la vita, almeno quella matematica.

La Corrispondenza di Curry-Howard, dunque, rappresenta uno dei più straordinari momenti di *unificazione concettuale* nella storia della matematica/informatica, due campi che sembravano completamente indipendenti che si rivelano essere la stessa cosa guardata da angolazioni diverse e se vi sembra poco pensate che è come se si scoprisse che cucinare è la stessa identica cosa che lanciare una pentola dal balcone. Sono due cosa così lontane che nessuno direbbe mai che possano essere la stessa cosa, me nell'identificare questo isomorfismo hanno aperto una porta enorme sullo scibile umano. In un famosissimo libro **Gödel, Escher, Bach: un'eterna ghirlanda brillante**, l'autore, tale Douglas Hofstadter, un genio a mio parere, scrive qualcosa del genere (sto pparafrasando a memoria): "hai capito davvero qualcosa quando riesci a creare un isomorfismo, cioè quando riusciamo a trasformare due concetti nello stesso concetto". Capite perché è così importante?

### L'Isomorfismo Fondamentale

Riassumiamo la struttura della Corrispondenza con una tabellina che farà sembrare le cose improvvisamente semplici (o disgustosamente complicate, a seconda della vostra predisposizione mentale):

| **Concetto di Programmazione** | **Concetto Logico Corrispondente** | **Esempio Concreto** |
|---|---|---|
| **Tipo** `T` | **Proposizione** `P` | Il tipo `Int` corrisponde alla proposizione "esiste un intero" |
| **Programma di tipo** `T` | **Prova della proposizione** `P` | Una funzione che produce un `Int` è una costruzione che *dimostra* che la proposizione `Int` è vera |
| **Funzione di tipo** `A → B` | **Implicazione logica** `A ⊃ B` | Una funzione che prende un `A` e ritorna un `B` è una dimostrazione che "se A, allora B" |
| **Coppia di tipi** `(A, B)` | **Congiunzione logica** `A ∧ B` | Una tupla che contiene un elemento di tipo `A` e uno di tipo `B` è una dimostrazione che "sia A che B sono veri" |
| **Tipo somma** `A ∨ B` (o `Either`) | **Disgiunzione logica** `A ∨ B` | Un valore che è *o* di tipo `A` *o* di tipo `B` dimostra che "almeno uno tra A e B è vero" |
| **Parametro di funzione** | **Ipotesi di deduzione** | Quando una funzione accetta un argomento di tipo `A`, state assumendo che la proposizione `A` è vera |
| **Corpo della funzione** | **Corpo della dimostrazione** | La sequenza di istruzioni costruisce effettivamente la conclusione dalla ipotesi |
| **Terminazione della funzione** | **Terminazione della dimostrazione** | Se la funzione non termina (loop infinito), la "dimostrazione" non arriva mai a conclusione—è invalida |

Tra l'altro la capacità di unificare i concetti è alla base dell'apprendimento automatico, quindi Hofstadter aveva ragione! Una nota, ma secondo voi Leonard Hofstadter di Big Bang Theory l'hanno chiamato così in onore di Douglas Hofstadter? Secondo me si sì!

## La Prova dell'Ovvio

Vi ricordate cos'è una tautologia vero? E' il contrario di una contraddizione, scusate, davvero è una cosa sempre vera, una roba che non conta il vostro punto di vista o quello che pensate sia corretto, una tautologia è sempre vera e una contraddizione è sempre falsa. Ora useremo una la **tautologia identità**, cioè la proposizione `P ⊃ P` ("se P allora P"), per comodità perché ci rende facile il lavoro. In logica questa tautologia si dimostra costruendo la funzione identità:

```haskell
idProof :: P -> P
idProof x = x
```

Qui stiamo dicendo che per dimostrare `P ⊃ P`, basta prendere un'ipotesi della forma P (il parametro `x`) e restituirla e questa è una dimostrazione *costruttiva* perché... NO non stiamo dicendo "è ovvio che se P è vero allora P è vero"... è più rigoroso, è perché stiamo *esibendo esplicitamente* come passare dall'ipotesi alla conclusione. Un logico intuitivo guarderebbe questo codice e direbbe: "Sì, questo è come dimostro `P ⊃ P` nel mio sistema di deduzione naturale". Invece un programmatore guarderebbe una dimostrazione di `P ⊃ P` e direbbe: "Oh, quindi devo scrivere una funzione che prende un argomento e lo restituisce". Sembra che stiano dicendo cose diverse e invece sono la stessa cosa.


## Il Vostro Codice è una Ricetta Logica

Quindi se il vostro compilatore accetta il codice (e parliamo di compilatori sofisticati, non di JavaScript dove potete mettere insieme un intero programma con il rigore di una pizza fatta in casa), allora state costruendo qualcosa che è logicamente valido. Inversamente, **se avete un bug di tipo**, state commettendo un'errore logico perché state provando a dimostrare qualcosa che non è dimostrabile. È come affermare che da una ipotesi P potete derivare una conclusione Q che non segue logicamente e il compilatore producendo quell'errore sta dicendo quello che diceva il vostro professore di logica quando vi bocciava allo scritto perché il vostro teorema era sbagliato. Supponiamo per capirci di avere un sistema di tipi robusto (tipo quello di Haskell, o Idris, o ancora meglio Agda):

```haskell
-- Qui vogliamo dire: "Se la lista non è vuota, allora esiste una testa"
head :: NonEmptyList a -> a

-- Nel sistema di tipi, NonEmptyList è un tipo che incorpora il fatto che la lista non sia vuota
-- Quindi il programma che scrive head non può fallire, perché il tipo stesso garantisce la precondizione
```

Questo cosice sta a tutti gli effetti provando il teorema che segue: "Per ogni lista non-vuota L, esiste un elemento che è la testa di L". E la nostra funzione `head` è la costruzione esplicita di quella prova. Così se il codice compila, il teorema è vero altrimenti il teorema non è dimostrabile con quel sistema di ipotesi (che è diverso da dire che il teorema è falso!).

## I Vostri Bug Sono Teoremi Non-Dimostrabili

Supponiamo di avere un'applicazione web scritta in un linguaggio con un sistema di tipi debole (tipo TypeScript, che è fondamentalmente JavaScript con buone intenzioni). Avete scritto qualcosa come:

```typescript
function getUserEmail(userId: number): string {
  // Otteniamo l'utente dal database
  const user = database.getUser(userId);
  // Estraiamo l'email
  return user.email;  // CRASH! Se user è null, questo fallisce
}
```

Da un punto di vista della Corrispondenza di Curry-Howard il codice cerca di provare che per ogni user ID, esiste un'email associata, ma il vostro sistema di tipi non è abbastanza rigoroso da forzarvi ad affrontare il fatto che `getUser` potrebbe ritornare `null` (cioè, che il teorema potrebbe essere falso per alcuni input). Ma il compilatore non protestavperché TypeScript ha una nozione molto ottimistica di "correttezza" anche se logicamente, state affermando un teorema che non è universalmente vero, solo sperando che non vi venga mai assegnato un userId per cui non esiste un utente. È come affermare che per ogni numero naturale n, esiste un numero primo p > n senza fornire alcuna costruzione, lo dice e sperate che sia vero perché solo perché è intuitivamente plausibile... ma questo è disastroso e si fa la fine del tacchino induttivista che vi racconterò un'altra volta. Invece in un linguaggio con un sistema di tipi più robusto, come Haskell:

```haskell
getUserEmail :: Integer -> Maybe String
getUserEmail userId = do
  user <- database.getUser userId  -- Questo ritorna Maybe User
  return (user.email)
```

Qui state dicendo che per ogni user ID, *potrebbe* esserci un'email (o potrebbe non esserci)... infatti il tipo `Maybe String` codifica esplicitamente l'incertezza. Non potete restituire un `String` puro ma dovete avvolgere il risultato nel costruttore `Just` se l'email esiste, oppure ritornare `Nothing`. Qui il compilatore vi costringe a gestire entrambi i casi per forza... e a questo punto state provando che per ogni user ID, o esiste un'email, o non esiste e questo è effettivamente provabile (il vostro codice lo dimostra), e il compilatore infatti vi fa compilare.


### La Lezione Pratica

Ecco dunque una lezione pratica che nessun corso vi darà esplicitamente, il vero significato della Corrispondenza di Curry-Howard nel mondo reale:

> **Un sistema di tipi sufficientemente espressivo è una macchina per trasformare i vostri bug in errori di compilazione.**

Più il vostro sistema di tipi è ricco (cioè, più proposizioni logiche potete esprimere), più cose il compilatore può provare circa la correttezza del vostro codice e quindi più i vostri programmi saranno robusti e immuni a bug.

**Nota:**

E potete anche vederla dal punto di vista della semantica assiomatica perché se un algoritmo è una dimostrazione costruttiva allora una precondizione è un'ipotesi perché quando dite "questa funzione richiede che l'input non sia nullo," state assumendo che l'input non sia nullo e dimostrate che il risultato è ben definito. E quando provate che un ciclo mantiene una proprietà, beh, state dimostrando un lemma che supporta la dimostrazione più grande della correttezza dell'algoritmo, quindi un invariante di ciclo è un lemma intermedio del teorema.


## Per i Masochisti Intellettuali

Abbiamo visto che la corrispondenza collega la logica proposizionale con il lambda calcolo tipizzato semplice, la corrispondenza è stabilita come segue:

- Ogni proposizione P corrisponde a un tipo τ
- Ogni prova di P corrisponde a un termine (programma) di tipo τ
- Ogni regola di deduzione logica corrisponde a una regola di formazione dei tipi

Ad esempio, la regola logica:
```
Γ ⊢ P → Q    Γ ⊢ P
━━━━━━━━━━━━━━━━━━━
        Γ ⊢ Q
```

"se abbiamo una prova di P → Q e una prova di P, allora abbiamo una prova di Q, corrisponde  alla regola di applicazione di funzione:
```
Γ ⊢ f : σ → τ    Γ ⊢ e : σ
━━━━━━━━━━━━━━━━━━━━━━━━━━━
      Γ ⊢ f e : τ
```

cioè se abbiamo una funzione che mappa σ in τ, e un'espressione di tipo σ, applicandola otteniamo un valore di tipo τ, sono *letteralmente lo stesso sistema formale*, solo con una notazione diversa.

Se invece vogliamo dimostrare teoremi più interessanti, servono quantificatori universali (`∀x. P(x)`) e esistenziali (`∃x. P(x)`). Questi corrispondono a:

- **Quantificazione universale** <--> **Funzioni polimorfe** (funzioni che funzionano per *qualsiasi* tipo)
- **Quantificazione esistenziale** <--> **Tipi esistenziali** (cioè, "esiste un tipo T tale che...")

Una funzione polimorfa come:

```haskell
length :: forall a. [a] -> Int
```

In realtà sta dicendo: "Per *tutti* i tipi `a`, una lista di `a` ha una lunghezza che è un intero" e questo è isomorfo al teorema `∀a. List(a) → Int`.

Ma possiamo andare più lontano qui la Corrispondenza di Curry-Howard, nella sua forma originale, corrisponde alla **logica intuizionista**. Ma qual è la differenza? Nella logica classica, vale il principio del terzo escluso che ci dice che per ogni proposizione P, è vero che `P ∨ ¬P` (o P è vero, o la sua negazione è vera). Nella logica intuizionista, questo non è accettato come un assioma e si deve costruire esplicitamente una prova di P o una prova di ¬P. Quindi perché un programma è una costruzione esplicita? Non si può dire dire che il risultato è vero o falso, ma non vi dico quale, serve produrre un valore effettivo, che codifica quale sia la risposta. Quindi la logica classica si adatta a dimostrazioni che ammettono il terzo escluso mentre la logica intuizionista si adatta a programmi che devono necessariamente ritornare un risultato esplicito

Se tentaste di scrivere una funzione con il seguente tipo:

```haskell
mysterium :: P -> (P ∨ ¬P)
```

Per dire dato P, dimostrami che o P è vero o P è falso, non potreste farlo in logica intuizionista senza sapere effettivamente cosa sia P. In logica classica, potremmo tranquillamente affermare "bene, uno dei due è vero, per il terzo escluso." Ma in un linguaggio di programmazione tipizzato (che segue la logica intuizionista), dovete costruire il valore di ritorno specificando che è o un `Left (x : P)` oppure un `Right (f : P -> False)`. Non potete semplicemente ondeggiare la mano e magicamente dire che uno di questi esiste.

## Esempio 1

Supponiamo di voler provare il seguente teorema algebrico: per tutti i numeri naturali a, b, c, vale che `(a + b) + c = a + (b + c)`.

In logica, scriveremmo:
```
∀a, b, c : ℕ. (a + b) + c = a + (b + c)
```

Come codifichiamo questa proprietà nel nostro sistema di tipi? Con un tipo che rappresenta l'**uguaglianza**:

```haskell
data Eq (a : Type) (x y : a) : Type where
  Refl : Eq a x x
```

Il tipo `Eq a x y` rappresenta "una prova che x e y sono uguali nel tipo a". L'unico costruttore è `Refl`, che dice "se x e y sono sintatticamente identici, allora sono uguali". Ora, la dimostrazione dell'associatività dell'addizione diventa un programma:

```haskell
plus_assoc : ∀ (a b c : ℕ) -> Eq ℕ ((a + b) + c) (a + (b + c))
plus_assoc zero b c = Refl
plus_assoc (succ a) b c = 
  let ih = plus_assoc a b c  -- ipotesi induttiva
  in cong succ ih
```

(dove `cong` è una funzione che dice "se x = y, allora f(x) = f(y)")

Cosa succede qui? Qui stiamo scrivendo un programma che, per ogni scelta di a, b, c, costruisce una prova che le due espressioni sono uguali e il programma segue la struttura di un'induzione matematica dove il caso base è quando a = 0 e passo induttivo quando a = succ(a'). Se il programma compila, avete appena provato formalmente un teorema di algebra, pazzesco vero? Non è una dimostrazione scritta su carta, è un programma che il compilatore ha verificato essere logicamente coerente ma sono la stessa cosa.

#### Esempio 2

Un altro esempio classico è il tipo delle liste non-vuote, in un sistema di tipi sufficientemente espressivo (tipo Idris con **dependent types**), potete definire:

```agda
data List⁺ (a : Type) : Type where
  [_] : a -> List⁺ a
  _∷_ : a -> List⁺ a -> List⁺ a
```

Questo tipo è una lista che contiene almeno un elemento, cioè logicamente, il tipo `List⁺ a` significa "una lista di almeno un elemento di tipo a." Ora, potete scrivere:

```agda
head : {a : Type} -> List⁺ a -> a
head [ x ] = x
head (x ∷ _) = x
```

Ora questa funzione è totale (non può generare un errore di runtime) perché il tipo di input `List⁺ a` garantisce che la lista non è vuota e non serve gestire il caso di lista vuota, perché è impossibile passare una lista vuota a questa funzione. Questo è come provare cje se L è una lista non vuota di elementi di tipo a, allora esiste un elemento di tipo a che è la testa di L. La vostra funzione `head` è la costruzione esplicita che estrae questo elemento.

#### Esempio 3

Uno degli usi più sofisticati della Corrispondenza di Curry-Howard è la formalizzazione delle **monadi**. Una monade è un'astrazione che codifica un "contesto computazionale", tipo, computazioni che potrebbero fallire, o computazioni che hanno uno stato, o computazioni che fanno IO.

Consideriamo la monade `Maybe`, che codifica "una computazione che potrebbe non produrre un risultato":

```haskell
data Maybe a = Just a | Nothing

class Monad m where
  return :: a -> m a
  (>>=) :: m a -> (a -> m b) -> m b
```

La struttura monadica corrisponde a un sistema di gestione delle proposizioni il cui valore di verità è contingente (cioè, dipendente da circostanze esterne). Quindi quando scriviamo qualcosa come:

```haskell
do
  user <- getUser userId      -- Maybe User
  email <- getEmail user      -- Maybe String
  return email                -- Maybe String
```

Stiamo costruendo una catena di inferenze dove ognuna dipende dal risultato della precedente, ma tutte sono contingenti nel senso che potrebbero fallire. Il sistema monadico ci assicura che se una qualsiasi computazione ritorna `Nothing`, l'intero risultato sia `Nothing`. Se usate JavaScript, TypeScript senza modo strict, o simili, state dicendo che non volete che il compilatore verifichi che il mio codice sia logicamente coerente. Da una prospettiva della Corrispondenza di Curry-Howard, questo è *affascinantemente* sciocco. Vuol dire che state rinunciando alla possibilità di avere il vostro compilatore che vi aiuta a provare che il vostro codice è corretto e JS lo permette perchè usa un sistema di tipi deboli che dal punto di vista della logica, sono sistemi dove potete affermare proposizioni senza provare che siano vere.

## Dependent Types

Se volete prendere la Corrispondenza di Curry-Howard al suo massimo livello dovete entrare nel territorio dei tipi che dipendono da valori in fase di runtime, i cosidetti **dependent types**. Un esempio classico:

```agda
data Vec (a : Type) : Nat -> Type where
  [] : Vec a zero
  _∷_ : {n : Nat} -> a -> Vec a n -> Vec a (succ n)
```

Qui, `Vec a n` è un vettore di elementi di tipo a che ha n elementi e la lunghezza è parte del tipo stesso, quindi con i dependent types, potete scrivere funzioni come:

```agda
safeIndex : {n : Nat} -> Vec a n -> (i : Nat) -> i < n -> a
safeIndex (x ∷ xs) zero _ = x
safeIndex (x ∷ xs) (succ i) prf = safeIndex xs i (prf_pred prf)
```

In questo modo la funzione `safeIndex` richiede una prova che l'indice sia valido come parte dell'argomento.......... da finire.... qui il codice è una dimostrazione che tiene conto di proprietà arbitrarie che decidete siano importanti. Si potrebbe dire che tutto questo è una enorme perdita di tempo perché il codice può comuqnue essere sbagliato. Ovvio che può essere sbagliato! La Corrispondenza di Curry-Howard garantisce la correttezza logica, non la correttezza della specifica. Se scrivete:

```haskell
-- Calcola la somma di due numeri
sum :: Int -> Int -> Int
sum a b = a * b  -- Oops, moltiplica invece di sommare
```

Il tipo è corretto ma se non è quello che intendete fare è un problema del programmatore che non sapeva cosa volesse fare. La Corrispondenza di Curry-Howard dice che se il codice compila, è una dimostrazione valida della proposizione codificata dal tipo ma non dice che è una dimostrazione della proposizione che intendevamo dimostrare. Per evitare questo problema, dovete essere più espliciti nella vostra specifica:

```haskell
-- Dimostriamo che sum(a, b) = a + b per induzione
sum_correct : ∀ a b -> sum a b = a + b
sum_correct a b = sorry  -- Se completate questa dimostrazione, avete provato che sum è corretta
```

E' chiaro che con un linguaggio come Python o Go potete scrivere ottime applicazioni web, interfacce utente, ecc, anche se hanno sistemi di tipi modesti però, avete rinunciato a una classe di bug che il compilatore avrebbe potuto catturare. Se scrivete in Rust, non dovrete mai preoccuparvi di dangling pointers o data races. Se scrivete in Haskell, non dovrete mai combattere con effetti collaterali nascosti che rendono il codice hard-to-reason-about. Il punto non è  che più il vostro sistema di tipi vi consente di esprimere proprietà del codice, più il compilatore può aiutarvi a verificare la correttezza e più il vostro codice sarà affidabile.


## Il Lato Oscuro: Ciò Che Non Potete Provare

Gödel ci ha detto, nel 1931, che in ogni sistema formale sufficientemente potente, esistono proposizioni vere che non possono essere provate all'interno del sistema stesso quindi **esistono programmi "corretti" (nel senso che fanno quello che dovrebbero fare) la cui correttezza non può essere provata all'interno del sistema di tipi. Ad esempio, considerate un algoritmo di ordinamento, potete provare che l'algoritmo termina? Non sempre, a meno che il vostro sistema di tipi non supporti tipi dipendenti sofisticati. Potete provare che produce un risultato ordinato? Di nuovo, dipende dal vostro sistema.

Quindi non esiste e non può esistere un sistema di tipi perfetto e non potete incapsulare ogni proprietà logica di interesse nel vostro tipo. A un certo punto, dovete scendere a compromessi, accettare che alcuni invarianti devono essere verificati a runtime (o peggio, affidati al test), e ammettere che il vostro compilatore ha limiti. Ma nonostante questi limiti, la Corrispondenza di Curry-Howard rimane uno dei regali più straordinari che l'informatica teorica abbia offerto alla pratica. 

Se siete a un seminario e un professore presuntuoso afferma che "la programmazione e la matematica sono discipline completamente diverse e non dovrebbero mai incontrarsi," voi potete tranquillamente rispondere:

> "In realtà, la Corrispondenza di Curry-Howard ci mostra che un programma tipizzato è esattamente una dimostrazione costruttiva di un teorema. Non sono discipline diverse, sono la stessa cosa guardata da angolazioni sintattiche differenti. Se lei ritiene che la programmazione non sia matematica, allora sta implicitamente rifiutando una delle più profonde scoperte dell'informatica teorica dell'ultimo mezzo secolo."

Detto con un sorriso educato, naturalmente. I professori sono sensibili.

---

## Per i Veramente Ossessionati

Considerate la classica funzione `map`, che applica una funzione a ogni elemento di una lista:

```haskell
map :: (a -> b) -> [a] -> [b]
map f [] = []
map f (x:xs) = f x : map f xs
```

Quale teorema stiamo provando qui? Apparentemente, stiamo provando:

> "Se esiste una funzione che trasforma elementi di tipo a in elementi di tipo b, allora esiste una funzione che trasforma liste di a in liste di b."

In realtà stiamo provando un'istanza di uno dei lemmi più fondamentali della teoria delle categorie, il **funtore identità preserva la struttura**. `map` è una trasformazione naturale che rispetta la struttura di liste. Se aggiungiamo ai nostri tipi delle proprietà più sofisticate, tipo, che vogliamo provare che map preserva la lunghezza della lista—arriviamo a un teorema più ricco:

```haskell
map_preserves_length : ∀ (a b : Type) (f : a -> b) (xs : [a]) ->
                       length (map f xs) = length xs
map_preserves_length f [] = Refl
map_preserves_length f (x:xs) = 
  cong (\l -> 1 + l) (map_preserves_length f xs)
```

Qui stiamo provando, per induzione, che applicare una funzione a ogni elemento di una lista non cambia la lunghezza della lista stessa. È un teorema elementare, ma la sua struttura illustra come il sistema di tipi catturi le invarianti matematiche.

Ora un'osservazione ancora più sofisticata, le **monadi**, queste sappiamo che sono strutture categorie che catturano pattern comuni di computazione. In logica, una monade corrisponde a un'estensione del sistema di tipo che vi consente di ragionare su computazioni con contesto e quando scrivete:

```haskell
do
  x <- m_a
  y <- m_b x
  return (f x y)
```

Stiamo costruendo una dimostrazione sequenziale dove ogni passo dipende dal risultato del precedente, la struttura monadica vi consente di formalizzare il ragionamento su computazioni non pure (quelle che hanno effetti collaterali, accesso a risorse esterne, etc.).

La legge monadica di associatività:
```
m >>= (\x -> k x >>= h) = (m >>= k) >>= h
```

Corrisponde all'associatività della congiunzione logica, (A ∧ (B ∧ C)) è logicamente equivalente a ((A ∧ B) ∧ C).


## Conclusione

Se sceglierete di abbracciare il Curry-Howard, magari non nella sua forma più astratta, ma almeno come mentalità, scriverete codice migliore, e nei momenti in cui il compilatore vi rifiuta un pezzo di codice, invece di maledirlo, provate a apprezzare il fatto che vi sta salvando da una dimostrazione falsa. Perché un programma una dimostrazione eseguibile di un teorema logico.

E quella è una cosa bellissima...

---













