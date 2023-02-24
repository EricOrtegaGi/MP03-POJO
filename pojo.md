# POJO Models Toyota #

## Fet per: Eric Ortega Gisbert 1r DAM 2023/24 ##

### Definicio de la classe Toyota amb els valors dels objectes ###

```
public class Toyota implements Serializable {

    Scanner ent = new Scanner(System.in);

    //propietats de la classe --> definixen l'estat dels objectes
    private String model;
    private int any;
    private String motor;
    private double litros;
    private int cc;
    private int cilindros;
    private int hp;
    private char tipusMotor;
    private boolean turbo;
```
---

#### Constructors de objectes ####

**He fet servir tres constructors diferents**

- Aquest primer l'hem usat per si volem definir tots els parametres d'un objecte directament
```
    //Constructor formulari
    public Toyota(String model, int any, String motor, double litros, int cc, int cilindros,int hp, char tipusMotor, boolean turbo){
        this.model = model;
        this.any = any;
        this.motor = motor;
        this.litros = litros;
        this.cc = cc;
        this.cilindros = cilindros;
        this.hp = hp;
        this.tipusMotor = tipusMotor;
        this.turbo = turbo;
    }
```
- Aquest segon l'hem usat per definir un no objecte amb valors "default"

```
    // Constructor default
    public Toyota(){
        model = "?";
        any = 0;
        motor = "?";
        litros = 0;
        cc = 0;
        cilindros = 0;
        hp = 0;
        tipusMotor = '?';
        turbo = false;
    }
```
- I per ultim el constructor que tansols necessitara que diguem el model y tots els altres valors seran nulls

```
    //Constructor model
    public Toyota(String model){
        this.model = model;

    }

```

---

#### Metode mostrar() ####

**Aquest metode el farem utilitzar quan vulguem mostrar els models instanciats dins del nostre vector d'objectes d'una forma mes atractiva**

```
public String mostrar(){
        return "Model: "+model+", Any: "+any+", Motor: "+motor+", "
                +litros+", cc: "+cc+", cil: "+ cilindros+", cv: "+hp
                +", Motor(I:En linia, V o B:Boxer, H:Hybrid):"+tipusMotor+", "
                +(turbo?"Turboalimentat, ":"Atmosferic");
    }
```

---

#### Metodes accessors ####

- Getters

```
    public String getModel() {
        return model;
    }
    public int getAny() {
        return any;
    }
    public String getMotor() {
        return motor;
    }
    public double getLitros() {
        return litros;
    }
    public int getCc() {
        return cc;
    }
    public int getCilindros() {
        return cilindros;
    }
    public int getHp() {
        return hp;
    }
    public char getTipusMotor() {
        return tipusMotor;
    }
    public boolean isTurbo() {
        return turbo;
    }
```

- getAll();
```
public void getAll() {
        System.out.println("Model: "+getModel());
        System.out.println("del: "+getAny());
        System.out.println("Motor: "+getMotor());
        System.out.println(getLitros());
        System.out.println(getCc()+"cc");
        System.out.println(getCilindros()+" cil");
        System.out.println(getHp()+"cv");
        System.out.println("Motor en: "+getTipusMotor());
        System.out.println((isTurbo()?"turboalimentat":"atmosferic"));
    }
```

---

- Setters

```
public void setModel(String model) {
        this.model = model;
        this.any = 0;
        this.motor = " ";
        this.litros = 0.0;
        this.cc= 0;
        this.cilindros = 0;
        this.hp = 0;
        this.tipusMotor = ' ';
        this.turbo = false;
    }
    public void setAny(int any) {
        this.any = any;
    }
    public void setMotor(String motor) {
        this.motor = motor;
    }
    public void setLitros(double litros) {
        this.litros = litros;
    }
    public void setCc(int cc) {
        this.cc = cc;
    }
    public void setCilindros(int cilindros) {
        this.cilindros = cilindros;
    }
    public void setHp(int hp) {
        if (hp<0) return;
        this.hp = hp;
    }
    public void setTipusMotor(char tipusMotor) {
        this.tipusMotor = tipusMotor;
    }
    public void setTurbo(boolean turbo) {
        this.turbo = turbo;
    }
```
---

### Classe InputOutput ###

- En aquesta classe tenim dos metodes, write() i read()
- Com els seus noms indiquen un serveix per escriure objectes dins del fitxer i l'altre per llegirlo i despres afetgir els objectes que ja tenim de volta al vector

- Amb el write amb un bucle for recorrem el nostre vector y escribim els objectes dins al fitxer
```
public class InputOutput {
    public static File f = new File("models.db");
    public static void write(){
        ObjectOutputStream w = null;
        try {
            w = new ObjectOutputStream(new BufferedOutputStream(new FileOutputStream(f)));
            for (int i = 0; i < models.length && models[i]!=null; i++) {
                w.writeObject(models[i]);
            }
        } catch (IOException e) {
            System.out.println("Ha iagut un problema escribint les dades ");
            e.printStackTrace();
        }finally {
            try {
                w.close();
            } catch (IOException|NullPointerException e) {
                System.out.println("Ha iagut un problema al tancar el programa");
            }
        }
    }
```

-
```
    public static void read(){
        if (f.exists()){
            ObjectInputStream r = null;
            try {
                int i = 0;
                r = new ObjectInputStream(new BufferedInputStream(new FileInputStream(f)));
                while (true){
                    try {
                        while (true){
                            Toyota model = (Toyota) r.readObject();
                            models[i] = model;
                            i++;

                        }
                    }catch (ClassNotFoundException | EOFException e){
                        break;
                    }
                }
            }catch (IOException ex) {
                System.out.println("Error en obrir el fitxer");
            }finally {
                try {
                    r.close();
                }catch (IOException e) {
                    System.out.println("Error en tancar el fitxer");
                }
            }
        }
    }
}

```

---

### Classe Main ###

- Tenim definit de forma global el Scanner y tambe l'Array de Toyota

```
public static Toyota[] models = new Toyota[20];
    static Scanner ent = new Scanner(System.in);
```

- Primer que tot tenim la funcio read(); que ens llegira l'arxiu i plenara el vector dels objectes que te guardats
- A continuacio la variable "func" de tipus booleana sera la que controlara el funcionament de programa fins que el vulguem finalitzar nosaltres, entrarem al bucle
- i tindrem un altra variable "seleccio" que sera per opera amb el menu de seleccio

```
InputOutput.read();
int pos = 0;
boolean func = true;
try {
 while (func) {
  System.out.println("--------TOYOTA--------\n");
  System.out.print("Selecciona una opcio:\n\n" +
    "1- Afetgir Model\n2- Eliminar model\n3- Veure models\n4- Modificar model\n5- Guardar\n6- Sortir \n\n----------------------\n");
  int seleccio = ent.nextInt();
```

- Si la seleccio es 1 entrarem en la part de afetgir un nou model amb les seves caracteristiques
- Al final farem usar un constructor amb els parametres introduit per l'usuari previament
- tambe fem utilitzar un try-catch ja que com molts dels valors a introduir han de ser numerics, si hi ha algun error
- oblgiarem al usuari a tornar a omplir el formulari de forma correcta advertint-lo

```
if (seleccio == 1) {
                    for (int i = 0; i < 1; i++) {
                        try {
                            System.out.println("Introdueix el model (Separacions amb guions):");
                            String model = ent.next();
                            System.out.println("Introdueix l'any del model (2000, 1999, 2022...):");
                            int any = Integer.parseInt(ent.next());
                            System.out.println("Introdueix la referencia del motor  (Separacions amb guions):");
                            String motor = ent.next();
                            System.out.println("Introdueix els litres del motor en format '1,0  2,0  1,5  2,5  ':");
                            double litros = ent.nextDouble();
                            System.out.println("Introdueix la cilindrada del motor (2000, 1500, 1200, 3000...):");
                            int cc = Integer.parseInt(ent.next());
                            System.out.println("Introdueix la cantitat de cilindros del motor:");
                            int cil = Integer.parseInt(ent.next());
                            System.out.println("Introdueix els la potencia en cv del coche:");
                            int hp = Integer.parseInt(ent.next());
                            System.out.println("Introdueix el tipus del motor (I: en linia, V: en V, B: Boxer, H: hybrid):");
                            char tipusmot = ent.next().charAt(0);
                            System.out.println("Introdueix 1: si el motor es turboalimentat o 2: si es atmosferic");
                            boolean turbo;
                            if (ent.nextInt() == 1) turbo = true;
                            else turbo = false;
                            Toyota nou = new Toyota(model, any, motor, litros, cc, cil, hp, tipusmot, turbo);
                            int j = 0;
                            for (; j < models.length &&
                                    models[j] != null &&
                                    models[j].getModel().compareToIgnoreCase(nou.getModel()) < 0; j++)
                                ;
                            if (j == models.length) System.out.println("No es poden afetgir mes models");
                            else {
                                int k = models.length - 1;
                                for (; k < models.length && j < k; k--)
                                    models[k] = models[k - 1];
                                models[j] = nou;
                            }
                        } catch (NumberFormatException e) {

                            System.out.println("Valor invalid");
                        }
                    }
```

- Aqui el que tenim es una part del codi que ens ordenara de forma alfabetica dins de l'Array a mesura que anem introduint models

```
                  int j = 0;
                        for (;j < models.length &&
                                models[j]!=null &&
                                models[j].getModel().compareToIgnoreCase(nou.getModel())<0; j++);
                        if (j==models.length) System.out.println("No es poden afetgir mes models");
                        else {
                            int k=models.length-1;
                            for (;k < models.length && j<k; k--)
                                models[k]=models[k-1];
                            models[j]=nou;
                        }
                    }catch (NumberFormatException e ){
                        System.out.println("Te que ser un valor numeric, Torna a introduir el formulari");
                    }
                }
            }
```

- En el seguent cas si la seleccio es 2 sera per eliminar un model que ja estaba definit dins del Array
- La varibale delete servira per escollir el objecte del array que es vol eliminar
- despres amb un bucle desplaçarem els seguents objectes ordenant el vector per a que no iaguen espais repetits o nulls de per mig

```
else if (seleccio == 2) {
                    int delete;
                    if (models.length == 0) System.out.println("No hi han models per a eliminar");
                    else {
                        pos = 0;
                        System.out.println("Selecciona la posicio del model a eliminar: \n--------------------------------------------");
                        for (int i = 0; i < models.length && models[i] != null; i++) {
                            System.out.println(pos + ": " + models[i].mostrar());
                            pos++;
                        }
                        //Reordenem el vector al borrar el model seleccionat
                        try {
                            delete = ent.nextInt();
                            for (int i = delete + 1; i < models.length && models[i] != null; i++) {
                                models[i - 1] = models[i];
                            }
                            //Aqui busquem la ultima posicio no nula i la fem nula
                            if (models[delete] != null) {
                                for (int i = models.length - 1; i >= 0; i--) {
                                    if (models[i] != null) {
                                        models[i] = null;
                                        break;
                                    }
                                }
                            } else {
                                System.out.println("No hi ha res a esborrar aqui");
                                continue;
                            }
                            pos = 0;
                            System.out.println("Llista despres de eliminar el model:");
                            for (int i = 0; i < models.length && models[i] != null; i++) {
                                System.out.println(pos + ": " + models[i].mostrar());
                                pos++;
                            }
                            pos = 0;
                        } catch (ArrayIndexOutOfBoundsException e) {
                            System.out.println("No es una posicio valida");
                        }
                    }
```
-Hem fet utilitzar el "try catch" per evitar que siguin introduits valors no dessitjats com per exemple -1 o una possicio on hi ha un null, aixo ho controlem amb la variable "pos", de igual forma que si no hi han models guardats al array no podrem mostrar-los i ens surtira un avis

- Si la seleccio es 3 el que fara el codi es llegir el fitxer on es guarden els objectes i despres recorrer el vector i mostrar tots els models que tenim instanciats, tindrem que guardar despres de afetgir o eliminar un model per a que la llista sigue actualitzada 
```
else if (seleccio == 3) {
                InputOutput.read();
                for (int i = 0; i < models.length && models[i] != null; i++) {
                    System.out.println(models[i].mostrar());
                }
```
- Si la seleccio es 4 podrem modificar algun dels objectes que l'usuari vulgue modificar amb la variable "modificar"
- es mostra el vector i fa escollir al usuari quin model vol modificar
- seguidament amb el getAll i setters del nostre pojo donarem la eleccio al usuari de quin parametre vol modificar
- aixo ho tractarem amb un try-catch per evitar valors no dessitjats

```
else if (seleccio == 4) {
                    //amb la variable modificar despres podrem canviar alguns dels parametres del objecte usan tambe els setters
                    int modificar;
                    pos = 0;
                    System.out.println("Selecciona la posicio del model a modificar \n-------------------------------------------");
                    for (int i = 0; i < models.length && models[i] != null; i++) {
                        System.out.println(pos + ": " + models[i].mostrar());
                        pos++;
                    }
                    //aqui utilitzarem un switch que tractara diferents tipus de setters dins de un try-catch per modificar el parametre dessitjat
                    while (true) {
                        try {
                            modificar = ent.nextInt();
                            System.out.println("Selecciona que vols modificar");
                            models[modificar].getAll();

                            switch (ent.nextInt()) {
                                case 1: {
                                    System.out.println("Model: ");
                                    models[modificar].setModel(ent.next());
                                    break;
                                }
                                case 2: {
                                    System.out.println("Any: ");
                                    models[modificar].setAny(Integer.parseInt(ent.next()));
                                    break;
                                }
                                case 3: {
                                    System.out.println("Motor: ");
                                    models[modificar].setMotor(ent.next());
                                    break;
                                }
                                case 4: {
                                    System.out.println("Litres (1,5  2,0  4,9...): ");
                                    models[modificar].setLitros(ent.nextDouble());
                                    break;
                                }
                                case 5: {
                                    System.out.println("cc: ");
                                    models[modificar].setCc(Integer.parseInt(ent.next()));
                                    break;
                                }
                                case 6: {
                                    System.out.println("Cilindros: ");
                                    models[modificar].setCilindros(Integer.parseInt(ent.next()));
                                    break;
                                }
                                case 7: {
                                    System.out.println("hp: ");
                                    models[modificar].setHp(Integer.parseInt(ent.next()));
                                    break;
                                }
                                case 8: {
                                    System.out.println("Tipus Motor (I, V, B, H): ");
                                    models[modificar].setTipusMotor(ent.next().charAt(0));
                                    break;
                                }
                                case 9: {
                                    System.out.println("1: Turboalimentat \n2: Atmosferic");
                                    if (ent.nextInt() == 1) {
                                        models[modificar].setTurbo(true);
                                        break;
                                    } else {
                                        models[modificar].setTurbo(false);
                                        break;
                                    }
                                }
                            }
                            models[modificar].mostrar();
                            System.out.println("Estas d'acord amb el canvi? \n1: Guardar\n2: No guardar encara");
                            int guardar = ent.nextInt();
                            if (guardar == 1) {
                                InputOutput.write();
                                break;
                            } else if (guardar == 2) break;
                        } catch (IndexOutOfBoundsException | NullPointerException e) {
                            System.out.println("Selecciona una posicio valida");
                        }
                    }

```

- Si la seleccio es 5 es guardara el vector de objectes al arxiu models.db 

```
else if (seleccio == 5) {
 InputOutput.write();
}           
```
- Si la seleccio es 6 es tancara el programa

```
else if (seleccio == 6) {
    func = false;
}
```

