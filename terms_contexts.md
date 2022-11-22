# Basic operations and predicates

## Lift
- De Bruijn lift on variable indices `lift n k tm`

- lift on all types and bodies of a context : `lift_context n k Γ`

- We go from `Σ ; Γ ,,, [] ,,, Γ'' ,,, Γ''' |- tm`  
    to `Σ ; Γ ,,, Γ' ,,, lift_context #|Γ'| #|Γ'''| Γ'' ,,, lift_context #|Γ'| 0 Γ''' |- lift #|Γ'| #|Γ'' ,,, Γ'''| tm`

## Subst
- Substitution of variables `subst s k tm`

- subst on all types and bodies of a context : `subst_context s k Γ`
- (subst on all types and bodies of a telescope or *reverse context* : `subst_telescope s k Γ`)

- Assuming `Γ |- s : Γ'`, we go from `Σ ; Γ ,,, Γ' ,,, Γ'' ,,, Γ''' |- tm`  
    to `Σ ; Γ ,,, Γ'[:= s] ,,, Γ'' ,,, Γ''' |- tm`  
    to `Σ ; Γ ,,, subst_context s #|Γ'''| Γ' ,,, subst_context s 0 Γ''' |- subst s #|Γ'' ,,, Γ'''| tm`

## UnivSubst
- Substitution of universe variables `tm@[u]` or `subst_instance_constr u tm`

- Substitution of universe variables in all types and bodies of a context `Γ@[u]` or `subst_instance_context u Γ`


## Closed
- Whether the highest variable index is less than `k` `closedn k tm`

## Closed for universe variables
- Whether the highest universe variable index is less than `k` `closedu k tm`


## noccur_between (rare)
- Whether variables between k and n are not present in term (e.g. forall vs arrow) `noccur_between k n tm`


# Operations purely on contexts (or telescopes, term lists)

## context_assumptions, is_assumption_context
- Number of lambdas (as opposed to lets) in the context
- Is there only lambdas in this context

## Smash context
- `smash_context Δ Γ`: Transform `Γ ,,, Δ` into `ΓΔ` where we successively expand the lets from Γ in Δ and append the lambdas
- Single argument `smash_context Γ` is `smash_context [] Γ` : we expand the lets in the rest of the context only

## Substitution hypotheses
The following 3 give `Γ |- s : Δ` : terms `s` in context `Γ` (plus previous `s`) can replace context `Δ`
- `untyped_subslet Γ s Δ` : `s` has any term when no def, the exact body of the def substituted with the previous entries when def
- `subslet Σ Γ s Δ` : `untyped_subslet` but the terms in `s` have the type of the [substituted with the previous entries] context_decl
- `subs Σ Γ s Δ` : `subslet` but there is no def in `Δ`

- `ctx_inst Σ Γ s Δ` : Telescope `Δ` can be replaced by the terms in `s` *and the defs in `Δ`*; `s` has a term with the type of the [substituted with the previous entries] context_decl when no def, *no entry* when def

## Substitutions
- `extended_subst Γ n` : `Γ ,,, smash_context Γ' ,,, Γ'' |- extended_subst Γ' #|Γ''| : Γ'`
    + `extended_subst Γ n` : `Γ ,,, smash_context Γ' ,,, Γ'' |- extended_subst Γ' #|Γ''| : lift_context #|smash_context Γ'| #|Γ''| Γ'` is a corollary when Γ'' = []

- `expand_lets_k Γ k t`:
    + from `Γ ,,, Γ' ,,, Γ'' |- tm`,
        inserting smashed `Γ'` using `lift #|smash_context Γ'| #|Γ' ,,, Γ''| tm`, reaches
    + `Γ ,,, smash_context Γ' ,,, lift_context #|smash_context Γ'| #|Γ''| Γ' ,,, lift_context #|smash_context Γ'| 0 Γ'' |- lift #|smash_context Γ'| #|Γ' ,,, Γ''| tm`,
        from which using `subst (extended_subst Γ' 0) #|Γ''|` reaches
    + `Γ ,,, smash_context Γ' ,,, expand_lets_k_ctx Γ' #|[]| Γ'' |- expand_lets_k Γ' #|Γ''| tm`

- `to_extended_list_k Γ k` : under context `Γ ,,, Γ'`, pointers to Γ in order
