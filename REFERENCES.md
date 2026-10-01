# References

Curated catalog of skills from others that I draw from. Not vendored here; install straight from the source.

```bash
npx skills add <owner/repo>@<skill> --global -y   # one skill
npx skills add <owner/repo> --global -y           # whole repo
npx skills find <query>                           # search the registry
```

My own skills are in [README.md](README.md).

## Output ergonomics

| Skill | Install | Notes |
|---|---|---|
| i-have-adhd | `ayghri/i-have-adhd@i-have-adhd` (add `--agent '*'`) | Shapes output for a reader with ADHD |

## Core utilities (steipete/agent-scripts)

| Skill | Install |
|---|---|
| video-transcript-downloader | `steipete/agent-scripts@video-transcript-downloader` |
| brave-search | `steipete/agent-scripts@brave-search` |
| nano-banana-pro | `steipete/agent-scripts@nano-banana-pro` |
| openai-image-gen | `steipete/agent-scripts@openai-image-gen` |
| create-cli | `steipete/agent-scripts@create-cli` |
| instruments-profiling | `steipete/agent-scripts@instruments-profiling` |
| markdown-converter | `steipete/agent-scripts@markdown-converter` |
| native-app-performance | `steipete/agent-scripts@native-app-performance` |

## Web and cloud stacks

| Skill | Install | Notes |
|---|---|---|
| vercel-react-best-practices | `vercel-labs/agent-skills@vercel-react-best-practices` | Vercel Engineering |
| vercel-react-native-skills | `vercel-labs/agent-skills@vercel-react-native-skills` | Vercel Engineering |
| vercel-optimize | `vercel-labs/agent-skills@vercel-optimize` | Vercel Engineering |
| cloudflare | `cloudflare/skills@cloudflare` | Workers, Pages, KV/D1/R2, Agents SDK |
| workers-best-practices | `cloudflare/skills@workers-best-practices` | |
| wrangler | `cloudflare/skills@wrangler` | |

## Mobile and native

| Skill | Install | Notes |
|---|---|---|
| building-native-ui | `expo/skills@building-native-ui` | Expo, official |
| expo-api-routes | `expo/skills@expo-api-routes` | Expo, official |
| expo-cicd-workflows | `expo/skills@expo-cicd-workflows` | Expo, official |
| expo-deployment | `expo/skills@expo-deployment` | Expo, official |
| expo-dev-client | `expo/skills@expo-dev-client` | Expo, official |
| expo-tailwind-setup | `expo/skills@expo-tailwind-setup` | Expo, official |
| native-data-fetching | `expo/skills@native-data-fetching` | Expo, official |
| upgrading-expo | `expo/skills@upgrading-expo` | Expo, official |
| use-dom | `expo/skills@use-dom` | Expo, official |
| agent-device | `callstackincubator/agent-device@agent-device` | React Native device interaction (Callstack) |
| asc-* (iOS App Store Connect) | ships with the `asc` CLI (`brew install asc`) | Not installed via `npx skills`; the CLI registers them into `~/.agents/skills` and Claude only |

## Design and frontend polish

| Skill | Install |
|---|---|
| frontend-skill | `openai/skills@frontend-skill` |
| impeccable | `pbakaus/impeccable` |
| interface-design | `Dammyjay93/interface-design` |
| ui-skills | `ibelick/ui-skills` |

## Integrations and media

| Skill | Install |
|---|---|
| agent-browser | `vercel-labs/agent-browser@agent-browser` |
| agentmail | `agentmail-to/agentmail-skills@agentmail` |
| resend | `resend/resend-skills@resend` |
| remotion-best-practices | `remotion-dev/skills@remotion-best-practices` |

## Research and async coding workflows

| Skill | Install | Notes |
|---|---|---|
| mattpocock/skills (whole repo) | `mattpocock/skills` | `/grill-me`, `/grill-with-docs`, `/diagnose`, `/triage`, `/to-prd`, `/to-issues`, `/prd-to-plan`, `/request-refactor-plan`, `/improve-codebase-architecture`, `/qa`, `/handoff` |
| last30days | `mvanhorn/last30days-skill@last30days` | Research what people said about a topic in the last 30 days |
