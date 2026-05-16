<!-- source: https://core.telegram.org/bots/api -->
# getUpdates

- Long polling method for incoming updates.
- `offset` acknowledges updates with ids below the offset and prevents duplicates.
- `allowed_updates` filters update types.
- Updates are stored temporarily and are not kept longer than 24 hours.
