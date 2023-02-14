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

- setAll();
```
public void setAll(){
        System.out.println("Introdueix el model:");
        setModel(ent.nextLine());
        System.out.println("Introdueix l'any del model (2000, 1999, 2022...):");
        setAny(ent.nextInt());
        System.out.println("Introdueix la referencia del motor:");
        setMotor(ent.next());
        System.out.println("Introdueix els litres del motor en format '1,0  2,0  1,5  2,5  ':");
        setLitros(ent.next().charAt(0));
        System.out.println("Introdueix la cilindrada del motor (2000, 1500, 1200, 3000...):");
        setCc(ent.nextInt());
        System.out.println("Introdueix la cantitat de cilindros del motor:");
        setCilindros(ent.nextInt());
        System.out.println("Introdueix els la potencia en cv del coche:");
        setHp(ent.nextInt());
        System.out.println("Introdueix el tipus del motor (I: en linia, V: en V, B: Boxer, H: hybrid):");
        setTipusMotor(ent.next().charAt(0));
        System.out.println("Introdueix true: si el motor es turboalimentat o fals: si es atmosferic");
        setTurbo(ent.nextBoolean());
    }
```
---

### Classe InputOutput ###

---

### Classe Main ###
