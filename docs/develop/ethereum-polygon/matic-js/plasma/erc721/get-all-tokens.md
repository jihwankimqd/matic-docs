---
id: get-all-tokens
title: getAllTokens
keywords: 
- 'plasma client, erc721, getAllTokens, polygon, sdk'
description: 'Returns all tokens owened by specified user.'
---

`getAllTokens` method returns all tokens owened by specified user.

```
const erc721Token = plasmaClient.erc721(<token address>);

const result = await erc721Token.getAllTokens(<user address>, <limit>);

```

you can also limit the tokens by specifying limit value in second parmater.
