Otazka:

```
otázka číslo... no proste otázka: ked napíšem:  premenna.each do |prem|
vytvorim tak blok do-end hej? .. a teraz tá prem v tých pipe || to je
čo? to akože nahradím premennú premom?
```

Odpoved:

Presne neviem co tym myslis ale pokusim sa ti to viac objasnit takto

```
a = [1,2,3,4,5]   # toto je Array
```

stym mozes urobit nieco taketo:

```
a.each do |item|
  p item
end
```

... a to je presne to iste ako urobit toto

```
a.each { |item| p item } # ...ale iba na jeden riadok
```

este ta nejdem zatazovat tym ze toto je Enumerator a ako skutacne funguje,
zatial to len ber ze  kazdy objekt v tvojom Array ulozi nachvilu do
premenej (variable) `item`. Stou premenout `item` si potom mozes robyt
hocico co chces ako keby si povedal `item = 1` alebo `item = 1`, ...

To znamena ze ja ju vypysem len.

ono by si cely ten kod mohol prepisat takto

```
item = 1
p item


item = 2
p item


item = 3
p item

item = 4
p item

# atd...
```

Asi uz chapes benefity :) ?

Mozes stym robit aj nieco komplikovanejsie

```ruby
b = ['stanko', 'stol', 'strecha']
b.each do |hocico|
  c = hocico.upcase
  c = c.gsub('S', 'Z')
  puts "ahoj #{c}"
end
```

.. tento kod vypluje toto:

```
 ahoj ZTANKO
 ahoj ZTOL
 ahoj ZTRECHA
```
