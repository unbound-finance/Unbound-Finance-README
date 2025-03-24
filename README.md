# Unbound Finance 

# Description
Unbound Finance is a novel, non-custodial lending platform, driven towards enabling newer and better opportunities of yield with a view to improving the overall capital efficiency of the DeFi ecosystem. Through synthetic assets like UND stablecoin, Unbound aims to unlock the liquidity available in DeFi DEXs and to enable the easy flow of this liquidity from one chain to another without actually removing it.

## The key highlights of protocol are as follows :

Interest-free borrowing: Unbound does not charge any interest on the borrowed UND.
Perpetual borrowing: At Unbound, borrowers have unlimited maturities. Users can unlock the underlying collateral any time by simply paying off the outstanding debt.
Stablecoin UND: UND is the first flagship product of the Unbound protocol. It is a decentralized, cross-chain stablecoin designed to be native to the AMM space.
Factory Smart Contracts: Unbound makes use of liquidity lock contracts that are permissionless and support EVM-based AMMs like Uniswap, Balancer, Curve, SushiSwap and the like.
Collateralizing concentrated liquidity positions: Unbound is one of the first protocols that allows concentrated liquidity positions to be used as collateral for borrowing synthetic crypto assets such as UND stablecoin.

# Unbound Finance: Whitepaper

## Abstract
Unbound Finance is a decentralized, cross-chain lending protocol that enables DeFi users to borrow over-collateralized synthetic asset loans by pledging their idle interest-bearing tokens (ib tokens) at a 0% interest rate. While being used as collateral, these tokens continue to accrue transaction fees from liquidity provisioning. Borrowed funds can be deployed in various DeFi activities such as lending, borrowing, and trading, or can be used to obtain additional ib tokens for compounding returns. 

The rewards generated from automated yield farming of the deposited assets are compounded to boost users’ APY. The platform provides liquidity to the AMM LP tokens and issues **UND** as a stablecoin. The protocol unlocks the collateralized assets once UND is returned. Primarily geared toward creating a composable DeFi solution, Unbound is one of the first projects to enable **Uniswap v3 positions** to serve as collateral.

---

## Introduction
The advent of Automated Market Makers (AMM) revolutionized the decentralized finance sector, with prominent DEXs such as **Uniswap**, **Curve**, **SushiSwap**, and **Balancer** contributing to significant portions of DeFi liquidity across multiple blockchains. Despite their success in democratizing liquidity, **capital efficiency** remained a persistent challenge.

Unbound Finance recognized the opportunity in leveraging LP tokens to address this issue. With **Unbound v1**, the protocol introduced a robust lending architecture allowing users to borrow **interest-free** crypto loans by pledging **LP tokens**. By supporting mostly stablecoin pairs and maintaining **no liquidation** risk (due to reliance on a SAFU reserve), v1 marked a major step forward in unlocking liquidity from AMMs.

However, the emergence of next-gen AMMs (e.g., **Uniswap v3**) introduces capital efficiency via concentrated liquidity, where non-fungible tokens (NFTs) represent liquidity positions. These improvements significantly benefit the DeFi ecosystem but create complexities for reusing LP positions as collateral. 

This whitepaper presents the **latest iteration of Unbound** as the ultimate DeFi “money lego,” enabling users to borrow against AMM liquidity positions—including concentrated liquidity positions in Uniswap v3—without sacrificing their yield-earning capabilities. **Unbound v2** introduces liquidation and redemption mechanisms to protect the peg of **UND** while allowing more volatile asset pairs to serve as collateral.

---

## Key Features
1. **Interest-Free Borrowing**: Unbound does not charge any interest on loans taken out in **UND**.
2. **Perpetual Borrowing**: Borrowers have unlimited loan maturities. Collateral can be reclaimed anytime by repaying the borrowed UND and associated fees.
3. **UND Stablecoin**: A decentralized, cross-chain stablecoin pegged to the US Dollar, engineered to be native to the AMM space.
4. **Factory Smart Contracts**: Permissionless liquidity lock contracts support EVM-based AMMs like **Uniswap**, **Balancer**, **Curve**, **SushiSwap**, etc.
5. **Collateralizing Concentrated Liquidity**: Among the first protocols to allow **Uniswap v3** positions (non-fungible tokens) to serve as collateral for synthetic assets like UND.

---

## Core Functions
Unbound’s functionality centers around four primary services, all operated via fully automated smart contracts without third-party intervention.

### 1. Borrowing
Unbound allows users to borrow **interest-free** loans by depositing LP tokens as collateral. Loans are denominated in **UND**, a decentralized ERC-20 stablecoin pegged to 1 USD.

#### Unbound Vaults
- **Unbound v1** supported only stablecoin LP tokens and relied on a unified collateral factor.  
- **Unbound v2** introduces **vaults** for each collateral type (stable or volatile asset pairs, including concentrated liquidity positions).  
- When a new liquidity pool is whitelisted, a **new vault** is created to handle that asset type.  
- Borrowers can deposit eligible LP tokens (or tokenized concentrated liquidity positions) into one or more vaults.  
- The amount of UND a user can borrow depends on that vault’s **Minimum Collateralization Ratio (MCR)** and the USD value of the collateral.

  **Borrowing Capacity**  
  \[
  \text{Borrowing Capacity} = \left(\frac{\text{Value of collateral (USD)}}{\text{MCR} (\%)} \right) \times 100
  \]

#### Borrowing Fee
- Unbound charges **no interest** on UND loans but levies a **one-time borrowing fee** on each new loan drawn.  
- The fee is added to the total loan debt and is **variable** (0.5%–5%) to help maintain UND’s peg.  
- Formula:

  \[
  \text{Borrowing Fee} = (\text{baseRate} + 0.5\%) \times \text{UND Debt}
  \]

  **Example**:  
  - Collateral worth \$10,000  
  - Loan drawn: 6,000 UND  
  - Current base rate: 0.5%  
  - Borrowing fee = \((0.5\% + 0.5\%) \times 6000\) = 60 UND  
  - Total debt = 6,000 UND + 60 UND = 6,060 UND

### 2. Unlocking
Unbound loans are perpetual—no fixed deadline for repayment. Users can **unlock** their collateral at any time by repaying the outstanding UND plus the borrowing fee. The UND returned is **burned**, reducing supply. Collateral is **unlocked** according to real-time collateral ratios based on oracle price feeds.

### 3. Yield Farming
**Unbound v2** automates **yield farming** by staking collateralized assets in **trusted and profitable** yield pools. Rewards are distributed **pro-rata** among depositors. When a user unlocks their collateral, the protocol:
- **Unstakes** the LP tokens  
- **Claims** accumulated rewards  
- **Transfers** those rewards to the user’s wallet automatically

### 4. Earn
UND holders can:
- Provide liquidity to UND pools on various DEXs through the Unbound interface
- Stake the resulting LP tokens in supported farms  
- Potentially **re-collateralize** those LP tokens in Unbound to borrow more UND, creating a **compounding loop**

---

## Price Stability Mechanism

### Liquidation
Unbound employs an **over-collateralized** model, ensuring the total collateral value **exceeds** the borrowed UND value. Borrower positions can be **liquidated** if their **collateral ratio** falls below the **MCR** for that vault. 

- **Liquidator** repays borrower’s outstanding debt and receives equivalent collateral.  
- Borrowers can avoid liquidation by maintaining their collateral ratio (i.e., repaying part of the debt or depositing more collateral).

### Redemption
Redemption ensures **UND** maintains its peg. When UND < \$1, users can buy UND cheaply on the market and **redeem** it at face value (\$1) for collateral from vaults with the **lowest collateral ratio** first:

- Redeemers pay UND to the protocol and receive vault collateral at **par** value.  
- **Redemption Fee** applies to the **collateral** taken.  
- Portions of or entire debt positions may be redeemed, improving the Collateralization Ratio of the redeemed position. Unlike liquidation, a borrower **does not** lose net value; they lose only the amount of collateral equal to the redeemed UND.

#### Redemption Fee
\[
\text{Redemption Fee} = (\text{baseRate} + 0.5\%) \times \text{Collateral Drawn}
\]

**Example**:  
- Base rate = 0.5%  
- Collateral drawn = \$10,000  
- Redemption fee = \((0.5\% + 0.5\%) \times 10{,}000\) = \$100  
- Effective collateral = \$10,000 – \$100 = \$9,900

**Base Rate Dynamics**  
- Increment on each redemption by an amount proportional to the fraction of UND supply redeemed:

  \[
  b(t) = b(t-1) + \delta \times \frac{x}{y}
  \]

  where  
  \(\delta = 0.5\),  
  \(x = \text{UND redeemed}\),  
  \(y = \text{total UND in circulation}\).

- Decay over time since the last redemption or debt issuance:

  \[
  b(t) = b(t-1) \times (\lambda^{\Delta t})
  \]

  where \(\lambda\) is the **decay factor** (half-life of 12 hours).

---

## Tokens

### UND (Stablecoin)
- A decentralized, cross-chain, **ERC-20 stablecoin** pegged to the US Dollar.  
- Borrowers mint UND against their liquidity positions as collateral.  
- UND is **burned** upon repayment.

### UNB (Governance Token)
- The governance token granting voting rights in **Unbound DAO**.  
- Token holders propose and vote on critical parameters such as:
  - **New collateral asset pairs** to whitelist
  - **Borrowing rate** and **MCR** adjustments
  - **Global borrowing limits** for vaults
  - **Fee structures** (borrowing fee, redemption fee, etc.)

---

## Price Oracles
Unbound integrates **Chainlink** price feeds for accurate on-chain pricing of collateral assets. Collateral values in USD are critical for:
- Calculating borrowing capacity  
- Determining collateral ratios  
- Driving liquidation and redemption events

---

## Conclusion
Unbound Finance is a powerful catalyst in the DeFi space, enabling concentrated and traditional AMM liquidity positions to serve as collateral for **interest-free** loans. By issuing its **UND** stablecoin, the platform expands capital efficiency and fosters new liquidity flows across various chains. Meanwhile, the **UNB** governance token empowers community members to shape Unbound’s future. Through its advanced lending architecture, automated yield strategies, and robust price stability mechanisms, Unbound represents the next evolutionary step in unlocking the potential of DeFi liquidity.

---

## Unbound Finance Roadmap

## 2020
- **March 2020** - Research and ideation for Unbound begins.
- **April 2020** - First draft of the whitepaper is released.
- **May 2020** - Development of proof of concept kicks off.
- **June 2020** - Protocol is pitched to OGS for feedback.
- **August 2020** - Official registration of the Unbound Finance domain name.
- **December 2020** - Release of the inaugural official whitepaper.

## 2021
- **February 2021** - Unbound releases its application and landing page.
- **April 14th, 2021** - Unbound launches Zeta Testnet.
- **June 10th, 2021** - Unbound Finance closes its first round of investment.
- **August 19th, 2021** - Unbound unveils its initial official Roadmap.
- **September 2nd, 2021** - Unbound partners with Harmony.
- **September 28th, 2021** - Unbound Sandbox live on Ethereum Mainnet.
- **November 4th, 2021** - Unbound goes live on Ethereum mainnet.
- **November 5th, 2021** - Unbound partners with Kyber Network.
- **November 18th, 2021** - Unbound partners with Avalanche.
- **December 18th, 2021** - Unbound partners with Avalanche.
- **December 17th, 2021** - UNB listing available on MEXC.
- **December 20th, 2021** - UNB listing available on Gate.io.

## 2022
- **January 24th, 2022** - Unbound on-chain staking live on Ethereum and BSC.
- **March 2nd, 2022** - Unbound goes live on Polygon mainnet.
- **March 3rd, 2022** - Unbound partners with Quickswap.
- **March 12th, 2022** - Unbound launches on Fantom testnet Alpha version.
- **May 15th, 2022** - Unbound goes live on BSC mainnet.
- **May 15th, 2022** - $UNB on-chain staking live on Polygon.
- **May 25th, 2022** - Unbound partners with DFYN.
- **May 31st, 2022** - Unbound live on BNB chain.
- **June 2nd, 2022** - UND-USDC pool live on Kyberswap.
- **June 14th, 2022** - $UNB flexible staking live on Kucoin.
- **June 25th, 2022** - Unbound partners with Pangolin.
- **August 1st, 2022** - Unbound partners with Router Protocol.
- **August 7th, 2022** - Unbound partners with Multichain.
- **September 14th, 2022** - Unbound live on Fantom mainnet.
- **October 20th, 2022** - Unbound V2 public testnet live.
- **November 28th, 2022** - Unbound live on Lens protocol.
- **November 13th, 2022** - Unbound V2 testnet phase 2 live.
- **December 21st, 2022** - Unbound partners with DeFiEdge.

## 2023
- **January 8th, 2023** - Unbound V2 Second Security Audit completed.
- **March 25th, 2023** - UNB ready and live for trading on Changelly.
- **April 5th, 2023** - Unbound partners with Changelly.
- **April 11th, 2023** - Unbound V2 live on Arbitrum mainnet.
- **October 16th, 2023** - Unbound partners with Arbidex.
- **December 7th, 2023** - UNB transfers into an OFT through integration with LayerZero.
- **December 21st, 2023** - UNB bridging live on Stargate Finance.

## 2024
- **February 2024** - Unbound server launched on Discord.
- **April 2024** - Website and application revamped for an enhanced user experience.
- **May 14th, 2024** - Unbound DAO live.
- **July 27th, 2024** - $UNB bridging to Arbitrum chain live via the Stargate bridge.
- **September 24th, 2024** - Enabling Multichain Voting for UNB Holders in Unbound DAO Governance.

## 🔗 Key Announcements


### Unbound launches Zeta Testnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1382276993316573185)

![Zeta Testnet](screenshots/Zetatestnet.png)

### Sandbox mainnet live on Ethereum
🔗 [View Tweet](https://x.com/unboundfinance/status/1442555884954030081)

![Sandbox Mainnet](screenshots/sandboxmainnet.png)

### UNB flexible promotion live
🔗 [View Tweet](https://x.com/unboundfinance/status/1536276972900618240)

![Flexible Promotion](screenshots/unbflexible.png)


### Unbound partners with Kyber Network
🔗 [View Tweet](https://x.com/unboundfinance/status/1457614881566302210)

![Kyber Partnership](screenshots/kyber.png)

### Unbound live on Avalanche mainnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1552608999077740544)

![Avalanche Mainnet](screenshots/avalanchemainnet.png)


### UNB deposits and withdrawals available on MEXC
🔗 [View Tweet](https://x.com/unboundfinance/status/1471802223441027072)

![MEXC Deposits](screenshots/mexc.png)

### Unbound goes live on Polygon mainnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1493088991045840896)

![Polygon Mainnet](screenshots/polygonmainnet.png)


### Unbound debuts the first-ever Cross-Chain stablecoin UND on Polygon
🔗 [View Tweet](https://x.com/unboundfinance/status/1427291657553145861)

![Cross-Chain UND](screenshots/undcrosschainpolygon.png)

### Unbound partners with Quickswap
🔗 [View Tweet](https://x.com/unboundfinance/status/1494319037354246146)

![Quickswap Partnership](screenshots/quickswapdex.png)

### Unbound launches on Fantom testnet Alpha version
🔗 [View Tweet](https://x.com/unboundfinance/status/1502672889040224257)

![Fantom Testnet](screenshots/fantomtestnet.png)


### Unbound goes live on BSC mainnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1517083150111080448)

![BSC Mainnet](screenshots/bscmainnet.png)


### Unbound partners with Pangolin
🔗 [View Tweet](https://x.com/unboundfinance/status/1552238085009965056)

![Pangolin Partnership](screenshots/pagolin.png)


### Unbound partners with Router Protocol
🔗 [View Tweet](https://x.com/routerprotocol/status/1581991668496334854)

![Router Partnership](screenshots/router.png)


### Unbound partners with Multichain
🔗 [View Tweet](https://x.com/unboundfinance/status/1567385109871067136)

![Multichain Partnership](screenshots/multichain.png)

### Unbound live on Fantom mainnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1569301272326733825)

![Fantom Mainnet](screenshots/fantom.png)



### Unbound V2 testnet phase 2 live
🔗 [View Tweet](https://x.com/unboundfinance/status/1580225524315848704)

![V2 Testnet Phase 2](screenshots/unboundv2testnet.png)


### Unbound V2 releases its application and landing page
🔗 [View Tweet](https://x.com/unboundfinance/status/1776211603488162195)

![Application Release](screenshots/unboundv2testnet.png)


### UNB ready and live for trading on Changelly
🔗 [View Tweet](https://x.com/unboundfinance/status/1643653712051687424)

![Changelly Trading](screenshots/changelly.png)

### Unbound V2 live on Arbitrum mainnet
🔗 [View Tweet](https://x.com/unboundfinance/status/1645771111127461895)

![Arbitrum Mainnet](screenshots/arbitrummainnet.png)


### UNB bridging to Arbitrum chain live via the Stargate bridge
🔗 [View Tweet](https://x.com/unboundfinance/status/1732689026627293225)

![Stargate Bridge](screenshots/stargataUNBBridge.png)


### Unbound DAO live
🔗 [View Tweet](https://x.com/unboundfinance/status/1790354780507759093)

![DAO Live](screenshots/unbounddaolive.png)


© Unbound Finance 2025
