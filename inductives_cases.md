# Inductives

```coq
Inductive I¹ (p₁: P₁) ... (pₚ: Pₚ) : ∀(a¹₁: A¹₁) ... (a¹ₖ₁: A¹ₖ₁), S¹ :=
  | ₁C¹: ∀ (₁x¹₁: ₁X¹₁) ... (₁x¹ₗ₁: ₁X¹ₗ₁), I¹ (p₁: P₁) ... (pₚ: Pₚ) (₁t¹₁: A¹₁) ... (₁t¹ₖ₁: A¹ₖ₁)
  | ...
  | ₘ₁C¹: ∀ (ₘ₁x¹₁: ₘ₁X¹₁) ... (ₘ₁x¹ₗ₁: ₘ₁X¹ₗ₁), I¹ (p₁: P₁) ... (pₚ: Pₚ) (ₘ₁t¹₁: A¹₁) ... (ₘ₁t¹ₖ₁: A¹ₖ₁)

with ...

with Iⁿ (p₁: P₁) ... (pₚ: Pₚ) : ∀(aⁿ₁: Aⁿ₁) ... (aⁿₖ₁: Aⁿₖ₁), Sⁿ :=
  | ₁Cⁿ: ∀ (₁xⁿ₁: ₁Xⁿ₁) ... (₁xⁿₗ₁: ⁿ₁Xₗ₁), Iⁿ (p₁: P₁) ... (pₚ: Pₚ) (₁tⁿ₁: Aⁿ₁) ... (₁tⁿₖₙ: Aⁿₖₙ)
  | ...
  | ₘₙCⁿ: ∀ (ₘ₁xⁿ₁: ₘ₁Xⁿ₁) ... (ₘ₁xⁿₗ₁: ₘ₁Xⁿₗ₁), Iⁿ (p₁: P₁) ... (pₚ: Pₚ) (ₘ₁tⁿ₁: Aⁿ₁) ... (ₘ₁tⁿₖₙ: Aⁿₖₙ)
```

## Infos

### Mutual inductive infos [`mutual_inductive_body`] :
- [`ind_finite`] Inductive/CoInductive/Record
- [`ind_npars`] Number of paramaters $p$
- [`ind_params`] Parameter context $Γ_P = \big[(p_1: P_1), ..., (p_p: P_p)\big]$ (may include $p_z := t_z : P_z$), not counted towards $p$
- [`ind_bodies`] $n$ inductive defintions $I^1, ..., I^n$
- [`ind_universes`] Abstract universe declarations
- [`ind_variance`] Optional universe variance

### One inductive ($I^i$) infos [`one_inductive_body`] :
- [`ind_name`] Name $I^i$
- [`ind_indices`] Indices context $Γ^i = \big[(a^i_1: A^i_1), ..., (a^i_{k_i}: A^i_{k_i})\big]$ (may include $a^i_z := t^i_z : A^i_z$)
- [`ind_sort`] Sort $S^i$
- [`ind_type`] [redundant] Type of $I^i$ : $\big[∀Γ_P, ∀Γ^i, S^i\big]$ or (extended) $\big[∀(p_1: P_1), ..., (p_p: P_p), ∀(a^i_1: A^i_1) ... (a^i_{k_i}: A^i_{k_i}), S^i\big]$
- [`ind_kelim`] [redundant] Allowed eliminations sorts
- [`ind_ctors`] $m_i$ constructor definitions ${}_1C^i, ..., {}_{m_i}C^i$
- [`ind_projs`] [record only] list of projections
- [`ind_relevance`] [redundant] Relevance of $S^i$

### Constructor infos [`constructor_body`] :
- [`cstr_name`] Name ${}_jC^i$
- [`cstr_args`] Arguments context ${}_jΓ^i = \big[({}_{j}x^i_1: {}_{j}X^i_1), ..., ({}_{j}x^i_{l_j}: {}_{j}X^i_{l_j})\big]$
- [`cstr_indices`] Indices list ${}_jT^i = \big[({}_{j}t^i_1: A^i_1); ...; ({}_{j}t^i_{k_i}: A^i_{k_i})\big]$ (inductive indices context without letins)
- [`cstr_type`] [redundant] Type of ${}_jC^i$ : $\big[∀Γ_P, ∀{}_jΓ^i, (I^i\ @\ Γ_P)\ @\ {}_jT^i\big]$ or (extended) $\big[∀(p_1: P_1), ..., (p_p: P_p), ∀({}_{j}x^i_1: {}_{j}X^i_1) ... ({}_{j}x^i_{l_j}: {}_{j}X^i_{l_j}), I^i (p_1: P_1) ... (p_p: P_p) ({}_{j}t^i_1: A^i_1) ... ({}_{j}t^i_{k_i}: A^i_{k_i})\big]$
- [`cstr_arity`] Arity (size of argument context, without letins)

## Compact mathematical notation
gives

$$ \mathrm{Ind}[p](\Big[I^i: ∀Γ_P, ∀Γ^i, S^i\Big] := \Big[{}_{j}C^i: ∀Γ_P, ∀{}_jΓ^i, (I^i\ @\ Γ_P)\ @ \ {}_jT^i\Big]) $$

or (extended)

$$ \mathrm{Ind}[p](\Big[I^i: ∀(p_1: P_1) ... (p_p: P_p), ∀(a^i_1: A^i_1) ... (a^i_{k_i}: A^i_{k_i}), S^i\Big] \\ := \Big[{}_{j}C^i: ∀(p_1: P_1) ... (p_p: P_p), ∀({}_{j}x^i_1: {}_{j}X^i_1) ... ({}_{j}x^i_{l_j}: {}_{j}X^i_{l_j}), I^i (p_1: P_1) ... (p_p: P_p) ({}_{j}t^i_1: A^i_1) ... ({}_{j}t^i_{k_i}: A^i_{k_i})\Big]) $$

# Cases

```coq
match (c: Iⁱ (q₁: P₁) ... (qₚ: Pₚ) (r₁: Aⁱ₁) ... (rₖᵢ: Aⁱₖᵢ)) as (m: Iⁱ (q₁: P₁) ... (qₚ: Pₚ) (b₁: Aⁱ₁) ... (bₖᵢ: Aⁱₖᵢ))
  in Iⁱ (_: P₁) ... (_: Pₚ) (b₁: Aⁱ₁) ... (bₖᵢ: Aⁱₖᵢ)
  return (P[b₁, ..., bₖᵢ, m]: B[b₁, ..., bₖᵢ, m]) with
  | ₁Cⁱ (₁y₁: ₁Xⁱ₁) ... (₁yₗ₁: ₁Xⁱₗ₁) => (₁fⁱ[₁y₁, ..., ₁yₗ₁]: P[₁tⁱ₁, ..., ₁tⁱₖᵢ, ₁Cⁱ (p₁: P₁) ... (pₚ: Pₚ) (₁y₁: ₁Xⁱ₁) ... (₁yₗ₁: ₁Xⁱₗ₁)])
  | ...
  | ₘᵢCⁱ (ₘᵢy₁: ₘᵢXⁱ₁) ... (ₘᵢyₗ₁: ₘᵢXⁱₗₘᵢ) => (ₘᵢfⁱ[ₘᵢy₁, ..., ₘᵢyₗₘᵢ]: P[ₘᵢtⁱ₁, ..., ₘᵢtⁱₖᵢ, ₘᵢCⁱ (p₁: P₁) ... (pₚ: Pₚ) (ₘᵢy₁: ₘᵢXⁱ₁) ... (ₘᵢyₗₘᵢ: ₘᵢXⁱₗₘᵢ)]
end
```

gives (with $σ_P = [q_1; ...; q_P]$, $τ=[r_1; ...; r_{k_i}]$, $Δ = \big[(b_1: A^i_1), ..., (b_{k_i}: A^i_{k_i})\big]$, $Δ_+ = Δ, (m: (I^i\ @\ σ_P)\ @ \ Δ)$, ${}_jΔ = \big[({}_{j}y_1: {}_{j}X^i_1), ..., ({}_{j}y_{l_j}: {}_{j}X^i_{l_j})\big]$)

$$ \mathrm{case}\Big((c: (I^i\ @\ σ_P)\ @ \ τ)\ , ((λΔ_+, P[Δ_+]): ∀Δ_+, B[Δ_+]), \Big[λ({}_jΔ), {}_jf^i[{}_jΔ] : P[{}_jT^i, ({}_{j}C^i\ @\ σ_P)\ @\ {}_jΔ] \Big]\Big) $$

More compact notation: 
$$ \mathrm{case}\Big(c, (P: ∀Δ_+, B[Δ_+]), \Big[{}_jf^i : ∀({}_jΔ), (P\ @\ {}_jT^i)\ (({}_{j}C^i\ @\ σ_P)\ @\ {}_jΔ) \Big]\Big) $$

## Infos
### Case term info [`tCase: case_info -> predicate term -> term -> list branch -> term`]:
- case_info
- predicate
- `c`, matched term
- ${}_jf^i$, branch list

### Case_info:
- [`ci_ind`] Destructed inductive "$\mathrm{addr(I^i)}$"
- [`ci_npar`] Number of parameters $p$ (cf. `mutual_inductive_body.npars`)
- [`ci_rel`] Relevance of whole term (i.e. relevance of sort of $B[Γ^i, m]$)

### Predicate
- [`puinst`] Instantiation for declared universes
- [`pparams`] Inductive parameters values $σ_P$ (cf. `mutual_inductive_body.ind_params`)
- [`pcontext`] Global case context $Δ_+ = \big[Δ[Γ_P], m[Γ_P, Δ]\big]$ (cf. `ind_predicate_context`, only names are new)
- [`preturn`] Global return type $P[Δ_+]$

### Branch
- [`bcontext`] Branch context ${}_jΔ[Γ_P]$ (cf. `cstr_branch_context`, only names are new)
- [`bbody`] Branch term ${}_jf^i[{}_jΔ]$

## Other constructions
- [`context_assumptions`] : from context to number of abstract elements inside (no letins)
  + $p =$ `context_assumptions` $Γ_P$ ` = ci_npar` = $|σ_P|$ 
  + $k_i = |{}_jT^i| = $ `context_assumptions` $Γ^i$
  + `cstr_args = context_assumptions` ${}_jΓ^i$
- [`ind_predicate_context ind mdecl idecl`] = $\big[Γ^i , (\_: (I^i\ @\ Γ_P)\ @ \ Γ^i)\big]$
- [`inst_case_context `$σ_P$ ` puinst ` $Γ[Γ_P]$ = $Γ[Γ_P \leftarrow σ_P]$] (and universes)
- [`inst_case_predicate_context p`] = `p.`$Δ_+[Γ_P \leftarrow σ_P]$ (and universes)
- [`inst_case_branch_context p br`] = `br.`${}_jΔ[Γ_P \leftarrow σ_P]$ (and universes)
- [`iota_red npars p (`$σ_P$ `++` $τ$`) br`] = `br.`${}_jf^i[{}_jΔ[Γ_P \leftarrow σ_P] \leftarrow τ]$
- [`case_predicate_context ind mdecl idecl p`] = $Δ'_+ = \big[Γ^i[Γ_P \leftarrow σ_P] , (\_: (I^i\ @\ σ_P)\ @ \ Γ^i)\big][a_k \leftarrow b_k]$ = `inst_case_predicate_context p`
- [`cstr_branch_context ci mdecl cdecl`] = $\big[{}_jΓ^i , (\_: (I^i\ @\ Γ_P)\ @ \ Γ^i)\big]$
- [`case_branch_context ind mdecl p bctx cdecl`] = ${}_jΔ' = \big[{}_jΓ^i[Γ_P \leftarrow σ_P]\big][{}_jx_k \leftarrow {}_jy_k]$ = `inst_case_branch_context p br`
- [`case_branches_contexts ind mdecl idecl p brs`]: Map `case_branch_context` on all constructors
- [`case_branch_type ind mdecl idecl p br ptm i cdecl`]: Case branch context ${}_jΔ$ + Type $\big[(λΔ'_+, P[Δ'_+])\ @\ {}_jT^i[Γ_P \leftarrow σ_P]\ @\ ({}_jC^i\ @\ σ_P \ @\ {}_jT^i)\big]$
- [`wf_predicate mdecl idecl p`]: `context_assumptions` $Γ_P$ ` = ci_npar` and same [length and] binder annotation for `pcontext` $= Δ_+$ and $\big[Γ^i , (\_: (I^i\ @\ Γ_P)\ @ \ Γ^i)\big]$
- [`wf_branch cdecl br`]: Same [length and] binder annotation for `bcontext` $= {}_jΔ$ and ${}_jΓ^i$
- [`wf_branches idecl brs`]: Forall2 `wf_branch` on constructors and branches
