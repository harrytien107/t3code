# Permission modes

Permission modes control when an agent needs your approval to act. Choose a mode in the message
composer; it applies to that thread.

New threads start in **Full access** unless you choose another mode before sending. A thread
created from another thread inherits its mode.

| Mode                  | Behavior                                                                              |
| --------------------- | ------------------------------------------------------------------------------------- |
| **Supervised**        | Requests approval for commands and file changes.                                      |
| **Auto-accept edits** | Approves file edits automatically; other actions can still require approval.          |
| **Auto**              | Uses the provider's automatic review to approve routine actions and ask about others. |
| **Full access**       | Allows commands and edits without approval prompts.                                   |

Approve or reject requests in the conversation to let the agent continue. Permission modes do
not prevent the agent from asking questions about the task.

## Provider differences

Providers enforce permissions differently. Some read-only actions can proceed in **Supervised**.
**Auto** uses automatic review on Codex, Claude, and Cursor; providers without an equivalent,
including OpenCode and Antigravity, fall back to asking.

For Grok, **Always allow this session** remembers the matching command or tool input. Other
actions still require approval.

Antigravity can still send native approval requests in **Full access**. It only offers remembered
approvals for actions that support them.

See the [provider guides](./install.md#providers) for setup and provider-specific limits.

Use **Full access** for work in a worktree or a sandbox you can throw away.

Use **Supervised** on a repository where an unwanted command is expensive, or the first time you
run an unfamiliar task.

**Auto-accept edits** suits refactors where the edits are the point and you only care about the
shell commands.

## Provider Behavior

Each provider maps these modes onto its own approval and sandbox settings. Codex, for example,
translates the mode into its approval policy and sandbox level, so **Supervised** runs the CLI
with prompting enabled and a restricted workspace while **Full access** disables both. Grok
threads do the same: **Supervised** starts Grok in ask mode even if your Grok CLI config is
set to always-approve, and **Full access** starts Grok with always-approve. Oh My Pi threads map
the modes onto omp's approval flags: **Supervised** passes `--approval-mode=always-ask`,
**Auto-accept edits** passes `--approval-mode=write`, **Auto** passes `--auto-approve`, and
**Full access** passes `--approval-mode=yolo`. The labels above
describe what you get; the exact per-provider translation is internal and may change.

Mobile offers the same four modes with the same labels and descriptions.
