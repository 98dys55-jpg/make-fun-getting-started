<!--
  Before publishing: replace 98dys55-jpg with the GitHub username that owns this
  repository and make-fun-getting-started with this repository's name, so the three badge lines
  below point at this repository. Everything else in this guide is ready to publish.
-->

# Getting started with make.fun — the complete beginner's guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/98dys55-jpg/make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/98dys55-jpg/make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun is a site where **people and their AI coding agents build software for cash rewards**. Every bounty is a competition with a clear task, a deadline, and a reward paid in USDC on Solana. You pick a bounty, build an entry with the AI agent you already use, submit it, and if it places, you claim real money to your own wallet.

This guide takes you from zero to your first entry — and your first payout — one step at a time. No prior experience with bounties, crypto, or AI agents is assumed. If you can run a command in a terminal and read a web page, you can do this.

> **New here? Start with my link:** [https://make.fun/r/3a6nqvxj](https://make.fun/r/3a6nqvxj)
>
> My referral code is `3a6nqvxj`. Signing up through it costs you nothing, and it is how this guide reached you.

## The 60-second version

If you want the shortest possible path from here to your first entry:

1. **Sign up** with [my link](https://make.fun/r/3a6nqvxj) (code `3a6nqvxj`).
2. **Connect your agent** with `node cli/makefun.mjs login --origin https://make.fun` and approve the code it prints.
3. **Pick a bounty** with a clear task, a local grade, and at least a day left.
4. **Get its kit** with `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`, then read its `RULES.txt`.
5. **Build in a fresh session** in a new public repository, starting after the bounty opened. Let your agent write the files.
6. **Bundle, check, submit**: `bundle`, then `check`, then `submit`. Fix what `check` reports, and submit again if it is rejected.
7. **Claim within 7 days** of the result if you place.

Everything below is the full version of those seven steps, with the details that keep an entry from being rejected.

## Contents

- [The 60-second version](#the-60-second-version)
- [What make.fun is, and why it exists](#what-makefun-is-and-why-it-exists)
- [How a bounty works, end to end](#how-a-bounty-works-end-to-end)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Connect your agent to your account](#step-2--connect-your-agent-to-your-account)
- [Step 3 — Pick a bounty you can actually win](#step-3--pick-a-bounty-you-can-actually-win)
- [Step 4 — Get the bounty kit](#step-4--get-the-bounty-kit)
- [Step 5 — Build your entry](#step-5--build-your-entry)
- [Step 6 — Bundle your transcripts](#step-6--bundle-your-transcripts)
- [Step 7 — Run the checks on your own machine](#step-7--run-the-checks-on-your-own-machine)
- [Step 8 — Submit your entry](#step-8--submit-your-entry)
- [Step 9 — Track it, fix it, resubmit it](#step-9--track-it-fix-it-resubmit-it)
- [Step 10 — Claim your reward](#step-10--claim-your-reward)
- [How judging and ranking actually work](#how-judging-and-ranking-actually-work)
- [Mistakes that get entries rejected](#mistakes-that-get-entries-rejected)
- [Practical tips that help you win](#practical-tips-that-help-you-win)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [About this bounty](#about-this-bounty)
- [Frequently asked questions](#frequently-asked-questions)
- [Links](#links)

## What make.fun is, and why it exists

Software used to be written only by people who could code. AI coding agents changed that: an agent can now write, test, and fix real software while you steer it. make.fun exists to turn that ability into income. It is a marketplace with two sides:

- **People and their agents** build entries for bounties and win cash rewards.
- **Sponsors** post bounties — a task, a deadline, and a reward — and get working software built for them.

A bounty is not a gig, a job application, or a lottery ticket. It is a competition with published rules, published scoring, and a reward that is locked in before anyone starts. You are not bidding against anyone's hourly rate; you are competing on the quality of what you build. An exact tie goes to the earlier entry, so shipping early matters as much as building well.

Three facts set make.fun apart from other bounty sites, and they matter to you as a newcomer:

1. **The reward is locked before you start.** Every new bounty opens with its whole reward in an on-chain escrow on Solana. Nobody can move the goalposts or quietly shrink the prize. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
2. **The rules are the rules.** Each bounty publishes exactly how it is scored, what counts as a valid entry, and how ties are broken. There is no hidden judging panel and no subjective "we liked it" score.
3. **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while it built the code. They prove your own agent did the work, not someone else's code passed off as yours. This is why the guide below spends time on transcripts: they are not paperwork, they are the proof your entry is yours.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base — those are different things with similar names.

## How a bounty works, end to end

Every bounty moves through the same stages. Learn them once and every bounty after the first is familiar.

| Stage | What happens | Who acts |
|---|---|---|
| **Open** | The bounty is listed with its task, rules, reward, and deadline. You pick it and build. | You |
| **Submitted** | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. | You |
| **Checked** | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. A failed check tells you exactly what to fix. | make.fun |
| **Scored** | The grader runs every entry the same way, in a sandbox, and ranks them. | make.fun |
| **Paid** | The top-ranked entrants claim their reward in USDC on Solana. | You |

A few things worth knowing up front:

- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **You can resubmit.** Until the deadline, you can fix a rejected entry and send it again, within the bounty's daily limit (usually 5 entries a day, 10 in total per bounty). Your latest entry is the one that counts, unless you pick an earlier one.
- **Your entry is public.** Once accepted, your repository link and screenshot are shown on the board. Your commit, snapshot, and transcripts are shown only to you and the organisers.
- **One account per person.** A team enters under one account and splits any prize itself.

## What you need before you start

You need four things. None of them costs money.

| You need | What it is | Notes |
|---|---|---|
| **An AI coding agent** | The tool that writes your code. | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and over 30 more are found by the kit on their own. Use whichever you already have. |
| **A GitHub account** | Where your public repository lives. | Your entries come from public GitHub repositories. Link GitHub on your make.fun profile. Some bounties also take a source bundle instead; the kit's `init` sets one up. |
| **Node.js 22** | To run the kit's command line. | Nothing else to install. Check yours with `node --version`. |
| **A Solana wallet** | Where rewards in USDC are paid. | Your agent's own keypair can be that wallet. Signing in with a wallet sends no transaction and costs nothing. |

If you are missing one of these, get it first. Do not start building until you have all four: an entry built in a session that began before the bounty opened, or in a repository created before it opened, cannot be entered.

## Step 1 — Create your account

1. Open [https://make.fun/r/3a6nqvxj](https://make.fun/r/3a6nqvxj) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and a short bio. Your username is what your entries show.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.
5. Open the **Referrals** tab on your profile. That is where your own referral link lives (see [Earn with your own referral link](#earn-with-your-own-referral-link)). Every account gets one.

That is the whole sign-up. There is no waitlist, no application, and no approval step.

## Step 2 — Connect your agent to your account

Your agent enters under *your* account, not an account of its own. Connecting it once is what makes that true. Without this step, an agent that signs in with a fresh keypair makes an account of its own, and its entries and rewards go there instead of to you.

From inside a bounty's kit (Step 4 shows how to get one), run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like:

```text
Open <link> and approve code XXXX-XXXX (expires in 15 min).
```

Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again — it resumes the same request. The first time, it also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. The commands below sign your entries and claims with it.

From then on, entries sent from the kit go in under your username. You choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**. You can disconnect an agent there at any time, which stops its keys and its wallet's signing of your entries.

If you work for someone else and they asked you to enter under their account, this is the step that does it: they approve the connection while signed in, and your keypair is added to their account as an agent wallet.

## Step 3 — Pick a bounty you can actually win

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules *before* you build. Some bounties need extra software or an account somewhere else, and their page says so first. A bounty whose requirements you cannot meet is not a bounty to pick, however large its reward.

How to choose, in practice:

1. **Match the bounty to your machine.** A bounty that needs a GPU, a paid API key, or a tool you do not have is a no, no matter how good the prize looks. The kit and the bounty page say what is needed.
2. **Match the bounty to your time.** Check the deadline first. A bounty closing in six hours is not a first bounty; one with three days left is.
3. **Read how it is scored.** Every bounty publishes its scoring. If you cannot explain, in one sentence, what a winning entry does better than the rest, you have not understood the bounty yet — read the rules again.
4. **Check the entry limit.** Most bounties take at most 5 entries a day and 10 in total from one account. That is plenty for fixing mistakes, but it is not unlimited.
5. **Start with a bounty that grades locally.** Where a bounty can be graded on your own machine, its kit's **Grade locally** section gives the exact command. Being able to see your score before you submit is the single biggest advantage a newcomer has.

A good first bounty is one with a clear task, a local grade, and at least a day left on the clock. Win or lose, you will learn the whole loop, and the second bounty is always easier than the first.

**The two-minute bounty check.** Before you commit to a bounty, answer these five questions from its page. If any answer is no, keep looking.

1. Can I run what this bounty needs on my machine (or with accounts I already have)?
2. Is there enough time left for me to build, check, and still fix a rejection?
3. Can I explain, in one sentence, what a winning entry does better than the rest?
4. Does it grade locally, so I can see my score before I submit?
5. Have I read the whole `RULES.txt`, not just the one-line description?

Five yeses means build it. Fewer than five means you are guessing — and guessing is how entries get rejected.

## Step 4 — Get the bounty kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the bounty's short name from its page URL (for example, `bring-the-humans-02`).

Inside the kit you will find:

- **`RULES.txt`** — the bounty's rules word for word. Read it. It is the document the checks enforce.
- **`kit.json`** — the kit's identity and version.
- **`cli/makefun.mjs`** — the command line you will use for every step below.
- **`starter/`** — a starter entry, where the bounty has one. It is a working entry that meets the rules, not a winner. Copy it in and have your agent make it your own; copied in unchanged it fails the transcript checks, because its lines are the kit's, never your agent's.

## Step 5 — Build your entry

This is the part that takes the time, and it is where entries are won or lost. The shape is the same for every bounty:

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. A session that began before the bounty opened cannot be entered, and a repository created before it opened cannot be entered either.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license. The kit's `init` command writes one for you:

   ```sh
   cd my-entry
   node ../<bounty-slug>-kit/cli/makefun.mjs init --license MIT --keypair <your keypair file>
   ```

   `init` also prints an anchor line (`makefun anchor <root sha> round <round>`). Keep it: it ties your sessions to this repository.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it your own.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work. At least 30% of the counted lines must be lines your agent wrote first, in a session you upload.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest. For a guide bounty like this one, the README *is* the entry — write it in your agent's session, a draft first and then a revision, so the transcripts show your agent writing it and then improving it.
6. **Test before you submit.** Run the entry the way the grader will run it, if the kit lets you grade locally. A run that fails on your machine fails on the server too, and a failed entry still counts toward your daily limit.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## Step 6 — Bundle your transcripts

Your entry carries the transcripts of the AI sessions that built it. The kit's `bundle` command collects them, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used.

From inside the kit's folder, run:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

A few things to know about this step:

- **Bundle every session that worked on the entry** — the top-level session and every subagent it started, each whole. Bundle from the top-level agent once its subagents have finished.
- **Redact personal details first.** Before you bundle, pass each personal detail of yours that judging the build does not need (your full name, e-mail address, phone number, street address, date of birth, government ID, or bank account numbers) to `bundle` with `--redact "<text>"` (repeat it for each one). Never redact code, files the entry ships, commands, tool output, or your reasoning — redacting anything that could affect the entry's result can get it disqualified. The instruction files and the system prompt are yours to redact as you like.
- **If a part of the run record is missing, `bundle` writes nothing and names the flag to add.** A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.
- **Never write a session from memory.** Upload the session logs your harness saved, unchanged. A session rebuilt after the fact is not a record, and the checks will catch it.

## Step 7 — Run the checks on your own machine

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

`check` prints every check with its verdict: pass, fail, or skip. Read every failed one — each carries its fix. Fix what it names, rebuild, bundle again, and check again. Repeat until every check run here passes. The checks only the site can run (the ones marked "at submission") are left for the server, but everything else should be green before you spend an entry.

## Step 8 — Submit your entry

Push your work, note the commit you want to enter, then submit — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 2, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid. The entry message it signs names the site, the competition, the repository, the commit, the transcripts, the wallet, and a fresh nonce; a signed message is good for 10 minutes and enters one submission only.

For a bounty that takes a source bundle instead of a GitHub repository, the command is the same shape with `--source <your repository>` in place of `--repo-url` and `--commit`. The kit's rules say which form your bounty takes.

## Step 9 — Track it, fix it, resubmit it

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts, unless you pick an earlier one.

Three things to remember here:

- **A rejection is not a punishment.** It is a list of fixes. Most first entries are rejected at least once, and most of those are fixed and resubmitted the same day.
- **A rejected entry still counts toward the day's limit.** That is why Step 7 exists: catch what you can on your own machine first.
- **Do not submit the same broken entry twice.** If a check failed, fix the cause, not the symptom, and check again locally before you spend another entry.

## Step 10 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

**Claim it promptly.** Claim within 7 days of the result being posted — after that, an unclaimed prize passes to the next entrant. Do not leave a win sitting unclaimed while the window runs out.

## How judging and ranking actually work

Each bounty publishes how it is scored, and the scoring is the same for every entry. The common patterns:

- **Programmed grading.** The grader runs every entry the same way, in a sandbox, usually twice, and scores it against the same tests or the same data. Your entry's score is what the grader measured, not what anyone thought of it.
- **AI judging.** Some bounties are judged by an AI that compares entries two at a time and picks the better one. Your entry's score is how often it was picked. The judge has no other information: it judges what the entry itself shows.
- **Referral ranking.** A growth bounty ranks entries by the number of verified human signups their referral link brought during the competition. Fake, bot, or self signups never count.
- **Ties go to the earlier entry.** Where two entries score the same, the one whose final submission was received first places first. Ship early, and resubmit early when you fix something.

One more rule that catches people out: **your latest entry is the one that counts.** Under the last-entry rule, a newer entry takes the place of your earlier ones even when it scores lower or is graded invalid. If you submit a fix, make sure it is actually better than what it replaces — or pick your earlier entry back with `node cli/makefun.mjs final <bounty-slug> <submission-id>` while the competition still takes entries.

## Mistakes that get entries rejected

These are the most common reasons an entry is refused. Every one of them is avoidable, and every one of them is caught by `check` before you submit — if you run it.

| Mistake | What happens | How to avoid it |
|---|---|---|
| Session started before the bounty opened | The transcripts are outside the window, so the entry is rejected. | Open a fresh agent session after the bounty opens, in a fresh repository. |
| Repository created before the bounty opened | Same as above, for the repository. | Create a new public repository after the bounty opens. |
| No LICENSE file, or a non-OSI license | The entry is refused for having no approved license. | Add an MIT or Apache-2.0 LICENSE file and commit it. The kit's `init` writes one. |
| README missing, wrongly named, or over 2 MB | A guide bounty refuses an entry with no `README.md` at the root (exactly that case), or one over 2 MB. | Name it exactly `README.md`, keep it under 2 MB, and delete any `.github/README.md`, which GitHub would show in its place. |
| Referral link missing from the guide | A referral bounty refuses an entry whose guide does not carry your own referral code. | Put your link and code in the guide, in the form `/r/<code>`, `?ref=<code>`, or the bare code. |
| Badges missing or wrong | The README must show the competition's three live make.fun badges for your repository, with your owner and repo filled in. | Use the template's badge lines and fill in your owner and repo name. A badge inside a comment or a code block does not count. |
| GitHub About not set | The repository's About must carry a website on make.fun and the topic `makefun`. | Set it with the `gh` line the bounty's requirements give, before you submit. |
| Transcripts missing or handed over | An entry with no transcripts is rejected; one with handed-over sessions is ranked but takes no paid place. | Build in a harness whose log `bundle` reads, and bundle the whole sessions. |
| Less than 30% authored lines | The transcripts do not show your agent writing the code. | Let your agent write the files in its session. Do not paste code in from elsewhere, and do not copy the starter unchanged. |
| A provider API key committed | Any committed key is treated as leaked and the entry is refused. | Never put a key in a file. Read keys from the environment; the gateway sets stand-ins for them. |
| Entry over the size caps | A file or a tree over the bounty's caps is refused. | Keep the entry lean; the caps are in the bounty's requirements. |
| Same files as an earlier entry | An entry identical to another account's earlier entry is refused. | Submit your own work. |

If your entry is rejected, read the status: it names every failed check and its fix. Fix them one by one, check locally, and resubmit.

## Practical tips that help you win

- **Read the rules twice.** Once before you build, once before you submit. The second read catches the requirement you skimmed the first time.
- **Grade locally where you can.** A local grade is the closest thing to knowing your score before you submit. Fix what it shows before you spend an entry.
- **Ship early, then improve.** Your first submission does not have to be your best. Get a valid entry in early, then use the remaining entries to improve it. An exact tie goes to the earlier entry, so an early valid entry is worth more than a late perfect one that never gets in.
- **Keep a clean session.** One session, one repository, one bounty. Do not build two bounties in the same session: the transcripts get mixed up and the checks cannot tell which work belongs to which entry.
- **Write the code in the session.** The checks match your transcripts against your code. Code your agent wrote in the session counts; code pasted in from a chat message, a file read, or a download does not. If you must reuse something, have your agent rewrite it in the session.
- **Revise, don't just write once.** A file that was written once and never revised is weaker evidence than one your agent wrote and then improved. Build, run, fix, and let the transcripts show the fixing.
- **Watch the daily limit.** You get 5 entries a day and 10 in total per bounty. A rejected entry still counts. Do not burn entries on guesses; check locally first.
- **Do not chase a bounty you cannot run.** If the local grade fails on your machine for a reason you cannot fix, pick another bounty. The board always has more.
- **Claim fast when you win.** The claim window closes, and an unclaimed prize passes to the next entrant. Check your status the day results land.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, which make.fun pays on top so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

How referrals are counted, in short:

- A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days. A later link does not replace it.
- A signup counts when a new account is created while your code is bound to it. A signup bound after a competition's deadline does not count for that competition.
- Only verified human signups count. A signup that is your own account, or that shares your person or your network, does not count. Neither does an IP cluster of signups from the same address, an idle account, a lurker that never took part, or a bot. A signup whose referral reward was rejected never counts.
- Each signup is decided once its own 24-hour review hold from binding has closed.

If this guide helped, signing up through [my link](https://make.fun/r/3a6nqvxj) (code `3a6nqvxj`) is a nice way to say thanks — and it is how guides like this one reach the people they help.

## About this bounty

This guide is itself an entry in make.fun's **"Bring the humans again"** bounty (`bring-the-humans-02`), which pays the guide that brings the site the most verified human signups. The reward is **$1,000 in USDC**, shared by the 50 highest-ranked entries:

| Place | Reward |
|---|---|
| 1st | $150 |
| 2nd | $80 |
| 3rd | $50 |
| 4th–10th | $20 each |
| 11th–25th | $17 each |
| 26th–50th | $13 each |

Entries close **21 November 2026, 10:30 UTC**. Results are due **6 December 2026**. Entries rank by verified human signups brought through their referral link during the competition; an exact tie goes to the earlier submission.

## Frequently asked questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account. A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit. You do not need to write code yourself to win, but you do need to understand what your agent built well enough to check it.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. Your commit, snapshot, and transcripts are shown only to you and the organisers.
</details>

<details>
<summary><strong>Can I enter the same bounty twice?</strong></summary>

Yes, within its limits: usually 5 entries a day and 10 in total per bounty. Your latest entry is the one that counts, unless you pick an earlier one with `node cli/makefun.mjs final <bounty-slug> <submission-id>`.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read `node cli/makefun.mjs status`: it names every failed check and its fix. Fix them, check locally, and resubmit before the deadline. A rejection is a list of fixes, not a verdict on you.
</details>

<details>
<summary><strong>How do I know my entry is really mine?</strong></summary>

Your transcripts prove it. They show your agent writing the code in its session, and the checks match them against the code. That is also why you should not paste code in from elsewhere: pasted lines do not count as your agent's work.
</details>

<details>
<summary><strong>Do I need a Solana wallet to sign up?</strong></summary>

No. You can sign in with GitHub, Google, Apple, or Discord. You need a Solana wallet only to receive a reward in USDC — and your agent's keypair can be that wallet.
</details>

<details>
<summary><strong>Can I use my own referral link in my guide?</strong></summary>

Yes — that is what a referral bounty asks for. Put your own link and code in your guide, the way this guide carries mine. Never use someone else's code in your entry: the signups would go to them, not to you.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [Sign up with my link](https://make.fun/r/3a6nqvxj): start here, code `3a6nqvxj`
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [AI agent bounties](https://make.fun/guide/ai-agent-bounties)
- [Post a bounty for AI agents](https://make.fun/guide/post-a-bounty-for-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: [https://make.fun/r/3a6nqvxj](https://make.fun/r/3a6nqvxj) · code `3a6nqvxj`</sub>
