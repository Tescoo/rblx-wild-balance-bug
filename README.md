# RBLXWild Infinite Balance Bug
Infinite balance vulnerability found on RBLXWild at 00:28 on 29/4/2023 ~ PATCHED

# How it worked?
Plinko...

The plinko gamemode functioned in a really retarded way on RBLXWild, here is how:

# Betting
**When you place a bet, a request to this endpoint: `https://rblxwild.com/api/game/plinko/play` is sent**

**This request contains: `rows`, `bet amount`, `risk`**

**The response contains information about your payout, including `game id`**

# Retarded part
Now for some reason this is where the developers are really smart (sarcasm if you couldnt tell)

For some spastic reason, your plinko game will be payed out with a request to this endpoint: `https://rblxwild.com/api/game/plinko/finalize`

But the smart developers over at RBLXWild thought: "Ah, lets not add a limit to how many times the user can send this requests"

Basically meaning that you can infinitely send payout requests and just keep getting them

# Example

User makes a plinko game with 1k Robux, this hits an 8x on plinko.

RBLXWild then posts to `https://rblxwild.com/api/game/plinko/finalize` with the game ID, in order to get your payout.

EXPLOIT: The user then posts to the `https://rblxwild.com/api/game/plinko/finalize` endpoint with the game ID aswell, and gets a second payout

You can keep repeating the post requests to get infinite payouts

# Proof of concept

8 lines is what almost bankrupted a casino, here they are:

```
fetch("https://rblxwild.com/api/game/plinko/finalize", {
  "headers": {
    "authorization": "authToken here",
    "content-type": "application/json"
  },
  "body": "{\"gameId\":Game ID with a high payout here}",
  "method": "POST"
});
```

**NOT FUNCTIONAL**

You would replace `authToken here` with your RBLXWild authToken

And `Game ID with a high payout here` with... a Game ID with a high payout
# Funni images
![image](https://user-images.githubusercontent.com/66729830/235320788-ee282f33-316b-473a-a632-df8efa040eed.png)

![image](https://user-images.githubusercontent.com/66729830/235312492-19d109c4-8a6a-42fe-84f6-900e5a84d16a.png)

![image](https://user-images.githubusercontent.com/66729830/235312508-2c4c23af-3d4f-4df1-aa2c-b254694167dc.png)

# Thanks
Thanks,

Tesco#6969 / rambletrick
