---
prev: false
next: false
---

# Always Replying to Messages

It is sometimes necessary to always send messages as replies, especially for bots that are meant to be used in groups.
We usually do this by adding `reply_parameters` to the methods that send the message: `sendText`, `reply`, `sendPhoto`, `replyWithPhoto` and etc.
However, if you're doing this for every single message, it can get messy and boring.

This plugin sets the properties of `reply_parameters` for all `reply*` and `send*` methods that support it to make every message a reply to the message and chat that triggered it.

You can pass an options object with a `allowSendingWithoutReply` property to both `addReplyParam` and `autoQuote` functions, which will allow your bot to send messages even if the message being replied to does not exist anymore.

## Usage

### In a Specific Context

If you want all messages sent within a specific context (like a specific command), you can specifically apply the plugin to them:

::: code-group

```ts [TypeScript]
import { Bot } from "grammy";
import { addReplyParam } from "@roziscoding/grammy-autoquote";

const bot = new Bot("");

bot.command("demo", async (ctx) => {
  ctx.api.config.use(addReplyParam(ctx));
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.start();
```

```js [JavaScript]
const { Bot } = require("grammy");
const { addReplyParam } = require("@roziscoding/grammy-autoquote");

const bot = new Bot("");

bot.command("demo", async (ctx) => {
  ctx.api.config.use(addReplyParam(ctx));
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.start();
```

```ts [Deno]
import { Bot } from "https://deno.land/x/grammy/mod.ts";
import { addReplyParam } from "https://deno.land/x/grammy_autoquote/mod.ts";

const bot = new Bot("");

bot.command("demo", async (ctx) => {
  ctx.api.config.use(addReplyParam(ctx));
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.start();
```

:::

### In Every Context

If you want every sent message to reply the messages that triggered them, you can apply the plugin this way:

::: code-group

```ts [TypeScript]
import { Bot } from "grammy";
import { autoQuote } from "@roziscoding/grammy-autoquote";

const bot = new Bot("");

bot.use(autoQuote());

bot.command("demo", async (ctx) => {
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.command("hello", async (ctx) => {
  await ctx.reply("Hi there :)"); // this quotes the user's message, too
});

bot.start();
```

```js [JavaScript]
const { Bot } = require("grammy");
const { autoQuote } = require("@roziscoding/grammy-autoquote");

const bot = new Bot("");

bot.use(autoQuote());

bot.command("demo", async (ctx) => {
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.command("hello", async (ctx) => {
  await ctx.reply("Hi there :)"); // this quotes the user's message, too
});

bot.start();
```

```ts [Deno]
import { Bot } from "https://deno.land/x/grammy/mod.ts";
import { autoQuote } from "https://deno.land/x/grammy_autoquote/mod.ts";

const bot = new Bot("");

bot.use(autoQuote());

bot.command("demo", async (ctx) => {
  await ctx.reply("Demo command!"); // this is going to quote the user's message
});

bot.command("hello", async (ctx) => {
  await ctx.reply("Hi there :)"); // this quotes the user's message, too
});

bot.start();
```

:::

## Plugin Summary

- Name: Autoquote
- Source: <https://github.com/roziscoding/grammy-autoquote>
- API Reference: <https://deno.land/x/grammy_autoquote/mod.ts>
