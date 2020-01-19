# Analogy for understanding Throughput, Response Time, Processing Time and Latency


## Definitions

**Processing Time:** The acutal time takes to serve/process the request.

**Response time:** Time between a client sending a request and receiving response.

**Latency:** Is the duration that a request is waiting to be handled.  While referring to Latency, it’s that delay we are talking about.

**Throughput:** Number of records we can process per second.  


## Analogy

There is a road between point A and B. The road has capacity to accomodate `4` cars at a time. Say there are 4 cars standing at point A, ready to move towards point B. And if everything is fine, then it takes `5s` for cars to reach B from point A. But dues to potholes in between, a guy standing at point B, sees the cars at `7s`.

```
  ----------------------------------------------------------
  [__]
  [__]
  --      --      --      --      --      --      --      --
  [__]
  [__]
  ---------------------------------------------------------- 
  A <-------------------- 5s ----------------------------> B

```

Then here, 

- Processing time: `5s`
- Response time: `7s`
- Latency: `2s`
- Throughtput: `4`

