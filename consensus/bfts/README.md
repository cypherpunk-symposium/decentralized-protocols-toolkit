## byzantine fault tolerant ramblings

<br>

* [minimmit: fast finality with even faster blocks, by kobayashi chou et al (2025)](https://arxiv.org/pdf/2508.10862)
  - bft state machine with significantly lower latency through an innovative view-change mechanism.
  - on a total of `n` processors or replicas, at most `f` of them may be bizantine, where `n >= 5f + 1`.
  - key insight: `n` decoupling view progression from tx finalizatin (l-notarizations). protocol allows view progression with only `2f + 1` votes (m-notarizations).
  - design leads to ~17% redux in tx latency. 
