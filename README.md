# BEVADAT_beadando_repo
Ez a projekt egy többrétegű neurális hálózatot valósít meg, amelynek célja a BMW gépjárművek eladási volumenének osztályozása (High/Low) a műszaki és piaci adatok alapján.
Tartalomjegyzék:
  Adat előkészítés
  Modell architektúra
  Tanítási folyamat
  Eredmények és kiértékelés

Adat-előkészítés

Outlier szűrés: Az IQR (Interquartile Range) módszerrel eltávolítom a kiugró értékeket a folyamatos változókból (ár, futásteljesítmény, motorméret), így megvédve a modellt a torzítástól.

Standardizálás: A StandardScaler segítségével az összes numerikus jellemzőt átlagolom és skálázom, hogy a neurális hálózat tanulása hatékonyabb legyen.

Kategorikus kódolás: A get_dummies (One-Hot Encoding): a szöveges adatokat (modell, régió, üzemanyag típusa) bináris oszlopokká alakítom.

Adatok felosztása: Az adatbázist 70% tanító, 20% validációs és 10% tesztelő halmazra bontottam.

Modell Architektúra:
A projekt egy Szekvenciális Neurális Hálózatot használ, amely "tölcsér-elvet" követ az adatok tömörítése és a minták felismerése érdekében:

Bemeneti réteg: 64 neuron, ReLU aktivációval.

Rejtett rétegek: 
32 neuron (ReLU)

16 neuron (LeakyReLU aktivációval az információvesztés ellen)

8 neuron (ReLU)

Dropout rétegek: Minden rejtett réteg között Dropout-ot alkalmaztam (30%, 20%, 20%, 10% mértékben), hogy megakadályozzam az overlearning (túltanulás) jelenségét.

Kimeneti réteg: 1 neuron, Sigmoid aktivációval a bináris osztályozáshoz.

Tanítási folyamat
A tanítás során Adam optimalizálót és Binary Crossentropy veszteségfüggvényt használtam.

A túltanulás elleni védekezés kulcsa az Early Stopping mechanizmus:

Monitor: val_loss (validációs veszteség).

Patience: 4 (ha 4 korszakon keresztül nem javult a modell, a tanítás leállt).

Restore Best Weights: A tanítás végén a hálózat automatikusan visszatöltötte azt az állapotot, ahol a legkisebb volt a hiba.


Eredmények és Kiértékelés:

Validációs Pontosság (Accuracy): ~99.38%

AUC (Area Under the Curve): Az elért AUC érték közelíti az 1.0-át, ami azt jelenti, hogy a hálózat szinte tökéletesen képes megkülönböztetni a népszerű és a kevésbé népszerű BMW modelleket.

Konfúziós Mátrix: A vizualizáció alapján a téves riasztások (False Positive) és a kihagyott esetek (False Negative) száma minimális.
