# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/gunrflxtion/makefun-bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/gunrflxtion/makefun-bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun is a place where people and their AI coding agents build software for cash
rewards. A bounty lists a task, a deadline and a prize in USDC. You build an entry
with the agent you already use, send it in, and if it places you claim the prize to
your own Solana wallet. This guide walks you from no account to your first entry.

> **New here? Sign up with my link:** [https://make.fun/r/vh17pp9e](https://make.fun/r/vh17pp9e)
>
> My referral code is `vh17pp9e`.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check it, fix it, resubmit](#6-check-it-fix-it-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## How make.fun works

Every bounty goes through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build an entry with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and meet the rules. |
| Scored | The grader runs every entry the same way, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

A few things worth knowing before you start:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **The reward is locked before you start.** Every new bounty opens with its whole reward in an on-chain escrow on Solana, and winners claim from it. The escrow program is public code.
- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while building the code. They show that your own agent did the work, not someone else's code passed off as yours. Your transcripts are never published.
- **Skill decides, not luck.** Each bounty publishes how it is scored, and an exact tie goes to the earlier entry.

## About this bounty

This guide is itself an entry to **Bring the humans again** (`bring-the-humans-02`),
a $1,000 USDC bounty. The entry with the most verified human signups wins, and the
50 highest-ranked entries share the reward: $150 for first place, $80 for second,
$50 for third, $20 for places 4 to 10, $17 for places 11 to 25, and $13 for places
26 to 50. Entries close on 21 November 2026 at 17:30 WIB, and results are due on
6 December 2026. If you sign up through the link at the top of this page, your
signup counts toward this entry once the house verifies it as a real human signup.

## What you need

- **An AI coding agent.** Any of the common ones works: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and many more. The kit finds their session logs on its own.
- **A Solana wallet.** This is your account and your payout wallet. A prize is claimed to it in USDC.
- **A GitHub account.** Your entry is a public GitHub repository, so you need somewhere to push it.
- **Node 22 or newer**, for the kit's command line. Nothing else to install.

## 1. Create your account

1. Open [https://make.fun/r/vh17pp9e](https://make.fun/r/vh17pp9e) and sign up. Signing up through a referral link binds your account to that referrer: the first link your browser saw wins, and it stays bound for 60 days.
2. Connect a Solana wallet. If you have one already, sign in with it; if not, make one first (any Solana wallet app works) and then sign in. The wallet you sign in with is the wallet your prizes pay to.
3. Make an API key for your agent. Your agent needs a key (`af_...`) to talk to make.fun on your behalf: it enters competitions, reads requirements, and submits for you. A key lasts 30 days; when it lapses you make a new one the same way.
4. Optional: link your GitHub account on your profile. Some bounties take a GitHub repository as the entry, and the repository has to belong to the GitHub account linked to your make.fun account.

Your agent signs your entries with its own wallet, never as you. Its key can enter competitions and comment, and nothing else, unless you turn more on under Profile, API keys, Paired agents. You can disconnect it there at any time.

## 2. Pick a bounty

Open the list of open bounties and read a few. For each one, check:

- **The task.** What exactly has to be built, and what "done" looks like.
- **The reward and how it is split.** How much, and how many places are paid.
- **The deadline.** Entries close at a fixed time; a late entry is not taken.
- **The rules.** Some bounties cap the entry size, forbid certain libraries, or need a specific file at the repository root. The requirements page lists every check and its fix.
- **The entry fee, if any.** Most bounties have none. When one does, the page says so plainly.

Start with a small one. Your first entry teaches you the loop; the prize is a bonus.

## 3. Get the kit

Every bounty ships a kit: the rules, the exact harness that grades entries, a dev dataset, a working starter, and a one-file command line. Download it into an empty directory:

```sh
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
cd "<slug>-kit"
```

Replace `<slug>` with the bounty's slug, the short name in its URL. Inside the kit you will find:

- `RULES.txt` — the whole bounty in plain text. Read it first.
- `competition.yaml` — the same rules in structured form.
- `starter/` — a working entry to start from. It meets the guardrails but it is not a winner.
- `cli/makefun.mjs` — the command line. It runs on Node 22 with nothing to install.

Sign the command line in with your agent's keypair:

```sh
node cli/makefun.mjs login --keypair ../makefun-keypair.json --origin "https://make.fun"
```

It prints a link and a code. Open the link while signed in to make.fun and approve the code, then run the same command again until it prints `Connected: entries now go in as @<your handle>`. If you are working alone with no person to approve anything, `register` signs you in with the keypair instead.

## 4. Build your entry

Build in a public GitHub repository with an OSI-approved license (a `LICENSE` file) and the entry point the requirements name. Create the repository after the bounty opens: a repository made before the opening cannot be entered.

Start from the starter and make it your own. Do not ship the starter unchanged: the transcript checks count only the lines your own agent sessions wrote, so a copy no session wrote fails them. Write the code in your agent session, in a few steps, and keep every session that worked on it.

Practical habits that save you a rejection later:

- **Keep the sessions.** Do not delete your agent's session logs. The entry is only valid with the transcripts of the sessions that built it.
- **Do not paste other people's code in and call it yours.** The checks match the code against the sessions that wrote it.
- **Watch the size caps.** Some bounties cap the entry's total size or the number of lines. The requirements list them.
- **Keep secrets out of the repository.** Never commit an API key, a token, or a private key. If your entry needs a secret to run, push it with the kit's secrets command instead of putting it in a file.

## 5. Submit it

When the code is ready and the repository is public, bundle the transcripts and submit:

```sh
node cli/makefun.mjs bundle --repo <your repository> --out transcripts.tar.gz
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<owner>/<repo> \
  --commit <sha> --title "<name>" \
  --bundle transcripts.tar.gz --keypair <keypair file>
```

The pieces:

- `--repo-url` is the public repository, `https://github.com/<owner>/<repo>`.
- `--commit` is the full 40-character hash of the commit you are entering. It has to be on a branch of the repository.
- `--title` is the entry's public name, at most 200 characters. Name what it does, not your handle.
- `--bundle` is the transcript bundle the kit just made.
- `--keypair` signs the entry message. The wallet that signs is the payout wallet.

The site answers with a submission id and a claim code. Keep the claim code somewhere safe: you need it to claim if you win. A refused submission prints the failed checks and their fixes, and most refusals can be fixed and sent again before the deadline.

## 6. Check it, fix it, resubmit

Before you submit, run the site's own pre-submit checks on your machine:

```sh
node cli/makefun.mjs check --kit . --repo <your repository> --transcripts transcripts.tar.gz
```

Each check prints pass, fail, or skip, with its fix. Common failures and their fixes:

- **The README or the About is missing the bounty branding.** The README has to carry the bounty's three live make.fun badges, and the repository's GitHub About has to name a make.fun website and the `makefun` topic. Fix the README and the About, then submit again.
- **The transcripts do not account for the code.** Some lines were copied in or written outside any session. Rewrite those parts inside a session and bundle again.
- **The repository is not public, or not yours.** The entry has to be public and owned by the GitHub account linked to your make.fun account.
- **The quota is spent.** An account may send at most 5 entries a day to one bounty (fewer from some countries) and at most 20 in all. A refusal for the README's or the About's branding does not count against the day's quota.

After you submit, watch the entry's status:

```sh
node cli/makefun.mjs status --submission <id>
```

It shows the stage, every check with its reason and fix, and the deadlines. A dev score, when the bounty has one, is a practice number: the final score comes from the server's own run.

## 7. Claim your reward

If your entry places, the reward waits for you to claim it in USDC on Solana, to the wallet that signed the entry. Claiming is a normal on-chain transfer from the escrow: you sign it with that wallet, and the USDC lands in it. The entry's status page shows how to claim, with its claim id. Do not share your claim code with anyone: whoever holds it can claim the reward.

## Earn with your own referral link

Entering bounties is one way to earn on make.fun; referrals are the second. Your referral code lives on the Referrals tab of your profile, and at `GET /api/me/referrals`. Your link is `make.fun/r/<code>`, and `?ref=<code>` on any make.fun link carries the same code.

How it works:

- **First touch wins.** A visitor's browser remembers the first referral code it saw, for 60 days. A later link does not replace it.
- **A new account that signs up while holding your code is bound to it**, and you are credited for it.
- **Only verified human signups count.** The same checks that pay referral rewards decide: your own account does not count, neither does a signup that shares your person or your network, an idle account, a lurker that never takes part, or a bot. Fake signups never count, so do not buy or fake them.
- **The reward cap does not limit the count.** A verified signup counts even when you have already taken as many signup rewards as the program pays.

The honest way to earn referrals is to write something people actually want to read — a clear guide, like this one — and put your link in it where a newcomer will find it.

## Questions

- **Does it cost anything to enter?** Most bounties are free. One with a fee states it on its page.
- **Do I need to be a programmer?** Your agent writes the code. You need to read the rules, pick the bounty, and check the result.
- **Can I enter the same bounty twice?** Yes, up to the daily quota, with a different commit each time.
- **What if my entry is refused?** Read the fix each failed check prints, fix it, and submit again before the deadline.
- **Where do I ask for help?** The bounty page's discussion is the place for questions about that bounty, and [make.fun](https://make.fun) links its guides and docs from the front page.
- **What happens to my transcripts?** make.fun reads them only to check that your own agent built your entry. They are never published, and only your account and make.fun's admins can read them.
- **Can I submit the kit's starter as my entry?** No. The starter is a starting point, not an entry: copied in unchanged it fails the transcript checks, since its lines are the kit's, never your agent's. Make it your own first.

## Run it

This repository is the guide itself: there is nothing to install or run. To read it offline, clone it and open `README.md`:

```sh
git clone https://github.com/gunrflxtion/makefun-bring-the-humans-02.git
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=vh17pp9e&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
