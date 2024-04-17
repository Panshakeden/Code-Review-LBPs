Balancer-V2LiquidityBootsrappingPools

Balancer V1 was launched in 2020 and quickly became one of DeFi’s building blocks. It focused on capital efficiency and aimed to make liquidity both customizable and easily accessible.V1 was key for facilitating Initial Dex Offerings (IDOs) thanks to Liquidity Bootstrapping Pools’ flexibility. This offered protocols a gateway into DeFi and made token launches simple and straightforward. Liquidity mining, another Balancer innovation, revolutionized token launches, with Yearn Finance’s YFI being a prime example. It created a new meta which is still followed by many industry participants for their own launches.

Balancer V1 also addressed novel token concepts and market volatility. Protocols with rebasing tokens leveraged Balancer’s ‘smart pools’ to manage price volatility and protect against malicious trading strategies. Surge pricing tackled volatility spikes by tailoring their trading fees to reflect short-term fluctuations.

Another innovation that was pioneered alongside V1 is Snapshot. This open-source governance platform was incubated by Balancer in its early days. It has since turned into a critical pillar of DeFi governance.Balancer V1 showed the world what possibilities DeFi had and set a high bar. It was now time for V2 to take it to the next level.

One of the biggest changes it brought was the introduction of the Vault. It is central to Balancer’s arcthitecture now and it plays a crucial role in maintaining efficiency, The vault serves as the central hub of balancer, functioning as a smart contract responsible for storing and overseeing all tokens within Balancer pools. It acts as a gateway for most balancer transactions, including swaps, joining pools, and existing pools.  It also unlocks advanced DeFi features such as flash loans, thus addressing an even wider audience.

Another change that came with V2 was the implementation of a three-tiered protocol fee system. It originally included trading fees, withdrawal fees, and flash loan fees. The system laid the groundwork for the protocol’s current revenue model and was a crucial step towards even higher resilience.
Speaking of resilience and stability, V2 rolled out two types of price oracles. They added another layer of the protocol’s usability and safeguarded price feeds from sandwich attacks.

Read more https://medium.com/balancer-protocol/the-balancer-report-v1-v2-v3-8ea976ebc06e

LiquidityBootsrappingPools

Liquidity bootstrapping pools are pools in balancer that can adjust the balance between two tokens dynamically over time. For example, the ratio of token A to token B can change from 1:99 to  99:1. LBP uses weighted math, where the weights change based on time. The pool owner chooses the starting and ending weights and the duration of these changes. They also can pause swaps in the pool. Only the owner can add liquidity to the pool, controlling composition over time.

 CONTRACT REVIEW LIQUIDITYBOOTSTRAPPINGPOOL

NOTE: Some libraries and interface are imported within some contract because they have been explained at the bottom of this documment.

LiquidityBootstrappingPool

>pragma solidity ^0.7.0;

The pragma solidity ^0.7.0; in Solidity specifies the version of the Solidity compiler that should be used to compile the smart contract. In this case, it specifies that the compiler version should be greater than or equal to version 0.7.0

>pragma experimental ABIEncoderV2;

In Solidity code, it allows you to use functions that accepts or returns structs types or arrays of structs as arguments or return values. This can be particularly useful for organizing and handling complex data structures in your smart contract.


  =>import "./Math.sol";

       imported  "./BalancerErrors.sol" 

abs(int256 a):

Returns the absolute value of a signed integer.
Uses assembly to efficiently compute the absolute value.

add(uint256 a, uint256 b):

Returns the addition of two unsigned integers of 256 bits, reverting on overflow.
Checks if the result c is greater than or equal to a, reverting with Errors.ADD_OVERFLOW if overflow occurs.

add(int256 a, int256 b):

Returns the addition of two signed integers, reverting on overflow.
Checks if the result c is within the valid range, depending on the signs of a and b, reverting with Errors.ADD_OVERFLOW if overflow occurs.

sub(uint256 a, uint256 b):

Returns the subtraction of two unsigned integers of 256 bits, reverting on underflow.
Checks if b is less than or equal to a, reverting with Errors.SUB_OVERFLOW if underflow occurs.

sub(int256 a, int256 b):

Returns the subtraction of two signed integers, reverting on overflow or underflow.
Checks if the result c is within the valid range, depending on the signs of a and b, reverting with Errors.SUB_OVERFLOW if overflow or underflow occurs.

max(uint256 a, uint256 b):

Returns the larger of two unsigned integers of 256 bits.

min(uint256 a, uint256 b):

Returns the smaller of two unsigned integers of 256 bits.

mul(uint256 a, uint256 b):

Returns the multiplication of two unsigned integers of 256 bits, reverting on overflow.
Checks if a * b divided by a equals b, reverting with Errors.MUL_OVERFLOW if overflow occurs.

div(uint256 a, uint256 b, bool roundUp):

Performs division of two unsigned integers with an option to round up or down.
Uses divDown or divUp based on the roundUp parameter.

divDown(uint256 a, uint256 b):

Performs division of two unsigned integers, rounding down.
Checks if the divisor b is not zero, reverting with Errors.ZERO_DIVISION if it is.

divUp(uint256 a, uint256 b):

Performs division of two unsigned integers, rounding up.
Checks if the divisor b is not zero, reverting with Errors.ZERO_DIVISION if it is.
Uses assembly to efficiently calculate the rounded-up division.


=> import "./LogExpMath.sol";

This library provides functions for exponentiation, logarithms, and natural logarithms with fixed-point arithmetic. Here's an explanation below:

Constants: Several constants are defined with fixed-point arithmetic (18 decimal places) for mathematical calculations.

Exponential and Logarithmic Functions:

pow(uint256 x, uint256 y): Calculates the exponentiation of x to the power of y. It uses logarithms and exponentiation properties to compute the result.

exp(int256 x): Computes the natural exponential function (e^x) for a signed fixed-point decimal x.
log(int256 arg, int256 base): Calculates the logarithm of arg with respect to the base base.
ln(int256 a): Computes the natural logarithm (ln) of a fixed-point decimal a.

Internal Functions:
_ln(int256 a): Calculates the natural logarithm using a Taylor series expansion for high precision.
_ln_36(int256 x): Calculates the natural logarithm with 36 decimal places of precision for values close to one.
Constants for Taylor Series:
The code includes constants and calculations for Taylor series expansions used in logarithmic and exponential computations.

In summary,this library provides accurate mathematical functions for working with fixed-point decimals, useful in financial and numerical applications.



=>import "./InputHelpers.sol"; Below are it's imports:

    import "./IERC20.sol";
    import "./BalancerErrors.sol";

Function ensureInputLengthMatch:

This is used to check if two or three input values are equal.
Checks if an array of addresses (or ERC20 tokens) is sorted in ascending order.
Converts an array of IERC20 tokens to an array of addresses and then calls the internal function for address arrays.
The assembly code  is used to convert the array of tokens (IERC20[]) to an array of addresses (address[]) for sorting.

Error Handling:
The _require function is used for error handling and reverting transactions if conditions are not met. The error codes are defined in BalancerErrors.sol.
Overall, this library provides useful functions for ensuring input data integrity, particularly for sorting arrays and checking input lengths. It also demonstrates the usage of error handling in Solidity contracts.

>import "./ScalingHelpers.sol"; Scaling.sol has the following imports below:

         >import "./FixedPoint.sol";
         >import "./Math.sol";
         >import "./ERC20.sol";
         >import "./InputHelpers.sol";

Scaling Functions:

_upscale, _downscaleDown, and _downscaleUp functions deal with scaling and reversing scaling based on a scalingFactor. These functions are used to normalize token amounts to a standard representation, typically with 18 decimals.
FixedPoint library likely provides fixed-point arithmetic for precise calculations involving decimals.
Array Scaling Functions:

_upscaleArray, _downscaleDownArray, and _downscaleUpArray are similar to their single-value counterparts but operate on arrays of values. They mutate the input arrays to apply or reverse scaling.
Compute Scaling Factor:

_computeScalingFactor calculates the scaling factor for a given ERC20 token based on its decimal precision (decimals). It assumes tokens with more than 18 decimals are not supported.
Comments and Notes:

Comments within the code provide explanations and context for various operations and assumptions made, such as normalizing token balances to simplify pool logic and handling decimals uniformly.
Overall, this code segment is part of a larger system that manages token balances, scaling, and arithmetic operations in a standardized manner, likely to ensure consistency and accuracy in token-related computations within a smart contract.



=>import "./BasePoolMath.sol"; Below is the import:

      import "./FixedPoint.sol";
   
using FixedPoint for uint256;: Enables using the fixed-point arithmetic functions defined in the FixedPoint library on uint256 variables within this library.

computeProportionalAmountsIn Function:

Computes the proportional amounts in (per token) based on balances, BPT total supply, and BPT amount out (bptAmountOut).
Uses fixed-point arithmetic which was imported (mulUp) to handle rounding up in the calculations.
Returns an array (amountsIn) containing the calculated proportional amounts in for each token in the pool.

computeProportionalAmountsOut Function:

Computes the proportional amounts out (per token) based on balances, BPT total supply, and BPT amount in (bptAmountIn).
Uses fixed-point arithmetic (mulDown) to handle rounding down in the calculations.
Returns an array (amountsOut) containing the calculated proportional amounts out for each token in the pool.

In summary, this library provides essential functions for performing proportional calculations within a token pool, crucial for managing balances and liquidity in decentralized finance (DeFi) applications.


=>import "./PoolRegistrationLib.sol";

         =>Pool registration imports Ivault Which Also Have Imports:

                    import "./IERC20.sol";
                    import "./IAuthentication.sol";
                    import "./ISignaturesValidator.sol";
                    import "./ITemporarilyPausable.sol";
                    import "./IWETH.sol";
                    import "./IAsset.sol";
                    import "./IAuthorizer.sol";
                    import "./IFlashLoanRecipient.sol";
                    import "./IProtocolFeesCollector.sol";

In summary, this pool registration library provides functions to register pools and tokens in a vault contract. It ensures the correctness of inputs, handles specialized pool registrations, and manages token registration and deregistration within pools


=>import "./LiquidityBootstrappingPoolSettings.sol";

The contract imports various other Solidity file :

                    import "./IMinimalSwapInfoPool.sol";
                    import "./Math.sol";
                    import "./ScalingHelpers.sol";
                    import "./NewBasePool.sol";
                    import "./GradualValueChange.sol";
                    import "./WeightedMath.sol";
                    import "./LiquidityBootstrappingPoolStorageLib.sol";

Contract Structure:
The contract is abstract (abstract contract), meaning it cannot be instantiated directly but can be inherited by other contracts.

Constructor:

The constructor initializes the contract with essential parameters like the Vault, pool ID, tokens, swap fee percentage, and other settings required.
It calculates and stores scaling factors for each token based on their decimals to normalize token balances.

State Variables:

_poolState: Stores various pool parameters such as swap enabled status, recovery mode, timestamps, and weights in a compact manner using bit manipulation techniques.
_swapFeePercentage: Represents the current swap fee percentage applicable to this pool.

Events:

SwapFeePercentageChanged: Emits when the swap fee percentage is changed.

SwapEnabledSet: Emits when the swap functionality is enabled or disabled.

GradualWeightUpdateScheduled: Emits when a gradual weight update is scheduled.

getSwapEnabled, getSwapFeePercentage, getNormalizedWeights, getGradualWeightUpdateParams: External functions to retrieve pool parameters.

setSwapEnabled, setSwapFeePercentage, updateWeightsGradually: External functions to set pool parameters like swap enabled status, swap fee percentage, and schedule gradual weight updates.

_getNormalizedWeights, _startGradualWeightChange: Internal functions used for internal logic like calculating normalized weights and initiating gradual weight updates.

_scalingFactor, getScalingFactors, inRecoveryMode, _setRecoveryMode: Functions related to scaling factors, recovery mode, and owner actions.
Modifiers:

The contract uses custom modifiers like authenticate and whenNotPaused to control access to certain functions based on authentication and contract state.

Error Handling:

The contract defines custom error messages and uses _revert and _require functions to handle errors and validate inputs.



  =>LiquidityBootstrappingPool

The contract imports various other Solidity file :

                    import "./WeightedPoolUserData.sol";
                    import "./Math.sol";
                    import "./ScalingHelpers.sol";
                    import "./BasePoolMath.sol";
                    import "./PoolRegistrationLib.sol";
                    import "./WeightedMath.sol";
                    import "./WeightedExitsLib.sol";
                    import "./WeightedJoinsLib.sol";
                    import "./LiquidityBootstrappingPoolSettings.sol";
                    import "./LiquidityBootstrappingPoolStorageLib.sol";

Constructor (constructor):

This function initializes the contract when it's deployed. It takes various parameters such as the vault, pool name, symbols, tokens, normalized weights, swap fee percentage, duration parameters, owner address, and swap enablement status.

It also calls PoolRegistrationLib.registerPool to register the pool with the vault, specifying the pool specialization based on the number of tokens (either TWO_TOKEN or MINIMAL_SWAP_INFO).
Swap Hooks (_onSwapGeneral, _onSwapMinimal):

These internal virtual functions handle swap operations within the pool.
_onSwapGeneral is not implemented and reverts with an error message (Errors.UNIMPLEMENTED).
_onSwapMinimal calculates token swap amounts based on input and output balances, weights, and swap fees.

Initialize Hook (_onInitializePool):
This internal view function is called when the pool is initialized.
It checks if the caller is the owner, verifies the join kind, and calculates the initial pool invariant and BPT (Balanced Pool Tokens) amount.

Join Hook (_onJoinPool):
This internal view function is called when tokens are added to the pool.
It checks if the caller is the owner, calls _doJoin to handle the join operation based on the join kind provided in the user data, and returns the BPT amount and token amounts to be received by the pool.

Exit Hook (_onExitPool):
This internal view function is called when tokens are withdrawn from the pool.
It calls _doExit to handle the exit operation based on the exit kind provided in the user data and returns the BPT amount to be burned and token amounts to be sent to the recipient.

Recovery Mode Exit (_doRecoveryModeExit):
This internal pure function handles exits during recovery mode.
It calculates the BPT amount to be burned and the token amounts to be sent based on balances, total supply, and user data.

Dispatch Functions (_doJoin, _doExit):
These internal view functions dispatch the join and exit operations based on the join and exit kinds specified in the user data.
They call functions from WeightedJoinsLib and WeightedExitsLib to perform specific join and exit actions, such as exact tokens in for BPT out, token in for exact BPT out,



CONTRACT INTERFACES

import "./IProtocolFeesCollector.sol";

This interface defines the structure and functionality for managing protocol fees, including setting and retrieving fee percentages, withdrawing fees, and interacting with related contracts such as the authorizer and vault

import "./ITemporarilyPausable.sol";

PausedStateChanged: Emitted whenever the pause state changes.

getPausedState: Returns information about the current paused state, including pause window end time and buffer period end time.

In summary, this interface is designed to be implemented by contracts that support temporary pausing functionality, providing methods to check the paused state and related time-based information.

import "./IWETH.sol";

IWETH is an interface specifically designed for interacting with Wrapped Ether (WETH), providing functions to deposit and withdraw Ether, along with inheriting ERC-20 standard functions from IERC20

import "./IAsset.sol";

It doesn't define any specific functions or events but can be used to create new address-like types within Solidity code

import "./IAuthorizer.sol";

This interface is part of a permissioning or access control system within a smart contract or application, where certain actions require authorization from specific accounts or roles.


import "./IAuthentication.sol";

This interface defines a standard for contracts that implement authentication functionality, specifically the getActionId function for retrieving action identifiers associated with external functions.

import “./IERC20.sol”:

 imports the interface for the ERC20 standard, which defines a common interface for fungible tokens. This import is used to interact with the ERC20

import "./ISignaturesValidator.sol";

This interface is designed to be implemented by contracts that provide signature validation functionality, particularly for meta-transactions. It defines methods for retrieving the EIP712 domain separator This struct represents the EIP712 domain separator, which is used to identify the domain in which a message is being signedand returns the next nonce for a given address used for signing messages.

import "./IMinimalSwapInfoPool.sol";

this interface defines the required function onSwap that pool contracts implementing the MinimalSwapInfo or TwoToken specialization settings should adhere to. It facilitates swaps between users and the pool while ensuring consistency and compatibility with the Vault contract.


LIBRARIES


import "./GradualValueChange.sol";

This library provides utilities for smoothly transitioning values over time, ensuring gradual changes without abrupt jumps or discontinuities, which is useful in various applications such as financial modeling, token vesting schedules, or dynamic parameter adjustments in smart contracts.

import "./WordCodec.sol";

This library provides utilities for efficiently packing and unpacking values within a single 256-bit word, which is beneficial for optimizing gas usage and storage in Solidity contracts

import "./ValueCompression.sol";

It provides a set of functions to efficiently compress and decompress numerical values, useful for optimizing storage and gas costs in Solidity contracts when dealing with large sets of data.

=>Import LiquidityBootstrappingPoolStorageLib
The contract imports various other Solidity file :

                    import "./ValueCompression.sol";
                    import "./WordCodec.sol
                    import "./GradualValueChange.sol";

This library provides a structured approach to managing storage and operations related to Liquidity Bootstrapping Pools in Ethereum smart contracts, optimizing gas usage and storage efficiency.



=>import "./lib/WeightedJoinsLib.sol";

The library imports several other Solidity files: 

                    import "./WeightedPoolUserData.sol";
                    import "./BasePoolMath.sol";
                    import "./ScalingHelpers.sol";
                    import "./WeightedMath.sol";

Library Functions:

joinExactTokensInForBPTOut: Calculates the amount of BPT tokens to be minted when exact amounts of tokens are deposited into the pool.

joinTokenInForExactBPTOut: Calculates the amount of tokens to be deposited to mint a specific amount of BPT tokens for a single token.

joinAllTokensInForExactBPTOut: Calculates the amounts of tokens to be deposited to mint a specific amount of BPT tokens for all tokens in the pool.
Usage of Other Libraries:

WeightedPoolUserData: Extends the functionality of the bytes type with methods related to weighted pool user data.

BasePoolMath and WeightedMath: Utilizes mathematical functions from these libraries for calculations related to joining the pool.



=>import "./lib/WeightedExitsLib.sol
        
The library imports several other Solidity files:

                    import "./WeightedPoolUserData.sol";
                    import "./BasePoolMath.sol";
                    import "./ScalingHelpers.sol";
                    import "./WeightedMath.sol

Library Functions:

exitExactBPTInForTokenOut: Computes the amount of tokens to be received when a specific amount of pool tokens (BPT) is burned for a single token.

exitExactBPTInForTokensOut: Computes the amounts of tokens to be received when a specific amount of BPT is burned for multiple tokens.
exitBPTInForExactTokensOut: Computes the amount of BPT needed to be burned to receive a specific amount of tokens for each token in the pool.
Usage of Other Libraries:

WeightedPoolUserData: Extends the functionality of the bytes type with methods related to weighted pool user data.

BasePoolMath and WeightedMath: Utilizes mathematical functions from these libraries for calculations related to exiting the pool.


=>import "./WeightedMath.sol";

The library defines several internal constants such as _MIN_WEIGHT, _MAX_WEIGHTED_TOKENS, _MAX_IN_RATIO, _MAX_OUT_RATIO, _MAX_INVARIANT_RATIO, and _MIN_INVARIANT_RATIO. These constants are used in various calculations within the library.

Library Functions:

_calculateInvariant: Computes the invariant for a pool given the normalized weights and balances of tokens in the pool.

_calcOutGivenIn and _calcInGivenOut: Compute how many tokens can be swapped given certain input and output amounts, respecting maximum ratio constraints.

_calcBptOutGivenExactTokensIn and _calcBptOutGivenExactTokenIn: Calculate the amount of pool tokens (BPT) to be minted when tokens are added to the pool.

_calcBptInGivenExactTokensOut and _calcBptInGivenExactTokenOut: Calculate the amount of pool tokens to be burned when tokens are removed from the pool.

_calcTokenInGivenExactBptOut and _calcTokenOutGivenExactBptIn: Compute the input or output token amount given a specific BPT amount.

_computeJoinExactTokensInInvariantRatio and _computeExitExactTokensOutInvariantRatio: Intermediate functions used to compute the invariant ratio in certain swap scenarios.
Error Handling:

The library uses a custom error handling mechanism, possibly defined in another part of the codebase (Errors.ZERO_INVARIANT, Errors.MAX_IN_RATIO, etc.).



import "./WeightedPoolUserData.sol";

Defines a library which contains functions for handling user data related to weighted pools.

Enums:

enum JoinKind : Defines an enumeration type JoinKind, which represents different kinds of joins in a weighted pool. 

enum ExitKind : Defines an enumeration type ExitKind, which represents different kinds of exits from a weighted pool.

Functions(Helper Function):

joinKind(bytes memory self) internal pure returns (JoinKind) : Decodes a byte array into a JoinKind enum value.

exitKind(bytes memory self) internal pure returns (ExitKind): Decodes a byte array into an ExitKind enum value.

Various functions like 
initialAmountsIn, 
exactTokensInForBptOut,
tokenInForExactBptOut, 
allTokensInForExactBptOut, 
exactBptInForTokenOut,
exactBptInForTokensOut,
and bptInForExactTokensOut
are defined to extract specific information from encoded byte arrays representing user data for joins and exits in weighted pools.



=> import "./BalancerErrors.sol"

Error Handling Functions:

_require(bool condition, uint256 errorCode) pure: Reverts the transaction if the condition is false, providing an error code.

_require(bool condition, uint256 errorCode, bytes3 prefix) pure: Similar to the previous function but allows specifying a custom error prefix.

_revert(uint256 errorCode) pure: Reverts the transaction with a default error prefix ('BAL') and the specified error code.

_revert(uint256 errorCode, bytes3 prefix) pure: Reverts the transaction with a custom error prefix and error code.
Error Codes:

The Errors library contains a range of error codes categorized into different sections like Math, Input, Shared pools, Pools, Lib, Vault, Fees, FeeSplitter, and Misc.
Each error code corresponds to a specific error condition that can occur during contract execution.

