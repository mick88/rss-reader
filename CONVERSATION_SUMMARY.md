# RSS Reader - Conversation Summary (2026-01-11)

## Project Overview
TUI RSS reader built in Rust with AI-powered summaries and Raindrop.io bookmarking.

## Features Implemented
- Two-pane layout (article list + AI summary)
- Claude API integration for summaries
- Raindrop.io bookmarking to "News Links" collection
- OPML import
- SQLite caching
- Auto-mark articles as read after 2 seconds viewing
- Only show unread articles by default
- Delete article functionality (d key)
- Firefox cookie-based content fetching for paywalled sites
- Cross-platform releases (Linux x86_64/aarch64, macOS Intel/Apple Silicon)

## Key Files
- `src/app.rs` - Main application state, summary generation, Raindrop saving
- `src/services/content_fetcher.rs` - Firefox cookie extraction for paywalled content
- `src/services/raindrop.rs` - Raindrop.io client with collection support
- `src/db/repository.rs` - SQLite CRUD operations
- `src/tui/handler.rs` - Key bindings
- `.github/workflows/release.yml` - CI/CD for releases

## Recent Changes (This Session)
1. **Firefox cookie-based content fetching** - Reads cookies from `~/.mozilla/firefox/*/cookies.sqlite` to fetch full article content from paywalled sites (The Verge, Puck.news, etc.)

2. **Raindrop description population** - Bookmark descriptions now include first sentence of summary or article content

3. **Fixed foreign key crash** - Race condition when deleting article during summary generation

4. **Fixed html5ever warning spam** - Switched from `readability` to `html2text` crate for HTML extraction

5. **Added rusqlite error variant** - `src/error.rs` now handles direct rusqlite errors

## Configuration
Location: `~/.config/rss-reader/config.toml`
```toml
claude_api_key = "sk-ant-..."
raindrop_token = "..."
```

## Key Bindings
| Key | Action |
|-----|--------|
| j/k | Navigate articles |
| Enter | Generate summary |
| r | Refresh feeds |
| s | Toggle starred |
| m | Mark read/unread |
| o | Open in browser |
| S | Save to Raindrop.io |
| f | Cycle filter |
| d | Delete article |
| i | Import OPML |
| q | Quit |

## GitHub
- Repository: https://github.com/leolaporte/rss-reader
- Releases use GitHub Actions for cross-platform builds

## Fish Function
Run with `rss` command (defined in `~/Sync/dotfiles/cachyos/sway/fish/functions/rss.fish`)

## Potential Future Work
- Test Firefox cookie fetching with actual paywalled sites
- Add more feed sources
- Keyboard shortcuts help screen
- Feed management UI
