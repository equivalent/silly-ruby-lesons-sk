# otazka

```
class Friends
  attr_accessor :names, :ages
  def initialize (names, ages)
    @names = []
    @ages = []
  end

  def << friend
    @names << name
    @ages << age
  end
end

3.times do 
  puts "Enter your friend's name and then his age"
  name = gets.chomp
  age = gets.to_i
end

friendname = Friends.new (names)
friendname << name
friendage = Friends.new (ages)
friendage << age
friendname.each do { |nam| puts nam }

friendage.each do { |age| puts age } 
```

 aby to vzal čert!
 tomy ja sa tu snažím o to aby si zadaval mená a veky priatelov a aby trieda Friends ich dávala do zoznamov @names a @ages 
ktoré by sa potom normálne zobrazia... ale čo čert nechcel, sťažuje sa mi program najprv na nezadefinované premenné names a ages
 a potom mi tu zase nechápe línie 23 a 25... ta ja neviem čo som domrdal... no .. jeden program mi už pekne funguje.. ale tento tu ma sere

# odpoved

`Friends.new (names)` a `Friends.new(names)` je rozdiel. Ta medzera spravi vela. 

V tvojom pripade to vyzera rovnako a sprava sa to podobne ale predstav si to takto 

```ruby
  def pozdrav(meno=nil, priezvysko=nil)
    "ahoj #{meno} #{priezvysko}"
  end

  pozdrav('stanko', 'stankovic')
  #=> "ahoj stanko stankovic" 

  pozdrav ('stanko', 'stankovic')
  # SyntaxError:

  # ale toto by fungovalo
  pozdrav ('stanko' + 'stankovic')
  # => "ahoj stankostankovic " 

  #pretoze to je to iste ako
  name = 'stanko' + 'stankovic'
  pozdrav(name, nil)
```

podstata je v tom ze ked das nieco do zatvorky s medzeru znamena to ze
to chces aby sa vyhodnotilo predtym nez to posunie do metody

rovnako ako v nasobilke

```ruby
2 * (1 + 1) # == 4
```

ty  robis nieco ako: 

```ruby
friendname = Friends.new (names)
```

malo by byt 

```
friendname = Friends.new(names)
```

avsak !! initialize ma tiez medzeru == Syntax chyba

```
class Friends
  attr_accessor :names, :ages
  # def initialize (names, ages) # zle 
  def initialize(names, ages)    # po uprave
    @names = []
    @ages = []
  end

  # ...
end
```

tezaz ked skusime 

```
friendname = Friends.new(names)
```

dostaneme iny error:

```
# ArgumentError: wrong number of arguments (1 for 2)
```

to hovori ze mi specifikujeme 1 argument (names) ale on ocakava dva
napriklad

```
friendname = Friends.new(names, ages)
```

skusim preskocit dalsie chyby a napisem ti len riesenie 

```
class Friends
  attr_accessor :names, :ages

  def initialize(names, ages)
    @names = names
    @ages = ages
  end

  def <<(name, age)
    @names << name
    @ages << age
  end
end

f = Friends.new(['adam', 'katka'], [10, 20])
f.names  # => ['adam', 'katka']
f.ages   # => [10, 20]
f.<<('tomi', 27)   #celkom skarede 
f.names  #  => ["adam", "katka", "tomi"]
f.ages   #  => [10, 20, 27] 
```

ok toto by sme mali avsak toto riesenie je velmi skarede  skusme
alternativu


```
class Friends
  attr_accessor :names, :ages

  def initialize(names, ages)
    @names = names
    @ages = ages
  end

  def add(name, age)
    @names << name
    @ages << age
  end
end

f = Friends.new(['adam', 'katka'], [10, 20])
f.names  # => ['adam', 'katka']
f.ages   # => [10, 20]
f.add tomi', 27 
f.names  #  => ["adam", "katka", "tomi"]
f.ages   #  => [10, 20, 27] 
```

to uz je krajsie len hmm tazko rozoznavame kto ma kolko rokov, co tak: 

```
class Friends
  attr_accessor :names, :ages

  def initialize(friends)
    @names = []
    @ages = []
    friends.each do |hash|
      add(hash)
    end
  end

  def add(hash)
    @names << hash[:name]
    @ages <<  hash[:age]
  end
end

f = Friends.new([{ name: 'adam', age: 10 }, { name: 'katka', age: 20 }])
f.names  # => ['adam', 'katka']
f.ages   # => [10, 20]
f.add name: 'tomi', age: 27 
f.names  #  => ["adam", "katka", "tomi"]
f.ages   #  => [10, 20, 27] 
```


zatial len tolko,

tomyyy, ja som sa s tým babral a špekuloval až som konečne donútil ten program pracovať tak ako som chcel ja.. no vypadá takto: 

class Friends
  def initialize(name, age)
    puts "Your friend's name and age:"
    @name = name
    @age = age
  end
  def his_name
    name = gets
    @name << name
  end
  def his_age
    age = gets
    @age << age
  end
  def display
    full_name = @name.capitalize
    puts "Your friend's names are #{full_name} and their ages are #{@age}"
  end
end

g = Friends.new("","")

3.times do
  g.his_name
  g.his_age
end
g.display
