# RSS Integration

## RSSHub

[RSSHub](https://github.com/DIYgod/RSSHub) - open-source RSS feed generator that supports various sources including Telegram channels.

### Telegram Channel RSS

To get RSS feed for a Telegram channel:

```sh
curl https://rsshub.app/telegram/channel/<channel_name>
```

Example: `https://rsshub.app/telegram/channel/example_channel`

## Maubot RSS Plugin Setup

For general maubot plugin setup instructions (creating bot user, getting access token, adding to room), see [`PLUGIN_SETUP.md`](../src/maubot/PLUGIN_SETUP.md).

### RSS-Specific Commands

After completing the general setup, use these commands to configure RSS subscriptions:

#### Subscribe to RSS Feed

```mxc
!rss subscribe <url>
```

Example:

```mxc
!rss subscribe https://rsshub.app/telegram/channel/example_channel
```

#### Add Custom Template

```mxc
!rss template <sub_id> $feed_title:

$title

$summary

[Read on the website]($link) | $date
```

Replace `<sub_id>` with the subscription ID returned from the subscribe command.
