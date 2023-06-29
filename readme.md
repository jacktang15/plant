# planet
**planet** is a blockchain built using Cosmos SDK and Tendermint and created with [Ignite CLI](https://ignite.com/cli).


## Start chain for train
start earth chain:
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ ignite chain serve -c earth.yml

  Blockchain is running

  ✔ Added account alice with address cosmos1lpx2wqhzjm0g0z8h80jv7h0x736538eyq7yzv6 and mnemonic:
    twelve gun paper modify display accuse begin brand random radio dignity uncle
    salt wood sunny twelve pear topic crouch radio engage federal genre romance

  ✔ Added account bob with address cosmos15epgsa068ahr867579dpwkcrldtgeca3vtwzkt and mnemonic:
    auto candy inmate slide fire athlete color frost spider online fortune armor
    flag midnight evoke view stove subject vast drift pull gravity reward journey

  🌍 Tendermint node: http://0.0.0.0:26657
  🌍 Blockchain API: http://0.0.0.0:1317
  🌍 Token faucet: http://0.0.0.0:4500

  ⋆ Data directory: /home/tomxiong/.earth
  ⋆ App binary: /home/tomxiong/go/bin/planetd

  Press the 'q' key to stop serve
  ```

Start mars chain:
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ ignite chain serve -c mars.yml
  
  ✔ Added account alice with address cosmos1a5lds3slurmj4knk2hasf8w92vsvfwynk0cwnq and mne
    clever cheap shoot consider property sleep gasp drop fold insect reject rocket
    tool dash ship metal dust sword lunch caught record eagle fossil tag          
  
  ✔ Added account bob with address cosmos1uvcx746lqtpslv07rz0u2vg2sf6j4g7mjslynk and mnemo
    absorb plastic distance aerobic fly student pyramid assist client virus target
    vital sibling embark current pass fiber gloom fossil favorite garden stomach  
    gain blue                                                                     
  
  🌍 Tendermint node: http://0.0.0.0:26659
  🌍 Blockchain API: http://0.0.0.0:1318
  🌍 Token faucet: http://0.0.0.0:4501
  
  ⋆ Data directory: /home/tomxiong/.mars
  ⋆ App binary: /home/tomxiong/go/bin/planetd
  
  Press the 'q' key to stop serve
```
# Start relayer:
config relayer
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ ls ~/.ignite/
ignite_cache.db  local-chains  plugins
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ ignite relayer configure -a   --source-rpc "http://0.0.0.0:26657"   --source-faucet "http://0.0.0.0:4500"   --source-port "blog"   --source-version "blog-1"   --source-gasprice "0.0000025stake"   --source-prefix "cosmos"   --source-gaslimit 300000   --target-rpc "http://0.0.0.0:26659"   --target-faucet "http://0.0.0.0:4501"   --target-port "blog"   --target-version "blog-1"   --target-gasprice "0.0000025stake"   --target-prefix "cosmos"   --target-gaslimit 300000
------
Setting up chains
------

? Source Account default
? Target Account default

🔐  Account on "source" is default(cosmos1gtsd9ujvy9zwc55alwkqfx5v9d68rlz8p2u04z)

 |· received coins from a faucet
 |· (balance: 200000stake,10token)

🔐  Account on "target" is default(cosmos1gtsd9ujvy9zwc55alwkqfx5v9d68rlz8p2u04z)

 |· received coins from a faucet
 |· (balance: 100000stake,5token)

⛓  Configured chains: earth-mars

```
start relayer
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ ignite relayer connect
------
Paths
------

earth-mars:
    earth > (port: blog) (channel: channel-0)
    mars  > (port: blog) (channel: channel-0)

------
Listening and relaying packets between chains...
------
```

# send one post from earth to mars:
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ planetd tx blog send-ibc-post blog channel-0 "Hello" "Hello Mars, I'm Alice from Earth" --from alice --chain-id earth --home ~/.earth
auth_info:
  fee:
    amount: []
    gas_limit: "200000"
    granter: ""
    payer: ""
  signer_infos: []
  tip: null
body:
  extension_options: []
  memo: ""
  messages:
  - '@type': /planet.blog.MsgSendIbcPost
    channelID: channel-0
    content: Hello Mars, I'm Alice from Earth
    creator: cosmos1lpx2wqhzjm0g0z8h80jv7h0x736538eyq7yzv6
    port: blog
    timeoutTimestamp: "1688051555027698098"
    title: Hello
  non_critical_extension_options: []
  timeout_height: "0"
signatures: []
confirm transaction before signing and broadcasting [y/N]: y
code: 0
codespace: ""
data: 12250A232F706C616E65742E626C6F672E4D736753656E64496263506F7374526573706F6E7365
events:
- attributes:
  - index: true
    key: ZmVl
    value: ""
  - index: true
    key: ZmVlX3BheWVy
    value: Y29zbW9zMWxweDJ3cWh6am0wZzB6OGg4MGp2N2gweDczNjUzOGV5cTd5enY2
  type: tx
- attributes:
  - index: true
    key: YWNjX3NlcQ==
    value: Y29zbW9zMWxweDJ3cWh6am0wZzB6OGg4MGp2N2gweDczNjUzOGV5cTd5enY2LzE=
  type: tx
- attributes:
  - index: true
    key: c2lnbmF0dXJl
    value: YldBMVJIVG1IOEdZNzFVMldKVUk4bkY0b214eE4xcFJleDEvSTI4ZHVLMEE3aXNRREFmN1NPVkRPZ2RTdktpSCtSQlFUdVFmNlc2NXptcEo1OE9iMkE9PQ==
  type: tx
- attributes:
  - index: true
    key: YWN0aW9u
    value: L3BsYW5ldC5ibG9nLk1zZ1NlbmRJYmNQb3N0
  type: message
- attributes:
  - index: true
    key: cGFja2V0X2RhdGE=
    value: EikKBUhlbGxvEiBIZWxsbyBNYXJzLCBJJ20gQWxpY2UgZnJvbSBFYXJ0aA==
  - index: true
    key: cGFja2V0X2RhdGFfaGV4
    value: MTIyOTBhMDU0ODY1NmM2YzZmMTIyMDQ4NjU2YzZjNmYyMDRkNjE3MjczMmMyMDQ5Mjc2ZDIwNDE2YzY5NjM2NTIwNjY3MjZmNmQyMDQ1NjE3Mjc0Njg=
  - index: true
    key: cGFja2V0X3RpbWVvdXRfaGVpZ2h0
    value: MC0w
  - index: true
    key: cGFja2V0X3RpbWVvdXRfdGltZXN0YW1w
    value: MTY4ODA1MTU1NTAyNzY5ODA5OA==
  - index: true
    key: cGFja2V0X3NlcXVlbmNl
    value: MQ==
  - index: true
    key: cGFja2V0X3NyY19wb3J0
    value: YmxvZw==
  - index: true
    key: cGFja2V0X3NyY19jaGFubmVs
    value: Y2hhbm5lbC0w
  - index: true
    key: cGFja2V0X2RzdF9wb3J0
    value: YmxvZw==
  - index: true
    key: cGFja2V0X2RzdF9jaGFubmVs
    value: Y2hhbm5lbC0w
  - index: true
    key: cGFja2V0X2NoYW5uZWxfb3JkZXJpbmc=
    value: T1JERVJfVU5PUkRFUkVE
  - index: true
    key: cGFja2V0X2Nvbm5lY3Rpb24=
    value: Y29ubmVjdGlvbi0w
  type: send_packet
- attributes:
  - index: true
    key: bW9kdWxl
    value: aWJjX2NoYW5uZWw=
  type: message
gas_used: "62921"
gas_wanted: "200000"
height: "2850"
info: ""
logs:
- events:
  - attributes:
    - key: action
      value: /planet.blog.MsgSendIbcPost
    - key: module
      value: ibc_channel
    type: message
  - attributes:
    - key: packet_data
      value: "\x12)\n\x05Hello\x12 Hello Mars, I'm Alice from Earth"
    - key: packet_data_hex
      value: 12290a0548656c6c6f122048656c6c6f204d6172732c2049276d20416c6963652066726f6d204561727468
    - key: packet_timeout_height
      value: 0-0
    - key: packet_timeout_timestamp
      value: "1688051555027698098"
    - key: packet_sequence
      value: "1"
    - key: packet_src_port
      value: blog
    - key: packet_src_channel
      value: channel-0
    - key: packet_dst_port
      value: blog
    - key: packet_dst_channel
      value: channel-0
    - key: packet_channel_ordering
      value: ORDER_UNORDERED
    - key: packet_connection
      value: connection-0
    type: send_packet
  log: ""
  msg_index: 0
raw_log: '[{"msg_index":0,"events":[{"type":"message","attributes":[{"key":"action","value":"/planet.blog.MsgSendIbcPost"},{"key":"module","value":"ibc_channel"}]},{"type":"send_packet","attributes":[{"key":"packet_data","value":"\u0012)\n\u0005Hello\u0012
  Hello Mars, I''m Alice from Earth"},{"key":"packet_data_hex","value":"12290a0548656c6c6f122048656c6c6f204d6172732c2049276d20416c6963652066726f6d204561727468"},{"key":"packet_timeout_height","value":"0-0"},{"key":"packet_timeout_timestamp","value":"1688051555027698098"},{"key":"packet_sequence","value":"1"},{"key":"packet_src_port","value":"blog"},{"key":"packet_src_channel","value":"channel-0"},{"key":"packet_dst_port","value":"blog"},{"key":"packet_dst_channel","value":"channel-0"},{"key":"packet_channel_ordering","value":"ORDER_UNORDERED"},{"key":"packet_connection","value":"connection-0"}]}]}]'
timestamp: ""
tx: null
txhash: 1304B192988692F1BEFEB853DE34E604BC6F1962090F929620BDA73874A651EF
```
# query result from mars
```
(base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ planetd q blog list-post --node tcp://localhost:26659
Post:
- content: Hello Mars, I'm Alice from Earth
  creator: blog-channel-0-
  id: "0"
  title: Hello
pagination:
  next_key: null
  total: "0"
  ```
  ```
  (base) tomxiong@DESKTOP-61U8AN0:~/cosmos/planet$ planetd q blog list-sent-post
SentPost:
- chain: blog-channel-0
  creator: ""
  id: "0"
  postID: "0"
  title: Hello
pagination:
  next_key: null
  total: "0"
  ```
