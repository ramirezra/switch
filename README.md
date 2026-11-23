# EM-Studio Go project template

A starting point for a new event-modeled Go project: a dev container with Go 1.24, Node.js,
the GitHub CLI and Claude Code, plus a script that connects the project to an EM-Studio board.

## One-time setup on your laptop

Set these personal environment variables once. `devcontainer.json` copies them into every
container, so Claude and EM-Studio sign in by themselves. They never go into Git.

| Variable | Where to get it |
| --- | --- |
| `CLAUDE_CODE_OAUTH_TOKEN` | Run `claude setup-token` (valid for one year) |
| `EVENTMODELERS_TOKEN` | EM-Studio: Account → API Tokens |
| `EVENTMODELERS_ORGANIZATION_ID` | EM-Studio: the code after `/org/` in the browser address |

- **Windows (PowerShell):** `setx EVENTMODELERS_TOKEN "your-token"` (repeat for each variable)
- **Mac:** add `export EVENTMODELERS_TOKEN="your-token"` (and the others) to `~/.zshrc`

Quit and reopen VS Code afterwards. Podman users: set VS Code's Docker Path to `podman`.

## Start a new project from this template

1. Create the board in EM-Studio and copy its board ID.
2. On this repository's GitHub page, click **Use this template → Create a new repository**
   (owner: your organization, visibility: Private). Or, in a terminal:
   `gh repo create <org>/<new-name> --template <org>/em-studio-go-template --private --clone`
3. Clone the new repository in VS Code and run **Dev Containers: Reopen in Container**.
4. In the container terminal: `./scripts/setup-em-studio.sh <board-id>`
5. Review Source Control, commit and push.

## Joining an existing project

Clone it, reopen in the container, and run `./scripts/setup-em-studio.sh <board-id>` with the
project's board ID. This recreates your personal EM-Studio files, which are not stored in Git.

## Daily use

- Model on the board: `npx @eventmodelers/cli run --modeling`
- Build Planned slices into Go code: `npx @eventmodelers/cli run`
- Check the setup: `npx @eventmodelers/cli status`

## Maintaining the template

- Change the template, not each project: improvements here apply to new projects only.
- `scripts/setup-em-studio.sh` pins the EM-Studio CLI version (`EM_CLI_VERSION`); bump it
  deliberately after testing a new version.
- If your company forks the Go build kit, change `BUILD_KIT_URL` in the script.
