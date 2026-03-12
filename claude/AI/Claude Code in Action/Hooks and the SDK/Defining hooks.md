

Open in Claude

Downloads

https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1773097175/queries.zip?response-content-disposition=attachment&Expires=1773283331&Signature=GrmtAhxcI667-C7S2W0E21eg97kwQObq9AMR2Xf3ATKdGiXQ2SgSV0svGjnbG0vYeiDKCqz7u4xigxUe3qlpscWMnatEcElQMAqbLqHi9xfDz1aGCwmgpYO8kSbDN87ys5BTQ18UnCSsKw3OPGSPjYE0Gk0Y5S-1dxH02OY7idYX~SchtRJJ3u2uJHkAJlfcKqvZYdWEMhWkvImdSNfFs-Gj3TiVccAzaXBwpI9eEtEte17vwOKdds754hEWxFKnGRpJMmQJ7vPkUV9kXRBdKduyUQoOF9Yl8CKoLcfHM1v2ZfWN96zoBW7sLzcu7IgQm25XIC6W~xZA~I0E512qkg__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ


https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1773097185/queries_COMPLETED.zip?response-content-disposition=attachment&Expires=1773283331&Signature=oTi4ml55eqloyqz4Ep0BqrFr7tSadoNCceJ7Bjlq-Gzj5sKHtrxcZfBOu1GcvtAnsDN4wNceJyCjSb-S91yGkARb2tTzzdAXfD~b1L-y~mzR2Lu2yZ5TWfxf-mXx12hRlhnUY3~ctse1kWOvuaYXVU0qj-axNVX6Ox-B7Sbv4KIGXWnL8gmCofN3n34~ctNYhZHetd4CA69qTTU9J8-WuyfS60rgFbXjT2WMs8x8ce~AGgoWKIh0j4YwuuMLZ~Gv87J~QkqKsN2HpDhVghGlwoCya0bF72rQBZRuQzjyivrYuWzprFTv4HgvHYEjpKa7mHMAPpfopM4z9KFsFN2bBA__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ


Hooks in Claude Code allow you to intercept and control tool calls before or after they execute. This gives you fine-grained control over what Claude can and cannot do in your development environment.

## Building a Hook

Creating a hook involves four main steps:

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1752618153%2F011_-_Defining_Hooks_05.1752618152864.png)

1. **Decide on a PreToolUse or PostToolUse hook** - PreToolUse hooks can prevent tool calls from executing, while PostToolUse hooks run after the tool has already been used
2. **Determine which type of tool calls you want to watch for** - You need to specify exactly which tools should trigger your hook
3. **Write a command that will receive the tool call** - This command gets JSON data about the proposed tool call via standard input
4. **If needed, command should provide feedback to Claude** - Your command's exit code tells Claude whether to allow or block the operation

## Available Tools

Claude Code provides several built-in tools that you can monitor with hooks:

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1752618153%2F011_-_Defining_Hooks_07.1752618153492.png)

To see exactly which tools are available in your current setup, you can ask Claude directly for a list. This is especially useful since the available tools can change when you add custom MCP servers.

## Tool Call Data Structure

When your hook command executes, Claude sends JSON data through standard input containing details about the proposed tool call:

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1752618154%2F011_-_Defining_Hooks_11.1752618154320.png)

```
{
  "session_id": "2d6a1e4d-6...",
  "transcript_path": "/Users/sg/...",
  "hook_event_name": "PreToolUse",
  "tool_name": "Read",
  "tool_input": {
    "file_path": "/code/queries/.env"
  }
}
```

Your command reads this JSON from standard input, parses it, and then decides whether to allow or block the operation based on the tool name and input parameters.

## Exit Codes and Control Flow

Your hook command communicates back to Claude through exit codes:

![](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1752618154%2F011_-_Defining_Hooks_16.1752618154725.png)

- **Exit Code 0** - Everything is fine, allow the tool call to proceed
- **Exit Code 2** - Block the tool call (PreToolUse hooks only)

When you exit with code 2 in a PreToolUse hook, any error messages you write to standard error will be sent to Claude as feedback, explaining why the operation was blocked.

## Example Use Case

A common use case is preventing Claude from reading sensitive files like `.env` files. Since both the `Read` and `Grep` tools can access file contents, you'd want to monitor both tool types and check if they're trying to access restricted file paths.

This approach gives you complete control over Claude's file system access while providing clear feedback about why certain operations are restricted.