# SMT Solvers, Pyowa October 2018

Chad Brewbaker

Flying Dog Solutions

chad@flyingdogsolutions.com

@SMT\_SOLVERS

(This will be republished as the Awesome SMT FAQ)


## When did SMT solvers become available?

Around 2005. They built upon advances in SAT solvers from the early 2000s.

For a history of advances in SAT solvers see [Volume 4, Fascicle 6: “Satisfiability”](https://www.amazon.com/Art-Computer-Programming-Fascicle-Satisfiability/dp/0134397606).

SAT is a subroutine use to solve [NP-Complete Problems](https://en.wikipedia.org/wiki/List_of_NP-complete_problems) like the "Traveling Salesman".

  


## What problems can SMT solvers be used on?

Traditional NP-Complete problems that SAT solvers are used for like solving Minesweeper.

Equations like pictoral linear equations popular on social media. 

[Concolic testing](https://en.wikipedia.org/wiki/Concolic_testing) or concrete + symbolic testing, is an extension of unit testing where you feed in source code and an SMT solver derives unit test cases or proves none exist. Programmers do this interactively with [code coverage](https://en.wikipedia.org/wiki/Code_coverage) test cases to hit all branches.

* Code coverage and with manual specification in Z3 Python or SMT-LIB.
* Automatic generation from source code with with KLEE or SAW.
* (Future) SMT solvers will be in all IDEs not just Visual Studio. Programing will become interactive theorem proving where the IDE uses SMT solvers and known code patterns to suggest function bodies given test constraints.

[Job scheduling](https://en.wikipedia.org/wiki/Job_shop_scheduling) is scheduling of tasks to work units. As we add more complex contraints like trasnsportation times this quickly becomes NP-Complete. As software engineers we keep in mind that a nanosecond the speed of light is about one foot. ![nanosecond](http://ids.si.edu/ids/deliveryService?id=NMAH-AHB2011q00082)

* Optimizing CI build times (software engineers)
* User Experience modeling of cognitive load (Amazon, HyVee, Wells Fargo)
* Farm operations (farmers, John Deere, Granular)
* Optimizing mainframe batch flow (Principal, Farm Bureau, Grinnell Mutual)
* Optimizing manufacturing flow (John Deere, Kinze, Pella, Winnebago)
* Retail logistics (Caseys, Hy-Vee, Fareway, Kum n Go)
* Combinatorial genetic selection (DuPont Pioneer, Monsanto)    


[Linear logic](http://girard.perso.math.cnrs.fr/Synsem.pdf) is the language of "smart" contracts that take into account the consumption of resources. SMT solvers allow businesses to verify there are no unkown failure modes. This also allows for formal speciifcaion of busines rules within an organization.

* Business contract assurance (Merchants Bonding, Nationwide)
* Formal specification of Iowa Code (lawmakers, attorneys)
* Database row locking by contract
* Formal specification of cloud service guarentees

## Where do I get a SMT solver?
[Z3](https://github.com/Z3Prover/z3) is Micosoft's open source SMT solver behind the Visual Studio Intellitest product.

[CVC4](https://cvc4.cs.stanford.edu/web/) is sponsored by Google and has an embeddable Android version in the works if it hasn't been relased yet.

## Who do I go to for more information?
[Cesare Tinelli](http://homepage.cs.uiowa.edu/~tinelli/) at University of Iowa maintains the SMT-LIB stanard. 

[Nikolaj Bjorner](https://github.com/Z3Prover/z3test) at Microsoft is very responsive to bug Z3 bug fixes if you send him a failing test case.

[Galois](https://saw.galois.com) offers SMT services to U.S. Department of Defense.

[Levent Erkok](https://github.com/leventerkok) maintains the Haskell SBV project with alllows you to call several SMT solvers in parallel to compare solutions.

[Dennis Yurichev](https://yurichev.com/writings/SAT_SMT_by_example.pdf) Maintains a cookbook of examples. 

[Carter Schonwald](https://github.com/cartazio) open source R/D from Megacorp financial services in New York working on a Linear Logic specification standard as user friendly as SQL. 


## Extra Links:
[Wikipedia entry](https://en.wikipedia.org/wiki/Satisfiability_modulo_theories)

[SMT-LIB standard](http://smtlib.cs.uiowa.edu)

## Snippets
SMT-LIB syntax is a Lisp.

```lisp
(echo "print something")
```

Here is an example that delares an integer "a", a function Int f(Int, Bool), requires "a" to be greater than ten, and requires f(a, True) to be less than one hundred.
```lisp
(declare-const a Int)
(declare-fun f (Int Bool) Int)
(assert (> a 10))
(assert (< (f a true) 100))
(check-sat)
(get-model)
```
It will return something like:

```lisp
sat
(model 
  (define-fun a () Int
    11)
  (define-fun f ((x!1 Int) (x!2 Bool)) Int
    (ite (and (= x!1 11) (= x!2 true)) 0
      0))
)
```
We use (push) and (pop) to add and remove constraints as we go.

Here is the Python syntax for the Z3 solver.

```python
from z3 import *

x = Real('x')
y = Real('y')
s = Solver()
s.add(x + y > 5, x > 1, y > 1)
print(s.check())
print(s.model())
```

[Pull request](https://github.com/DennisYurichev/yurichev.com/pull/2/files) showing how to use the Z3 optimizer syntax and convert from Z3 variable data types to basic Python datatypes.









