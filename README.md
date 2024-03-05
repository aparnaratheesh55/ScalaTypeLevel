# Scala Type Level Programming 
* Type level programming use the compiler as executable on the other hand other programs should be compiled and runned.
* Scala compiler actually have the power to solve the program quickly.
* It will be having some relationships which the compiler actually takes.
* Trait is basically used to share the interfaces(methods) in scala between classes.
* There should be a type defenition in scala
* Type alias means alternative names.
* Type members represent the types rather than the value.
```trait +[A <: Nat, B <: Nat] { type Result <: Nat }
object + {
    type Plus[A <: Nat, B <: Nat, S <: Nat] = +[A, B] { type Result = S }
    implicit val zero: Plus[_0, _0, _0] = new +[_0, _0] { type Result = _0 }
    implicit def basicRight[B <: Nat](implicit lt: _0 < B): Plus[_0, B, B] = new +[_0, B] { type Result = B }
    implicit def basicLeft[B <: Nat](implicit lt: _0 < B): Plus[B, _0, B] = new +[B, _0] { type Result = B }
    implicit def inductive[A <: Nat, B <: Nat, S <: Nat](implicit plus: Plus[A, B, S]): Plus[Succ[A], Succ[B], Succ[Succ[S]]] =
      new +[Succ[A], Succ[B]] { type Result = Succ[Succ[S]] }
    def apply[A <: Nat, B <: Nat](implicit plus: +[A, B]): Plus[A, B, plus.Result] = plus
}

def main(args: Array[String]): Unit = {
    println(show(+[_2, _3]))
}
```

* so here ith will show thw result as TypeTag as Succ[Succ[0]]=succ[succ[succ[0]]]=succ[succ[succ[succ[succ[0]]]]]
