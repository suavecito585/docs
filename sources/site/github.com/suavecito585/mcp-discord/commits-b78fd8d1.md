# Source: https://github.com/suavecito585/mcp-discord/commits?author=MayumiKohei

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## Branch selector

 main

## User selector

![](https://avatars.githubusercontent.com/u/122164552?v=4&size=32)

MayumiKohei

## Datepicker

All time

## Commit History

### Commits on May 7, 2026

- #### [feat: expose reactions in read\_messages + add get\_reaction\_users tool](https://github.com/suavecito585/mcp-discord/commit/22eb4c71ae786951ab4b130d8a8f2f247780c8ac 'feat: expose reactions in read_messages + add get_reaction_users tool
 
 Why
 ---
 discord.js Message オブジェクトには `reactions.cache` が REST fetch (no Gateway
 intent required) で populate されているのに、`readMessagesHandler` の formatter
 がこれを列挙せず捨てていた。reaction-watcher / approval-loop ワークフローを
 組む際、read_messages の応答に reactions が無いと使い物にならない。
 
 What
 ----
 1. `readMessagesHandler` (src/tools/channel.ts) の formattedMessages に
 `reactions` フィールドを追加。emoji.name / emoji.id / count / me を返す。
 Gateway intent は不要（既存 `messages.fetch()` の REST 応答に含まれる）。
 
 2. 新ツール `discord_get_reaction_users` 追加:
 - schema: GetReactionUsersSchema (channelId / messageId / emoji / limit)
 - handler: getReactionUsersHandler in src/tools/reactions.ts
 - 内部で `MessageReaction.users.fetch({ limit })` を呼び user_id を REST 取得
 - レスポンスに count, me, users[{id, username, bot}] を含む
 - こちらも Gateway intent 不要
 
 3. tools.ts / app.ts / server.ts / toolList.ts に新ツールを登録。
 
 Tested
 ------
 - npm run build (tsc) success
 - 既存 add/remove/multiple_reactions ハンドラの挙動は無変更
 - read_messages の response shape は backwards-compatible (新フィールド追加のみ)
 
 Use case
 --------
 GO/NO_GO 系絵文字承認ループ、品質フィードバック収集、複数ユーザー reactor の
 監視 (チーム化対応) 等。Discord API のメッセージ取得仕様 (Get Channel Messages
 が reactions array を含む) を素直に MCP 越しに見せるだけ。
 
 Related
 -------
 upstream PR を後ほど投稿予定。')
 
 Show description for 22eb4c7
 
 [![MayumiKohei](https://avatars.githubusercontent.com/u/122164552?v=4&size=32)](https://github.com/MayumiKohei) [MayumiKohei](https://github.com/suavecito585/mcp-discord/commits?author=MayumiKohei)
 
 committedMay 7, 2026
 
 [22eb4c7](https://github.com/suavecito585/mcp-discord/commit/22eb4c71ae786951ab4b130d8a8f2f247780c8ac)
 
 Copy full SHA for 22eb4c7