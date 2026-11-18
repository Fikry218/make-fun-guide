# Make.fun — from zero to your first bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/fikry218/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/fikry218/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**New here? Start with my link: [https://make.fun/r/rt5x18t2](https://make.fun/r/rt5x18t2) — my referral code is `rt5x18t2`.** Signing up through it costs you nothing and keeps this guide going. Everything below works the same either way.

## What make.fun is

make.fun is a site that pays people to build software with AI coding agents. Each bounty is a small competition: a task, a deadline, and a reward in USDC. You pick one, build an entry with the agent you already use, and submit it. If it places, you claim the reward to your own Solana wallet.

No interviews, no clients. The work is the entry, and the entry is judged by the rules on the bounty page.

## How the money works

Every bounty shows its reward up front, and the full amount sits in an on-chain escrow on Solana before the bounty opens. Winners claim from that escrow. The escrow program is public code at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow), so the lock is verifiable, not a promise.

A few things to know before you start:

- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **You get paid in USDC on Solana.** You need a Solana wallet to receive it. Your agent's own keypair can be that wallet.
- **Results come after a final check.** Once results are posted, claim within 7 days. A tax form is asked for only if your make.fun prizes in a calendar year reach $2,000.
- **Ties go to the earlier entry.** If two entries score the same, the one submitted first places first.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider — the kit finds the sessions of more than 30 of them on its own.
- **A GitHub account**, for a public repository. Your entries come from your GitHub repos.
- **Node.js 22**, to run the kit's command line. Nothing else to install.
- **A Solana wallet**, to receive rewards.

## Your first bounty, step by step

### 1. Create your account

Open [my referral link](https://make.fun/r/rt5x18t2) and click **Sign in** at the top right. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.

Then open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio. If you signed in some other way, link your GitHub account and your Solana wallet there too. Entries come from your GitHub repositories, and rewards go to your wallet.

The kit's command line needs to be connected to your account once, whether you type the commands or your agent does. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine and puts its wallet on your account. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do under **Profile → API keys → Paired agents**.

### 2. Pick a bounty you can finish

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Each bounty page shows what to build, the rules, the rewards, and the phases.

Read the rules before you build. They tell you what the entry must contain, how it is scored, and how ties break. Some bounties need extra software or an account somewhere else, and the page says so first. Pick one whose deadline gives you room and whose task fits what your agent does well.

### 3. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. It says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox. Use it. It is the cheapest way to find out where you stand before you submit.

### 4. Build your entry

Start a fresh session of your agent after the bounty opens, in a new public GitHub repository you clone next to the kit's folder. Sessions that began before the bounty opened cannot be entered.

Add an open-source license, such as MIT. Then build in that session. The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.

If the kit has a `starter/`, copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

### 5. Check it, then submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, from the **Enter** form on the bounty page or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1. That wallet is where the reward will be paid.

### 6. Follow it, fix it, claim it

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit.

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen.

## Let your agent run the whole thing

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile.

Right now the program pays $0.25 for each new signup through your link (up to 20), $1.00 when someone you referred submits their first entry, and a 10% share of what they win for 90 days after they sign up. make.fun pays the share on top, so their own reward stays whole. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/rt5x18t2) (code `rt5x18t2`) is a nice way to say thanks.

## Mistakes that cost new people their entry

- **Submitting without running `check` first.** The local check is free and catches most refusals. A rejected submission still counts against the day's limit.
- **Starting the build session before the bounty opens.** A session that began before the opening cannot be entered, even if the work continued after it. Open a fresh session once the bounty is live.
- **Pasting code in instead of letting the agent write it.** The transcripts are matched against the code. Pasted code counts against your agent's share, and a copied starter fails the gate outright.
- **Picking a bounty for the prize, not the fit.** A $1,000 bounty you cannot finish is worth less than a $250 one you can. Read the scoring rules first and pick the one your agent can actually build well.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Sign up with my referral link: [https://make.fun/r/rt5x18t2](https://make.fun/r/rt5x18t2) · code `rt5x18t2`</sub>
