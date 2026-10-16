[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23425496.svg)](https://doi.org/10.5281/zenodo.23425496)
# Distance to Vacuum Survival Floor — DESI DR2

### Measuring how close we live to the edge of vacuum decay

**Paper:** Nasir Khan (2026) — *Distance to Vacuum Survival Floor in Decaying Vacuum Model from DESI DR2 BAO* — arXiv: [to be added] — Submitted to JCAP

#### What is this?

If our vacuum is metastable, decay rate per volume is $\Gamma = A e^{-S_E}$.
To survive a Hubble time in a Hubble volume, we need $\Gamma H_0^{-4} \lesssim 1$,
which defines a survival floor:

$$ S_{\rm floor} \equiv \ln(A/H_0^4) \simeq 556 + \ln(A/M_{Pl}^4) $$

We define the convention-independent observable:

$$ \Delta \equiv S_E - S_{\rm floor} $$

- $\Delta \gg 1$: safely stable
- $\Delta \sim O(1)$: near-critical (like SM Higgs vacuum)
- $\Delta < 0$: excluded — we shouldn't exist

In the minimal decaying vacuum class $\dot\rho_\Lambda = -\Gamma\rho_\Lambda$,
$w_0 = -1 + \Gamma/3H_0$. So DESI's measurement of $w_0$ becomes a measurement of $\Delta$.

#### What this repo contains

- **CLASS_patch/**: 20-line modification to `background.c` to include `Gamma_over_H0`
- **cobaya_yamls/**: Cobaya yaml for DESI DR2 BAO + Planck PR3 + Pantheon+
- **chains/**: MCMC chains (Cobaya format) — Gelman-Rubin R-1<0.02
- **plots/**:
    - `P_Delta.pdf` — Posterior for $\Delta$
    - `corner_Gamma.pdf` — $\Gamma/H_0$ vs $\Omega_m$ vs $H_0$

#### Main Result

DESI DR2 + Planck + Pantheon+ (preliminary):

- $\Gamma/H_0 < 0.12$ (95% CL)
- $\Delta > 0.1$ (95% CL), peak at $\Delta \sim 1.2$ (68%: 0.3-2.5)
- Consistent with near-critical metastability $\Delta \lesssim O(1)$

Prefactor $A$ uncertainty shifts $S_{\rm floor}$ by additive constant; $P(\Gamma/H_0)$ is independent of convention.

#### Extra dimensions bound (illustrative)

KK tower of $n$ extra dims radius $R$ lowers $S_E$ by $\Delta S_E \approx -k n \ln(M_{Pl}R)$, $k\sim0.05-0.2$.
If $\Delta\sim O(1)$, requiring $|\Delta S_E|<1$ gives $n\ln(M_{Pl}R)\lesssim21$ (range 5-105 with coupling).
TeV-scale ADD disfavored if near-critical holds; high-scale extra dims allowed. Full one-loop bounce with tower via CosmoTransitions in progress.

#### How to reproduce

```bash
# 1. Patch CLASS
cd class && patch -p1 <../CLASS_patch/background.c.diff && make

# 2. Run Cobaya
cobaya-run../cobaya_yamls/desi_dr2_planck_pantheon.yaml
