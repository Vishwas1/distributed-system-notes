# Analogy for understanding Throughput, Response Time, Processing Time and Latency


## Definitions

**Processing Time:** The acutal time takes to serve/process the request.

**Response time:** Time between a client sending a request and receiving response.

**Latency:** Is the duration that a request is waiting to be handled.  While referring to Latency, it’s that delay we are talking about.

**Throughput:** Number of records we can process per second.  


## Analogy

There is a road between point A and B. The road has capacity to accomodate `4` cars at a time. Say, there are `4` cars standing in garrage and it takes `2s` for them to reach point A from the garrage. Once started from point A, it takes `5s` for them to reach B. A guy standing at point B, sees the cars at `7s` ultimately.

```
Cars waiting in garrage (at time 0):
[_a_], [_b_], [_c_], [_d_]

Cars ready to move (at time 2s):

  -----------------------------------------------------------
  [_a_]
  [_b_]
  --      --      --      --      --      --      --      --
  [_c_]
  [_d_]
  -----------------------------------------------------------
  A                                                         B

Cars reached the destination (at time 7s):

  -----------------------------------------------------------
                                                        [_a_]
                                                        [_b_]
  --      --      --      --      --      --      --      --
                                                        [_c_]
                                                        [_d_]
  -----------------------------------------------------------
  A                                                         B

```

Then here, 

- Processing time: `5s`
- Response time: `7s`
- Latency: `2s`
- Throughtput: `4`

