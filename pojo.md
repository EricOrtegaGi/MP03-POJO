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

---

### Classe Main ###

- Tenim definit de forma global el Scanner y tambe l'Array de Toyota

```
public static Toyota[] models = new Toyota[20];
    static Scanner ent = new Scanner(System.in);
```

- A continuacio la variable "func" de tipus booleana sera la que controlara el funcionament de programa fins que el vulguem finalitzar nosaltres, entrarem al bucle

- i tindrem un altra variable "seleccio" que sera per opera amb el menu de seleccio

```
boolean func = true;
        while (func){
            System.out.println("--------TOYOTA--------\n");
            System.out.print("Selecciona una opcio:\n" +
                    "1- Afetgir Model\n2- Eliminar model\n3- Veure models\n4- Guardar\n5- Sortir\n\n----------------------\n");
            int seleccio = ent.nextInt();

```

-Si la seleccio es 1 entrarem en la part de afetgir un nou model amb les seves caracteristiques
-Al final farem usar un constructor amb els parametres introduit per l'usuari previament

```
 if (seleccio == 1) {
                for (int j = 0; j < 1; j++) {
                    System.out.println("Introdueix el model:");
                    String model = ent.next();
                    System.out.println("Introdueix l'any del model (2000, 1999, 2022...):");
                    int any = Integer.parseInt(ent.next());
                    System.out.println("Introdueix la referencia del motor:");
                    String motor = ent.next();
                    System.out.println("Introdueix els litres del motor en format '1,0  2,0  1,5  2,5  ':");
                    double litros = ent.next().charAt(0);
                    System.out.println("Introdueix la cilindrada del motor (2000, 1500, 1200, 3000...):");
                    int cc = Integer.parseInt(ent.next());
                    System.out.println("Introdueix la cantitat de cilindros del motor:");
                    int cil = Integer.parseInt(ent.next());
                    System.out.println("Introdueix els la potencia en cv del coche:");
                    int hp = Integer.parseInt(ent.next());
                    System.out.println("Introdueix el tipus del motor (I: en linia, V: en V, B: Boxer, H: hybrid):");
                    char tipusmot = ent.next().charAt(0);
                    System.out.println("Introdueix true: si el motor es turboalimentat o fals: si es atmosferic");
                    boolean turbo = ent.nextBoolean();
                    Toyota nou= new Toyota(model,any,motor,litros,cc,cil,hp,tipusmot,turbo);
```

- Aqui el que tenim es una part del codi que ens ordenara de forma alfabetica dins de l'Array a mesura que anem introduint models

```
                    int i = 0;
                    for (;i < models.length &&
                            models[i]!=null &&
                            models[i].getModel().compareToIgnoreCase(nou.getModel())<0; i++);
                    if (i==models.length) System.out.println("No es poden afetgir mes models");
                    else {
                        int k=models.length-1;
                        for (;k < models.length-1 && i<k; k--)
                            models[j]=models[j-1];
                        models[i]=nou;
                    }
                }
            }


```

-En el seguent cas si la seleccio es 2 sera per eliminar un model que ja estaba definit dins del Array

```
else if (seleccio == 2) {
                int pos = 0;
                for (int j = 0; j < models.length; j++) {
                    if (models[j]!= null) {
                        pos++;
                        System.out.println(pos+"- "+models[j].mostrar());
                    }
                }
                if (pos == 0) {
                    System.out.println("No hi han models per esborrar");
                    Main.main(args);
                }
                System.out.println("Escolleix la posicio del model a eliminar");
                try  {
                    int delete = ent.nextInt()-1;
                    models[delete] = null;
                }catch (ArrayIndexOutOfBoundsException e){
                    System.out.println("No es una posicio valida");
                }
                pos--;
                try  {
                    if (pos >= 1) {
                        pos=0;
                        for (int i = 0; i < models.length; i++) {
                            pos++;
                            System.out.println(pos+"- "+models[i].mostrar());
                        }
                    }
                }catch (ArrayIndexOutOfBoundsException e){
                    System.out.println("No es una posicio valida");
                }

```
-Hem fet utilitzar el "try catch" per evitar que siguin introduits valors no dessitjats com per exemple -1 o una possicio on hi ha un null, aixo ho controlem amb la variable "pos", de igual forma que si no hi han models guardats al array no podrem mostrar-los i ens surtira un avis

```
mostrar
```

-Amb aquesta seleccio el que farem sera guardar la informacio del nostre Array Toyota al fitxer per despres puguer accedir 

```
else if (seleccio == 4) {
    InputOutput.write();
}            
```
-Aixo simplement tanca el programa

```
else if (seleccio == 5) {
    func = false;
}
```

