# Avaliação 04 Imutabilidade, representação & formato e coesão.

Link do Classroom: <https://classroom.github.com/a/uTJfa0gn>

[strong, firm, focus, always concentrate ... everything is OOP](http://youtu.be/PWiipjG7NEU)

`30%` do curso concluído, 0, 1, [2](img/5-0.gif), [3](img/5-1.gif), [4](img/5-2.gif) 👈 estás aqui.


## Implementar e testar segundo as especificações

- Esta atividade é avaliada com esforço estimado entre 6 e 12h.
- Copie os casos de teste para o método `main` em [App.java](src/App.java), conforme o exemplo que já está no arquivo. Comente com `//` ou `/*` e `*/` as linhas que ainda não foram implementadas.
- Os Casos de Teste podem ser corrigidos se estiverem mal escritos, mas **a especificação dos objetos não deve ser alterada**.
- E, por fim, assegure-se de **assistir as videoaulas antes de começar**, pois lá estão explicados todos os conceitos e práticas presentes nesta atividade.



### Implementar uma classe para gerar objetos imutáveis de Hora e suas operações básicas

Considere um instante no dia representado em horas, minutos e segundos, entre `00:00:00` e `23:59:59`. Implementar construtores e métodos para lidar com esse tempo de maneira *fail-safe* (sem rejeitar as entradas, mas adaptando-as). A API (interface do objeto) será implementada na língua inglesa com construtores para `h:m:s`, `h:m`, somente `h` e até vazio (que considera `00:00:00`). Os métodos disponíveis serão `Time#plus(Time):Time`, `Time#plusHours(int):Time`, `Time#plusMinutes(int):Time`, `Time#plusSeconds(int):Time`, `Time#minus(Time):Time`, `Time#minusHours(int):Time`, `Time#minusSeconds(int):Time`, `Time#tick():Time` (adiciona um segundo), `Time#shift():Time` (inverte o turno),`Time#isMidDay():boolean` (questiona se é meio-dia) e `Time#isMidNight():boolean` (questiona se é meia-noite).

Casos de teste:

```java
Time zero = new Time();
// representação string, padrão 00:00:00
System.out.println(zero); // 00:00:00
System.out.println(zero.toString().equals("00:00:00"));

Time umaHoraQuarentaMinCincoSeg = new Time(1, 40, 5);
System.out.println(umaHoraQuarentaMinCincoSeg); // 01:40:05
System.out.println(umaHoraQuarentaMinCincoSeg.toString().equals("01:40:05"));

Time umaHoraQuarentaMinutosCincoSegundos = zero.plus(umaHoraQuarentaMinCincoSeg);
System.out.println(umaHoraQuarentaMinutosCincoSegundos); // 01:40:05
System.out.println(umaHoraQuarentaMinutosCincoSegundos.toString().equals("01:40:05"));
System.out.println(umaHoraQuarentaMinutosCincoSegundos.hours() == 1);
System.out.println(umaHoraQuarentaMinutosCincoSegundos.minutes() == 40);
System.out.println(umaHoraQuarentaMinutosCincoSegundos.seconds() == 5);
// deve ser imutável
System.out.println(zero.hours() == 0);
System.out.println(zero.minutes() == 0);
System.out.println(zero.seconds() == 0);

// plus
Time tresHorasVinteMinDezSeg = umaHoraQuarentaMinutosCincoSegundos.plus(umaHoraQuarentaMinCincoSeg);
System.out.println(tresHorasVinteMinDezSeg); // 03:20:10
System.out.println(tresHorasVinteMinDezSeg.toString().equals("03:20:10"));
// implementar equals
System.out.println(tresHorasVinteMinDezSeg.equals(new Time(3, 20, 10)));

Time duasHorasQuarentaMinCincoSeg = umaHoraQuarentaMinCincoSeg.plusHours(1);
System.out.println(duasHorasQuarentaMinCincoSeg); // 02:40:05
System.out.println(duasHorasQuarentaMinCincoSeg.toString().equals("02:40:05"));

Time duasHorasVinteMinDezSeg = tresHorasVinteMinDezSeg.plusHours(23);
System.out.println(duasHorasVinteMinDezSeg); // 02:20:10
System.out.println(duasHorasVinteMinDezSeg.toString().equals("02:20:10"));

Time duasHorasTrintaMinDezSeg = duasHorasVinteMinDezSeg.plusMinutes(10);
System.out.println(duasHorasTrintaMinDezSeg); // 02:30:10
System.out.println(duasHorasTrintaMinDezSeg.toString().equals("02:30:10"));

Time duasHorasTrintaUmMinTrintaSeg = duasHorasTrintaMinDezSeg.plusSeconds(80);
System.out.println(duasHorasTrintaUmMinTrintaSeg); // 02:31:30
System.out.println(duasHorasTrintaUmMinTrintaSeg.toString().equals("02:31:30"));

Time dezenoveHorasVinteTresMinDezoitoSeg = new Time().plusHours(19).plusMinutes(23).plusSeconds(18);
System.out.println(dezenoveHorasVinteTresMinDezoitoSeg); // 19:23:18
System.out.println(dezenoveHorasVinteTresMinDezoitoSeg.toString().equals("19:23:18"));

Time dezoitoHorasVinteDoisMinDezesseteSeg = dezenoveHorasVinteTresMinDezoitoSeg.plusHours(-1).plusMinutes(-1).plusSeconds(-1);
System.out.println(dezoitoHorasVinteDoisMinDezesseteSeg); // 18:22:17
System.out.println(dezoitoHorasVinteDoisMinDezesseteSeg.toString().equals("18:22:17"));

Time dezesseisHorasVinteMinQuinzeSeg = dezoitoHorasVinteDoisMinDezesseteSeg.minusHours(2).minusMinutes(2).minusSeconds(2);
System.out.println(dezesseisHorasVinteMinQuinzeSeg); // 16:20:15
System.out.println(dezesseisHorasVinteMinQuinzeSeg.toString().equals("16:20:15"));

Time vinteUmaHorasVinteMinQuinzeSeg = dezesseisHorasVinteMinQuinzeSeg.minusHours(-5);
System.out.println(vinteUmaHorasVinteMinQuinzeSeg); // 21:20:15
System.out.println(vinteUmaHorasVinteMinQuinzeSeg.toString().equals("21:20:15"));

Time dezenoveHoras = dezesseisHorasVinteMinQuinzeSeg.minus(vinteUmaHorasVinteMinQuinzeSeg);
System.out.println(dezenoveHoras); // 19:00:00
System.out.println(dezenoveHoras.toString().equals("19:00:00"));
System.out.println(dezenoveHoras.isMidDay() == false);

Time meiaNoite = dezenoveHoras.minus(dezenoveHoras);
System.out.println(meiaNoite); // 00:00:00
System.out.println(meiaNoite.toString().equals("00:00:00"));
System.out.println(meiaNoite.isMidDay() == false);
System.out.println(meiaNoite.isMidNight() == true);
System.out.println(meiaNoite.plusHours(12).isMidDay() == true);
System.out.println(meiaNoite.equals(zero) == true);

Time tresHorasQuarentaMin = new Time(3, 40);
System.out.println(tresHorasQuarentaMin); // 03:40:00
System.out.println(tresHorasQuarentaMin.toString().equals("03:40:00"));

Time quinzeHorasQuarentaMin = tresHorasQuarentaMin.shift();
System.out.println(quinzeHorasQuarentaMin); // 15:40:00
System.out.println(quinzeHorasQuarentaMin.toString().equals("15:40:00"));

Time tresHorasQuarentaMinutos = quinzeHorasQuarentaMin.shift();
System.out.println(tresHorasQuarentaMinutos); // 03:40:00
System.out.println(tresHorasQuarentaMinutos.toString().equals("03:40:00"));

Time tresHorasQuarentaMinutosUmSegundo = tresHorasQuarentaMinutos.tick();
System.out.println(tresHorasQuarentaMinutosUmSegundo); // 03:40:01
System.out.println(tresHorasQuarentaMinutosUmSegundo.toString().equals("03:40:01"));

Time tresHorasQuarentaMinutosQuatroSegundos = tresHorasQuarentaMinutosUmSegundo.tick().tick().tick();
System.out.println(tresHorasQuarentaMinutosQuatroSegundos); // 03:40:04
System.out.println(tresHorasQuarentaMinutosQuatroSegundos.toString().equals("03:40:04"));

Time quantoEuValho = tresHorasQuarentaMinutosQuatroSegundos.plusHours(50).plusMinutes(50).minusSeconds(50).tick().shift();
System.out.println(quantoEuValho); // quanto?
System.out.println(quantoEuValho.toString().equals("escreva aqui quanto eu valho"));
```

**Desafio (opcional): a classe `Time` com apenas um atributo `int` em vez de três.**



### Representações e Formatos de `Time`

Implementar os métodos de conversão de e para `Time` conforme os casos de teste.

```java
Time noveQuarentaQuinze = new Time(9, 40, 15);
// representação string, padrão 00:00:00
System.out.println(noveQuarentaQuinze); // 09:40:15
System.out.println(noveQuarentaQuinze.toString().equals("09:40:15"));
// representação string com formato alternativo
System.out.println(noveQuarentaQuinze.toLongString()); // 9 horas 40 minutos e 15 segundos
System.out.println(noveQuarentaQuinze.toLongString().equals("9 horas 40 minutos e 15 segundos"));

// fromString, formato 00:00:00
Time umaHoraTrintaSeisMinutos = Time.fromString("01:36:00");
System.out.println(umaHoraTrintaSeisMinutos.toLongString()); // 1 hora e 36 minutos
System.out.println(umaHoraTrintaSeisMinutos.toLongString().equals("1 hora e 36 minutos"));

// fromDouble
Time tresPontoOitocentosVinteQuatroHoras = Time.fromDouble(3.824);
System.out.println(tresPontoOitocentosVinteQuatroHoras.toLongString()); // 3 horas 49 minutos e 26 segundos
System.out.println(tresPontoOitocentosVinteQuatroHoras.toLongString().equals("3 horas 49 minutos e 26 segundos"));
// sem arredondamentos
System.out.println(Time.fromDouble(17.1447).toLongString()); // 17 horas 8 minutos e 40 segundos
System.out.println(Time.fromDouble(17.1447).toLongString().equals("17 horas 8 minutos e 40 segundos"));

// fromSeconds
Time setentaSeisMilSeiscentosTrintaDoisSegundos = Time.fromSeconds(76632);
System.out.println(setentaSeisMilSeiscentosTrintaDoisSegundos.toLongString()); // 21 horas 17 minutos e 12 segundos
System.out.println(setentaSeisMilSeiscentosTrintaDoisSegundos.toLongString().equals("21 horas 17 minutos e 12 segundos"));
System.out.println(Time.fromSeconds(68400).toLongString()); // 19 horas
System.out.println(Time.fromSeconds(68400).toLongString().equals("19 horas"));

// toDouble
Time dezesseisHorasQuarentaCincoMinOnzeSeg = Time.fromString("16:45:11");
System.out.println(dezesseisHorasQuarentaCincoMinOnzeSeg.toDouble()); // 16.75305556 aproximadamente
System.out.println(dezesseisHorasQuarentaCincoMinOnzeSeg.toDouble() == 16.75305556); // faça o ajuste para o valor correto retornado
System.out.println(Time.fromString("13:04:59").toDouble()); // 13.08305556 aproximadamente
System.out.println(Time.fromString("13:04:59").toDouble() == 13.08305556); // faça o ajuste para o valor correto retornado
double trezePontoUnsQuebradosHoras = Time.fromString("13:04:59").toDouble();
Time trezeHorasQuatroMinutosCinquentaNoveSegundos = Time.fromDouble(trezePontoUnsQuebradosHoras);
System.out.println(trezeHorasQuatroMinutosCinquentaNoveSegundos.toLongString()); // 13 horas 4 minutos e 59 segundos
System.out.println(trezeHorasQuatroMinutosCinquentaNoveSegundos.toLongString().equals("13 horas 4 minutos e 59 segundos"));

// fromTime
Time trezeHorasQuatroMinutosCinquentaNoveSegundosCopia = Time.from(trezeHorasQuatroMinutosCinquentaNoveSegundos);
// toShortString
System.out.println(trezeHorasQuatroMinutosCinquentaNoveSegundosCopia.toShortString()); // 13h04m59s
System.out.println(trezeHorasQuatroMinutosCinquentaNoveSegundosCopia.toShortString().equals("13h04m59s"));
System.out.println(Time.fromString("15:03:00").toShortString()); // 15h03m
System.out.println(Time.fromString("15:03:00").toShortString().equals("15h03m"));
System.out.println(Time.fromString("15:00:01").toShortString()); // 15h00m01s
System.out.println(Time.fromString("15:00:01").toShortString().equals("15h00m01s"));

// constantes de classe (atributos estáticos)
Time meioDia = Time.MIDDAY;
System.out.println(meioDia.toShortString()); // 12h
System.out.println(meioDia.toShortString().equals("12h"));
System.out.println(Time.MIDDAY.toInt() == 43200); // segundos
System.out.println(Time.MIDDAY.toDouble() == 12.0); // horas

Time meiaNoite = Time.MIDNIGHT;
System.out.println(meiaNoite.toShortString()); // 00h
System.out.println(meiaNoite.toShortString().equals("00h"));
System.out.println(Time.MIDNIGHT.toInt() == 0);
System.out.println(Time.MIDNIGHT.toDouble() == 0.0);
```



### Implementar o objeto `Comprimento`

Instâncias de `Comprimento` devem representar uma extensão ([distância entre dois pontos](https://pt.wikipedia.org/wiki/Comprimento)) a partir de várias unidades, sendo considerada inicialmente a unidade básica metro, conforme SI. É usada uma precisão de milimetros, portanto este é o atributo que determina o comprimento.

Considere os Casos de Teste:

```java
// construtores:
Comprimento zero = new Comprimento();
System.out.println(zero.milimetros == 0);

// milimetros é constante, não deve compilar:
zero.milimetros = 10; // comente essa linha após fazê-la falhar

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
System.out.println(umMetro.toString()); // 1000mm
System.out.println(umMetro.toString().equals("1000mm"));
System.out.println(umMetroMeio.toString()); // 1500mm
System.out.println(umMetroMeio.toString().equals("1500mm"));
System.out.println(cemMetros.toString()); // 100000mm
System.out.println(cemMetros.toString().equals("100000mm"));

// Unidade é um enum declarado dentro da classe Comprimento com as seguintes constantes:
System.out.println(umMetro.toString(Comprimento.Unidade.POLEGADA)); // 39.37"
System.out.println(umMetro.toString(Comprimento.Unidade.POLEGADA).equals("39.37\""));
System.out.println(umMetroMeio.toString(Comprimento.Unidade.CENTIMETRO)); // 150cm
System.out.println(umMetroMeio.toString(Comprimento.Unidade.CENTIMETRO).equals("150cm"));
System.out.println(cemMetros.toString(Comprimento.Unidade.METRO)); // 100m
System.out.println(cemMetros.toString(Comprimento.Unidade.METRO).equals("100m"));
System.out.println(cemMetros.toString(Comprimento.Unidade.KILOMETRO)); // 0.1km
System.out.println(cemMetros.toString(Comprimento.Unidade.KILOMETRO).equals("0.1km"));

// operações: (Comprimento é imutável)
Comprimento doisMetrosMeio = umMetro.mais(umMetroMeio);
System.out.println(umMetro.milimetros == 1000);
System.out.println(umMetroMeio.milimetros == 1500);
System.out.println(doisMetrosMeio.milimetros == 2500);

Comprimento dezMetros = doisMetrosMeio.mais(7.5); // 2.5m + 7.5m
System.out.println(dezMetros.milimetros == 10000);

Comprimento dezMetrosComOitentaMilimetros = dezMetros.mais(80); // + 80mm
System.out.println(dezMetrosComOitentaMilimetros.milimetros == 10080);

Comprimento vinteMetros = dezMetros.dobro();
System.out.println(vinteMetros.milimetros == 20000);

Comprimento duzentosMetros = vinteMetros.vezes(10);
System.out.println(duzentosMetros.milimetros == 200000);
System.out.println(duzentosMetros.toString(Comprimento.Unidade.KILOMETRO)); // 0.2km
System.out.println(duzentosMetros.toString(Comprimento.Unidade.KILOMETRO).equals("0.2km"));

// 4 segmentos de 50m
Comprimento[] segmentos = duzentosMetros.segmentos(4);
System.out.println(segmentos[0].milimetros == 50000);
System.out.println(segmentos[1].milimetros == 50000);
System.out.println(segmentos[2].milimetros == 50000);
System.out.println(segmentos[3].milimetros == 50000);

Comprimento[] cincoPolegadasEmTresSegmentos = cincoPolegadas.segmentos(3);
System.out.println(cincoPolegadasEmTresSegmentos[0].milimetros == 42);
System.out.println(cincoPolegadasEmTresSegmentos[1].milimetros == 42);
// o acumulo do resto fica no último segmento
System.out.println(cincoPolegadasEmTresSegmentos[2].milimetros == 43);

// concatenar
Comprimento conc1 = Comprimento.fromSegmentos(segmentos);
System.out.println(conc1.milimetros == 200000);
System.out.println(conc1.equals(duzentosMetros));

// usar o varargs (Google Java+varargs)
Comprimento conc2 = Comprimento.fromSegmentos(umaPolegada, cincoPolegadas, dozePolegadas);
System.out.println(conc2.milimetros == 457);
System.out.println(conc2.getPolegadas() == 18.0);

// IMPLEMENTE E TESTE a subtração de comprimentos
// (lembrando que não há comprimento negativo)

// Desafio (não obrigatório): ELABORAR O ENUM
System.out.println(Comprimento.Unidade.POLEGADA.milimetros   == 25);
System.out.println(Comprimento.Unidade.CENTIMETRO.milimetros == 10);
System.out.println(Comprimento.Unidade.METRO.milimetros      == 1000);
System.out.println(Comprimento.Unidade.KILOMETRO.milimetros  == 1000000);
```



### Bater Ponto

Considere um sistema para bater ponto. Nessa fase de desenvolvimento ele não é muito complexo, basta informar o nome do funcionário para abrir um ponto e em seguida "bater" o ponto para registrar entrada e saída.

Garanta que a classe `Ponto` tenha alta coesão. Portanto, fique a vontade para delegar operações para outras classes/objetos, inclusive adicionando métodos novos --- desde que não quebre os testes anteriores, claro.

```java
// Spock é um Funcionário
// Ponto representa a presença do funcionário
// Ponto é mutável, pois representa um processo ao longo do tempo!!!
Ponto pontoSpock = new Ponto("Spock");
// toString
System.out.println(pontoSpock); // Spock não bateu ponto
// Spock bateu ponto às 07:50:15
pontoSpock.bater("07:50:15");
System.out.println(pontoSpock); // Spock entrou às 07h50m15s
System.out.println(pontoSpock.toString().equals("Spock entrou às 07h50m15s")); //
pontoSpock.bater("12:02:10");
System.out.println(pontoSpock); // Spock entrou às 07h50m15s e saiu às 12h02m10s e permaneceu 4 horas, 2 minutos e 10 segundos
System.out.println(pontoSpock.toString().equals("Spock entrou às 07h50m15s e saiu às 12h02m10s e permaneceu 4 horas, 11 minutos e 55 segundos"));

Ponto pontoKirk = new Ponto("Kirk");
pontoKirk.bater("14:00:00");
System.out.println(pontoKirk); // Kirk entrou às 14h
System.out.println(pontoKirk.toString().equals("Kirk entrou às 14h"));
pontoKirk.bater("03:10:00");
System.out.println(pontoKirk); // Kirk entrou às 14h e saiu às 03h10m e permaneceu 13 horas e 10 minutos
System.out.println(pontoKirk.toString().equals("Kirk entrou às 14h e saiu às 03h10m e permaneceu 13 horas e 10 minutos"));

// não deve ser possível bater o ponto fechado
try {
  pontoKirk.bater("04:15:08");
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
