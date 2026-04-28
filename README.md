# Bi-MLIPs

Machine-learning interatomic potential models for Bismuth (Bi), trained on Quantum ESPRESSO DFT data.

## Models

| Model | Type | Files |
|-------|------|-------|
| `ACE/Bi_ACE.yaml` | ACE (pacemaker) | `ACE/Bi_ACE.yaml`, `ACE/Bi_ACE.yace` |
| `GRACE/GRACE-BI-UPF1` | GRACE (TensorFlow) | `GRACE/GRACE-BI-UPF1/` |

---

## LAMMPS Usage

### ACE potential

Requires LAMMPS compiled with the **ML-PACE** package.

```lammps
mass 1 208.98040

pair_style pace
pair_coeff * * ACE/Bi_ACE.yaml Bi
```

The `.yace` file is the compiled binary form of the same potential and can be used as a drop-in replacement for faster loading:

```lammps
pair_style pace
pair_coeff * * ACE/Bi_ACE.yace Bi
```

### GRACE potential (GRACE-BI-UPF1)

Requires LAMMPS compiled with the GRACE support from [here](https://github.com/yury-lysogorskiy/lammps) following instructions [here](https://gracemaker.readthedocs.io/en/latest/gracemaker/install/#lammps-with-grace).

```lammps
mass 1 208.98040

pair_style grace
pair_coeff * * GRACE/GRACE-BI-UPF1 Bi
```

The `pair_coeff` path points to the **directory** containing `saved_model.pb` and `variables/`.

Cutoff: 6.0 Å (set internally by the model; no explicit cutoff needed in the input script).

---

## Validation



To recreate plots, install the required Python packages:

```bash
pip install -r requirements.txt
```

Then open and run the jupyter notebooks.

---

## Notes

- Both potentials are single-element (Bi only).
- Atomic mass of Bi: 208.98040 u.
- The ACE potential was generated with pacemaker v0.2.7 / tensorpotential.
- The GRACE model includes a `metadata.yaml` with model details (cutoff, chemical symbols).
