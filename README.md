![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/spl.png)

**Solana SPL Token Sniper Bot** that listens to new Raydium USDC or SOL pools and buys tokens for a fixed amount in USDC/SOL.
Depending on the speed of the RPC node, the purchase usually happens before the token is available on Raydium UI for swapping.

- `WSOL Snipe`
- `Auto-Sell`
- `TP/SL`
- `Min Liq`
- `Burn/Lock Check`
- `Renounce Check`
- `Fast Buy`

> [!NOTE]
> This is provided as is, for learning purposes.

## SETUP
To run the script you need to:
1. Create a new empty Solana wallet.
2. Transfer some SOL to it.
3. Convert some SOL to USDC or WSOL (you need USDC or WSOL depending on the configuration set below).
4. Download and extract the repository files: Use the command "git clone https://github.com/SolSniperLab/sol-sniper-bot" or click the green "Code" button and select "Download ZIP".
5. Install the Node.js environment on your computer : https://nodejs.org/en
6. The runtime environment should be a terminal or VSCode. Detailed steps are provided below, please read carefully.

`Jupiter Wrap` : https://jup.ag/

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/jupiterwrap.png)

## CONFIG
1. Configure the script by updating `.env.copy` file (**remove the .copy from the file name when done**).
2. `PRIVATE_KEY` (your wallet private key)
3. `RPC_ENDPOINT` (https RPC endpoint)
4. `RPC_WEBSOCKET_ENDPOINT` (websocket RPC endpoint)
5. `QUOTE_MINT` (which pools to snipe, USDC or WSOL)
6. `QUOTE_AMOUNT` (amount used to buy each new token)
7. `COMMITMENT_LEVEL`
8. `CHECK_IF_IS_BURNED` (liquidity burn check)
9. `CHECK_IF_IS_LOCKED` (liquidity lock check)
10. `USE_SNIPE_LIST` (buy only tokens listed in snipe-list.txt)
11. `SNIPE_LIST_REFRESH_INTERVAL` (how often snipe list should be refreshed in milliseconds)
12. `CHECK_IF_MINT_IS_RENOUNCED` (script will buy only if mint is renounced)
13. `MIN_POOL_SIZE` (script will buy only if pool size is greater than specified amount)
14. `TAKE_PROFIT=200` (in %)
15. `STOP_LOSS=50` (in %)
16. `BIRDEYE_API_KEY=` (TP/SL, Burn/Lock) generate here : https://docs.birdeye.so/docs/authentication-api-keys

**Don't forget to check Birdeye API, if API key is not working, some bot functions such as TP/SL, Min/Max Liquidity etc may not work correctly or not work at all. If you follow the instructions there should be no errors.**

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/bird.png)

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/ebc668d0b63204e3a211b8ac7a970902107a6d91/readme/botenv.png)
  
## INSTALL
1. Install dependencies by typing: `npm install`
3. Run the script by typing: `npm run buy` in terminal

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/preview.png)

## TAKE PROFIT

> [!NOTE]
> By default, 200 % 

## STOP LOSS

> [!NOTE]
> By default, 50 %

## AUTO SELL
By default, auto sell is enabled. If you want to disable it, you need to:
1. Change variable `AUTO_SELL` to `false`
2. Update `MAX_SELL_RETRIES` to set the maximum number of retries for selling token
3. Update `AUTO_SELL_DELAY` to the number of milliseconds you want to wait before selling the token (this will sell the token after the specified delay. (+- RPC node speed)).

If you set AUTO_SELL_DELAY to 0, token will be sold immediately after it is bought.
There is no guarantee that the token will be sold at a profit or even sold at all. The developer is not responsible for any losses incurred by using this feature.

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/token.png)

## SNIPE LIST
By default, script buys each token which has a new liquidity pool created and open for trading.
There are scenarios when you want to buy one specific token as soon as possible during the launch event.
To achieve this, you'll have to use snipe list.
1. Change variable `USE_SNIPE_LIST` to `true` 
2. Add token mint addresses you wish to buy in `snipe-list.txt` file (add each address as a new line).

This will prevent script from buying everything, and instead it will buy just listed tokens.
You can update the list while script is running. Script will check for new values in specified interval (`SNIPE_LIST_REFRESH_INTERVAL`).

Pool must not exist before the script starts.
It will buy only when new pool is open for trading. If you want to buy token that will be launched in the future, make sure that script is running before the launch.

![](https://github.com/SolSniperLab/sol-sniper-bot/blob/b37a2fec33bffa000f49a47239270085fea14eaf/readme/snipelist.png)


## COMMON ISSUES

> [!IMPORTANT]
> If you have an error which is not listed here, please create a new issue in this repository.
> To collect more information on an issue, please change `LOG_LEVEL` to `debug`.
> 
> ### EMPTY TRANSACTION
> If you see empty transactions on SolScan most likely fix is to change commitment level to `finalized`.
> 
> ### UNSOPPORTED RPC NODE
> If you see following error in your log file:  
> `Error: 410 Gone:  {"jsonrpc":"2.0","error":{"code": 410, "message":"The RPC call or parameters have been disabled."}, "id": "986f3599-b2b7-47c4-b951-074c19842bad"}`  
> It means your RPC node doesn't support methods needed to execute script.
> FIX: Change your RPC node. You can use Shyft, Helius or Quicknode. 
> 
> ### NO TOKEN ACCOUNT
> If you see following error in your log file:  
> `Error: No SOL token account found in wallet:`  
> it means that wallet you provided doesn't have USDC/WSOL token account.
> FIX: Go to dex and swap some SOL to USDC/WSOL. When you swap sol to wsol you should see it in wallet.

## CONTACT

The program has undergone multiple audits and tests, demonstrating strong profitability. If you have any suggestions, please contact:

Discord: `@solmemelab`

## DISCLAIMER

> [!IMPORTANT]
> Use this script at your own risk.
