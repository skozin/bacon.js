Fantasy Land
------------

Bacon.js implements some of the algebraic structures defined in the
[Fantasy Land
Specification](https://github.com/puffnfresh/fantasy-land). To match the
specification, I've added a few aliases:

```coffeescript
EventStream.of = Bacon.once
EventStream.empty = Bacon.never
Property.of = Bacon.constant
Observable :: chain = Observable :: flatMap
```

### Functor

Both `EventStream` and `Property` implement `Functor`, with their `map`
function.

### Monad

`EventStream` implements `Monad`:

```coffeescript
EventStream.of("fun").chain((x) -> EventStream.of(x))
```

`Property` also supports the monadic interface, but I'm not sure if it's
strictly a Fantasy Land monad, because the `chain` method actually
returns an `EventStream`

### Applicative

`Property` implementa `Applicative`. The `ap` function is based on
`compose` so it combines latest values of two Properties.

`EventStream` also implements `Applicative`, but only because the
specification currently dictates that all Monads must be Applicative too. The `ap` function uses
composition by flatMap to be consistent with the monadic interface.

### Monoid, Semigroup

`EventStream` implements Monoid and thus Semigroup though `empty` and
`concat`.


