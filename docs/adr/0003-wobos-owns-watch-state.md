# WobOS owns watch state

GrannySwift supplies operations and factual events, through one Beeper watcher; WobOS, as a consumer, owns watch subscriptions, expiry, conditions, checkpoints, deduplication, decisions and notifications, and recovers after sleep or restart by reconciling history, because a live event stream is not a durable replay guarantee. This keeps GrannySwift usable without WobOS and avoids building a second orchestration system inside it.
