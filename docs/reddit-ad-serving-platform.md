# Building Reddit's Ad Serving Platform (GopherCon 2018)

[Talk on YouTube](https://www.youtube.com/watch?v=tjcugWj37gA)

- User visits a page on Reddit
- Reddit makes call to an ad serving microservice
- This microservice runs some business logic and an auction to choose ads to serve
- Log (into Kafka) which ads were chosen
- After ad is served, log some more stuff into Kafka
- Run Spark jobs on Kafka logs to compute stuff like # of ads per advertiser, etc
- To build services, use go-kit, especially if you need logging, monitoring, metrics, etc
