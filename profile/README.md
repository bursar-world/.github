<p align="center">
  <img src="./assets/banner.svg" alt="Bursar: spending mandates for AI agents" width="100%">
</p>

Bursar gives an AI agent a budget it cannot overspend. A principal opens a mandate account on
Robinhood Chain and sets its limits: how much per payment, per day and per month, which providers
the agent may pay, and the amount above which a person has to approve. The agent pays providers in
USDG over [x402](https://www.x402.org), the HTTP payment standard. Each payment waits in escrow
until the job is delivered and can be disputed until then. The limits are enforced by the contract
itself, so a payment outside them fails on chain whatever any service in front of it says.

## Live today

- **[Console](https://app.bursar.world).** Create and fund a mandate, set its limits, approve
  larger payments, see what your agents spent, and dispute a job that came back wrong.
- **Contracts on Robinhood Chain mainnet** (chain 4663), settling in USDG. Every address is listed
  in the [bursar repository](https://github.com/bursar-world/bursar#deployed-contracts).
- **Stocks and treasury.** A mandate can buy listed stock tokens at a price checked against
  Chainlink feeds, keep idle USDG in a short-term Treasury fund (SGOV), and draw USDG credit
  against stock tokens pledged as collateral.
- **Private mandates.** A mandate's terms can stay off the public record, with a zero-knowledge
  proof that each payment fits them. Funding and payments can go through a shielded USDG pool,
  and you choose who may read your records.
- **[Documentation](https://app.bursar.world/docs)** and the product site at
  [bursar.world](https://bursar.world).

The contracts hold real funds and have not had an external audit. They run with low limits: a
provider with no history can be paid at most 25 USDG per job, rising with its record to at most
125 USDG. Size what you fund accordingly.

## Repositories

| Repository | What it holds |
|---|---|
| [bursar](https://github.com/bursar-world/bursar) | The contracts, the TypeScript SDK and MCP server, the payment services and the console. MIT licensed. |
| [landing](https://github.com/bursar-world/landing) | The website at [bursar.world](https://bursar.world). |
| [.github](https://github.com/bursar-world/.github) | This page and the default security, contribution and conduct policies for every repository. |

## How it fits together

```mermaid
flowchart TB
  subgraph users["People and agents"]
    direction LR
    P["Principal wallet"]
    C["Console<br/>app.bursar.world"]
    A["Agent<br/>SDK or MCP server"]
  end

  subgraph offchain["Services"]
    direction LR
    F["Facilitator<br/>x402 payments"]
    U["Underwriter<br/>spend checks"]
    R["Resolver service<br/>dispute votes"]
    S["Provider sidecar<br/>runs on the provider"]
  end

  subgraph chain["Robinhood Chain, chain 4663"]
    subgraph mandates["Mandates"]
      MF["MandateAccountFactory"]
      MA["MandateAccount"]
      CM["Committed mandates<br/>and proof verifier"]
    end
    subgraph settle["Settlement and trust"]
      E["Escrow"]
      OR["OracleRegistry"]
      AR["AgentRegistry"]
      REP["Reputation"]
    end
    subgraph rwa["Stocks, treasury and credit"]
      RG["AssetRegistry, PriceGuard<br/>and StockSpendRouter"]
      TP["TreasuryPark"]
      CV["CollateralVault<br/>and CreditPool"]
    end
    subgraph privacy["Privacy"]
      DR["DisclosureRegistry"]
      SL["SolvencyLog"]
      SP["ShieldedPool<br/>and Entrypoint"]
    end
    subgraph gov["Governance and token"]
      TL["AdminTimelock"]
      TOK["BRSR, Staking<br/>Vesting, Buyback"]
    end
    subgraph ext["Robinhood Chain assets and markets"]
      USDG[("USDG")]
      CL["Chainlink price feeds"]
      UNI["Uniswap v4"]
    end
  end

  P -->|"creates, funds, sets limits"| C
  P -.->|"approves payments above threshold"| MA
  C --> MF
  MF -->|"one account per mandate"| MA
  A -->|"pays inside its limits"| MA
  A -->|"x402 payment"| F
  F -->|"checks the spend"| U
  U -->|"reads limits"| MA
  F -->|"settles"| E
  MA -->|"locks each payment"| E
  CM -->|"locks each payment"| E
  S -->|"delivers and releases"| E
  AR -->|"provider caps"| E
  E -->|"records outcomes"| REP
  E -->|"disputed jobs"| OR
  R -->|"commits and reveals votes"| OR
  OR -->|"resolver bonds"| TOK
  MA -->|"stock, treasury, credit"| rwa
  RG --> CL
  RG --> UNI
  CV --> CL
  C -->|"private mandates, shielded funding"| privacy
  E -.->|"balances in daily root"| SL
  TL -->|"administers"| settle
  MA --- USDG
  SP --- USDG

  classDef own fill:#faf8f7,stroke:#49345f,color:#49345f
  classDef extn fill:#ffffff,stroke:#ecb29d,color:#49345f
  class P,C,A,F,U,R,S,MF,MA,CM,E,OR,AR,REP,RG,TP,CV,DR,SL,SP,TL,TOK own
  class USDG,CL,UNI extn
```

A principal sets limits in the console, and the factory deploys one mandate account for them. An
agent pays through that account, directly or as an x402 payment the facilitator checks and
settles. Each payment is locked in escrow until the provider's sidecar delivers the work and
releases it. A disputed job goes to bonded resolvers, who vote on chain. A static copy of this
diagram is in [architecture.svg](./assets/architecture.svg).

## Get started

**Principals.** Open [app.bursar.world](https://app.bursar.world), connect a wallet on Robinhood
Chain, create a mandate and fund it with USDG. Give your agent a key of its own and name its
address as the mandate's agent. Start with a small balance.

**Agent developers.** Pay from code with the [SDK](https://github.com/bursar-world/bursar/tree/main/packages/sdk),
or give an agent the same abilities through the
[MCP server](https://github.com/bursar-world/bursar/tree/main/packages/mcp). The packages are not on
npm yet; build them from the [bursar repository](https://github.com/bursar-world/bursar#quick-start).

**Providers.** Charge for your service over x402 through the
[facilitator](https://github.com/bursar-world/bursar/tree/main/services/facilitator), and run the
[provider sidecar](https://github.com/bursar-world/bursar/tree/main/services/sidecar) to take on
jobs from escrow, deliver them and collect payment. What you can be paid per job grows with your
settlement record.

## Security

Please report vulnerabilities privately to [security@bursar.world](mailto:security@bursar.world)
or through GitHub private vulnerability reporting on the affected repository. The
[security policy](https://github.com/bursar-world/.github/blob/main/SECURITY.md) explains what
to include and what happens next.

## Contact

[bursar.world](https://bursar.world) · [X @UseBursar](https://x.com/UseBursar) ·
[hello@bursar.world](mailto:hello@bursar.world) · [security@bursar.world](mailto:security@bursar.world)
