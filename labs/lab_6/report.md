![image](https://user-images.githubusercontent.com/68211239/158256611-7220dd10-16f5-48fd-89ed-f41fa7fb1f53.png)
First image



```{r}
import gzip
from string import ascii_lowercase as lowercase

import networkx as nx

#-------------------------------------------------------------------
#   The Words/Ladder graph of Section 1.1
#-------------------------------------------------------------------


def generate_graph(words):
    G = nx.Graph(name="words")
    lookup = dict((c, lowercase.index(c)) for c in lowercase)

    def edit_distance_one(word):
        for i in range(len(word)):
            left, c, right = word[0:i], word[i], word[i + 1:]
            j = lookup[c]  # lowercase.index(c)
            for cc in lowercase[j + 1:]:
                yield left + cc + right
    candgen = ((word, cand) for word in sorted(words)
               for cand in edit_distance_one(word) if cand in words)
    G.add_nodes_from(words)
    for word, cand in candgen:
        G.add_edge(word, cand)
    return G


def words_graph():
    """Return the words example graph from the Stanford GraphBase"""
    fh = gzip.open('words_dat.txt.gz', 'r')
    words = set()
    for line in fh.readlines():
        line = line.decode()
        if line.startswith('*'):
            continue
        w = str(line[0:5])
        words.add(w)
    return generate_graph(words)


if __name__ == '__main__':
    G = words_graph()
    print("Loaded words_dat.txt containing 5757 five-letter English words.")
    print("Two words are connected if they differ in one letter.")
    print("Graph has %d nodes with %d edges"
          % (nx.number_of_nodes(G), nx.number_of_edges(G)))
    print("%d connected components" % nx.number_connected_components(G))

    for (source, target) in [('chaos', 'order'),
                             ('plots', 'graph'),
                             ('moron', 'smart'),
                             ('flies', 'swims'),
                             ('mango', 'peach'),
                             ('pound', 'marks')]:
        print("Shortest path between %s and %s is" % (source, target))
        try:
            sp = nx.shortest_path(G, source, target)
            for n in sp:
                print(n)
        except nx.NetworkXNoPath:
            print("None")
```

Loaded words_dat.txt containing 5757 five-letter English words. <br>
Two words are connected if they differ in one letter. <br>
Graph has 5757 nodes with 14135 edges <br>
853 connected components <br>
Shortest path between chaos and order is <br>
chaos <br>
choos <br>
shoos <br>
shoes <br>
shoed <br>
shred <br>
sired <br>
sided <br>
aided <br>
added <br>
adder <br>
odder <br>
order <br>
Shortest path between plots and graph is <br>
plots <br>
plats <br>
plate <br>
prate <br>
grate <br>
grape <br>
graph <br>
Shortest path between moron and smart is <br>
moron <br>
boron <br>
baron <br>
caron <br>
capon <br>
capos <br>
capes <br>
canes <br>
banes <br>
bands <br>
bends <br>
beads <br>
bears <br>
sears <br>
stars <br>
start <br>
smart <br>
Shortest path between flies and swims is <br>
flies <br>
flips <br>
slips <br>
slims <br>
swims <br>
Shortest path between mango and peach is <br>
mango <br>
mange <br>
marge <br>
merge <br>
merse <br>
terse <br>
tease <br>
pease <br>
peace <br>
peach <br>
Shortest path between pound and marks is <br>
None <br>



```{r}
import gzip
from string import ascii_lowercase as lowercase

import networkx as nx

#-------------------------------------------------------------------
#   The Words/Ladder graph of Section 1.1
#-------------------------------------------------------------------


def generate_graph(words):
    G = nx.Graph(name="words")
    lookup = dict((c, lowercase.index(c)) for c in lowercase)

    def edit_distance_one(word):
        for i in range(len(word)):
            left, c, right = word[0:i], word[i], word[i + 1:]
            j = lookup[c]  # lowercase.index(c)
            for cc in lowercase[j + 1:]:
                yield left + cc + right
    candgen = ((word, cand) for word in sorted(words)
               for cand in edit_distance_one(word) if cand in words)
    G.add_nodes_from(words)
    for word, cand in candgen:
        G.add_edge(word, cand)
    return G


def words_graph():
    """Return the words example graph from the Stanford GraphBase"""
    fh = gzip.open('words_dat2.txt.gz', 'r')
    words = set()
    for line in fh.readlines():
        line = line.decode()
        if line.startswith('*'):
            continue
        w = str(line[0:4])
        words.add(w)
    return generate_graph(words)


if __name__ == '__main__':
    G = words_graph()
    print("Loaded words_dat2.txt containing 5757 four-letter English words.")
    print("Two words are connected if they differ in one letter.")
    print("Graph has %d nodes with %d edges"
          % (nx.number_of_nodes(G), nx.number_of_edges(G)))
    print("%d connected components" % nx.number_connected_components(G))

    for (source, target) in [('cold', 'warm'),
                             ('love', 'hate'),
                             ('good', 'evil'),
                             ('pear', 'beef'),
                             ('make', 'take')]:
        print("Shortest path between %s and %s is" % (source, target))
        try:
            sp = nx.shortest_path(G, source, target)
            for n in sp:
                print(n)
        except nx.NetworkXNoPath:
            print("None")
```

Loaded words_dat2.txt containing 4273 four-letter English words. <br>
Two words are connected if they differ in one letter. <br>
Graph has 4273 nodes with 21047 edges <br>
81 connected components <br>
Shortest path between cold and warm is <br>
cold <br>
wold <br>
word <br>
ward <br>
warm <br>
Shortest path between love and hate is <br>
love <br>
hove <br>
have <br>
hate <br>
Shortest path between good and evil is <br>
good <br>
goad <br>
glad <br>
glid <br>
elid <br>
elit <br>
exit <br>
exil <br>
evil <br>
Shortest path between pear and beef is <br>
pear <br>
bear <br>
beer <br>
beef <br>
Shortest path between make and take is <br>
make <br>
take <br>



```{r}
import gzip
import itertools
from string import ascii_lowercase as lowercase

import networkx as nx

#-------------------------------------------------------------------
#   The Words/Ladder graph of Section 1.1
#-------------------------------------------------------------------


def generate_graph(words):
    G = nx.Graph(name="words")
    lookup = dict((c, lowercase.index(c)) for c in lowercase)
    def edit_distance_one(word):
        hold = itertools.permutations(word, 5)
        for new_word in hold:
            newt = "".join(new_word)
            for i in range(len(newt)):
                left, c, right = newt[0:i], newt[i], newt[i + 1:]
                j = lookup[c]  # lowercase.index(c)
                for cc in lowercase[j + 1:]:
                    yield left + cc + right
    candgen = ((word, cand) for word in sorted(words)
               for cand in edit_distance_one(word) if cand in words)
    G.add_nodes_from(words)
    for word, cand in candgen:
        G.add_edge(word, cand)
    return G


def words_graph():
    """Return the words example graph from the Stanford GraphBase"""
    fh = gzip.open('words_dat.txt.gz', 'r')
    words = set()
    for line in fh.readlines():
        line = line.decode()
        if line.startswith('*'):
            continue
        w = str(line[0:5])
        words.add(w)
    return generate_graph(words)


if __name__ == '__main__':
    G = words_graph()
    print("Loaded words_dat.txt containing 5757 five-letter English words.")
    print("Two words are connected if they differ in one letter.")
    print("Graph has %d nodes with %d edges"
          % (nx.number_of_nodes(G), nx.number_of_edges(G)))
    print("%d connected components" % nx.number_connected_components(G))

    for (source, target) in [('chaos', 'order'),
                             ('plots', 'graph'),
                             ('moron', 'smart'),
                             ('flies', 'swims'),
                             ('mango', 'peach'),
                             ('pound', 'marks')]:
        print("Shortest path between %s and %s is" % (source, target))
        try:
            sp = nx.shortest_path(G, source, target)
            for n in sp:
                print(n)
        except nx.NetworkXNoPath:
            print("None")
```

Loaded words_dat.txt containing 5757 five-letter English words. <br>
Two words are connected if they differ in one letter.<br>
Graph has 5757 nodes with 112278 edges<br>
16 connected components<br>
Shortest path between chaos and order is<br>
chaos<br>
chose<br>
chore<br>
coder<br>
order<br>
Shortest path between plots and graph is<br>
plots<br>
opals<br>
plash<br>
sharp<br>
graph<br>
Shortest path between moron and smart is<br>
moron<br>
manor<br>
roams<br>
smart<br>
Shortest path between flies and swims is<br>
flies<br>
isles<br>
semis<br>
swims<br>
Shortest path between mango and peach is<br>
mango<br>
conga<br>
nacho<br>
poach<br>
peach<br>
Shortest path between pound and marks is<br>
pound<br>
mound<br>
monad<br>
moans<br>
roams<br>
marks<br>


```{r}
import gzip
import itertools
from string import ascii_lowercase as lowercase

import networkx as nx

#-------------------------------------------------------------------
#   The Words/Ladder graph of Section 1.1
#-------------------------------------------------------------------


def generate_graph(words):
    G = nx.Graph(name="words")
    lookup = dict((c, lowercase.index(c)) for c in lowercase)
    def edit_distance_one(word):
        #hold = itertools.permutations(word, 5)
        #for new_word in hold:
            #newt = "".join(new_word)
            newt = word
            for i in range(len(newt)):
                left, c, right = newt[0:i], newt[i], newt[i + 1:]
                j = lookup[c]  # lowercase.index(c)
                for cc in lowercase[j + 1:]:
                    yield left + cc + right
    candgen = ((word, cand) for word in sorted(words)
               for cand in edit_distance_one(word) if cand in words)
    G.add_nodes_from(words)
    for word, cand in candgen:
        G.add_edge(word, cand)
    return G


def words_graph():
    """Return the words example graph from the Stanford GraphBase"""
    fh = gzip.open('words_dat2.txt.gz', 'r')
    words = set()
    for line in fh.readlines():
        line = line.decode()
        if line.startswith('*'):
            continue
        w = str(line[0:4])
        words.add(w)
    return generate_graph(words)

def prior(word, words):
    hold = words.neighbors(word)
    for x in hold:
        print(x)
    return
    
    

if __name__ == '__main__':
    G = words_graph()
    print("Loaded words_dat.txt containing 5757 four-letter English words.")
    print("Two words are connected if they differ in one letter.")
    print("Graph has %d nodes with %d edges"
          % (nx.number_of_nodes(G), nx.number_of_edges(G)))
    print("%d connected components" % nx.number_connected_components(G))

    for (target) in ['slid', 'dote', 'herd', 'omen', 'nine', 'sell', 'stat', 'what']:
        print("Prior/Follow: " + (target))
        try:
            prior(target, G)
        except nx.NetworkXNoPath:
            print("None")
```

Loaded words_dat.txt containing 5757 four-letter English words.<br>
Two words are connected if they differ in one letter.<br>
Graph has 4273 nodes with 21047 edges<br>
81 connected components<br>
Prior/Follow: slid<br>
elid<br>
glid<br>
skid<br>
sled<br>
slic<br>
snid<br>
slie<br>
slil<br>
slim<br>
slin<br>
slip<br>
slit<br>
Prior/Follow: dote<br>
cote<br>
date<br>
dete<br>
doge<br>
dole<br>
dome<br>
done<br>
dope<br>
dose<br>
hote<br>
mote<br>
note<br>
tote<br>
vote<br>
dove<br>
dowe<br>
doye<br>
doze<br>
dott<br>
Prior/Follow: herd<br>
hard<br>
head<br>
heed<br>
herb<br>
nerd<br>
perd<br>
hord<br>
here<br>
hero<br>
hert<br>
Prior/Follow: omen<br>
amen<br>
emen<br>
omeg<br>
open<br>
oven<br>
Prior/Follow: nine<br>
dine<br>
fine<br>
line<br>
mine<br>
nice<br>
pine<br>
sine<br>
tine<br>
vine<br>
wine<br>
none<br>
nise<br>
nite<br>
nixe<br>
ninj<br>
ninn<br>
nint<br>
Prior/Follow: sell<br>
bell<br>
cell<br>
dell<br>
fell<br>
hell<br>
jell<br>
kell<br>
sall<br>
seal<br>
sela<br>
self<br>
tell<br>
well<br>
yell<br>
sill<br>
sull<br>
Prior/Follow: stat<br>
scat<br>
seat<br>
skat<br>
slat<br>
spat<br>
stab<br>
stac<br>
staf<br>
stag<br>
stai<br>
stak<br>
stal<br>
stam<br>
stan<br>
stap<br>
star<br>
stas<br>
swat<br>
stet<br>
stav<br>
stay<br>
Prior/Follow: what<br>
chat<br>
that<br>
whac<br>
whal<br>
wham<br>
whan<br>
whar<br>
wrat<br>
whet<br>
whit<br>
