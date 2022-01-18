Binance Alpha Bot AKA apebot.eth  << yes, you can also send donations to this ENS domain.


This program is a trading bot i built between february 2021 and January 2022.

It acts on new token listings on binance, and purchases them as quickly as possible onchain, sends them to binance, and then sells them there within the initial pump.

It does all sorts of fun things, like maintaining a list of cached endpoints so that we know which one to hit and when, relaying all the requests trough a mesh of proxy servers to avoid throttling, and has full support for EIP-1559.

Trades get routed throug 0x, so that we can have a gas efficient and dex-independant way of executing trades.

I am OSSing this as there are other competing OSS products out there which started after i launched this, and as the alpha is gone.

I currently no longer have the crypto capital neceessary to compete against a wallet with 700KUSD+ and insane gas fees offered to bribe miners, so i am calling it quits and using this as a proof of expertise and knowledge in this domain.

*I am currently for hire, you can contact me at david.leonardi@gmail.com*

I am proficient in NodeJS/TS development, but I'd much rather work for a DAO in a non-technical role. 
Bizdev, evangelism, "salesy" roles.
I currently work as a technical director/consultant working with large corporates, and I'm currently selling NFT projects for large very known brands which i cannot disclose due to NDAs.
I have 10+ years of exeprience as a dev, and 2+ years of experience on the sales/consulting side.
I used to be team lead/senior in most projects where i worked on, for what that's worth, but i'm sure you omegabrains out there will teach me a bunch of new cool stuff.
Open to learning solidity, and any new skill that is required.

Find my CV here: https://docs.google.com/document/d/1YWvrUaLKJOeDarbZPF7CQXJZdwYylHTptzWqnEGFadM

I will accept payments in both fiat and crypto.

----

Some basic setup info:

Please go and fill in the .env file with necessary info.

You will need the following third parties:
-Twilio
-CCXT pro
-https://proxymesh.com/
-A server to deploy this to. I used AWS Lightsail. The basic tier is not powerful enough. Take the second smallest.


---


How to run locally:
 
Use Docker to provide youu with mongo:
$ docker-compose up
$ yarn install
$ yarn run main_announcement

How to run on a server:

Provision yourself a lightsail instance.
Get all the third parties ready, and whitelist the APIs for those IPs.


run the setup.sh script in the root folder
Then run the commands contained in montosetup.txt

There are some additional notes below if you run into problems with ssh keys.








There are a few jobs that this can run:

main_announcement : This is the main Binance API crawler. It does everything from monitoring the APIs to creating entries in mongo.
main_dex_purchasing : This goes and analyses tokens, validates which chain they are on, and if its a good one, buys it on 0x. Originally it moved funds automatically to binance, but this is currently commented out and was executed as a manual step, because tokens can dump earlier than binance lists them and i wanted a kind of manual step. This also triggers calls / SMS to twilio.

main_apicrawler: This is an experimental "dump all binance shit" test app, which i used to try and find a new edge over the peeps over at https://www.cryptomaton.org/. Sometimes it picks up listings 3 seconds faster than they do, but it's till too slow to be the absolute first, who currently is listed out in targets.txt. 

main_selling: This sells tokens we moved on to binance.

****


----------
Debugging help

git config --global --add url."git@github.com:".insteadOf "https://github.com/"

initial build of docker images:

to fix:
#21 12.06 Load key "/root/.ssh/id_rsa": invalid format
#21 12.06 git@github.com: Permission denied (publickey).
#21 12.06 fatal: Could not read from remote repository.
#21 12.06 

use:
docker-compose build --build-arg SSH_PRIVATE_KEY="$(cat ~/.ssh/id_rsa)" --build-arg SSH_PUBLIC_KEY="$(cat ~/.ssh/id_rsa.pub)"