# Universes

## Sorts :
- Prop
- SProp
- Type@{u} (u: LevelAlgExpr.t)

## Levels :

## Concrete universe levels
Basically nats

## Abstract universe levels

### Level.t
- Zero
- NamedLevel_for_mono of string
- DeBruijnVarLevel_for_poly of nat

Under a valuation (for_mono: string -> positive; for_poly: nat -> nat), they get mapped to nats

### LevelExpr.t
- Shifted Level.t; you add a nat

### LevelAlgExpr.t
- NonEmptySet of LevelExpr.t; you take the max


## More

### ConstraintType.t
- Le of (z: Z) (`fun u u' => [[u]] + z <= [[u']]`)
- Eq (`fun u u' => [[u]] = [[u']]`)
### UnivConstraint.t
- (u: Level.t, constraint, u': Level.t) `(fun (v: valuation) => [[constraint]] (v u) (v u'))`
### ConstraintSet.t
- set of UnivConstraint.t; conjunction of it all

### Instance.t
- list of Level.t; to replace the DeBruijnVarLevel_for_poly in a term (why not LevelExpr.t ?)

Under a UnivSubst, does that substitution
closedu checks how many (how high) DeBruijnVarLevel_for_poly there are (go)

### UContext.t
- list of names, an Instance.t, a ConstraintSet.t
a full context for universe level arguments in universe-polymorphic declarations (names for names, instance is the identity substitution with the right number of variables, constraints)

### AUContext.t
- list of names, a ConstraintSet.t
a reduced context for universe level arguments in universe-polymorphic declarations (names and constraints, the instance can be generated based on the length of the list of names)

### ContextSet.t
- a set of levels, a set of constraints; the set of all declared levels (should be only NamedLevel_for_monos) and their constraints (global_env-scale)

### Variance.t
- Irrelevant
- Covariant
- Invariant
Something to generate constraints for inductives to follow

### universes_decl
- Monomorphic_ctx (no ctx)
- Polymorphic_ctx (AUContext.t)
beared by all environment declarations (and what global_env_ext has that global_env doesn't, for some reason)

### universes_entry
Older? version of universes_decl where Monomorphic have their ContextSet.t (set of declared levels)

### Some operations
- satisfies{0,} : finally apply the constraints, on a valuation
- consistent : there exists a valuation which satisfies the constraints
- {leq,eq}{0,}_levelalg_n : all valuations which satisfy φ give that constraint on u, u' (or true if not check_univs)
- valid_constraints : φ is stronger than φ'
