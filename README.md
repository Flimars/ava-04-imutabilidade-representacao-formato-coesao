# Avaliação 04 Imutabilidade, representação & formato e coesão.

Link do Classroom: <PENDENTE>

[strong, firm, focus, always concentrate ... everything is OOP](http://youtu.be/PWiipjG7NEU)

`30%` do curso concluído, [ava-02](img/5-0.gif), [ava-03](img/5-1.gif), [ava-04](img/5-2.gif) 👈 estás aqui.


## Implementar e testar segundo as especificações

- Esta atividade é avaliada com esforço estimado entre 6 e 12h.
- Copie os casos de teste para o método `main` em [App.java](src/App.java), conforme o exemplo que já está no arquivo. Comente com `//` ou `/*` e `*/` as linhas que ainda não foram implementadas.
- Os Casos de Teste podem ser corrigidos se estiverem mal escritos, mas **a especificação dos objetos não pode ser alterada**.
- E, por fim, assegure-se de **assistir as videoaulas antes de começar**, pois lá estão explicados todos os conceitos e práticas presentes nesta atividade.



### Implementar uma classe para gerar objetos imutáveis de Tempo e suas operações básicas

Considere um instante no tempo em horas, minutos e segundos, entre `00:00:00` e `23:59:59`. Implementar construtores e métodos para lidar com esse tempo de maneira *fail-safe* (sem rejeitar as entradas, mas adaptando-as). A API (interface do objeto) será implementada na língua inglesa com construtores para `h:m:s`, `h:m` e somente `h`. Os métodos disponíveis serão `Time#plus(Time):Time`, `Time#plusHours(int):Time`, `Time#plusMinutes(int):Time`, `Time#plusSeconds(int):Time`, `Time#minus(Time):Time`, `Time#minusHours(int):Time`, `Time#minusSeconds(int):Time`, `Time#tick():Time` (adiciona um segundo), `Time#shift():Time` (inverte o turno),`Time#isMidDay():boolean` (questiona se é meio-dia) e `Time#isMidNight():boolean` (questiona se é meia-noite).

Casos de teste:

```java
Time t1 = new Time();
// representação string, padrão 00:00:00
System.out.println(t1.toString().equals("00:00:00"));
Time t2 = new Time(1, 40, 5);
System.out.println(t2.toString().equals("01:40:05"));
Time t3 = t1.plus(t2);
System.out.println(t3.toString().equals("01:40:05"));
System.out.println(t3.hours() == 1);
System.out.println(t3.minutes() == 40);
System.out.println(t3.seconds() == 5);
// deve ser imutável
System.out.println(t1.hours() == 0);
System.out.println(t1.minutes() == 0);
System.out.println(t1.seconds() == 0);
// plus
Time t4 = t3.plus(t2);
System.out.println(t4.toString().equals("03:20:10"));
// implementar equals
System.out.println(t4.equals(new Time(3, 20, 10)));
Time t5 = t2.plusHours(1);
System.out.println(t5.toString().equals("02:40:05"));
Time t6 = t4.plusHours(23);
System.out.println(t6.toString().equals("02:20:10"));
Time t7 = t6.plusMinutes(10);
System.out.println(t7.toString().equals("02:30:10"));
Time t8 = t7.plusSeconds(80);
System.out.println(t8.toString().equals("02:31:30"));
Time t9 = new Time().plusHours(19).plusMinutes(23).plusSeconds(18);
System.out.println(t9.toString().equals("19:23:18"));
Time t10 = t9.plusHours(-1).plusMinutes(-1).plusSeconds(-1);
System.out.println(t10.toString().equals("18:22:17"));
Time t11 = t10.minusHours(2).minusMinutes(2).minusSeconds(2);
System.out.println(t11.toString().equals("16:20:15"));
Time t12 = t11.minusHours(-5);
System.out.println(t12.toString().equals("21:20:15"));
Time t13 = t11.minus(t12);
System.out.println(t13.toString().equals("19:00:00"));
System.out.println(t13.isMidDay() == false);
Time t14 = t13.minus(t13);
System.out.println(t14.toString().equals("00:00:00"));
System.out.println(t14.isMidDay() == false);
System.out.println(t14.isMidNight() == true);
System.out.println(t14.plusHours(12).isMidDay() == true);
Time t15 = new Time(3, 40);
System.out.println(t15.toString().equals("03:40:00"));
Time t16 = t15.shift();
System.out.println(t16.toString().equals("15:40:00"));
Time t17 = t16.shift();
System.out.println(t17.toString().equals("03:40:00"));
Time t18 = t17.tick();
System.out.println(t18.toString().equals("03:40:01"));
Time t19 = t18.tick().tick().tick();
System.out.println(t19.toString().equals("03:40:04"));
Time t20 = t19.plusHours(50).plusMinutes(50).minusSeconds(50).tick().shift();
System.out.println(t20.toString().equals("quanto vale t20? escreva aqui"));
```

**Desafio: a classe `Time` com apenas um atributo `int` em vez de três.**



### Representações e Formatos de `Time`

Implementar os métodos de conversão para `Time` conforme os casos de teste.

```java
Time tr1 = new Time(9, 40, 15);
// representação string, padrão 00:00:00
System.out.println(tr1.toString().equals("09:40:15"));
// representação string com formato alternativo
System.out.println(tr1.toLongString().equals("9 horas 40 minutos e 15 segundos"));
// fromString, formato 00:00:00
Time tr2 = Time.fromString("01:36:00");
System.out.println(tr2.toLongString().equals("1 hora e 36 minutos"));
// fromDouble
Time tr3 = Time.fromDouble(3.824);
System.out.println(tr3.toLongString().equals("3 horas 49 minutos e 26 segundos"));
// sem arredondamentos
System.out.println(Time.fromDouble(17.1447).toLongString().equals("17 horas 8 minutos e 40 segundos"));
// fromSeconds
Time tr4 = Time.fromSeconds(76632);
// System.out.println(tr4.toLongString().equals("21 horas 15 minutos e 32 segundos")); // PATCH:
System.out.println(tr4.toLongString().equals("21 horas 17 minutos e 12 segundos"));
// --------------------------------------------------------------------------------
System.out.println(Time.fromSeconds(68400).toLongString().equals("19 horas"));
// toDouble
Time tr4 = Time.fromString("16:45:11");
System.out.println(tr4.toDouble()); // 16.75305556 aproximadamente
System.out.println(Time.fromString("13:04:59").toDouble()); // 13.08305556 aproximadamente
double tr5double = Time.fromString("13:04:59").toDouble();
Time tr5 = Time.fromDouble(tr5double);
System.out.println(tr5.toLongString().equals("13 horas 4 minutos e 59 segundos"));
// fromTime
Time tr6 = Time.from(tr5);
// toShortString
System.out.println(tr6.toShortString().equals("13h04m59s"));
System.out.println(Time.fromString("15:03:00").toShortString().equals("15h03m"));
System.out.println(Time.fromString("15:00:01").toShortString().equals("15h00m01s"));
// constantes
Time tr7 = Time.MIDDAY;
System.out.println(tr7.toShortString().equals("12h"));
Time tr8 = Time.MIDNIGHT;
System.out.println(tr8.toShortString().equals("00h"));
System.out.println(Time.MIDDAY.toInt() == 43200);
System.out.println(Time.MIDNIGHT.toInt() == 0);
```



### Implementar o objeto `Comprimento`

Instâncias de `Comprimento` devem representar uma extensão ([distância entre dois pontos](https://pt.wikipedia.org/wiki/Comprimento)) a partir de várias unidades, sendo considerada inicialmente a unidade básica metro conforme SI.

Considere os Casos de Teste:

```java
// construtores:
Comprimento zero = new Comprimento();
System.out.println(zero.milimetros == 0);

// milimetros é constante, não deve compilar:
zero.milimetros = 10;

// construtor double metro:
Comprimento umMetro = new Comprimento(1.0);
System.out.println(umMetro.milimetros == 1000);

Comprimento umMetroMeio = new Comprimento(1.5);
System.out.println(umMetroMeio.milimetros == 1500);

Comprimento cemMetros = new Comprimento(100.0);
System.out.println(cemMetros.milimetros == 100000);

// construtor inteiro milimetros:
Comprimento umCentimetro = new Comprimento(100);
System.out.println(umCentimetro.milimetros == 100);

// comprimentos inválidos, negativo!
// Faça lançar exceção e abrace-as com try/catch
Comprimento invalido1 = new Comprimento(-1.0);
Comprimento invalido2 = new Comprimento(-10);

// métodos estáticos fábrica:
Comprimento umaPolegada = Comprimento.fromPolegadas(1.0);
System.out.println(umaPolegada.milimetros == 25);

Comprimento cincoPolegadas = Comprimento.fromPolegadas(5.0);
System.out.println(cincoPolegadas.milimetros == 127);

Comprimento dozeMilimetros = Comprimento.fromString("12mm");
System.out.println(dozeMilimetros.milimetros == 12);

Comprimento dozeCentimetros = Comprimento.fromString("12cm");
System.out.println(dozeCentimetros.milimetros == 120);

Comprimento dozePolegadas = Comprimento.fromString("12\"");
// seria 304.8mm, mas os mm devem ser truncados, não arredondados.
System.out.println(dozePolegadas.milimetros == 304);

Comprimento dozeMetros = Comprimento.fromString("12m");
System.out.println(dozeMetros.milimetros == 12000);

// qualquer string fora deste padrão [0-9](mm|cm|m|") deve ser rejeitada
// faça lançar exceção e abrace-as com try/catch
Comprimento.fromString("12");
Comprimento.fromString("12e");
Comprimento.fromString("12 m");
Comprimento.fromString("12M");

// consultas: (pode ser ajustado para o arredondamento, exceto de mm que é truncado)
System.out.println(cincoPolegadas.getCentimetros() == 12.7);
System.out.println(cincoPolegadas.getMetros() == 0.127);
System.out.println(cemMetros.getPolegadas() == 3937.0);
System.out.println(dozeMetros.getMilimetros() == 12000);

// toString
System.out.println(umMetro.toString().equals("1000mm"));
System.out.println(umMetroMeio.toString().equals("1500mm"));
System.out.println(cemMetros.toString().equals("100000mm"));

// Unidade é um enum declarado dentro da classe Comprimento com as seguintes constantes:
System.out.println(umMetro.toString(Comprimento.Unidade.POLEGADAS).equals("39.37\""));
System.out.println(umMetroMeio.toString(Comprimento.Unidade.CENTIMETROS).equals("150cm"));
System.out.println(cemMetros.toString(Comprimento.Unidade.METROS).equals("100m"));
System.out.println(cemMetros.toString(Comprimento.Unidade.KILOMETROS).equals("0.1km"));

// operações: (Comprimento é imutável)
Comprimento doisMetros = umMetro.mais(umMetroMeio);
System.out.println(umMetro.milimetros == 1000);
System.out.println(umMetroMeio.milimetros == 1500);
System.out.println(doisMetros.milimetros == 2000);

Comprimento dezMetros = doisMetros.mais(8.0);
System.out.println(dezMetros.milimetros == 10000);

Comprimento vinteMetros = dezMetros.dobro();
System.out.println(vinteMetros.milimetros == 20000);

Comprimento duzentosMetros = vinteMetros.vezes(10);
System.out.println(duzentosMetros.milimetros == 200000);
System.out.println(duzentosMetros.toString(Comprimento.Unidade.KILOMETROS).equals("0.2km"));

// 4 segmentos de 50m
Comprimento[] segmentos = duzentosMetros.segmentos(4);
System.out.println(segmentos[0].milimetros == 50000);
System.out.println(segmentos[1].milimetros == 50000);
System.out.println(segmentos[2].milimetros == 50000);
System.out.println(segmentos[3].milimetros == 50000);

Comprimento[] cincoPolegadasEmTres = cincoPolegadas.segmentos(3);
System.out.println(cincoPolegadasEmTres[0].milimetros == 42);
System.out.println(cincoPolegadasEmTres[1].milimetros == 42);
// o acumulo do resto fica no último segmento
System.out.println(cincoPolegadasEmTres[2].milimetros == 43);



// IMPLEMENTE E TESTE:
//

```


### Ponto

Considere um sistema para bater ponto. Nessa fase de desenvolvimento ele não é muito complexo, basta informar o nome do funcionário para abrir um ponto e em seguida "bater" o ponto para registrar entrada e saída.

Garanta que a classe `Ponto` tenha alta coesão. Portanto, fique a vontade para delegar operações para outras classes/objetos, inclusive adicionando métodos novos --- desde que não quebre testes anteriores, claro.

```java
// Spock é um Funcionário
// Ponto representa uma presença do funcionário
// Ponto é mutável, pois representa um processo ao longo do tempo!!!
Ponto ponto = new Ponto("Spock");
// toString
System.out.println(ponto); // Spock não bateu ponto
// Spock bateu ponto às 07:50:15
ponto.bater("07:50:15");
System.out.println(ponto); // Spock entrou às 07h50m15s
System.out.println(ponto.toString().equals("Spock entrou às 07h50m15s")); //
ponto.bater("12:02:10");
System.out.println(ponto); // Spock entrou às 07h50m15s e saiu às 12h02m10s e permaneceu 4 horas, 2 minutos e 10 segundos
System.out.println(ponto.toString().equals("Spock entrou às 07h50m15s e saiu às 12h02m10s e permaneceu 4 horas, 11 minutos e 55 segundos"));

Ponto ponto2 = new Ponto("Kirk");
ponto2.bater("14:00:00");
System.out.println(ponto2); // Kirk entrou às 14h
System.out.println(ponto2.toString().equals("Kirk entrou às 14h"));
ponto2.bater("03:10:00");
System.out.println(ponto2); // Kirk entrou às 14h e saiu às 03h10m e permaneceu 13 horas e 10 minutos
System.out.println(ponto2.toString().equals("Kirk entrou às 14h e saiu às 03h10m e permaneceu 13 horas e 10 minutos"));

// não deve ser possível bater o ponto fechado
try {
  ponto2.bater("04:15:08");
  System.out.println(false); // falhou
} catch (IllegalStateException e) {
  System.out.println(e.getMessage()); // Entrada e saída já foram batidas e o ponto está fechado
  System.out.println(true); // ok, passou!
}
```

* * *

> There are known knowns. These are things we know that we know.
> There are known unknowns. That is to say, there are things that we know we don't know.
> But there are also unknown unknowns. There are things we don't know we don't know.
>
> -- **Donald Rumsfeld**
