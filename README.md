# μDBug

The μDBug (pronounced Mud-Bug, an eponym of the freshwater crustacean)
is a logic database or knowledge store designed with modern
considerations.  The project builds from ideas first explored in the
semantic-web but incorporates past learning from logic programming
languages such as prolog and relational databases such as SQL. Naming
and addressing is given by URIs allowing resources to be described
across databases, and JSON is used as a universal interchange format.

## Typed 

The language is *typed* using a variant of Hindley Milner polymorphic
typing. This allows it to be used as a primary database storage
system, something which prolog, being untyped, militates against.

Datatypes can be created from a set of primitive types which include
all of the standard SQL datatypes. This is then extended with
*inductive* types which combine these types to create more complex
elements.

## Logical

A μDBug *predicate* is the building block of the way we express
relationships. A predicate ``p(A,B,...,C)`` expresses that the fact
``p`` holds, yielding a JSON stream with the free variables ``A...C``
as names binding to the respective values for which the query is true
like so: ``{'prefix:A' : v_a , ... 'prefix:C' : v_c}``. The ``prefix``
will be the currently specified default prefix, which is usually the
name of the current knowledge base. If the query is not satisfiable,
there will be nothing returned.

## Persistent

The μDBug knowledge store is persistent and updatable. We can use it
as a replacement for SQL as it is provides a superset of the
functionality. The additions are essentially a more web-aware syntax
and the ability perform recursive queries.

Some predicates can be marked as *ground* which allows them to be
treated much the way a table is in SQL. This allows us to add
indexing, fast updates, and simplies joins and queries for certain
types of non-recursive query. 

Ground queries admit direct updates to facts stored in the
database. This allows us to persistently represent information as is
done in SQL.

Derived predicates are essentially *views* as in SQL. We can update
views with a syntax very like the one used for changing ground facts,
but which uses quoted source.

## Performance Oriented

The goal of μDBug is to be a high-permance solution to knowledge
stores which is flexible and allows more application logic to live in
the Database itself. Model driven software needs models to reside
somewhere, and the most sensible place for this to live is in a
database. Increasing the ease by which developers can place complex
information in the database, helps to relieve the application of
complicated logical derivations which are better done in a logic based
language.

Performance in μDBug is possible due to the following features, not
often found in logic programming languages: 

* Types 

Unlike prolog, we have a strongly typed language that allows us to
layout data in an efficient manner. All types can be marked
as indexible by providing a total order. This also enables the
determinacy and coverage to be checked automatically in some cases.

* Determinacy and coverage

Predicates can be checked to see if there are no (vacuous), none or
one (semidet), exactly one (det) or none or many (nondet). In the case
of deterministic predicates, we check the coverage of the inputs on a
given *mode*. Modes allow predicates to be called in various ways with
various unknowns.

* Recursive

Big data recursive queries are inefficient currently as they require
repeated round-trips to the database in order to follow links. There
are ad-hoc solutions provided with *follow* type clauses in various
extentions to SQL but they are generally an overthought tacked on, and
they serve to present transitivity, but do not express such notions as
greatest and least fixed points, which are central logical
requirements for reasoning about graphs.

