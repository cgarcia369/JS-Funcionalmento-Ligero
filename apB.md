# Functional-Light JavaScript
# Appendix B: The Humble Monad

Let me just start off this appendix by admitting: I did not know much about what a monad was before starting to write the following. And it took a lot of mistakes to get something sensible. If you don't believe me, go look at the commit history of this appendix in the Git repo for this book (https://github.com/getify/Functional-Light-JS)!

I am including the topic of monads in the book because it's part of the journey that every developer will encounter while learning FP, just as I have in this book writing.

We're basically ending this book with a brief glimpse at monads, whereas most other FP literature kinda almost starts with monads! I do not encounter in my "functional light" programming much of a need to think explicitly in terms of monads, so that's why this material is more bonus than main core. But that's not to say monads aren't useful or prevalent -- they very much are.

There's a bit of a joke around the JavaScript FP world that pretty much everybody has to write their own tutorial or blog post on what a monad is, like the writing of it alone is some rite-of-passage. Over the years, monads have variously been depicted as burritos, onions, and all sorts of other wacky conceptual abstractions. I hope there's none of that silly business going on here!

> A monad is just a monoid in the category of endofunctors.

We started the preface with this quote, so it seems fitting we come back to it here. But no, we won't be talking about monoids, endofunctors, or category theory. That quote is not only condescending, but totally unhelpful.

My only hope for what you get out of this discussion is to not be scared of the term monad or the concept anymore -- I have been, for years! -- and to be able to recognize them when you see them. You might, just maybe, even use them on occassion.

## Type

There's a huge area of interest in FP that we've basically stayed entirely away from throughout this book: type theory. I'm not going to get very deep into type theory, because quite frankly I'm not qualified to do so. And you wouldn't appreciate it even if I did.

But what I will say is that a monad is basically a value type.

The number `42` has a value type (number!) that brings with it certain characteristics and capabilities that we rely on. The string `"42"` may look very similar, but it has a different purpose in our program.

In object oriented programming, when you have a set of data (even a single discrete value) and you have some behavior you want to bundle with it, you create an object/class to represent that "type". Instances are then members of that type. This practice generally goes by the name "Data Structures".

I'm going to use the notion of data structures very loosely here, and assert that we may find it useful in a program to define a set of behaviors and constraints for a certain value, and bundle them together with that value into a single abstraction. That way, as we work with one or more of those kinds of values in our program, their behaviors come along for free and will make working with them more convenient. And by convenient, I mean more declarative and approachable for the reader of your code!

A monad is a data structure. It's a type. It's a set of behaviors that are specifically designed to make working with a value predictable.

Recall in Chapter 8 that we talked about functors: a value along with a map-like utility to perform an operation on all its constitute data members. A monad is a functor that includes some additional behavior.

## Loose Interface

Actually, a monad isn't a single data type, it's really more like a related collection of data types. It's kind of an interface that's implemented differently depending on the needs of different values. Each implementation is a different type of monad.

For example, you may read about the "Identity Monad", the "IO Monad", the "Maybe Monad", the "Either Monad", or a variety of others. Each of these has the basic monad behavior defined, but it extends or overrides the interactions according to the use cases for each different type of monad.

It's a little more than an interface though, because it's not just the presence of certain API methods that makes an object a monad. There's a certain set of guarantees about the interactions of these methods that is necessary, to be monadic. These well-known invariants are critical to usage of monads improving readability by familiarity; otherwise, it's just an ad hoc data structure that must be fully read to be understood by the reader.

As a matter of fact, there's not even just one single unified agreement on the names of these monadic methods, the way a true interface would mandate; a monad is more like a loose interface. Some people call a certain method `bind(..)`, some call it `chain(..)`, some call it `flatMap(..)`, etc.

So a monad is an object data structure with sufficient methods (of practically any name or sort) that at a minimum satisfy the main behavioral requirements of the monad definition. Each kind of monad has a different kind of extension above the minimum. But, because they all have an overlap in behavior, using two different kinds of monads together is still straightforward and predictable.

It's in that sense that monads are sort of like an interface.

## Maybe

It's very common in FP material to cover well-known monads like Maybe. And actually, the Maybe monad is really a pairing of two other simpler monads: Just and Nothing.

Since a monad is a type, you might think we'd define `Maybe` as a class to be instantiated. That's a valid way of doing it, but it introduces `this`-binding issues in the methods that I don't want to juggle; instead I'm going to stick with just a simple function / object approach.

Here's a minimal implementation of Maybe:

```js
var Maybe = { Just, Nothing, of/* aka: unit, pure */: Just };

function Just(val) {
	return { map, chain, ap, inspect };

	// *********************

	function map(fn) { return Just( fn( val ) ); }
	// aka: bind, flatMap
	function chain(fn) { return fn( val ); }
	function ap(anotherMonad) { return anotherMonad.map( val ); }

	function inspect() {
		return `Just(${ val })`;
	}
}

function Nothing() {
	return { map: Nothing, chain: Nothing, ap: Nothing, inspect };

	// *********************

	function inspect() {
		return "Nothing";
	}
}
```

**Note:** The `inspect(..)` method is included here only for our demonstration purposes. It serves no direct role in the monadic sense.

Don't worry if most of this doesn't make sense right now. We're not gonna obsess much over the details or the math/theory behind the design of the Monad. Instead, we'll focus more on illustrating what we can do with it.

Any monad instances of both `Just(..)` and `Nothing()` will all have `map(..)`, `chain(..)` (also called `bind(..)` or `flatMap(..)`), and `ap(..)` methods, as do all monads. The purpose of these methods and their behavior is to provide a standardized way of multiple monad instances working together. You'll notice that whatever `val` value a `Just(..)` instance holds, it's never changed. All methods create new monad instances instead of mutating it.

Maybe is the pairing of these two monads. If a value is non-empty, it's represented by an instance of `Just(..)`; if it's empty, it's represented by an instance of `Nothing()`. Notice there's no imposition here of what "empty" means -- your code gets to decide that. More on that in the next section.

But the value of this kind of monad representation is that whether we have a `Just(..)` instance of a `Nothing()` instance, we'll use it the same. `Nothing()` instances have no-op definitions for all methods. So if such a monad instance shows up in our monadic operations, it has the effect of basically short-circuiting to ignore behavior.

The power of the Maybe abstraction is to encapsulate that behavior/no-op duality implicitly.

### Different Maybes

Many implementations of a JavaScript Maybe monad include a check (usually in `map(..)`) to see if the value is `null` / `undefined`, and skipping the behavior if so. In fact, Maybe is trumpeted as being valuable precisely because it sort of automatically short-circuits its behavior with the encapsulated empty-value check.

Here's how Maybe is typically illustrated:

```js
// instead of unsafe `console.log( someObj.something.else.entirely )`:

Maybe.of( someObj )
.map( prop( "something" ) )
.map( prop( "else" ) )
.map( prop( "entirely" ) )
.map( console.log );
```

In other words, if at any point in the chain we get a `null` / `undefined` value, the Maybe magically switches into no-op mode -- it's now a `Nothing()` monad instance! -- and stops doing anything for the rest of the chain. That makes the nested property access safe against throwing JS exceptions if some property is missing/empty. That's cool, and a nice helpful abstraction for sure!

But... that approach to Maybe is not a pure monad.

The core spirit of a Monad says that it must be valid for all values and cannot do any inspection of the value, at all -- not even a null check. So those other implementations are cutting corners for the sake of convenience. It's not a huge deal, but when it comes to learning something, you should probably learn it in its purest form first before you go bending the rules.

The earlier implementation of the Maybe monad I provided differs from other Maybes primarily in that it does not have the null-check in it. Also, we present `Maybe` as a loose pairing of `Just(..)` / `Nothing()`.

So wait. If we don't get the automatic short-circuting, why is Maybe useful at all?!? That seems like its whole point.

Never fear! We can simply provide the empty-check externally, and the rest of the short-circuting behavior of the Maybe monad will work just fine. Here's how you could do the `someObj.something.else.entirely` nested-property access from before. But we'll do it more "correctly":

```js
function isEmpty(val) {
	return val === null || val === undefined;
}

var safeProp = curry( function safeProp(prop,obj){
	if (isEmpty( obj[prop] )) return Maybe.Nothing();
	return Maybe.of( obj[prop] );
} );

Maybe.of( someObj )
.chain( safeProp( "something" ) )
.chain( safeProp( "else" ) )
.chain( safeProp( "entirely" ) )
.map( console.log );
```

We made a `safeProp(..)` that does the empty-check, and selects either a `Nothing()` monad instance if so, or wraps the value in a `Just(..)` instance (via `Maybe.of(..)`). Then instead of `map(..)`, we use `chain(..)` which knows how to "unwrap" the monad that `safeProp(..)` returns.

We get the same chain short-circuiting upon encountering an empty value. We just don't embed that logic into the Maybe.

The benefit of the monad, and Maybe specifically, is that our `map(..)` and `chain(..)` methods have a consistent and predictable interaction regardless of which kind of monad comes back. That's pretty cool!

## Humble

Now that we have a little more understanding of Maybe and what it does, I'm going to put a little twist on it -- and add some self-deferential humor to our discussion -- by inventing the Maybe+Humble monad. Technically, `Humble(..)` is not a monad itself, but a factory function that produces a Maybe monad instance.

Humble is an admittedly contrived data structure wrapper that uses Maybe to track the status of an `egoLevel` number. Specifically, `Humble(..)`-produced monad instances only operate if their ego level value is low enough (less than `42`!) to be considered humble; otherwise it's a `Nothing()` no-op. That should sound a lot like Maybe; it's pretty similar!

Here's our factory function for our Maybe+Humble monad:

```js
function Humble(egoLevel) {
	// accept anything other than a number that's 42 or higher
	return !(Number( egoLevel ) >= 42) ?
		Maybe.of( egoLevel ) :
		Maybe.Nothing();
}
```

// TODO

## Summary

What is a monad, anyway?

A monad is a value type, an interface, an object data structure with encapsulated behaviors.

But none of those definitions are particularly useful. Here's an attempt at something better: a monad is how you organize behavior with a value in a more declarative way.

As with everything else in this book, use monads where they are helpful but don't use them just because everyone else talks about them in FP. Monads aren't a universal silver bullet, but they do offer some utility when used conservatively.