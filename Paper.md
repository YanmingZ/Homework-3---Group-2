# Research on DODODex applying Proactive AMM

### 2. The machanism of DODODex

In traditional AMMs, liquidity providers (LPs) deposit equal amounts of two assets into a pool and receive tokens representing their share of the pool. Trades occur by swapping one asset for another, and the price is determined based on the ratio of the two assets in the pool. However, when there is high demand for one asset and low demand for another, the price can become volatile and lead to impermanent loss for LPs. Proactive AMMs aim to mitigate this risk by dynamically adjusting the pool ratio based on recent trades and external data from an oracle.

Suppose that $B_{0}$ and $Q_{O}$ are the initial amounts of base and quote tokens deposited by the liquidity providers respectively. In the meantime, we use $B$ and $Q$ to denote the current amounts of base and quote tokens in the pool. As can be seen easily, the target of pAMM is to keep $\frac{B}{Q}$ as closer to $\frac{B_{0}}{Q_{0}}$ as possible. When the ratio of assets in pool change, the pAMM will proactively alter the prices based on a mathematical model and imputs from an oracle, encouraging traders to push the ratio of assets to the initial level through arbitrages. The marginal prices of base and quote tokens are calculated as below:

$$P_{margin}=iR$$

where $i$ is the market price provided by the oracle, and $R$ is is defined to be the piecewise function below:

If $B < B_{0}$, then $$R=1-k+(\frac{B_{0}}{B})^{2}k$$ 
If $Q < Q_{0}$, then $$R=1/(1-k+(\frac{Q_{0}}{Q})^{2}k)$$
If $B = B_{0}$, which is equivalent to $Q = Q_{0}$, then $$R=1$$

where $k$ is the liquidity parameter set in advance. As we can see, when $k$ is 0, the protocol naively sells or buys at the market price, with no promotion on the liquidity balance. When $k$ increases to 1, the algorithm becomes the standard AMM. Normally, $k$ is recommended to be a relatively small value, such as 0.1, which could provide liquidity 10 times better than the standard AMM algorithm.

In conclusion, when a trader sells/sells base tokens, the base token balance of the capital pool is higher/lower than the base token regression target; conversely, the quote token balance is now lower/higher than the quote token regression target. In this state, the pAMM will try to sell the excess/buy the shortage base tokens, lowering/highering the base token balance and increasing/decreasing the quote token balance, in order to move this state back to the state of equilibrium. 

### 3. The use cases of DODODex

Proactive Automated Market Making aims at minimizing impermanent loss and maximizing capital efficiency by incorporating external price guidance and customized pricing strategies. There are several use cases where PMM can be particularly beneficial:

The first one is proactive market making with external price guidance. PMM can retrieve market prices from external sources for mainstream assets like BTC and ETH to adjust mid-prices and minimize impermanent loss. This use case enables single-token liquidity provision and unlocks higher capital efficiency than traditional AMM platforms.

PMM also allows for low barrier-to-entry automated market making. For long-tail asset markets, PMM can help asset issuers with initial liquidity without requiring large amounts of capital to pair up with assets. This use case gives pricing power to takers entirely and drastically reduces the barrier-to-entry for smaller projects.

PMM also provide the possibility to create fully customizable liquidity pools and free market making. This use case is intended for experienced and ambitious market makers who want the highest degree of freedom and customizability possible to execute their own market making strategies. Market makers have full control over all pool parameters, can dynamically adjust the asset price, and can deposit to and withdraw from these liquidity pools in arbitrary ratios, without affecting the asset price.

Another important use case is Crowdpooling. This use case is an innovation compared to current asset issuance mechanics. Crowdpooling allows participants to receive tokens at the same unit price and enables token trading after the conclusion of the sale. The remaining unsold tokens and liquidity collected from the last phase are used to construct a DODO Vending Machine.

Finally, PMM are also capable of supporting stablecoin trading scenarios. PMM with configurations i = 1 and k = 0.001 (or 0 for 1-to-1 ratio) is virtually identical to Curve in terms of performance and capital efficiency, with the added benefit of flexibility.
