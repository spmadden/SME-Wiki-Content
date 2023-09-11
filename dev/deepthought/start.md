## DeepThought

DeepThought is an IRC bot that trolls the SSE and Factset IRC Networks.

### Basic Commands

#### Addressing

DT Responds to Direct Queries by matching against

    ^DeepThought[:,] (.+)$ 

As well as the following bang commands:

-   [!roll (\\d+)d(\\d+)](/dev/DeepThought/dice)
-   [!man (.+)](/dev/DeepThought/man)
-   [!quote](/dev/DeepThought/quoting)
-   [!roulette (.+)?](/dev/DeepThought/roulette)
-   [!wiki (.+)](/dev/DeepThought/wiki)

Bang commands do not need to be directly addressed to DT as he will listen for those at any time.

#### Questions

DT has the ability to answer some basic questions as well.
