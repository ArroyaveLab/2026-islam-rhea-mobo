# Changelog

## v0.1.3 (2026-11-02)

- Compute the Young's modulus objective with the ORB v2 interatomic potential
  (`ORBCalculator(model="orb-v2")`) instead of the `materialsframework` default,
  M3GNet. The dependency extra changes from `materialsframework[matgl,sqsgen]`
  to `materialsframework[orb,sqsgen]`, so `matgl` and its Lightning and PyTorch
  Geometric dependencies leave the lock and `orb-models` joins it. Young's
  modulus values from this release will not match values computed with v0.1.2.
- Build the SQS generator and elastic-constant analyzer once per process in
  `rhea_mobo.objective` and share them with `run_optimization`. Previously
  `objective()` created new instances on every call and reloaded the potential
  for each composition it evaluated. `scripts/bo_script_full.py` gets the same
  change.
- Run the pre-commit hooks through `prek` in the lint workflow instead of
  calling `ruff check` and `ruff format --check` directly. Reformat
  `tests/test_crack_configuration.py` so it passes `ruff format`.
- Stop Dependabot from opening `pip` update PRs. It still tracks `uv`, GitHub
  Actions, and pre-commit hooks.
- Update locked dependencies to torch 2.14.1, pandas 3.1.0, numpy 2.5.4,
  scikit-learn 1.9.1, matplotlib 3.11.2, and tqdm 4.70.1. `requirements-toy.txt`
  now pins torch 2.14.1 and numpy 2.5.4. Dev tooling moves to pytest 9.2.0,
  ruff 0.17.3, and prek 0.5.7, and the build backend accepts `uv_build` up to
  0.13.
- Update package and citation metadata to v0.1.3. The citation DOI still
  identifies the software's all-versions archive.

Validation: 24 tests and lint passed in the locked Python 3.12 and Torch 2.14.1
environment. The test suite does not run the Young's modulus calculation, so
ORB v2 output has not been compared with the earlier M3GNet values. No new
Thermo-Calc or experimental results are claimed by this release.

## v0.1.2 — 2026-09-08

- Rename the repository to `ArroyaveLab/2026-islam-rhea-mobo` and link the
  manuscript entry in the ArroyaveLab publications index.
- Fix composition construction using explicit elemental fractions.
- Correct acquisition score shape for candidate batches while retaining
  sequential candidate selection (`q=1`).
- Describe the acquisition modifier consistently as dimensionless supply risk.
- Align the crack-susceptibility configuration with the manuscript.
- Document that the original 250 evaluations and their sequential history are
  unavailable and that licensed physical calculations have not been rerun.
- Add a license-free synthetic BO example with an exhaustive feasible oracle
  and a random-sampling baseline sharing the initial design and evaluation budget.
  The example demonstrates the pipeline; it is not statistical validation.
- Update package and citation metadata to v0.1.2. The citation DOI identifies
  the software's all-versions archive.

Validation: 15 focused tests and lint passed for the synthetic example and core
optimization helpers. The example also completed in the pinned Python 3.12
and Torch 2.13.0 environment. No new Thermo-Calc or experimental results are
claimed by this release.
