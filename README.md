# Discordia

**Discord API library written in Lua for the Luvit runtime environment**

This is a lightweight branch of Discordia that provides a minimal Lua library.
- Gateway events are not automatically handled except for a partial `READY` handler
- Client events are raw gateway events using `payload.t` and `payload.d`
- REST API and WebSocket gateway methods are still available
- No automatic caching, manual management is required
- No container classes, raw tables should be used
- No voice features are provided

### Example

```lua
local discordia = require('discordia')
local client = discordia.Client()

client:on('READY', function(data)
	print('Logged in as '.. data.user.username)
end)

client:on('MESSAGE_CREATE', function(data)
	if data.content == '!ping' then
		local success, msg = client.api:createMessage(data.channel_id, {
			content = '!pong'
		})
		if success then
			p('Message sent:', msg)
		end
	end
end)

client:run('INSERT_TOKEN_HERE')
```
