# OCUDU gNB certification gate

[![CNTi cert](https://github.com/martin-mat/ocudu-gate/raw/badges/cnti-badge.svg)](https://github.com/martin-mat/ocudu-gate/actions/workflows/cnti.yml)

The [OCUDU](https://gitlab.com/ocudu) gNB (open CU/DU by SRS) — a RAN workload — certified by the
[CNTi Test Suite GitHub Action](https://github.com/lfn-cnti/testsuite-action) on a plain
GitHub-hosted runner.

- [`cnti-testsuite.yaml`](cnti-testsuite.yaml) — the CNF: the upstream
  [`ocudu-gnb`](https://gitlab.com/ocudu/ocudu_elements/ocudu_helm) chart from the OCUDU OCI
  registry, at a pinned version (Renovate proposes bumps).
- [`gnb-values.yaml`](gnb-values.yaml) — gNB **test mode**: a dummy radio unit (`ru_dummy`), no core
  network (`no_core`), and the built-in traffic generator (`test_mode.test_ue`), so the whole
  CU/DU stack runs except the fronthaul; one 20 MHz cell sized for a 4-vCPU runner.
- [`.github/workflows/cnti.yml`](.github/workflows/cnti.yml) — one step: the action runs
  `cnti-testsuite cert` on a kind cluster. The job passes if the certification criterion is met,
  fails if not.

No kernel modules, no SR-IOV, no hugepages: nothing is prepared on the runner. Runs nightly, on
demand, and on changes to the CNF description. The badge is published by the action to the
[`badges`](https://github.com/martin-mat/ocudu-gate/tree/badges) branch after each run on `main`.
