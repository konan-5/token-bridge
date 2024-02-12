# CrossChain Token Exchange

## Overview
The token exchange architecture facilitates seamless token swaps between the Binance Smart Chain (BSC) and the Polygon network (MATIC). This document outlines the processes involved in both directions of the exchange and the control mechanisms to ensure token balance integrity.

## Exchange BSC => Polygon
1. **Initiating Exchange:**
   - User calls the `swapStart` function of the `BscVault` contract on the BSC network.
   - Before calling, the user must approve the BSW token for exchange.

2. **Processing Exchange:**
   - Upon receiving the `SwapStart` event from `BscVault`, the server calls the `swapEnd` function of the `MaticMinter` contract on the Polygon network (MATIC).
   - `swapEnd` mints the specified amount to the recipient on the Polygon network.

3. **Completing Exchange:**
   - After receiving the `SwapEnd` event from `MaticMinter`, the server calls the `setSwapComplete` function of `BscVault` to finalize the exchange.

## Exchange Polygon => BSC
1. **Initiating Exchange:**
   - User calls the `swapStart` function of the `MaticMinter` contract on the Polygon network (MATIC).

2. **Processing Exchange:**
   - Upon receiving the `SwapStart` event from `MaticMinter`, the server calls the `swapEnd` function of the `BscVault` contract on the BSC network.
   - `swapEnd` unlocks the specified BSW Token amount in favor of the recipient on the BSC network.

3. **Completing Exchange:**
   - After receiving the `SwapEnd` event from `BscVault`, the server calls the `setSwapComplete` function of `MaticMinter` to finalize the exchange.

## Controlling Token Balance Integrity
- Upon completing all exchanges, the deposit count of `MaticMinter` should match `BscVault`.
- The balance of `BscVault` must equal the total BSW token supply in the Polygon network (MATIC).

## Conclusion
This architecture enables efficient and secure token swaps between BSC and Polygon networks, ensuring integrity through careful control mechanisms.
