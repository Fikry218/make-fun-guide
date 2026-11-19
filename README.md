# Make.fun — from zero to your first bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/fikry218/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/fikry218/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**New here? Start with my link: [https://make.fun/r/rt5x18t2](https://make.fun/r/rt5x18t2) — my referral code is `rt5x18t2`.** Signing up through it costs you nothing and keeps this guide going. Everything below works the same either way.

## Contents

- [What make.fun is](#what-makefun-is)
- [How the money works](#how-the-money-works)
- [What you need](#what-you-need)
- [Your first bounty, step by step](#your-first-bounty-step-by-step)
- [Let your agent run the whole thing](#let-your-agent-run-the-whole-thing)
- [Referrals: a second way to earn](#referrals-a-second-way-to-earn)
- [Mistakes that cost new people their entry](#mistakes-that-cost-new-people-their-entry)
- [Questions](#questions)
- [Links](#links)

## What make.fun is

make.fun is a site that pays people to build software with AI coding agents. Each bounty is a small competition: a task, a deadline, and a reward in USDC. You pick one, build an entry with the agent you already use, and submit it. If it places, you claim the reward to your own Solana wallet.

No interviews, no clients. The work is the entry, and the entry is judged by the rules on the bounty page.

A bounty is not a job ad. The page for each one spells out the task, the grading, the tie-break, and what every paid place wins — read that page before you write a line of code.

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

Your first half hour, in short: sign up, link GitHub and your wallet, connect the kit with `login`, and read the rules of one bounty that closes in a few days. You are ready to build after that — everything else in this guide you learn by doing it once.

### 2. Pick a bounty you can finish

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Each bounty page shows what to build, the rules, the rewards, and the phases.

Read the rules before you build. They tell you what the entry must contain, how it is scored, and how ties break. Some bounties need extra software or an account somewhere else, and the page says so first. Pick with your head, not your excitement:

- **Start with a task you understand in one reading.** If you cannot explain what a winning entry looks like, your agent will not be able to build one either.
- **Check the deadline against your time.** A bounty closing in six hours is not a first bounty.
- **Check how many places are paid.** A $1,000 bounty paying 50 places is a friendlier first target than a $1,000 bounty paying one.
- **Look at the scoring, not just the prize.** A bounty scored by an AI judge rewards polish and presentation; one scored by a test suite rewards exactness. Pick the kind of work your agent is good at.

Deadlines on the bounty page are in UTC, so convert them to your own timezone before you plan. A bounty closing at 08:00 UTC closes at 15:00 in Jakarta.

### 3. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it — it is the only document that decides whether your entry counts. It says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox. Use it. It is the cheapest way to find out where you stand before you submit.

### 4. Build your entry

Start a fresh session of your agent after the bounty opens, in a new public GitHub repository you clone next to the kit's folder. Sessions that began before the bounty opened cannot be entered.

Add an open-source license, such as MIT. Then build in that session. The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.

If the kit has a `starter/`, copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included. And paste the scoring section of the bounty's `RULES.txt` into your agent's first prompt, so it builds toward the thing that is actually measured instead of toward what looks impressive.

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

### 6. Follow it and fix it

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit. Your latest entry is the one that counts, unless you pick an earlier one.

Two things about the board that trip up newcomers: early scores are provisional, computed from a small number of matches, and they move a lot as more entries arrive. And an exact tie goes to the earlier entry, so there is no reason to leave your submission to the last hour.

### 7. Claim your USDC

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. Claim it promptly: the claim window is limited, and an unclaimed prize can pass to the next entry in line. A tax form is asked for only where US law requires one — a W-9 for a US person, a W-8BEN for anyone else — and only once your prizes from make.fun in a calendar year reach the $2,000 reporting threshold.

## Let your agent run the whole thing

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks. An agent left alone can choose a bounty you would not have chosen, or burn its whole budget on a dead end.

## Referrals: a second way to earn

Winning is not the only way make.fun pays. Every account gets a referral link, `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile, and you claim referral rewards there too.

You earn:

- **$0.25 USDC** when an account you referred signs up, for your first 20 signups.
- **$1.00 USDC** when an account you referred first wins a reward.
- **10% of what they win** for 90 days after they sign up.

That 10% is paid by make.fun on top — the person you referred keeps their whole reward. The small numbers add up if you keep sharing: twenty signups at $0.25 comes to $5.00, and one referred win adds $1.00 plus 10% of their prize on top of it.

Two details worth knowing. First, a referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days — a later link does not replace it. Second, only real people count: the same checks that pay referral rewards decide which signups count, so your own account, signups that share your network, idle accounts that never take part, and bots never pay out. Each reward is reviewed for at least a day before you can claim it, and it settles on Solana once approved.

If this guide helped you, signing up through [my link](https://make.fun/r/rt5x18t2) — code `rt5x18t2` — is a good way to say thanks, and it costs you nothing. The link again, plain: https://make.fun/r/rt5x18t2

## Mistakes that cost new people their entry

- **Submitting without running `check` first.** The local check is free and catches most refusals. A rejected submission still counts against the day's limit.
- **Starting the build session before the bounty opens.** A session that began before the opening cannot be entered, even if the work continued after it. Open a fresh session once the bounty is live.
- **Pasting code in instead of letting the agent write it.** The transcripts are matched against the code. Pasted code counts against your agent's share, and a copied starter fails the gate outright.
- **Picking a bounty for the prize, not the fit.** A $1,000 bounty you cannot finish is worth less than a $250 one you can. Read the scoring rules first and pick the one your agent can actually build well.
- **Forgetting the license.** An entry without an OSI-approved license is refused. MIT takes a minute to add, and a missing license is one of the silliest reasons to lose an entry.
- **Leaving the submission to the last hour.** Ties go to the earlier entry, and a last-minute rejection leaves no time to fix and resubmit.

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

<details>
<summary><strong>Can I enter as a team?</strong></summary>

One account per person. A team enters under one account and splits any prize itself.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Its status names every failed check and its fix. Fix them and submit again before the deadline — that is what the resubmission limit is for.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Sign up with my referral link: [https://make.fun/r/rt5x18t2](https://make.fun/r/rt5x18t2) · code `rt5x18t2`</sub>
