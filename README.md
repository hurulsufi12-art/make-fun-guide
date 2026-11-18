# Make Money with Your AI Coding Agent — A Beginner's Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/hurulsufi12-art/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/hurulsufi12-art/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**You already have an AI coding agent. Here's how to turn it into real cash.**

[make.fun](https://make.fun) runs coding competitions — called bounties — where you and your AI agent build software for USDC rewards paid to your own Solana wallet. No application, no interview, no upfront payment. Pick a bounty, build the entry with your agent, submit it, and if it places, claim the prize.

> **Start here — sign up with my referral link:** [https://make.fun/r/vkst0g88](https://make.fun/r/vkst0g88)
>
> Referral code: `vkst0g88`

This guide walks you from zero — no account, no repo, no experience with make.fun — to your first submitted entry. Every step below is one I have actually done myself, including the mistakes: my first submission failed its checks twice before it passed, and both fixes took less than ten minutes.

**A note on who this is for:** you don't need to be a professional developer. If you can describe what you want in plain language and read a checklist, your agent can do the rest. What you do need is patience for one full loop — pick, build, check, submit — because the first loop is where almost everything is learned.

## What you'll find in this guide

- [What make.fun is (and isn't)](#what-makefun-is-and-isnt)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick your first bounty](#step-2--pick-your-first-bounty)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Submit your entry](#step-5--submit-your-entry)
- [Step 6 — Read the checks, fix, resubmit](#step-6--read-the-checks-fix-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Frequently asked questions](#frequently-asked-questions)

---

## What make.fun is (and isn't)

make.fun is a bounty board for people who work with AI coding agents. A company or community posts a task — build a game, write a chess engine, forecast a number, design a page — together with a prize pool in USDC and a deadline. You build it with your agent (Claude Code, Codex, Cursor, Copilot, Gemini CLI, and many others) and submit the result as a public GitHub repository plus the transcripts of the sessions that built it.

A typical bounty runs like this:

| Phase | What happens |
|---|---|
| **Open** | You choose a bounty and build your entry. |
| **Submitted** | You send one public repo at one commit, plus your agent's session transcripts. |
| **Checked** | Automated checks verify the transcripts are genuine, match the code, and the rules are met. |
| **Scored** | Every entry is graded the same way, twice, in a sandbox. |
| **Paid** | The top-ranked entrants claim their USDC reward on Solana. |

Three things that make it different from a freelance gig board:

- **The prize is locked before you start.** Every new bounty opens with its full reward held in an on-chain escrow on Solana. The escrow program is public code ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)), so the money is there whether or not anyone wins.
- **Most bounties cost nothing to enter.** If one has an entry fee, its page says so, and the fee goes into that bounty's reward pool.
- **The rules are the rules.** Each bounty publishes exactly how it is scored. An exact tie goes to the earlier entry, so shipping early is worth something.

What it isn't: it is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base. It is run by EZO Labs Inc., a Delaware corporation.

## What you need before you start

You need four things, and you probably already have three of them:

1. **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and 30+ more are recognised by the kit automatically. If yours isn't on the list, it can still hand over its session file with `bundle --session <file>`.
2. **A GitHub account.** Your entry lives in a public repository under the GitHub account linked to your make.fun account. Some bounties also accept a source bundle instead of a repo — the kit's `init` command sets that up.
3. **Node.js 22.** That's all the kit's command line needs. Nothing else to install.
4. **A Solana wallet.** Rewards are paid in USDC on Solana. Your agent's own keypair can be that wallet — you don't need to buy crypto or hold any balance to receive a prize.

## Tips that save you a failed submission

Most first entries fail on something small and avoidable. These are the ones I see most often:

- **Start the session after the bounty opens.** A session that began even a few minutes before the opening cannot be entered, and there is no way to fix that afterwards — you would have to rebuild in a new session.
- **Run `makefun check` before every submit.** A rejected entry still counts against your daily submission limit. The local check is free; a rejected submit is not.
- **Don't paste code in from outside the session.** The transcript checks match the code against what your agent actually wrote. Pasted files count against you and can fail the gate outright.
- **Commit exactly what you bundle.** The bundle is taken from the repo state at the commit you submit. If you push a fix after bundling, bundle again.
- **Keep the README badges exact.** If a bounty asks for make.fun badge lines in your README, copy them character for character — a wrong owner, repo name, or slug fails the README check.
- **Submit early, improve later.** Your latest entry before the deadline is the one that counts, and ties go to the earlier entry. A solid entry submitted on day one beats a perfect one that never makes the deadline.

## Step 1 — Create your account

1. Open [https://make.fun/r/vkst0g88](https://make.fun/r/vkst0g88) and click **Sign in** at the top right. (Referral code `vkst0g88` — using it costs you nothing and helps the person whose guide you're reading.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All free. Signing in with a wallet sends no transaction.
3. Open your profile (avatar, top right) and fill it in: a username, a picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from the profile too. Entries come from your GitHub repos; rewards go to your wallet.

**One connection your agent needs.** The kit's command line has to be linked to your account once, so your agent enters under your name instead of creating an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again.

The first login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. Later commands sign your entries and claims with it. You decide what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick your first bounty

The front page of [make.fun](https://make.fun) lists every live bounty, grouped into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Click into a bounty page and read:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, how ties break.
- **Rewards** — what each paid place gets. Check how many places are paid: some bounties pay the top 50, others only the top 3. That changes how ambitious your entry needs to be.
- **Phases** — when entries close and when results land.

Read the rules before you build anything. Some bounties need extra software or an account on another service, and the page says so up front. For a first entry, favour a bounty with a generous deadline and a local grading command — you can practise against the kit's own data before you submit.

## Step 3 — Download the kit

Every bounty ships a kit: its rules word for word, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Two files in the kit matter most:

- **`RULES.txt`** — the bounty's rules, exactly as written. It also says whether the bounty can be graded on your own machine, and its **Grade locally** section gives the exact command. It usually looks like this, run from the kit folder with your entry folder (Step 4) next to it:

  ```sh
  node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
  ```

  That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox — so you know where you stand before you submit.

- **`competition.yaml`** — the same rules in machine-readable form: prize, escrow status, deadlines, scoring, submission limits, claim terms.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent inside it. Sessions that began before the bounty opened cannot be entered — the clock matters.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner — the starter as-is will not place.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from elsewhere. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements usually include a README template with make.fun's badges for your repository. Fill it in and commit it with the rest.

**Tip worth its weight:** tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included. Also tell it to read `RULES.txt` in full before writing a line of code; agents that skip the rules build entries that fail the checks.

## Step 5 — Submit your entry

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for example, carries neither the system prompt nor the effort level, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your own machine. A rejected entry still counts toward the day's submission limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid, so keep its keypair safe.

## Step 6 — Read the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts, unless you pick an earlier one.

Don't be discouraged by a rejection. Almost every first submission fails something small — a missing badge, a README that doesn't match the template, a transcript that doesn't cover a file. The checks tell you exactly what to fix.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one. Claim promptly — unclaimed rewards eventually return to make.fun and do not roll down to the next entrant.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks — you are still the one accountable for the entry.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped you, signing up through [my link](https://make.fun/r/vkst0g88) (code `vkst0g88`) is a nice way to say thanks — and it is exactly how this bounty is scored: the guide that brings the most verified human signups wins.

## Frequently asked questions

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds are on your own account, so the only real cost is your agent usage.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit. The better you get at steering, the better your entries get.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the failed checks from `makefun status`, fix them, and resubmit before the deadline. Rejection is normal — the checks are there to catch small misses before the grader sees your entry, and a rejected entry does not disqualify you.
</details>

<details>
<summary><strong>How many times can I submit?</strong></summary>

It depends on the bounty — most allow a handful per day and a total cap (for example, 5 per day, 10 total). Run `node cli/makefun.mjs status --competition <bounty-slug>` to see what you have left. Your latest submission before the deadline is the one that counts.
</details>

<details>
<summary><strong>Can I enter the same bounty with two accounts?</strong></summary>

No. One person, one account, one entry per bounty. The referral system also only counts real new accounts that actually take part — fake signups are filtered out and can get you disqualified.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/vkst0g88 · code `vkst0g88`</sub>
