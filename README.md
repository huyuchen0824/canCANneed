# canCANneed
canCANneed is a newly designed protocol intended as an upward substitution for existing communication protocols. It focuses on the emerging demand for highly robust communication in robotics and automotive applications. 
> ⚠️ **Draft Alert** – the spec is still under active development; issues, PRs, and wild ideas are all welcome!
---
## Why another protocol?
Automotive and robotics stacks already sport a crowded zoo of buses—**CAN/CAN-FD/CAN-XL**, **FlexRay**, **EtherCAT**, **10Base-T1S**, **LIN**, etc.  
They share two traits:

1. **Heritage weight** – decades of compatibility baggage that make radical latency or throughput gains costly.
2. **Design-time trade-offs frozen in silicon** – once you pick FlexRay for determinism or EtherCAT for bandwidth, you’re locked into its wiring, transceivers, and licensing.

canCANneed was started to break those trade-offs:

| Pain Point | Legacy answer | canCANneed take |
|------------|---------------|-----------------|
| **Latency spikes** | Event-triggered arbitration (CAN) or static TDMA (FlexRay) | Deterministic time-slot scheduler with micro-slot pre-emption |
| **Speed ceiling** | 8 Mbps (CAN-FD) / 10 Mbps (10Base-T1S) | 20 Mbps+ on the same two-wire differential pair |
| **EMC & length** | Add shielding, drop speed | Differential + active wave-shaping keeps 20 m @ 20 Mbps unshielded |
| **Migration cost** | new PHY | As cheap as new PHY |

---

## Roadmap

| Milestone | ETA | Deliverable |
|-----------|-----|-------------|
| **v0.1 Draft** | 2025-09 | Complete basic protocol |
| **v0.1 Release** | 2026 | hardware Demo |
| **v0.2** | TBD | TBD |
| **v1.0** | TBTBD | Open standard ratified, transceiver samples |
---

## Contribute
No special format requirements, just be kind.
