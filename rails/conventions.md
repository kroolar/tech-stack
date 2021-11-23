# Conventions


1. [Optimize for programmer happines](#one)
2. [Convention over Configuration](#two)
3. [The menu is omakase](#three)
4. [No one paradigm](#four)
5. [Exalt beautiful code](#five)
6. [Provide sharp knives](#six)
7. [Value integrated systems](#seven)
8. [Progress over stability](#eight)
9. [Push up a big tent](#nine)

### <a name="one">1. Optimize for programmer happines</a>

Rails jest frameworkiem, który stawia szczęście programistów ponad wszystko inne nawet wydajność kodu. Na pierwszy rzut oka może to się wydawać absurdalne ale jak pokazuje życie społeczność Railsów dalej cieszy się duży zainteresowaniem. Rails stara się kontunuować koncepcje języka Ruby jako prostego, czytelnego i łatwego w użyciu języka. Jedną z reguł Rubiego była The Principle of Least Surprise. Tutaj mamy przykład.

``` Ruby
[1, 2, 3].length # => 3
[1, 2, 3].size   # => 3
```

Dzięki niej programista dokładnie to czego się spodziewał. Rails zastąpił tą regułe regułą The Principle of The Bigger Smile, która może być podobna to PoLS ale dzięki niej możemy znaleźć w kodzie np. metodę, która pobiera 42 obiekt z tablicy. 

``` Ruby
users = User.all
user.forty_two # => John Doe
```

Dobrym przykładem jest także klasa inflector, która zamienia liczbę pojedynczą na liczbę podwójną.

``` Ruby
'People'.singularize => 'Person'
```

Dla programistów nieznających języka Rails może wydawać się to śmieszne ale klasa ta jest podstawą dzięki, której kolejna zasada Convention over Configuration nie byłaby możliwa do zrealizowania.

### <a name="two">2. Convention over Configuration</a>

Rails oferuję wiele konwencji, którymi programista powinien podążać. Pozwala to nie przejmować się trywialnymi problemami, a skupianiu się na ważniejszych rzeczach. Dzięki temu także możemy mieć bardziej czytelny kod.

``` Ruby
has_many   :people
belongs_to :person
```

Pozwala to także na mniejszy próg wejścia dla początkującyh ponieważ nie muszą sobie zdawać sprawy z rzeczy, które są konfigurowane domyślnie.

Oczywiście Rails pozwala na odejśćie od konwencji dlatego warto wiedzieć kiedy taka zmiana ma sens.

``` KONWENCJE W RAILS ```

### <a name="three">3. The menu is omakase</a>

Omakase to wyrażenie używane podczas zamawiania jedzenia w restauracjach, któ©e oznacza "zostawie to tobie".

Rails przejmuje ciężar indywidualnych wyborów programisty na rzecz dedykowanych przez niego. Sczególnie na początku programista może nie zdawać sobie sprawy, które narzędzie będzie do tego najlepsze dlatego Rails robi to za nas. Jest ku temu kilka powodów:
  1. Jeśli duża liczba programistów używa tego samego narzędzia mają oni wspólne doświadczenia, łatwiej jest rozwiązywać błędy oraz tworzyć lepsze narzędzia.
  2. Railsy mają wiele ruchomych części dlatego, które są ze sobą połączone oraz mają na siebie wpływ. Mając ten sam zestaw narzędzi jesteśmy pewni, że interakcje między nimi będą takie same.
  3. Tak jak w przypadku konwencji dalej możemy zamieniać już istniejące narzędzia na inne

``` RUBY TOOOLBOx and deafult gem ```

### <a name="four">4. No one paradigm</a>

Rails nie posiada jednego pradygmatu. Można powiedzieć, żę ma ich wiele i w jakimś stopniu stara się je połączyć oraz mieszać. Powoduje to, że jest on bardzo dynamiczny i dzięki temu możemy do skroić do naszych potrzeb.

### <a name="five">5. Exalt beautiful code</a>

Piszemy kod, żeby był zrozumiały nie tylko dla komputera ale także dla programistów. Jest to spowodowane dlatego, że większość czasu czytamy kod dlatego tak ważen jest aby kod był jak najbardziej zrozumiały dla osoby, która widzi go pierwszy raz (lub dla nas samych po długim okresie czasu).

Nie można dokładnie sprecyzować jak wygląda czytelny kod ale kiedy go uwidzimy od razu wiemy, że taki jest. 


Czasem różnice mogą być bardzo subtelne na pierwszy rzut oka

``` Ruby
if people.include? person

if person.in? people
```
Te dwa staements robią dokładnie to samo ale czytając je mamy zupełnie różne wyobrażenia.


6. Provide sharp knives
7. Value integrated systems
8. Progress over stability
9. Push up a big tent

Sources:
- https://rubyonrails.org/doctrine/

