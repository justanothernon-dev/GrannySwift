# Messages through Beeper alone

Messages reads, search, supported actions, media and events go through Beeper, extending its existing CLI where needed instead of writing a new direct-SDK Messages engine. We dropped the earlier Beeper plus imsg hybrid, with imsg history and a second imsg watcher, so there is one source of identity and history and no silent cross-vendor fallback; imsg stays only as a source reference for the narrow Send Later reader.
