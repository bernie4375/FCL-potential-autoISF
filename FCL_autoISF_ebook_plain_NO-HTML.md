**The Practical Guide to**

# Full Closed Loop

\* \* \*

*And a Comprehensive Exploration of autoISF*

**Authored by Bernd Herpichboehm, PhD**

*Restructured and edited for clarity*

⁂

**Author**

**Bernd Herpichboehm, PhD**\*

This edition used AI to restructure and edit Bernie's original e-book for improved clarity.\
The original materials are available at:

`github.com/Bernie4375/FCL`

> **Important Note:** This edition may not be thoroughly reviewed or updated by Bernie or other key authors of original autoISF material. Use of this edition is at your own risk.
>
> Please cross-check any important information against the original material, and be sure to alert the community or original authors of anything that may require correction.

To contact Bernie or to access a wealth of additional resources and information,\
please visit the Full-Closed-Looping community Discord channel:

`discord.gg/EYxzq7GMX`

---

\* PhD in Technical Chemistry. Focus of research: Calculating permanently disturbed and re-establishing equilibria in chemical reactors.

Having lived with T1D for decades, trying to understand what's going on in my little "reactor" (my stomach and body cells) is second nature, though it remains a struggle 🙂 …

# Table of Contents

The book is organized in **seven Parts** that map the journey from "should I do this?" through setup, day-to-day operation, and long-term monitoring. The Parts are cumulative — each assumes you've done the work of the ones before it.

### Front Matter

- Disclaimer · Please Read This First
- Preface · How to Use This Book

### Part I — Getting Oriented

*What this is, whether it's for you, and what the journey looks like.*

- Introduction · What Is autoISF Full Closed Loop?
- Beginner's Roadmap · The Journey to Full Closed Loop

### Part II — Foundations

*What must be true before you start, and how the algorithm actually works.*

- Chapter 1 · Prerequisites for Full Closed Loop
- Chapter 2 · How autoISF Works

### Part III — Core Setup

*The multi-week project at the heart of the book — widening safety limits, installing the new guardrails, and tuning ISF weights to your meals.*

- Chapter 3 · General FCL Settings
- Chapter 4 · Meals: Setting Your ISF Weights

### Part IV — Day-to-Day Operations

*Nudging the loop when it needs nudging — snacks, exercise, sick days, and everything else that isn't a normal meal.*

- Chapter 5 · Modulating Loop Aggressiveness
- Chapter 6 · Exercise and Activity

### Part V — Alternative Modes

*Gentler paths when full autoISF FCL isn't the right fit — hybrid with Meal Announcement, simpler FCL via AAPS Automations, and the broader landscape.*

- Chapter 7 · Advanced HCL with Meal Announcement
- Chapter 8 · Other Avenues to Full Closed Loop

### Part VI — Monitoring & Troubleshooting

*Keeping the loop healthy once it's running, and fixing it when something goes wrong.*

- Chapter 9 · Performance Monitoring
- Chapter 10 · Troubleshooting

### Part VII — Tools

*Optional but powerful: the Emulator for replaying and analyzing your loop's decisions.*

- Chapter 11 · The Emulator on Your PC
- Chapter 12 · The Emulator on Your Phone

### Back Matter

- Final Remark
- Appendix A · Glossary
- Appendix B · Case Studies Index

# Disclaimer · Please Read This First
**This book is not medical advice.**

The authors are people living with Type 1 diabetes (or parents of children with T1D). We are not medical professionals. What you will read is our limited understanding, based on personal experience, shared openly to contribute to a growing body of community knowledge.

autoISF is an **early-stage development tool**. It is not a medical product. Good safety features exist, but they only work as well as the person using them understands them. The user interface was not built to protect people who stray from the intended ways of using it.

If you choose to try any of what follows, you do so entirely at your own risk. Anything you conclude or implement from this book is your responsibility.

## Ground rules if you decide to proceed

1. **Never copy another person's settings.** Your body is not theirs. What works for someone else can be dangerous for you. Investigate, test, and adjust based on *your* data.
2. **Do not "learn by doing" with dangerous tools.** Pressing buttons without understanding them, with a DIY closed-loop insulin system, is a serious risk.
3. **Start disconnected.** In your early testing phase, run the system as a dummy — not attached to your body — in parallel with your current glucose management, until you understand its behavior.
4. **Stay connected to the community.** Share experiences. The only way this work improves is through users who keep talking to each other and to the developers.

# Preface · How to Use This Book
## Who this book is for

This book is for people with Type 1 diabetes who already run a **well-tuned hybrid closed loop (HCL)** and want to explore going fully hands-off — letting the algorithm manage meals without any bolus, carb entry, or meal announcement from the user.

It was written for users of **AAPS** (AndroidAPS) with the **autoISF** development variant. Most of the content applies equally to users of **Trio** and **iAPS** (the iPhone-based oref variants), with some caveats noted where those systems lack certain features.

If you are not yet comfortably running a hybrid closed loop, or if you are still using Autotune or dynamicISF to paper over underlying profile problems, **please pause here**. Chapter 1 explains why that foundation matters so much. Without it, the rest of this book will not help you.

## How the book is organized

The chapters follow the order you should work through them.

- **Part I — Getting Oriented** explains what autoISF Full Closed Loop is, how it differs from a hybrid loop, and whether it is a realistic goal for you.
- **Part II — Foundations** covers what must be true about your current system before you begin (Chapter 1), and a mental model of how autoISF actually works (Chapter 2, later).
- **Part III — Core Setup** walks through the settings you will change in AAPS Preferences (Chapter 3) and the heart of the project: tuning your ISF weights to your meal spectrum (Chapter 4).
- **Part IV — Day-to-Day Operations** shows how to nudge the loop when it needs nudging, and how to handle exercise.
- **Part V — Alternative Modes** describes partial or less-intensive paths to FCL if you cannot or do not want to commit to the full project.
- **Part VI — Monitoring & Troubleshooting** covers what to watch and how to diagnose problems.
- **Part VII — Tools** explains the Emulator, an optional but powerful way to replay and analyze your loop's decisions.

## A note on the writing

Throughout the book, you will see callout boxes:

> ⚠️ **Warning** — A safety issue you must not skip.

> 💡 **Tip** — A practical shortcut or lesson learned the hard way.

> 📖 **Background** — An aside for readers who want the reasoning behind a recommendation. Safe to skip on first reading.

> 🧭 **Example** — The author's personal numbers, given for illustration. Do not copy them.

When a section references another part of the book, it will say "(see Chapter X)" or "(see §X.Y)". Cross-references are there to help you circle back; you are not expected to jump around on first reading.

# Introduction · What Is autoISF Full Closed Loop?
## From hybrid to full closed loop

In a **hybrid closed loop (HCL)**, the loop manages your basal insulin and delivers small correction boluses (SMBs) between meals, but *you* still bolus for meals. You tell the system you are about to eat; it does the rest.

In a **full closed loop (FCL)**, you do nothing at mealtime. No bolus, no carb entry, no announcement. The loop watches your blood glucose, notices when it starts to rise, and delivers insulin on its own.

The attraction is obvious: for most people with T1D, meal management is the single biggest daily burden. Eliminating it — cleanly, safely, and with good time-in-range — is the prize.

## Two approaches to FCL

The AAPS ecosystem now offers **two** ways to run a full closed loop:

1. **FCL with Automations (AAPS Master).** Available since autumn 2023. Simpler to set up. Uses personalized Automations to boost insulin delivery when a rise is detected. Covered in Chapter 8 (Other Avenues).
2. **FCL with autoISF.** The subject of this book. More sophisticated, more work to set up, capable of higher time-in-range and more daily "freedom" from intervention.

A clinical study of 16 AAPS users running the simpler Automations-based FCL showed an average of roughly 80% time-in-range without much tuning effort. That is a respectable outcome and a reasonable starting point if autoISF feels overwhelming.

autoISF aims higher — but it asks substantially more of the user up front.

## Is autoISF FCL for you?

This is worth a moment of honest self-assessment.

**autoISF FCL is probably a good fit if:**

- You have a well-tuned hybrid closed loop already — your profile ISFs, basal, and IC are experimentally correct, not "covered up" by Autotune or dynamicISF.
- You use Lyumjev or Fiasp (or, with caveats, Apidra).
- You use a Dexcom G6 or another CGM with reliably smooth values.
- You have several weeks of "free head" to invest in set-up.
- You enjoy reading, analyzing, and iterating on your own data.
- You are comfortable with the idea that some meals will not be perfect, and you are not chasing an HbA1c under 5.5%.

**autoISF FCL is probably not for you if:**

- Your hybrid loop is held together by many custom Automations or "tricks."
- You use an insulin slower than Fiasp.
- Your CGM is jumpy or you have unreliable Bluetooth connectivity.
- You are chasing very tight time-in-range (time above 140 mg/dL < 10%) — that level of control generally still requires hybrid looping with meticulous pre-boluses, and often low-carb diet and/or a GLP-1 co-medication.
- You are looking for something you can set up in a weekend and then forget.
- You prefer to proceed mostly by trial and error.

> 📖 **A reality check about industry "FCL" claims**
>
> You will see headlines about commercial systems achieving "full closed loop" results. Read the fine print. Most of those studies enroll patients with HbA1c in the 7–9% range and simply show that the commercial FCL is "no worse" than the patient's previous HCL. That is a meaningful advance for that population. It is not what this book is about. DIY FCL plays in a different league — it demands more from you, and it can deliver more.

## A different goal, a different mindset

Going into this project, please internalize this idea:

> **With 18 tuneable parameters, you can always "trick" your loop into handling one meal beautifully. But settings that handle *one* meal well are not the same as settings that handle *all* your meals well.**

Every chapter that follows is in service of the second goal. The author's experience is that it is entirely possible to find a single set of settings that gets you through your normal meal spectrum with good time-in-range. It just takes discipline to get there.

## If autoISF is too much right now

Several gentler on-ramps exist:

- **AAPS Master with FCL Automations** — see Chapter 8.
- **Meal Announcement mode** — keep giving a small pre-bolus, but otherwise let autoISF do the work. See Chapter 7.
- **Other dev variants** — Boost, AIMI, EatingNow, Tsunami. Each trades off differently. Briefly surveyed in Chapter 8.

There is no shame in picking a simpler path. The best loop is the one you can actually run.

## A note for iPhone users (Trio and iAPS)

autoISF has been ported into rapidly evolving development branches of Trio and iAPS for iPhone. The algorithm is the same, but Trio and iAPS users are at some disadvantage for FCL because:

- They lack Automations (Trio's "Shortcuts" have limited options).
- There is no e-book variant written specifically for their systems.
- Many users did not go through the AAPS "Objectives" tutorial sequence, and may not have the solid vanilla HCL starting point this book assumes.

For Trio users, general documentation is still being written. If you are a Trio user, the best plan is to get your HCL rock-solid first — by the time you are ready for FCL, there will probably be more Trio-specific material.

iOS Loop users: there is no comparable FCL option, because the iOS Loop algorithm depends heavily on carb inputs.

## Where to find the software

- **autoISF quick guide and ongoing development:** https://github.com/ga-zelle/autoISF
- **AAPS build with autoISF:** https://github.com/T-o-b-i-a-s/AndroidAPS/ (use the highest available version)
- **Trio with autoISF (TAI):** https://github.com/mountrcg/Tai
- **iAPS with autoISF:** https://github.com/mountrcg/iAPS
- **Discord community:** https://discord.gg/tamvhh57Xs

Always use the most recent branch compatible with your AAPS version. Note that the newest autoISF sometimes lags the newest AAPS Master by a few weeks; if you are migrating, read the current Discord threads before upgrading.

# Beginner's Roadmap · The Journey to Full Closed Loop
This chapter gives you the **whole journey in one view** before you start digging into the details. Read it once, come back to it as a checkpoint, and use it to decide where you are in the project.

## The big picture: four phases

```
Phase 1 — Make sure you're ready     (weeks -2 to 0)
Phase 2 — Configure safety settings  (week 1)
Phase 3 — Tune ISF weights to meals  (weeks 2–6)
Phase 4 — Handle exceptions          (weeks 6+)
```

**Total realistic timeline: 4–8 weeks of actively working on it, on top of your normal diabetes management.** Some people take longer. Nobody does it overnight.

## Phase 1 — Make sure you're ready (Chapter 1)

Before you touch a single autoISF setting, confirm all of the following are true:

- ☐ Your hybrid closed loop is tuned and performing satisfactorily.
- ☐ Your profile ISFs, basal, and IC are experimentally correct (not derived from Autotune).
- ☐ You are not relying on dynamicISF to cover up an incorrect profile.
- ☐ You use Lyumjev or Fiasp.
- ☐ Your CGM values are smooth and reliable (ideally Dexcom G6, overlapped).
- ☐ Your pump/cannula/pod setup delivers reliably, without frequent occlusions.
- ☐ Your Bluetooth connectivity is stable 24/7.
- ☐ You have a few weeks of mental space to work on this.

If any of these is shaky, **fix it before you begin**. The rest of the project will either fail, or it will paper over the weakness in ways that hurt you later.

Chapter 1 goes into each of these in depth.

## Phase 2 — Configure safety settings (Chapter 3)

You cannot run FCL on HCL-era safety restrictions. In HCL, the user gives big boluses for meals, so the loop never needs to deliver big SMBs. In FCL, the loop must deliver big SMBs — because you are not bolusing.

So first, **you widen the guardrails, and then you install new ones.**

Specifically, in this phase you will:

1. Widen the max allowed SMB size (SMB range extension).
2. Widen the max allowed ISF amplification (autoISF_max).
3. Nudge up the SMB delivery ratio.
4. **Install your iob threshold (iobTH)** — this is your most important new safety setting.
5. Configure a handful of other AAPS preferences (Autosens off, exercise settings, odd/even target logic, etc.).

You will **not** enable "ISF adaptation by glucose behavior" yet. That is Phase 3.

Chapter 3 walks through each setting.

## Phase 3 — Tune ISF weights to your meals (Chapter 4)

This is the heart of the project, and where most people spend the most time.

autoISF has **five ISF "weight" parameters** that each apply during a different phase of the post-meal glucose curve:

| Parameter              | When it matters                             |
|------------------------|---------------------------------------------|
| **bgAccel_ISF_weight** | The first signs of a rise (acceleration)   |
| **pp_ISF_weight**      | The steep linear rise after a big meal      |
| **bgBrake_ISF_weight** | The curve flattening toward the peak        |
| **dura_ISF_weight**    | Stuck-high plateaus, especially fatty meals |
| **bg_ISF_weight**      | Very high bg levels                         |

You tune them **in that order**, starting with bgAccel_ISF.

The rule of thumb is: within ~20 minutes of a rise being detected, the loop should have delivered about the same amount of insulin you would have bolused in HCL for that meal. That is the benchmark you're calibrating against.

You iterate. You look at two or three meals from your normal spectrum. You check the AUTO ISF tab (or use the Emulator — Chapter 11 — to make this easier). You adjust, watch another day or two of meals, adjust again.

> 💡 **The most important discipline in Phase 3**
>
> **Work through meals with your normal insulin sensitivity only.** Do not try to tune during an illness, a sports day, a hormonal shift, or anything else that changes your insulin need. You are trying to build a baseline that the rest of the system adapts *from*.

Chapter 4 walks through each weight, how to start, and how to iterate.

## Phase 4 — Handle exceptions (Chapters 5 and 6)

Once your meal management is working, you turn to everything else:

- **Chapter 5 — Modulating aggressiveness.** Automations that switch the loop between "standard," "milder," and "more aggressive" modes. Odd/even target tricks for emergency SMB shutoff. The concept of a "DIY cockpit" — custom buttons on your AAPS home screen for recurring situations (snacks, kids' meals, etc.).
- **Chapter 6 — Exercise and activity.** Dynamic iobTH, the exercise mode, the activity monitor (step-counter-driven sensitivity adjustment), and the particularly tricky "exercise after a meal" scenario.

Most users do not need everything in these chapters. Pick what maps to your actual life.

## A staged implementation strategy

You do not have to do everything at once. Many people start by running FCL only at:

- A single meal per day (e.g., only dinners).
- Weekdays only.
- A specific time window, with a fallback to HCL otherwise.

This is a **very good idea** in your first few weeks. You can expand once you see the loop behave the way you expect.

## What success looks like

When the project is done, you should see:

- Most meals handled hands-off, with glucose staying below ~180 mg/dL.
- Iob rising quickly after meal start (within 10–20 minutes) and then capping at your iobTH.
- Occasional need for a small snack to catch an insulin "tail" — this is normal.
- Very few manual interventions per day.
- A rolling weekly time-in-range you are happy with — for most adults on a normal diet, somewhere in the 75–90% range.

You are *not* trying to never go above 140 mg/dL. If that is your goal, FCL is the wrong path. See the discussion in Chapter 1.

## Safety rail: how to exit FCL

You can always go back to HCL. Two ways:

1. **AAPS Preferences → OpenAPS SMB → autoISF → "Enable ISF adaptation by glucose behavior" OFF.** This disables autoISF entirely. You are now running vanilla OpenAPS SMB+UAM.
2. **Tap the violet FCL loop icon** on the AAPS home screen and pick the green HCL icon (if your version supports it).

You will need to re-enable the Insulin button (AAPS Preferences → Overview → Buttons) to bolus for meals again.

Keep this escape route in mind throughout. If something feels wrong, go back to HCL. Always.

## A note on case studies

The original document refers frequently to numbered "case studies" (e.g., "Case Study 4.1: Pizza," "Case Study 6.2: Biking day with hi-carb lunch"). These sit alongside the main text on the author's GitHub. As you work through this book, look up the case study for any situation that feels close to your own. They are the most concrete material available and will save you a lot of reasoning from first principles.

A full index of case studies is in Appendix B.

# Chapter 1 · Prerequisites for Full Closed Loop
Everything in this chapter is about what must be true *before* you begin. If any of these foundations is missing, FCL will either fail outright or fail quietly by trading off things you did not realize you were trading off.

> ⚠️ **The most common way this project fails** is not a tuning error. It is someone who skipped a prerequisite, told themselves they could work around it, and spent six weeks chasing a symptom whose cause was a weak foundation.

## 1.1 A well-tuned hybrid closed loop

Your first prerequisite is a hybrid closed loop that is already performing satisfactorily. That means:

- You have experimentally determined, correct **profile ISFs** for each hour of the day (not ISFs produced by Autotune or implied by dynamicISF).
- Your **basal** holds you steady in open-loop testing.
- Your **insulin-to-carb ratio (IC)** has been validated against real meals.
- Your **DIA** is set correctly for your insulin.
- Your hybrid closed loop allows SMB sizes up to 120 minutes of basal without trouble.

There are three reasons this matters so much:

1. **autoISF is highly personalized.** The loop will be asked to mimic *your* successful HCL behavior. If your HCL behavior was the result of errors that happened to cancel out, autoISF will inherit and amplify those errors.
2. **autoISF multiplies your profile_ISF.** Every tuning parameter you will set in Chapter 4 is a *factor on your profile ISF for that hour.* If your profile ISF is wrong by 20%, every bgAccel, pp, and dura weight you tune will be calibrated to compensate — and will be wrong for the same reason.
3. **New parameters stack on old ones.** If you tune new parameters on top of an unfixed old profile, you create a system of balanced errors. This can work in individual scenarios but creates an unstable system overall, and is nearly impossible to untangle later.

> ⚠️ **If you've been running with dynamicISF, Autotune, or a maze of custom Automations**
>
> You may have "learned to live" with a profile that is not quite right, because the dynamic components were hiding the problem. Those components will now be turned off (for FCL, you will also turn off Autosens). The underlying problem will surface. **Fix it in HCL first**, or your FCL project will produce confusing, unstable results.

For help getting your HCL foundation right, see the neighboring HCL repository: https://github.com/bernie4375/HCL-Meal-Mgt.-ISF-and-IC-settings

## 1.2 A fast insulin

FCL only works with a fast insulin. Period.

In FCL, you are no longer pre-bolusing. The loop must recognize that a rise has started and deliver insulin fast enough to meaningfully limit the peak. With a slow insulin, by the time the insulin is active, the peak has already happened and passed.

**Use Lyumjev or Fiasp.**

Possible exceptions:

- **Apidra** may work — see Case Study 1.2 — though with a lower margin for error.
- **Humalog** does not work well with a normal-carb diet in FCL.
- If you are on a consistent low-carb diet, are on a GLP-1 drug, or have gastroparesis, a slower insulin may be acceptable. All three situations slow down your carb absorption enough to match a slower insulin.

A modelling study compared insulins in an FCL context and found that faster insulins:

- Produce significantly lower glucose peaks.
- Tolerate a few minutes of delay in detection without catastrophic peaks.
- Minimize the effect of meal size variability on peak height.

For deeper reading: *The artificial pancreas and meal control…* (available as a PDF in the HCL repo linked above).

## 1.3 Reliable insulin delivery

Your pump, cannula, and insulin must all cooperate reliably with your chosen fast insulin.

### Insulin tolerance

Occlusions kill FCL performance faster than almost anything else. If your pump and cannula do not tolerate Lyumjev (or Fiasp) well — if you see hard-to-explain glucose rises at ever-increasing "fake" iob before a scheduled cannula change — FCL will not work for you.

> 💡 **Cannula/pod timing**
>
> Many users find that 48 hours is the practical limit for their cannulas, well before any manufacturer-stated change interval. Change early. You can easily lose 25% time-in-range on a day where a site is starting to fail (see Case Study 1.1).

> ⚠️ **If you are coming from leaking pods or erratic sensitivity swings that you "kind of controlled" with dynamicISF**
>
> Do not start FCL. Resolve the pod/cannula problem first. FCL has no tolerance for erratic delivery.

### Bluetooth connectivity

In FCL, the loop must deliver the right SMB at the right moment. If the pump loses Bluetooth connection during the first five minutes of a meal, you have lost the most important window for insulin delivery.

- In AAPS Preferences → Local Alerts, turn on the connection-lost alert.
- Consider an Automation that fires an alarm if Bluetooth has been down for more than a few minutes.
- Keep your phone close to the pump 24/7.

See Case Studies 1.4 and 1.6 for what goes wrong when this prerequisite fails.

## 1.4 An excellent CGM

Because you are no longer giving a meal bolus, the CGM's job becomes dramatically more important. The loop is reading glucose values and deciding, in real time, "is this the start of a meal?" A jumpy CGM will produce false "yes" decisions.

Things to understand about your CGM, before starting FCL:

1. **Does it support "SMB always"?** You need SMBs to be deliverable even when cob = 0 (which is *always the case* in FCL).
2. **What smoothing, if any, is applied?** See https://androidaps.readthedocs.io/en/latest/Usage/Smoothing-Blood-Glucose-Data.html
3. **Does your CGM produce artefacts?** Review several days of your own data, looking for sudden jumps that the loop could mistake for a meal. Compression lows at night are a particularly common culprit.
4. **If your CGM requires calibrations**, calibration events often produce jumps. You will need a protocol for pausing FCL around calibrations.

### Standard 5-minute CGMs

The best-proven setup, as of this writing, is **Dexcom G6 with overlapping sensors** on each arm (Case Study 1.5). Overlap guarantees you always have at least one reliable sensor running.

G6 production is scheduled to end mid-2026. Alternatives are being evaluated; at time of writing, **Syai Ultra** (Syai Health, Singapore) and **Caresens Air** (i-Sens, South Korea) look promising based on a 10-CGM comparison by one autoISF FCL user. Watch the community for more data.

To ease the transition from G6 to a newer sensor:

- Consider stockpiling a few G6 sensors (via the Anubis extension, or from users who are switching).
- When you start your new sensor system, alternate: every second sensor is your G6. This lets you compare relative performance and build a stock of the new sensor.
- Share your findings! Case Study 1.5 needs updating with mixed-sensor data.

> 📖 **autoISF's built-in jump detector**
>
> autoISF automatically blocks SMBs if the delta between two consecutive 5-minute CGM values exceeds 30% of the current bg (or 20% at targets above 100 mg/dL). This protects against artefacts. The side effect is that a genuine steep rise — for example, after a large sweet drink — can also briefly block SMBs. For 5 minutes, you lose the opportunity for a large early SMB; the loop will catch up in subsequent decisions, but a bit of peak height is lost. This is one reason to think carefully about sweet drinks at meal start.

### 1-minute CGMs

autoISF has supported 1-minute CGM values since version 3.0.1. The data flow is **Libre → Juggluco → AAPS**, with exponential smoothing applied in AAPS.

Early results show smoother, more frequent, smaller SMBs. Whether the 1-minute sampling actually produces *earlier* acceleration detection is still being evaluated. For details, see the "Using 1-minute data in autoISF" chapter of the autoISF Quick Guide.

Some implications for later chapters:

- SMB range extension (Chapter 3) can usually stay at default 1.0.
- SMB delivery ratio (Chapter 3) should typically be under 0.5, not boosted.
- Logfile retention on the phone is shorter, so copy logs to your PC more often.

## 1.5 Meal-related limitations

**There are essentially no meal limitations for FCL, as long as you use a fast insulin.**

A few nuances:

- **Fat- and protein-rich meals** are easier, not harder. Late carb release covers the insulin tail.
- **Gastroparesis or GLP-1 drugs** also make FCL easier by slowing absorption.
- **Erratic consumption of small, fast-carb snacks or sweet drinks** is the main challenge. This can be handled via a "DIY cockpit" button (Chapter 5, §5.4) with a couple of keystrokes, but it is a deviation from the pure hands-off ideal.

You do not need a low-carb diet to run FCL. You do need to decide how much "nudging" you are willing to do for snacks and sweet drinks, and how much time-in-range you are willing to sacrifice if you don't.

## 1.6 Lifestyle-related considerations

### Technical reliability

FCL requires 24/7 reliability of:

- CGM signals
- Pump Bluetooth
- Phone proximity to both
- Cannula/pod performance

Depending on your lifestyle, this is either routine or burdensome. Be honest with yourself. If you regularly forget your phone, leave your pump on a table across the room, or let cannulas run to 72 hours hoping for the best — this project will frustrate you.

### Exercise preparation

In HCL, preparing for exercise means reducing iob ahead of time. In FCL, the algorithm is tuned to *raise* iob aggressively when a rise is detected. So setting a pre-exercise high temporary target and reduced %profile, effective *before* the meal, would sabotage your meal management.

Exercise management in FCL therefore needs its own strategy. Chapter 6 covers:

- Dynamic iobTH (the exercise mode's ability to auto-lower the iob cap).
- The activity monitor (step-counter-driven small adjustments).
- A "DIY cockpit" button for the exercise-after-meal scenario.

Unusual activity requires disciplined preparation — especially if you want to avoid mid-exercise snacking.

### Children

FCL for children presents extra challenges:

- Lyumjev may not be available or tolerated.
- Hourly basal rates are low, limiting SMB size.
- Diets often include fast carbs that produce steep spikes, made worse by small body volume.
- Sensitivity shifts and circadian changes happen more sharply.
- Bluetooth discipline and cannula site discipline are harder to enforce.
- Caregiver-child coordination adds complexity.

See Chapter 7 (Advanced HCL with Meal Announcement) for a gentler intermediary approach, which is often more practical for children.

## 1.7 Time to set up

Set up is a real project of real weeks. The exact timeline depends on:

- Your current HCL tuning quality.
- How varied your meals and lifestyle are.
- How much compromise you will accept (cannula changes more often, skipping meals when glucose is high, etc.).
- Your personal aptitude for data analysis and iteration.

### The structured path

Follow the chapter sequence. Do not shortcut.

But: **you do not have to implement everything at once.** Many users start by:

- Running FCL only for one meal type per day (dinners, for example).
- Running FCL only on weekends, with HCL during the work week.
- Finding feasible settings for the meal they most care about first, then expanding.

Once one meal is working well, expand to others, then turn to exercise and the other non-meal challenges in Chapters 7 and 8.

### The "trial and error" fast track

You will find FCL success stories from users who jumped in, added patches as problems arose, and never did the structured setup. Some of these solutions are good enough for the person who built them. But they tend to be:

- Unstable
- Poorly understood by their own author
- Nearly impossible for anyone to help debug
- Impossible to fine-tune later without starting over

If you go this route, be prepared to start over at some point. And recognize that as your own web of Automations and workarounds grows, no one in the community will be able to help you untangle it.

> 💡 **A word from the author**
>
> "Necessity is the mother of invention." Creative users regularly come up with solutions that push the whole community forward. I welcome that spirit. Just do it with your eyes open — expect some restarts, and document what you do so others can learn from it.

### Safety is non-negotiable

No matter how you approach FCL, these safeguards are mandatory:

1. **Set an iob threshold (iobTH)** above which no more SMBs will fire. This is a built-in feature of autoISF (Chapter 3, §3.4). For FCL methods that do not have a built-in iobTH, set up an Automation to mimic one.
2. **Know how to shut off SMBs quickly.** Setting an odd-numbered temporary target blocks all SMBs while active. This is your emergency brake. Use it for:
   - Anti-hypo snacks
   - Unusual situations where you do not want the loop to react aggressively
   - Any moment when something feels off
3. **Practice exiting FCL.** In your setup weeks, deliberately switch from FCL to HCL and back several times, so you know the motions by heart before you ever need them in a hurry. See Chapter 10 (Troubleshooting, §10.1) and Chapter 5 (§5.6).

## 1.8 Summary checklist

Before you move on to Chapter 2, confirm:

- ☐ My hybrid closed loop is satisfying, without relying on Autotune or dynamicISF.
- ☐ My profile ISFs, basal, and IC are experimentally validated.
- ☐ I am using Lyumjev or Fiasp.
- ☐ My pump, cannula, and insulin tolerate each other. Occlusions are rare.
- ☐ My CGM is smooth and reliable. I have a plan for calibration jumps.
- ☐ My Bluetooth connectivity is stable 24/7.
- ☐ I have 4–8 weeks of mental bandwidth for this project.
- ☐ I have identified a subset of meals to start with (e.g., dinners only).
- ☐ I know how to exit FCL back to HCL.
- ☐ I have joined the community (Discord link in the Introduction).

When every box is checked, you're ready for Chapter 2.

# Chapter 2 · How autoISF Works
Before you touch any settings, you need a mental model of what autoISF actually does. This chapter is for the "why" behind the "how."

## 2.1 The core idea

Every 5 minutes (every minute, if you're on a 1-minute CGM), autoISF does this:

1. **Reads the recent glucose curve** — last several CGM values, smoothed, with a parabola fitted to detect acceleration.
2. **Classifies the phase** — is this an acceleration? A steep linear rise? A deceleration? A plateau?
3. **Calculates an adapted ISF** (called `sens` in the AUTO ISF tab) by applying modulation factors to your profile_ISF for that hour.
4. **Asks the standard oref(1) UAM loop what insulin is needed** given that adapted ISF.
5. **Delivers an SMB and/or adjusts temp basal**, capped by several safety limits.

The key insight: **your profile_ISF is the anchor.** autoISF does not replace it. It multiplies it up (to deliver more insulin) or down (to deliver less), within bounds you set.

This is why Chapter 1 insisted on a correct profile_ISF. Every single thing in the rest of this book is a factor on that number.

## 2.2 The five weight parameters, mapped to the glucose curve

The most important consequence of autoISF's design is that **different phases of a meal's glucose curve get different ISF modulation**, each controlled by its own tuneable weight:

```
        Glucose ↑
          |              ___
          |           __/   \___
          |         _/          \___
          |        /                \__
          |   ____/                    \__
          |  /                            \___
    ──────┼──────────────────────────────────────→ Time
           ^  ^       ^        ^         ^
           |  |       |        |         |
           A  B       C        D         E

  A: Detection + acceleration →    bgAccel_ISF_weight
  B: Steep linear rise         →   pp_ISF_weight
  C: Deceleration to peak      →   bgBrake_ISF_weight
  D: Stuck-high plateau        →   dura_ISF_weight
  E: High bg correction        →   bg_ISF_weight (rarely used in FCL)
```

**In FCL, the first two (bgAccel and pp) do most of the work.** They are the "initial iob ramp-up" that replaces your former meal bolus. The others play supporting roles for specific meal types.

> 📖 **Origin story (skippable)**
>
> The lead developer, ga-zelle, arrived at these parameters by analogy rather than by reading endocrinology papers. `bgAccel_ISF` came from Newton's second law — if glucose is being "pushed up," the resistance (ISF strength) should scale with the push. `dura_ISF` came from control theory — a PID controller has a proportional, integral, and derivative term; the integral was missing from oref, so dura_ISF adds it. He later realized the body's own insulin response also has a fast initial phase and a slower sustained phase, which is roughly what the two mechanisms recreate. Interesting, not essential.

## 2.3 The guardrails

autoISF's aggressive ISF modulation is hemmed in by several settings you will configure in Chapter 3:

| Guardrail             | What it limits                                                            |
|-----------------------|---------------------------------------------------------------------------|
| **autoISF_max**       | Maximum amplification factor on your profile_ISF (default 2.0).          |
| **autoISF_min**       | Minimum factor — how soft the loop can go (default 0.3 in this book).    |
| **SMB range ext.**    | Max SMB size as a multiple of 2 hours of basal.                          |
| **SMB delivery ratio**| Fraction of calculated insulin need delivered via each SMB.              |
| **iobTH**             | Absolute ceiling — once iob exceeds this, SMBs stop firing.              |
| **max iob**           | Hard ceiling, separate from iobTH.                                        |
| **30% jump rule**     | SMBs auto-blocked if the CGM delta exceeds 30% of current bg.            |
| **Odd-numbered target**| Shuts off SMBs entirely. Your emergency brake.                          |

**iobTH is the most important one.** It is what separates "a loop that sometimes delivers 2U because the glucose curve looked ambiguous" from "a loop that kept firing SMBs until 12U of iob had accumulated." You will set it in Chapter 3.

## 2.4 Two safety mechanisms that people trip over

### Even/odd target rule

autoISF uses a clever trick to let you shut SMBs on and off with a single keystroke:

- **Even-numbered glucose target** (profile or TT) → SMBs allowed, as normal.
- **Odd-numbered glucose target** → SMBs blocked. The loop still adjusts via temp basal, but won't deliver an SMB.

For mmol/L users, the logic uses the first decimal — e.g., 5.0 is "even," 5.1 is "odd."

This feature is enabled in AAPS Preferences → OpenAPS SMB → autoISF settings → "Enable alternative activation of SMB depending on current target" = ON.

**In FCL you will keep this permanently on.** You will use odd-numbered targets as your emergency brake (for anti-hypo snacks, compression lows, "I want a moment to think," etc.).

### 30% jump rule

If the delta between two consecutive CGM values exceeds 30% of the current bg (20% at targets above 100 mg/dL), SMBs are automatically blocked for that cycle.

**Why this matters:** on a well-behaved CGM this almost never triggers for real meals. On a jumpy CGM, or with a sweet drink that causes a genuine sharp spike, it can block the very SMB you wanted.

Example: From 74 mg/dL, a jump to 97 mg/dL (+23, which is +31% of 74) blocks SMBs. That's 5 lost minutes of insulin delivery at the worst possible moment.

Mitigations, in preference order:
1. Use a CGM that doesn't produce artefacts (Dexcom G6 overlapped is the gold standard).
2. Avoid sweet drinks at meal start.
3. Review logs to see how often this triggers for you, and adjust behavior.

Do **not** change the 30% threshold in the code.

## 2.5 Where to look when you want to know what happened

Three places give you the information you need:

1. **The AUTO ISF tab** in AAPS. At any moment, shows the most recent loop decision in detail — profile_ISF, each modulation factor, the final sens, any limits that were hit, the calculated SMB size, and whether it was delivered or blocked and why.
2. **Extra graphs below the AAPS home screen glucose chart.** These can display iobTH, the autoISF factor contributions over time, the fitted parabola, and more. Enable them from the chart options.
3. **The Emulator** (Chapter 11–14). Replays your logfiles on a PC or phone and shows loop decisions in tabular form, plus lets you ask "what if I had used setting X instead?"

For setup and tuning, you will consult the AUTO ISF tab constantly. For deeper analysis, the Emulator is worth installing.

## 2.6 What autoISF does not do

A few common misconceptions:

- **autoISF does not replace Autosens or dynamicISF.** It serves a different purpose — reacting to the glucose curve in real time, not tracking longer-term sensitivity trends. For FCL, you will turn both Autosens and dynamicISF off.
- **autoISF does not "learn" from your meals over time.** It reads the current curve, applies your settings, and decides. Tuning is your job.
- **autoISF is not a carb-counting replacement.** It reacts to the curve, not to a meal. If you take a wildly out-of-spectrum meal, it will over- or under-treat, and you will need the manual levers in Chapter 5.
- **autoISF is not a bolus calculator.** It delivers many small SMBs based on predicted insulin need over the next 30–60 minutes, recalculated every 5 minutes. If you give a user bolus on top, you distort the curve autoISF is reading, and the predictions drift.

With this model in mind, let's start configuring.

# Chapter 3 · General FCL Settings
This chapter walks through the settings you change in AAPS Preferences **before** you enable autoISF's glucose-based ISF modulation. These settings widen the safety cage that HCL kept narrow, and install the new safety net (iobTH) that protects you from the wider cage.

> ⚠️ **Critical reminder from Chapter 1**
>
> Everything in this chapter assumes you already have a properly tuned hybrid closed loop with correct profile ISFs, and that you use a fast insulin. If not, stop and go back.

## 3.1 SMB range extension

**Setting path:** Preferences → OpenAPS SMB → autoISF settings → SMB delivery settings → `smb_max_range_extension`.

In AAPS Master, the maximum SMB size is 120 minutes of basal (2.0× hourly basal). In FCL, that's usually not enough — you need the loop to deliver insulin comparable in magnitude to what you used to bolus manually.

**For 5-minute CGMs (Dexcom G6/G7/ONE):** **Start with 2.0.** This doubles the limit to 4 hours of basal per SMB.

For a more precise estimate:

> 🧭 **Sizing calculation** (author's numbers in parentheses)
>
> Goal: within 10 minutes of a detected rise, deliver at least half of what you'd have bolused in HCL — roughly 2 SMBs worth.
>
> - Target SMB size: you want at least `(your HCL meal bolus ÷ 2)` as an achievable single SMB. With a typical 8U bolus → ~4U target. Allow ~3U as a workable individual SMB size.
> - Your hourly basal: e.g., 0.6U/h. AAPS Master's default 2× allows 1.2U per SMB.
> - Needed extension: `3U / 1.2U = 2.5`.

Very low basal rates can push this number up to 3.0 or higher. The maximum setting is 5.

Keep an eye on the AUTO ISF tab or Emulator output to see whether your loop is frequently bumping against this limit. If it is, widen it.

**For 1-minute CGMs (Libre 3 via Juggluco):** With values every minute, insulin delivery is spread across up to 5 SMBs per 5 minutes. You rarely need large individual SMBs.

**Start at 1.0** (the default). Only raise it if your basal is very low, or if your loop routinely fails to deliver small SMBs quickly enough.

## 3.2 autoISF min and max

**Setting path:** Preferences → OpenAPS SMB → autoISF settings → `autoISF_min` and `autoISF_max`.

These cap how far autoISF can amplify or soften your profile_ISF.

- **autoISF_max = 2.0** to start. Up to 2× stronger than profile_ISF, if the weights call for it.
- **autoISF_min = 0.3** to start. Down to 30% as strong (i.e., ISF is more than 3× weaker).

Do not leave `autoISF_min` at 0.5 or higher — it will prevent exercise mode from properly softening the loop.

Raise `autoISF_max` later if you find the AUTO ISF tab frequently reports "capped by autoISF_max." Don't raise it prophylactically.

## 3.3 SMB delivery ratio

**Setting path:** Preferences → OpenAPS SMB → autoISF settings → SMB delivery settings → `smb_delivery_ratio`.

Default is 0.5 — the loop delivers 50% of the currently-calculated insulin need per SMB cycle. The remaining need rolls into the next 5-minute decision.

**For 5-minute CGMs:** **Start at 0.6 or 0.7.** Higher values get you more insulin delivered 5–10 minutes earlier, which matters a lot in FCL (where you start late already).

A higher ratio also amplifies unwanted SMBs from CGM jitter. If your CGM is not rock-solid, stay near 0.5–0.6.

Do not go above ~0.8. A 100% delivery ratio works against you in two ways:
- Every noisy SMB is amplified too.
- You end up forced to compensate by narrowing other parameters (lower autoISF_max, lower bgAccel_ISF_weight), which makes the whole system less dynamic and costs time-in-range.

**For 1-minute CGMs:** Set **below 0.5** (typically 0.3–0.4). The extra sampling frequency already gives you the "early delivery" benefit; a high delivery ratio on top would be too aggressive.

## 3.4 iobTH — your most important safety setting

**Setting path:** Preferences → OpenAPS SMB → autoISF settings → Full_Loop_settings → `iob_threshold_percent`.

iobTH is an iob ceiling. Once your total iob exceeds it, **no more SMBs will fire**. Temp basal can still run, but big insulin delivery stops. This is what keeps an aggressively-tuned FCL from stacking too much insulin.

> ⚠️ **Everything else in autoISF settings is meaningless without a sensible iobTH.**

### First — set max iob

First, check that your `maxIOB` (Preferences → OpenAPS SMB → Maximum total IOB) is set correctly.

- If you have historical iob data: look at the max iob you've ever needed (including times of elevated insulin resistance). Set maxIOB slightly above that.
- If you don't: `maxIOB = hourly basal + (max meal carbs digested in ~2.5h / IC) + (correction from highest meal-start bg to target / ISF)`, then multiply by ~1.2 for a cushion.

### Find your iob target

Look at your historical data. For the biggest high-carb meals you handle, what iob level (bolus + SMBs) was genuinely useful?

> 🧭 **Author's example:** Big meals sometimes needed up to 8U of iob. TDD ~40U. maxIOB = 10U.

### Calculate iob_threshold_percent

Decide how much of that "big meal iob" you want autoISF to deliver rapidly via SMBs. A common choice is ~75%.

> 🧭 **Example:** Target iob via rapid SMBs = 75% × 8U = 6U. With maxIOB of 10U: `iob_threshold_percent = 6/10 = 0.6 → 60%`.

Enter this value in AAPS Preferences.

### The +30% overshoot rule

The **last SMB allowed** can exceed the effective iobTH by up to 30%. This is on purpose: it lets iob run higher for genuinely big meals (where the final SMB is still large) without needing to set iobTH itself higher.

- At bg targets above 100 mg/dL, the overshoot is capped at +20% instead of +30%.
- An individual SMB that would overshoot by more than 30% is cut to 130% of iobTH.
- Once iob is above the effective threshold (plus overshoot), only temp basal adds more insulin.

### High-carbers: lower iobTH slightly

If you eat big meals, keep in mind that the +30% overshoot will push your actual peak iob above the stated iobTH. Pick your `iob_threshold_percent` so that `iobTH × 1.3` is the real ceiling you're comfortable with.

### iobTH auto-modulation

iobTH is not a fixed number in daily operation. Several things modulate it:

- **Low TT** (e.g., an EatingSoon TT) → iobTH goes *up*, allowing more iob for the meal.
- **High TT** (e.g., an exercise TT) → iobTH goes *down* sharply, limiting iob for exercise.
- **Exercise button** (yellow, combined with TT > target) → further sharpens the reduction.
- **%profile setting** → iobTH scales proportionally (80% profile → 80% of iobTH).
- **Activity monitor** → small automatic adjustments based on step count.

All of these changes show up in the AUTO ISF tab — the "effective iobTH" is reported at the top of the results section.

### Enable odd/even target logic

In Preferences → OpenAPS SMB → autoISF settings → SMB delivery settings:

- ☐ **"Enable alternative activation of SMB depending on current target"** = ON.

This is required by autoISF 3.0.1+ and enables the even/odd emergency brake (§2.4).

### Setting iobTH with Automations

You can override iobTH via an Automation. Be careful: setting a different `iobTH_percent` via an Automation **does not automatically revert** when the Automation ends. You need a tandem "restore" Automation to put it back.

For this reason, **prefer modulating iobTH indirectly** — via TT, %profile, or the exercise mode — which revert automatically.

## 3.5 EatingSoon TT — skip for now

FCL works perfectly well without any EatingSoon TT. You can skip this section on first setup and return later if needed.

Briefly: setting a low TT (e.g., 74 mg/dL) before a meal:
- Makes early SMBs slightly larger.
- Raises the dynamic iobTH slightly, so SMBs keep firing for bigger meals.
- Avoids halving the bgAccel_ISF `cap_weight` that would otherwise apply when bg sits below target.

The author's preferred approach is **not to set an EatingSoon TT manually**, but to use an Automation that sets a low TT automatically at the first sign of a rise (e.g., when bg delta exceeds +10 mg/dL, iob is low, meal time window applies, and no TT is already running). The duration is brief (~30 minutes).

Benefits:
- First 1–2 SMBs fire before the trigger, so low-carb meals don't get over-treated.
- Bigger meals automatically get the boost on SMBs 3+ and the elevated dynamic iobTH.

Drawbacks:
- Random bg bumps in the time window can trigger unwanted aggressive SMBs. Tune the trigger delta carefully.
- Blocks other "no TT set" Automations during that window.

Details are in §5.2 (automatic modulation). Don't worry about this on first setup.

## 3.6 Other AAPS preferences to verify

Quick checklist — the ones requiring actual attention are in **bold**. The rest, leave at defaults or as specified.

1. ☐ **Enable SMB, SMB with high TT, SMB always, and UAM.** All ON.
2. ☐ **Autosens: OFF.** autoISF is incompatible with Autosens in FCL mode. You'll see a warning when Autosens is on without carb inputs.
3. ☐ **Autotune: do not use.** Likewise, **dynamicISF (in iAPS/Trio): OFF**. And **dynamic CR, sigmoid: OFF**.
4. ☐ **SMB frequency:** 3 minutes (standard), 1 minute for Libre 3.
5. ☐ **"High TT raises sensitivity": ON.** Required for the exercise mode math.
6. ☐ **"Low TT lowers sensitivity": OFF** at first. Turn ON later, once you understand how aggressive your loop can go.
7. ☐ **"Resistance lowers target" and "Sensitivity raises target": OFF**. These interact poorly with autoISF — especially the even/odd target logic.
8. ☐ **Half-basal exercise target: 160 mg/dL** placeholder. You'll tune this in Chapter 6.
9. ☐ **"Activity modifies sensitivity": OFF** until Chapter 6. (You can turn it on sooner if you're already sure about your step-count tuning.)
10. ☐ **Advanced → "Always short avg delta": OFF** unless your CGM is jittery. Smoothing costs you early detection time.
11. ☐ **Smoothing** (AAPS Configuration Builder → Smoothing): None is preferred for excellent CGMs. Average is next best. Exponential smooths nicely but hides the early rise that FCL depends on. G7 users typically need exponential smoothing.
12. ☐ **Safety multipliers** (Preferences → OpenAPS SMB → Advanced): roughly **double** the HCL defaults, so the loop can do up to 500% TBR.
13. ☐ **`iob_threshold_percent`**: enter the value from §3.4.
14. ☐ **Password-protect Preferences** with a short password, to avoid accidental changes while scrolling.
15. ☐ **Disable bottom buttons** (Preferences → Overview → Buttons: Insulin, Calculator, etc. all OFF). Especially important if a child uses the phone, or if it might be temporarily out of your control. The insulin button allows a direct insulin shot, which is dangerous.
16. ☐ **Alarms:** review your past outlier data and set xDrip / AAPS alarms that would have caught those issues.
17. ⚠️ **autoISF settings**: do not yet enable "Enable ISF adaptation by glucose behavior." You will do this when you start Chapter 4.

## 3.7 Summary: you are ready when…

- ☐ SMB range extension set (§3.1).
- ☐ autoISF_max = 2.0, autoISF_min = 0.3 (§3.2).
- ☐ SMB delivery ratio set (§3.3).
- ☐ maxIOB, iob_threshold_percent configured (§3.4).
- ☐ Odd/even target logic enabled (§3.4).
- ☐ AAPS preferences cleaned up (§3.6).
- ☐ Password set on Preferences.
- ☐ Bottom buttons (Insulin, Calculator) disabled.
- ☐ "Enable ISF adaptation by glucose behavior" **still OFF**.

When every box is checked, move to Chapter 4.

# Chapter 4 · Meals: Setting Your ISF Weights
This chapter is where you tune autoISF's five ISF weights to your meals. Each weight targets a phase of the post-meal glucose curve (§2.2). When you're done, your loop will handle your normal meal spectrum on its own.

Budget three to six weeks. Do not rush.

## 4.1 Getting started

### Rules recap

1. **Tune on days with normal insulin sensitivity only.** No illness, no heavy exercise, no hormonal shifts. You are calibrating the baseline that the rest of the system adapts from.
2. **Start with typical meals from your own spectrum.** Not extremes. Not novelty meals. Not sweet drinks at meal start.
3. **Iterate on 2–3 different meals, not one.** Settings optimized for a single meal will rarely work for the rest. (Case Study 8.2 is the negative example.)
4. **Do not give a bolus** during this phase. Any user bolus distorts the glucose curve that autoISF is reading, and invalidates your tuning.
5. **Start narrow.** Many users begin with only one meal per day (e.g., dinners), with an Automation that turns autoISF off for the other 20 hours. Expand once one meal works.
6. **Do not copy another person's numbers.** Every example in this chapter is illustrative only.

### Turn autoISF on

Now — and only now — turn on **Preferences → OpenAPS SMB → autoISF settings → "Enable ISF adaptation by glucose behavior"**.

During your tuning period, you can automate this to be ON only during your chosen meal window (e.g., 11 AM – 6 PM for lunches) and OFF the rest of the time.

Alternatively, leave it always on and use an odd-numbered profile target for the hours you don't want it aggressive. See §5.2.

### Watch the curves

Two things to do habitually during tuning:

1. **Watch your bg, iob, and insulin activity curves develop on the AAPS home screen.** Over days you'll build intuition about what "good" looks like.
2. **Open the AUTO ISF tab** at key moments to see exactly what the loop decided and why.

The Emulator (Chapter 11) makes this dramatically easier — you can replay a day's decisions and see everything in one place. Install it early if you're comfortable with a little Python.

### Resist reaching for later tools

You'll read about the DIY cockpit, Automations, exercise mode, and activity monitor. All of those are for **after** your weights are tuned. If you add them early, each one compensates for some weakness in your weights — and you lose the ability to tell which setting is actually doing what. Untangling that later is painful. Tune the weights first; layer the rest on top.

## 4.2 bgAccel_ISF — catching the first rise

**Setting:** `bgAccel_ISF_weight` in Preferences → OpenAPS SMB → autoISF settings.

This is your most important weight. It drives the first 3–4 SMBs after a rise is detected — the SMBs that replace your old meal bolus.

### The target

Within about 20 minutes of acceleration detection, the first 3–4 SMBs should together deliver roughly the same iob you would have bolused for this meal in HCL. In practical terms, for a big meal, you want two of those first three SMBs to each be **¼ to ⅓ of your old HCL bolus**.

- **Above ⅓ per SMB** is too aggressive: low-carb meals get over-treated, snacks trigger full meal responses, and CGM artefacts fire real SMBs.
- **Below ¼ per SMB** is too shy: the peak runs high, and dura_ISF has to work overtime to clean up the mess.

### Starting point

**Start with `bgAccel_ISF_weight = 0.02`.** Yes, that small. It's a multiplier inside a formula — it adds up fast.

Test on a medium-to-high-carb meal from your normal spectrum. Don't try a pizza. Don't try a salad either. Pick something representative.

### Iterate in small steps

Increase in small steps — e.g., 0.020 → 0.022 → 0.025 → 0.030 → 0.035 → 0.040 — and watch 2–3 meals over the next few days before the next change. Never change two things at once; you won't know which one caused the effect.

### CGM quality is the main variable

The main thing that distorts this tuning is **CGM quality.** autoISF checks a recent window of values for stability before acting on a detected acceleration.

- A jumpy or dropout-prone CGM will either (a) soften the loop's response by delaying acceleration recognition, or (b) fail to recognize it at all.
- You have three options:
  1. Use a well-performing CGM (overlapping G6 is the gold standard).
  2. Only tune on days you know are good CGM days.
  3. Live with average CGM quality and accept weaker/later SMBs and narrower overall dynamic range.

> ⚠️ **The trap:** tuning on bad CGM days pushes you to overly aggressive weights, which then backfire on good CGM days.

### The cap_weight rule

autoISF has a built-in `cap_weight` safety factor. When bg is **below** target at the moment of acceleration detection, `cap_weight` halves the effective bgAccel_ISF contribution — the loop stays conservative when catching a rise from a low starting point. Above target, the cap doesn't apply.

This is one reason a low EatingSoon TT (§3.5) helps at meal start: it lifts your effective target above actual bg, so `cap_weight` stays at full strength and the first SMBs aren't halved.

### Good vs bad tuning

| Observation                                | What it suggests                            |
|--------------------------------------------|---------------------------------------------|
| Big meals routinely peak at 200+ mg/dL     | bgAccel_ISF too weak                        |
| First SMBs are smaller than ¼ of HCL bolus| bgAccel_ISF too weak                        |
| Snacks and low-carb meals trigger big SMBs | bgAccel_ISF too aggressive                  |
| iob bounces over iobTH on every meal       | bgAccel_ISF too aggressive *or* iobTH low   |
| Need for post-meal snacks to avoid hypos   | bgAccel_ISF too aggressive *or* dura_ISF too strong |
| Low-carb meals look fine, big ones run high| bgAccel_ISF probably about right, try pp_   |

### Fit for your meal spectrum

A single bgAccel_ISF setting has to work for:

- Low-carb meals (first SMBs must stay small)
- Medium meals
- High-carb meals (first SMBs must drive iob to iobTH fast)

This is possible, because accelerations and deltas in low-carb meals are naturally smaller than in high-carb meals, so the same weight produces smaller SMBs. Your circadian profile_ISF handles breakfast-vs-lunch-vs-dinner differences automatically.

If you genuinely cannot find one setting that works:

- Use an Automation to set different `bgAccel_ISF_weight` in different time windows (§5.2). Note only bgAccel and iobTH_percent are available as Automation targets.
- Use a temporary %profile switch for the brief meal window (e.g., 60% profile for 45 minutes at low-carb meals).
- Preset custom DIY cockpit buttons for snacks and special meals (§5.4).
- Accept slightly reduced performance — most users find this easier than maintaining a complex Automation web.

### A note on deceleration

In the late phase of falling glucose, after the peak, the curve re-accelerates mathematically (in the downward direction). autoISF handles this internally and reduces ISF modulation as the algorithm predicts the glucose minimum. You don't need to tune anything for this phase.

## 4.3 pp_ISF — managing the steep linear rise

**Setting:** `pp_ISF_weight`.

pp stands for "post-prandial." This weight drives SMBs during the steep, roughly-linear rise that follows acceleration in a big-carb meal. In low-carb meals, this phase barely exists.

### When it matters

- High-carb meals, especially with sweet drinks: bg delta is large and sustained. If bgAccel_ISF hasn't already driven iob to the ceiling, pp_ISF will.
- Low-carb meals: usually skipped entirely — the curve flattens before this phase really establishes.

### Tuning

**Only tune pp_ISF after bgAccel_ISF is in a reasonable place.** An over-aggressive bgAccel can cover up a pp_ISF problem, and vice versa.

- **Start with `pp_ISF_weight = 0.005`.** Very small.
- Test on your highest-carb meals in your normal spectrum.
- Step up by 10–20% when cautious, more when you have clear evidence.

> 📖 **The math (skippable)**
>
> The developer's Quick Guide gives:
> `pp_ISF = 1 + pp_ISF_weight × internalFactor`
> `effective ISF = profile_ISF / pp_ISF` (when pp dominates)
>
> The `internalFactor` scales with bg delta above target. So pp_ISF grows with the steepness of the rise.
>
> Same trial-and-error principle as bgAccel: doubling the weight roughly doubles the amplification effect at a given bg delta.

### When the loop has already acted

For moderate-to-big-carb meals, the combination of bgAccel and pp_ISF will usually drive iob to (or just past) your iobTH by the time the rise reaches its peak. Once you're above iobTH, only temp basal adds insulin; the rest of the weights (bgBrake, dura, bg) become less influential.

This is good. It means you've done the main job.

### One weight often fits all meals

Different meal types produce different delta patterns, but pp_ISF scales with delta — so naturally larger deltas produce larger responses. Combined with a circadian profile_ISF (different ISFs for different hours), a single pp_ISF_weight usually covers the full spectrum.

### Watch for false ceilings

If your AUTO ISF tab frequently shows SMBs being capped by:

- `smb_max_range_extension`, or
- `autoISF_max`,

…then your pp_ISF tuning is fighting a restriction instead of doing the real job. Widen the restriction first (Chapter 3) and retune.

## 4.4 bgBrake_ISF — the decelerating rise

**Setting:** `bgBrake_ISF_weight`.

At the end of the rise, before the peak, the glucose curve decelerates. In high-carb meals, by this point your iob is usually already at iobTH and no more SMBs are firing — so bgBrake_ISF is irrelevant.

In **low-carb meals** (or with gastroparesis, or on a GLP-1 drug), the curve may decelerate before iobTH is reached, and bgBrake_ISF controls how much insulin continues to be delivered as the rise slows.

### Starting point

**Start at about half your bgAccel_ISF_weight.** So if bgAccel is 0.04, start bgBrake at 0.02.

This reflects the reality that when bg is decelerating, insulin need drops — you usually want the loop to be softer here, not sharper.

### What it does

The same formula as bgAccel applies, but with a negative internalFactor during deceleration. The effective ISF comes out *bigger* than profile_ISF (softer), not smaller. A larger bgBrake weight means a softer effective ISF during deceleration.

### Tune only if relevant

For high-carb eaters, bgBrake_ISF rarely matters — skip the fine-tuning. Half of bgAccel is a reasonable default.

For low-carb eaters or slow-absorption meals, this weight plays a real role. Start at half of bgAccel and adjust based on whether your low-carb meals run high (reduce the weight → sharper ISF) or produce late hypos (increase the weight → softer ISF).

## 4.5 dura_ISF — stuck at high

**Setting:** `dura_ISF_weight`.

dura_ISF activates when glucose plateaus at an elevated level for 10+ minutes. It boosts insulin in proportion to:

- How long the plateau has persisted
- How far above target the plateau is

This is what handles the "fatty meal second peak" or the long stuck-high plateau that high-FPU meals (pizza, burgers, cheesy pasta) produce.

### When it matters

- **Fatty / high-protein meals** — the classic late plateau, sometimes a second peak 2–4 hours after the meal.
- **Low-carb meals** — if carb absorption is slow enough to keep bg stable at mildly elevated levels for an extended period, dura_ISF picks up the slack.

### Starting point

**Start with `dura_ISF_weight = 0.2`**, and raise it cautiously. The late action of dura_ISF means a weight set too high will hypo you 2–3 hours after a meal, when you're not paying attention.

### Protecting against late dura hypos

dura_ISF keeps working the whole time a plateau lasts. That's useful for a genuine fatty-meal plateau — but dangerous if the plateau is actually an insulin tail fading out. Two Automation patterns help:

- **Fade dura out as the plateau ages.** Set a low TT near the actual target when a high plateau is clearly meal-related. This lets dura act sharpest at the start of a persistent high, then taper off.
- **Block dura below ~140 mg/dL.** An Automation that shuts off SMBs when a mild plateau forms below that threshold. Late insulin at that level rarely pays off; hypo risk does.

These are refinements you add after your weights are stable. The `04_ISF_weights_effects` spreadsheet (in the book's repo) lets you model how your specific dura_ISF setting responds before you commit to a pattern.

Start with the default weight and tune conservatively first.

### What good tuning looks like

- Persistent highs resolve over 1–2 hours, not 4+.
- No late hypos (2–4 hours post-meal).
- dura_ISF shows contributions in the AUTO ISF tab during plateaus but isn't the dominant factor during acute rises.

### If you see late hypos

In order of preference:
1. **Fix bgAccel_ISF and pp_ISF first.** If the initial rise is handled better, the peak is lower and the plateau shorter — dura_ISF doesn't need to work as hard.
2. **Lower dura_ISF_weight** in small steps.
3. **Add an Automation** to cap dura contributions once iob exceeds a threshold — advanced, see Chapter 5.

## 4.6 bg_ISF — generally not needed in FCL

**Setting:** `bg_ISF_weight` (under Preferences → OpenAPS SMB → autoISF settings → bg_ISF settings).

bg_ISF strengthens ISF at high bg and softens it at low bg, independent of meal phase. In HCL it can be useful; in FCL it mostly isn't.

### Why FCL skips it

In FCL you already get most of your insulin early, through bgAccel and pp_ISF, when bg is still relatively low. Boosting ISF again at high bg risks over-delivery; softening at low bg reduces the early SMBs you rely on.

### Recommended FCL settings

- `lower_ISF_range_weight = 0.0`
- `higher_ISF_range_weight = 0.0`

If you have specific evidence that you'd benefit from mild modulation (e.g., you reliably run slightly below target after correcting a high), try 0.1–0.2 on the relevant side and analyze.

## 4.7 How the loop copes without carb entry

Since you give no carb inputs in FCL, the oref UAM (Unannounced Meal) algorithm has to estimate carbs on its own. It works in two directions:

- **Looking back** — given the observed bg change and your profile ISF/IC, it calculates how many grams "must have been" absorbed in the last 5-minute window.
- **Looking forward** — it projects continued absorption for the next 1–3 hours, based on recent "carb deviation" data.

The prediction isn't perfect, but it's often no worse than a user's eCarb estimate — and it's recalculated against reality every 5 minutes. The practical consequence: you don't need to know how many grams were on the plate.

FCL still has to manage the late-meal phase carefully — fading insulin tail meets uncertain remaining carbs. That's what dura_ISF and a well-set iobTH are there for.

## 4.8 Iterating across meals

Take 2–3 meals from your normal spectrum. For each:

1. Observe the full ~3 hours after the meal.
2. Note where the loop did well and where it fell short (too-high peak? late hypo? over-reacted to a snack?).
3. Pick the *first* thing to change — usually the earliest-acting weight with a problem.
4. Make a ~10–20% change.
5. Repeat for a few more meals before changing again.

> 💡 **The temptation to optimize for one meal is the single biggest mistake in this project.**
>
> A weight set that handles your pizza perfectly will probably fail on your salad. Iterate across meal types, always.

### Quality check — the AUTO ISF tab

At key moments during a meal, open the AUTO ISF tab. Check:

- Which ISF component (acce / pp / brake / dura / bg) is dominating `final ISF factor`?
- Is the resulting sens within the autoISFmax / autoISFmin bounds, or bouncing against a limit?
- Is the SMB size capped by `smb_max_range_extension` or `autoISF_max`?
- Is bg below target, triggering the cap_weight halving?
- Is iob above iobTH, triggering SMB shutoff?

Any of these can mask a setting you meant to tune. Fix the masking issue before continuing.

### Meals that simply won't fit

For unusual meals that resist any reasonable fit:

1. **Accept slightly worse time-in-range** for those meals and move on.
2. **Keep a small snack on hand** for when the insulin tail drops you after a high peak.
3. **Manually intervene** — a brief odd TT for a snack situation, for example.
4. **Define a User Action Automation** that gives that meal type its own settings. See §5.4.
5. **Fall back to HCL** for those specific meals.

## 4.9 Focus your effort

> 💡 **Priority order for your weight tuning:**
>
> 1. **bgAccel_ISF_weight** — by far the most important. Spend the most time here.
> 2. **iobTH_percent** — revisit after bgAccel is stable.
> 3. **pp_ISF_weight** — second most impactful.
> 4. **dura_ISF_weight** — mostly for low-carb or fatty meals.
> 5. **bgBrake_ISF_weight** — leave at half of bgAccel unless low-carb is a big part of your diet.
> 6. **bg_ISF_weight** — leave at 0 in FCL.

Once you've found settings that work across your normal spectrum, **don't keep tuning.** Chapter 9 (Performance Monitoring) covers when re-tuning is actually warranted — almost always, the answer is "not now."

## 4.10 Complex scenarios — where they're covered

Everything beyond "my normal weekday meals" is handled in later chapters:

- **Snacks, sweet drinks, out-of-spectrum meals** → Chapter 5 (modulation).
- **Exercise before, during, or after a meal** → Chapter 6.
- **Illness, hormonal shifts, steroid days** → Chapter 5 (%profile switch).
- **Kids** → Chapter 7 (Meal Announcement mode is often better).

Finish tuning for your normal spectrum first. Then layer the rest on top.

# Chapter 5 · Modulating Loop Aggressiveness
Once Chapter 4 is done, your FCL handles normal meals hands-off. This chapter is about everything else — snacks, sick days, rough CGM days, diet deviations, nights, compression lows, and all the rest of ordinary life.

You have **five levers** for adjusting loop aggressiveness. Some are automatic, some manual, some you pre-program into buttons on your AAPS home screen.

## 5.1 The five levers

| Lever                          | What it does                                                |
|--------------------------------|-------------------------------------------------------------|
| **Odd-numbered target**        | Shuts SMBs off entirely (§2.4). Emergency brake.         |
| **Change ISF weights**         | Shifts the acceleration/duration behavior.                  |
| **Change iobTH_percent**       | Raises or lowers the iob ceiling.                           |
| **Change %profile**            | Multiplies everything (basal, ISF, iobTH) proportionally.   |
| **Set a temp target (TT)**     | Low TT → more aggressive; high TT + exercise → less.        |

All five are also accessible in AAPS Automations, which means any pattern you can describe can be triggered automatically when your conditions are met.

> 💡 **The core discipline:** keep it simple. A loop that works because of five Automations interacting with each other is a loop nobody — including you — understands. Do the basics well; add Automations sparingly.

## 5.2 Fully automatic modulation

This section is about configurations that run without user action. Use these for recurring, predictable situations.

### Disable outside meal windows

Some users keep autoISF active only during the day (or only at meal times), and run vanilla HCL — without ISF adaptation — overnight.

Two ways to do it:

- **Automation on**: define time windows when "Enable ISF adaptation by glucose behavior" turns ON; rest of the day it's off.
- **Automation off**: conversely, turn it off at bedtime and on in the morning.

This is a common starting pattern — especially valuable in your first weeks, when you want aggressive FCL for dinners but peace of mind overnight.

### Odd targets during quiet hours

A simpler alternative: set an **odd-numbered profile target** for the hours you want SMBs blocked (e.g., night hours).

- autoISF keeps running.
- Temp basal still adjusts insulin delivery dynamically.
- But no SMBs fire during the odd-target hours.

This is the author's preferred night-time solution, especially for users who get compression lows at night. The loop stays "awake" enough to handle light corrections but can't overreact to a bg jump caused by rolling onto the sensor.

> 💡 **Allowing a few SMBs anyway** — e.g., after a late fatty meal that might plateau high. Define an Automation that temporarily sets an *even* target under specific conditions (bg high, iob low, late at night). Use short durations; the same Automation will retrigger if conditions persist.

### Different settings by time slot

You can differentiate by time of day via Automations that set different values for:

- `iob_threshold_percent`
- `bgAccel_ISF_weight`
- Enable/disable ISF adaptation
- (plus TT and %profile, always)

Example use cases:

- Breakfast at home: standard settings.
- School lunches: milder bgAccel to avoid over-treating a quick cafeteria snack.
- Dinners at home: highest iobTH for big meals.

> ⚠️ **Most users don't need this.** Unless your meals differ dramatically by time slot, the circadian profile_ISF alone (your hourly ISF schedule) handles the natural differences between breakfast, lunch, and dinner. Try to tune one broader spectrum first (Chapter 4). Only differentiate if that genuinely fails.

### Activity Monitor

The Activity Monitor uses your phone's step counter to auto-adjust insulin sensitivity for recent (last ~60 minutes) activity levels. See §6.6 for tuning details.

Enabling it in Preferences → OpenAPS SMB → "Activity modifies sensitivity" gives you automatic hands-off handling of things like "I walked the dog after lunch" or "I've been on the couch all afternoon." It's capped at +20% insulin (for detected inactivity) and −30% (for activity).

**For users whose daily variability is mostly step-count driven, this single feature can close most of the gap toward truly 24/7 hands-off FCL.**

### How hands-off can FCL really be?

Fully hands-off 24/7 FCL is achievable for adults with:

- Stable technical setup (cannula, CGM, Bluetooth).
- Moderate and relatively regular meals.
- Moderate %TIR expectations (upper 70s to low 80s).
- Some willingness to use an Automation or two for recurring situations.

It's less realistic for users with highly varied meals, heavy sports, or extreme %TIR goals. For those, expect to do some nudging (§5.3–7.4).

## 5.3 Manual modulation — the "FCL cockpit"

Your AAPS home screen has three buttons at the top: **%profile**, **Exercise**, **TT**. In FCL these are your cockpit — the fastest way to adjust loop behavior without going into Preferences.

### The three top buttons

| Button    | Grey means       | Yellow means                                               |
|-----------|------------------|------------------------------------------------------------|
| %profile  | 100% profile     | Temporary %profile active (<100% softer, >100% sharper)    |
| Exercise  | Off              | On — dynamic exercise mode armed (needs elevated TT to activate) |
| TT        | No temp target   | Temp target active (color also hints at above/below profile target) |
|           |                  |                                                            |

All three buttons yellow (`YYY` or `yyy` depending on direction) is the "exercise mode with modified profile" combination. All three grey (`GGG`) is default profile operation.

> 📖 **The full color-combination table** (read only if you're curious)
>
> Lowercase `y` means softer than default; uppercase `Y` means more aggressive. Position matters: `%profile / exercise / TT`. So `YGY` = elevated profile × no exercise × elevated TT (unusual), `yyy` = softened profile × exercise × elevated TT (classic exercise combination).
>
> Most users only use three real combinations:
> - `GGG` — default.
> - `yyy` or `Gyy` — exercise with TT, optionally softened profile.
> - `GGY` — lowered TT (e.g., EatingSoonTT) for more aggressive response.
>
> The remaining combinations exist for special cases. Don't memorize them; look them up if needed.

### Quick mode changes

**Temporary %profile.** A single number that scales everything.

- 110% for an afternoon when you feel resistant → slightly sharper everywhere.
- 80% for the evening after a heavy exercise day → slightly softer everywhere.
- Safety limits (Chapter 3) must be wide enough that a 110% doesn't get cut off.

**Temporary target (TT).** Use this freely:

- Low TT (e.g., 74 mg/dL) → loop aims for a lower target and applies sharper ISF. Common "EatingSoon" usage.
- High TT → loop aims higher and softens ISF. Common for exercise.
- **Even** vs **odd** target — remember, odd numbers block SMBs.

**Exercise button.** Toggle with the middle top button. When on *and* a TT above profile target is also set, the dynamic exercise mode activates — see Chapter 6 for the math.

### Temporary settings in Preferences

Sometimes you want to change an `ISF_weight` or `iobTH_percent` value directly. You *can* — go into Preferences, enter your password, make the change. But this route has real problems:

1. It requires multiple taps and a password.
2. You will forget to change it back.

For this reason, **use the three top buttons (TT / %profile / exercise) for temporary adjustments.** They revert on their own. Save Preferences edits for permanent tuning changes.

## 5.4 The "DIY cockpit" — custom buttons from User Action Automations

You can add your own buttons to the bottom of the AAPS home screen by defining an Automation with the **"User action"** checkbox ticked. The button appears only during the time window you configure, and only while any other conditions you set remain true.

This is how you pre-program responses to recurring situations.

### A snack button

Suppose you sometimes have a 15g fast-carb snack in the afternoon. You don't want the loop to treat it like a full meal:

1. Create an Automation named "Snack 15g fast-C."
2. Set **User action** = ticked. Configure a time window (e.g., 2 PM – 6 PM) when the button should appear.
3. Under **Actions**:
   - Set a low TT (e.g., 74 mg/dL) for ~20 minutes (sharpens the initial SMBs).
   - Raise `bgAccel_ISF_weight` briefly (or set a temporarily higher %profile).
   - **Lower `iob_threshold_percent`** to prevent over-insulinization (e.g., to 35%).
4. Save.

Now, any afternoon you're about to snack, you tap the button and your loop will handle the snack differently.

> ⚠️ **Critical: iobTH and bgAccel_ISF_weight do not auto-revert.**
>
> Setting a low `iob_threshold_percent` via an Automation **permanently shifts it** until something else puts it back. You need a **tandem Automation** — see §5.5.

> ⚠️ **Don't press the snack button twice.** The lowered iobTH won't allow enough iob for a full meal. If you find yourself snacking more than planned, just let the regular meal response run instead.

### Other cockpit button uses

- **Exercise announcement** — see §6.4.
- **Meal-before-exercise** — the tricky scenario in §6.5.
- **Sweet drink** — like the snack, but with different settings.
- **"Pause FCL"** — briefly disable ISF adaptation, for a difficult situation.

### Managing your Automation list

Over time your list grows. Discipline:

- **Shelve unused Automations** — untick the top-left checkbox to make them inactive. They stay in the list for reactivation but don't execute.
- **Review periodically** — if you haven't used an Automation in months, remove it.
- **Make evening a review habit** — before bed, glance at what's active for tomorrow. Turn on what you'll need; shelve what you won't.

## 5.5 The tandem Automation pattern — critical

Many Automation Actions (iobTH_percent, bgAccel_ISF_weight, ISF adaptation on/off) **cannot be set with a duration**. Once your Automation runs, that setting stays changed forever, until something else restores it.

The solution: a second Automation, running in tandem, whose job is to **restore the default value when the first Automation's conditions are no longer met**.

### How to structure it

Imagine you have several Automations that might lower your `iob_threshold_percent` (snack mode: 35%, exercise-after-meal: 40%, etc.). Your default is 60%.

Create one restore Automation:

- **Conditions:** iob_threshold_percent > 45% (or whatever's higher than any lowered value), AND no TT active, AND time window is back to normal.
- **Action:** Set iob_threshold_percent = 60%.

This runs after any of your lowering Automations time out.

### Automation interactions

A set TT often **blocks other Automations** from running. This is by design — once you're in a "special mode," you don't want random Automations overriding your manual choice. Consequences:

- Short TT durations are better. If your conditions still apply, the Automation will simply retrigger.
- Sequence matters — if you have many Automations, the loop evaluates them in order.
- If you need an Automation to run *during* a TT, think carefully about whether that's right, and build a test for it.

> 💡 **Don't build loops inside your loop.** If you find yourself writing Automations that rapidly set low TTs, then cancel them, then trigger other Automations based on bg deltas — stop. You're likely duplicating what autoISF already does internally, only 5 minutes late. Fix the underlying weight instead.

## 5.6 Temporarily exiting FCL

Sometimes the best move is to stop FCL entirely and go back to manual meal bolusing.

### Three ways to exit

1. **Switch off ISF adaptation.** Preferences → OpenAPS SMB → autoISF settings → "Enable ISF adaptation by glucose behavior" = OFF. Fastest complete shutdown.
2. **Temporarily set `bgAccel_ISF_weight` to 0.** Keeps dura_ISF and the rest working, but disables the aggressive first-SMB behavior.
3. **Tap the loop icon** (violet circle → green circle) if your AAPS version includes this UI feature. This will switch the Overview buttons back on too.

After exiting, you need to remember to:

- **Re-enable the insulin button** (Preferences → Overview → Buttons → Insulin) to manually bolus.
- **Bolus for meals yourself.**
- **Re-enable FCL when ready** — nothing does this automatically.

### A "Pause FCL" button

Because forgetting to re-enable is common, consider a User Action Automation with:

- **Conditions:** User action, time window, short duration.
- **Action:** Set `bgAccel_ISF_weight` = 0.
- **Tandem restore Automation:** restores the weight to your tuned default after the time window.

This gives you a fast pause that automatically ends.

> ⚠️ **Test it.** The User Action Automation feature for time-limited FCL pause is newer. Verify yours reverts correctly before you rely on it.

## 5.7 Recognizing the current loop state

At any moment, four places tell you what your loop is actually doing:

1. **The three top buttons** (§5.3) — yellow or grey.
2. **The `ai: %` indicator** under Autosens% on the home screen — shows whether autoISF is adapting right now.
3. **The AUTO ISF tab** — full detail on the most recent loop decision, including:
   - Starting profile_ISF (including any Activity Monitor or TT adjustment).
   - Each component's contribution (acce / pp / bg / dura).
   - Final effective ISF (`sens`).
   - Effective iobTH in use.
   - Whether any safety limit capped the SMB.
4. **Optional extra graphs** below the main AAPS glucose chart — iobTH corridor, ISF factor contributions, fitted parabola.

Between these, you should always be able to answer "why did the loop do that?"

## 5.8 Managing snacks — a worked example

Snacks are the most common situation where users need modulation. A summary of your options:

| Snack type                             | Best handling                                    |
|----------------------------------------|--------------------------------------------------|
| Small anti-hypo snack (glucose tabs)   | Odd TT for ~30 min to block SMBs.                |
| Small, slow, low-carb snack            | Let FCL handle it. Check iob to be sure.         |
| 15–30g fast-carb fun snack (ice cream) | DIY cockpit button — low iobTH, sharper weights. |
| Multi-snack situation (evening grazing)| Set 80–90% %profile for a few hours + mindfulness.|
| Mid-sports snack                       | See Chapter 6. Usually odd TT + no special action.|

Case Study 5.2 (Sweet snacks / Glühwein with DIY cockpit) gives a detailed worked example.

## 5.9 Summary

- Five levers, three buttons, and a handful of well-designed Automations handle nearly every non-meal situation.
- Keep Automations few and simple. Always pair aggression-changing Automations with tandem restore Automations.
- Use odd TT as your emergency brake.
- Pause FCL if things feel wrong — re-enable when ready.
- Consult the AUTO ISF tab any time you're confused about what the loop is doing.

# Chapter 6 · Exercise and Activity
Exercise is the single biggest source of unplanned hypoglycemia in any looping setup. This chapter covers the tools autoISF gives you for it.

The key insight: **you cannot prepare for exercise the way you did in HCL**, because FCL is tuned to react to rising bg with aggressive insulin. Setting a pre-exercise high TT before a meal would sabotage the meal response. Setting one after the meal starts is too late — the aggressive insulin is already on board.

autoISF gives you three tools to navigate this:

1. **Dynamic iobTH** — the iob ceiling auto-adjusts based on TT and exercise button.
2. **Temporary %profile switch** — scales everything down.
3. **The "DIY cockpit" + Automation sequence** — pre-programs the whole thing into one button press.

## 6.1 You don't need every tool here

Skim the sections below, then focus on what applies to you:

- **Light exercise only** (dog walks, gardening, light housework) — the **Activity Monitor** (§6.6) probably handles you. Skip to that.
- **Regular specific exercise** (biking, gym, hikes) — you'll use Dynamic iobTH (§6.2) and the DIY cockpit (§6.4).
- **Occasional unusual exercise** — the cockpit button (§6.4) can be pre-configured and then activated only on those days.

You can also always drop back into HCL and handle exercise the traditional way while you're setting up FCL.

**At the bare minimum, keep snacks on hand.** That is always the fallback.

## 6.2 Dynamic iobTH — the main exercise tool

Dynamic iobTH is how autoISF recognizes exercise: when both the exercise button is on *and* the active TT is above profile target, the iob ceiling drops automatically. No extra Automation needed.

Two inputs control how aggressive the drop is:

- **`half_basal_exercise_target`** in Preferences → OpenAPS SMB. Default 160 mg/dL. **Lower values produce more aggressive softening.**
- **The TT you set** for the specific exercise (plus the exercise button being on).

### What happens during exercise

When exercise mode is active (exercise button yellow + TT above profile target), everything scales by a single factor called `sens.ratio`:

- `temp basal = profile basal × sens.ratio`
- `temp ISF = profile ISF / sens.ratio` (softer, i.e., higher)
- `temp iobTH = set iobTH × sens.ratio`

A `sens.ratio` of 0.5 means half the basal, half the iobTH, and double the ISF for the duration.

### The math

The formula is `sens.ratio = (HBET − 99) / ((HBET − 99) + (TT − 99))`, where HBET is your half-basal exercise target. Picking your TT and HBET together picks your `sens.ratio`:

| half-basal target →  | 180   | **160 (default)** | 140   | 120   |
|----------------------|-------|-------------------|-------|-------|
| **TT = 100**         | 1.00  | 1.00              | 1.00  | 1.00  |
| **TT = 120**         | 0.79  | 0.74              | 0.66  | 0.50  |
| **TT = 140**         | 0.66  | 0.60              | 0.50  | 0.34  |
| **TT = 160**         | 0.57  | 0.50              | 0.40  | 0.26  |
| **TT = 180**         | 0.50  | 0.43              | 0.34  | 0.21  |

(The constant 99 is AAPS's internal "normalTarget." It changed from 100 to 99 in AAPS 4.2.1 to accommodate mmol/L users; the effect on `sens.ratio` is small.)

### Worked example

Your settings: iobMAX 10U, iobTH 60% (= 6U), profile ISF 39 mg/dL/U, half-basal target = 160 (default).

Scenario: exercise button on, TT = 160 mg/dL.

- `sens.ratio = (160−99) / ((160−99) + (160−99)) = 0.50`.
- Temp iobTH = 6U × 0.50 = **3.0U**. Temp ISF = 39 / 0.50 = **78 mg/dL/U** (softer).

Add a 70% %profile on top and the effects multiply: temp iobTH = 3.0 × 0.7 = **2.1U**. That's about a third of your normal insulin ceiling — a meaningful guardrail during exercise.

### What to look up

You don't have to compute any of this. Open the AUTO ISF tab (or the graph that plots iobTH over time) and you'll see:

- Profile ISF.
- Modifying factors currently active (Activity Monitor, %profile, TT, exercise mode).
- Effective ISF in use.
- Effective iobTH in use.

Every time you change a TT or the exercise button, glance at the AUTO ISF tab to confirm the loop is in the state you intended.

### Tuning the exercise setup

Personalize step by step:

1. Set `half_basal_exercise_target` in Preferences. **Lower number = more dynamic range.** Start at the default 160; lower only if you need more softening at moderate TTs.
2. For each kind of exercise you do regularly, find a TT that produces the right amount of softening. Mnemonic: choose a memorable number so "TT = 140 = my jogging TT" is easy to remember.
3. Iterate across a few sessions.

### Even vs odd exercise TT

An odd-numbered TT (e.g., 141, 159) blocks SMBs entirely; an even TT (140, 160) allows them but softened. Which you pick matters:

| Choice       | Behavior                                             | Use when...                                                  |
|--------------|------------------------------------------------------|--------------------------------------------------------------|
| **Odd TT**   | No SMBs at all during exercise                       | Calm, steady activity; want zero chance of SMB interfering   |
| **Even TT**  | SMBs allowed, but softened via reduced sens.ratio    | Adrenaline-heavy sports; occasional spikes you'd like treated|

Odd TT is simpler and often the right default. It does have downsides: once set, any Automation that requires "no TT active" won't run; and a brief automatic SMB (for an unexpected spike) is impossible. Know your exercise pattern.

### Manual iobTH (rarely needed)

You *can* change `iob_threshold_percent` directly in Preferences for exercise. The author doesn't recommend it:

- Multiple taps + password.
- You will forget to change it back.
- The dynamic mechanism above does the same job automatically.

Skip this route unless you have a specific reason.

## 6.3 Temporary %profile switch

The %profile switch (top-left button on the AAPS home screen) multiplies **basal, ISF, and iobTH** by a fixed percentage. Easy, complementary to the TT/exercise mechanism.

Common uses:

- Before/during/after exercise: 70–80% profile for a few hours to days, to cover "long-waved" sensitivity increase.
- During the day after a long sports day: 80% profile.
- Brief meal-specific nudge: 60% profile for 45 minutes at a low-carb meal.

%profile effects multiply with the exercise-mode sens.ratio. You can stack both for maximum softening during high-intensity exercise.

**Caveat:** a reduced %profile also reduces max SMB size (because it shrinks basal). At exercise this is usually desired, because you don't want big SMBs while already running soft.

## 6.4 The DIY cockpit for exercise

For exercise you do regularly, prepare a custom button. Click once, get the full setup.

### A simple exercise button

User Action Automation:

- **Conditions:** User action ticked; time window when you might exercise (e.g., 4 PM – 8 PM if you bike after work).
- **Actions:**
  - Set an exercise TT (e.g., 140 mg/dL) for 1–2 hours.
  - Turn the exercise button on (yellow).
  - Set %profile = 80% for 2 hours.

Tap the button when you're about to start exercise. Everything above activates.

### Dynamic vs traditional mode

Two ways to soften the loop for exercise:

- **Traditional mode** — %profile reduced and a TT set, but the exercise button stays grey. You get manual softening from the %profile, with the TT as an extra lever. No dynamic `sens.ratio`.
- **Dynamic mode** — exercise button on (yellow). The `sens.ratio` from §6.2 applies, giving much stronger softening at moderate TTs.

**Use dynamic mode.** It's more precise, and you tune it through one parameter (the half-basal exercise target) instead of guessing profile percentages.

### When to set it up

Before your next planned exercise. Even a rough first version is better than nothing. Refine after each use.

## 6.5 Exercise after a meal — the tricky one

This is the hardest scenario in FCL and deserves careful handling.

### The problem

In HCL you'd reduce your meal bolus. In FCL you don't give a meal bolus — but you also can't pre-set an exercise TT, because that would sabotage the aggressive initial response to the meal.

You want **full meal response** for the initial rise, **capped early** so exercise doesn't have too much insulin working.

### Manual approach

1. Before the meal: **lower `iob_threshold_percent`** (e.g., from 60% to 40%). Keep everything else normal.
2. After iobTH is exceeded (approximately when the first meal SMBs finish): **set an elevated TT** and the exercise mode.

The first step caps how much iob accumulates. The second kicks in the dynamic exercise behavior.

The problem: two interventions, one of them time-critical. You'll forget or mistime it.

### Automated 3-step sequence

This is the recommended pattern. Three Automations, only one of which you trigger manually.

**Automation #1 — "Meal before exercise" (User Action):**
- Conditions: User action ticked; meal-window time slot; no TT active.
- Actions: Lower `iob_threshold_percent` to your exercise value (e.g., 40%). Optionally raise `bgAccel_ISF_weight` briefly (full aggressive initial response).
- Tap this button before your pre-exercise meal starts.

**Automation #2 — "Meal served — switch to exercise mode" (Automatic):**
- Conditions: iob has exceeded the lowered iobTH (or a proxy signal: iob > 4U, the elevated bgAccel flag still set, etc.).
- Actions: Set %profile = 70%. End any active TT — a new one has to be set fresh in #3.

**Automation #3 — "Activate exercise TT" (Automatic):**
- Conditions: %profile just switched to 70% *and* no TT is currently active.
- Actions: Set the exercise TT (e.g., 125 mg/dL) for the exercise duration.

Now one button tap at meal start handles:
1. Full meal response.
2. Early iob cap.
3. Transition to exercise mode.

See Case Study 6.2 for a detailed worked example.

### The laissez-faire option

Simpler but less optimal:

- Set an elevated TT + exercise mode **before** the meal.
- Accept that the meal peak will run higher than usual.
- Especially works if the meal is protein/fat-heavy (slow absorption), or if you're OK starting exercise at a higher bg.

Logic: for fast-carb meals you want FCL aggressive up to a lowered iob cap, like a reduced HCL bolus. For slow meals at modest bg peaks, pre-softened FCL is perfectly fine.

Choose based on your own pattern.

## 6.6 Activity Monitor — step-counter-driven adjustment

The Activity Monitor uses your phone's step counter to quietly nudge insulin sensitivity based on recent activity — no buttons, no Automations, just a small continuous adjustment.

### When it runs

- **Enabled** in Preferences → OpenAPS SMB → "Activity modifies sensitivity" + set scaling factors.
- **Active** whenever no TT is running.
- **Pauses silently** when any TT is set (so exercise mode takes over cleanly). Resumes the moment the TT expires.

### What it adjusts

Step count over the last ~60 minutes → small automatic adjustment of:

- Basal
- ISF
- iobTH

All proportional. All capped: at most +20% insulin for detected inactivity, at most −30% for detected activity.

### Why use it

If your daily sensitivity variation is mostly driven by "desk day vs walking day," the Activity Monitor handles it automatically in a ~60-minute feedback loop. This is **much faster than Autosens** (8–24 hours) and is one of the things that makes hands-off FCL feasible.

### Tuning the scaling factors

Set scaling factors in Preferences. You personalize them to how your own body responds to gentle activity. The autoISF Quick Guide (page 9) covers the mechanics.

Rough approach:
1. Turn Activity Monitor on with starting factors.
2. On a few typical days (some walking-heavy, some sedentary), check the AUTO ISF tab to see what it's doing.
3. If it over-softens during light walks, reduce the activity factor.
4. If it doesn't soften enough, increase the activity factor.
5. Same for inactivity.

### A side benefit for snacks

If you sometimes use brief even/odd target switches (e.g., to sneak in a small snack without an SMB), the Activity Monitor resumes its work immediately after the TT ends. You don't lose your step data.

## 6.7 Summary

- **Dynamic iobTH + exercise TT + half-basal exercise target** are the core exercise tools.
- The **3-Automation pattern** handles the "meal before exercise" problem with one button tap.
- The **Activity Monitor** handles ordinary daily variation automatically.
- Keep **odd-TT** as your emergency SMB shutoff during surprise exercise.
- **Snacks on hand** are always the fallback. Never trust any configuration enough to skip that.

# Chapter 7 · Advanced HCL with Meal Announcement
Full Closed Loop is not the only good destination. For many users — and especially for children, or for adults who lack one of the FCL prerequisites — a smarter hybrid loop with **Meal Announcement (MA)** is a better fit.

This chapter describes how to use autoISF in a hybrid loop where you still give a bolus at meal time, but skip carb counting. Most of the setup overlaps with FCL. The differences are what this chapter is about.

## 7.1 What Meal Announcement is, and who it's for

**Meal Announcement (MA) mode:** you give a small pre-meal bolus (or a full meal bolus), but you do not enter carbs. autoISF's ISF modulation does the rest.

It sits in the middle ground:

- **More than HCL:** less per-meal thinking than full HCL, because you don't need to count carbs or calculate bolus sizes precisely.
- **Less than FCL:** you still bolus at meal time, so you don't get the hands-off experience.

### Who it's a good fit for

- **Children**, where Lyumjev tolerance, basal rates, or caregiver coordination make full FCL risky.
- Anyone who can't tolerate Lyumjev or Fiasp well — MA accommodates slower insulins because you're bolusing.
- **Users without perfect Bluetooth discipline** — MA gives you a safety margin when a few minutes of lost connection won't immediately sink the meal.
- **Users with leaking pods or occasional pump reliability issues** — MA tolerates these better than FCL.
- **Users with jumpy CGMs** — MA doesn't need aggressive early acceleration detection.
- **Users with very low hourly basal** — MA doesn't require super-boosted SMBs.
- **Anyone transitioning** who isn't ready to commit to full FCL.

MA can also be a **staging post**. Set up your system for MA first; move to full FCL later if and when the missing prerequisites fall into place.

## 7.2 Hurdles for FCL, and how MA bridges them

| FCL deficit                                                          | Bridging via MA                                                                                                  |
|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Lyumjev/Fiasp not tolerated, or frequent occlusions                  | Pre-bolus with a different insulin, even via pen (with manual AAPS entry). Different cannulas / pods may help.  |
| Poor 24/7 Bluetooth discipline                                       | The meal bolus + profile basal cover most of the meal even if Bluetooth drops.                                  |
| Leaking pods                                                         | Pre-bolus (via pen if needed) bypasses the worst failure moments.                                               |
| Jumpy CGM                                                            | Use stronger smoothing and a much weaker bgAccel_ISF_weight — MA doesn't need early aggressive action.           |
| CGM doesn't allow "SMB always" at cob = 0                            | Dexcom and Libre 3 both work. MA has cob > 0 immediately after bolus, avoiding this edge case.                  |
| Very low hourly basal                                                | No need for boosted SMBs — the bolus covers the meal.                                                            |
| Erratic sweet drinks and snacks                                      | Much less of an issue when a bolus is given with the drink; bgAccel_ISF stays dialled softer.                   |

## 7.3 Optimize your HCL first

Before setting up MA, your HCL needs to be in good shape. The same rules apply as for FCL:

1. **Switch off dynamicISF.** Ignore Autotune. Make sure your profile parameters are correct.
2. **Meal management tuning:** check that your ISFs handle the rising bg after your meal bolus loses power.
3. **With correct ISFs, expand SMB sizes to 120 minutes of basal.**
4. **Handle fatty-meal insulin resistance.** Two options:
   - An Automation that increases %profile at signs of post-meal fatty acid resistance (see the AAPS readthedocs "Stagnation at high bg values" section).
   - Switch to the autoISF dev variant of AAPS, with **only the dura_ISF component enabled** (leave the other ISF weights at 0 or off).

Resources for HCL tuning: https://github.com/bernie4375/HCL-Meal-Mgt.-ISF-and-IC-settings

Once your HCL is satisfying, proceed.

## 7.4 Setting up MA with autoISF

Follow Chapters 5 and 6, but with **softer settings throughout**. You still get a bolus, so autoISF doesn't need to be as aggressive.

**Critical differences from FCL settings:**

| Setting                            | FCL recommendation              | MA recommendation                                      |
|------------------------------------|----------------------------------|--------------------------------------------------------|
| `smb_max_range_extension` (Ch. 5) | 2.0–3.0                          | Lower — your bolus covers most insulin need           |
| `autoISF_max` (Ch. 5)              | 2.0                              | Lower — say 1.5                                        |
| `bgAccel_ISF_weight` (Ch. 6)       | Tune aggressively                | Much softer — aggressive action not needed            |
| `smb_delivery_ratio` (Ch. 5)       | 0.6–0.7                          | **Keep at 0.5** (especially with remote bolusing)     |
| `iob_threshold_percent` (Ch. 5)    | ~60% or as tuned                 | Same discipline — install it, do not skip             |

> ⚠️ **For remote bolusing setups (parent + child via NSClient):** do **not** raise `smb_delivery_ratio` above 0.5. If a parent initiates a bolus remotely while autoISF is also delivering SMBs, an elevated delivery ratio amplifies the risk of insulin overlap.

> ⚠️ **Always install your iobTH** (Chapter 3, §3.4). MA is safer than FCL in most respects, but that's precisely because it uses fewer aggressive tools — iobTH is still essential.

## 7.5 Pre-bolussing strategies

Once the basics are in place, the main design decision in MA is: **how much to pre-bolus, and how long before the meal.**

### The full meal bolus

Same as classic HCL, no carb entry: you give a calculated meal bolus 10–20 minutes before eating. autoISF runs in the background and supplements with SMBs if glucose behaves unexpectedly.

**Pros:** familiar; minimal thinking; reliable outcomes.
**Cons:** you're still counting carbs mentally, even if you're not entering them. You're doing most of the work that a full FCL would do for you.

**When to use it:** meals where you're confident of your carb estimate, especially meals with fast absorption.

### The small pre-bolus

A strategy halfway between FCL and full HCL: give a small, fixed pre-bolus (e.g., 2–3U, or 25–50% of your usual meal bolus) 5–10 minutes before the meal. autoISF handles the rest via SMBs.

**Pros:** less mental effort than counting carbs. Still kicks autoISF into the right zone.
**Cons:** tuning the fixed pre-bolus size is personal. Over-pre-bolusing on a smaller meal can hypo you; under-pre-bolusing leaves autoISF with too much catch-up work.

**When to use it:** for consistent meal patterns where you can calibrate the pre-bolus once and forget.

### Conclusions on pre-bolussing

> 📖 **To pre-bolus or not to pre-bolus?**
>
> A short developer paper addresses this question, available in the autoISF repo: *To prebolus or not to prebolus…* (https://github.com/ga-zelle/autoISF).
>
> The tradeoff: a pre-bolus gives you a head start on the glucose rise, but the insulin on board from the pre-bolus creates a "gap" later (zero-temping) that makes late-meal management trickier. What you gain in peak height, you partly lose in hand-over quality from bolus-dominant to SMB-dominant management.
>
> Further investigations by MA users are welcome. The "best" answer depends on your meal variability and pre-bolus consistency.

## 7.6 Disturbances, sensitivity, and exercise in MA

All the tools from Chapters 7 and 8 apply:

- **Manual nudging** (§5.3) — odd TT, %profile, bg target.
- **Automations** (§5.2) — for recurring situations.
- **Custom cockpit buttons** (§5.4) — for your "DIY cockpit."
- **Exercise** (Chapter 6) — simpler in MA, because you can just reduce the meal bolus.

**For exercise specifically in MA:** you handle exercise the traditional HCL way — reduce the meal bolus ahead of exercise. The "exercise after meal" problem from §6.5 is much simpler, because the reduced bolus itself provides the needed iob cap.

You still benefit from dynamic iobTH and the exercise mode for exercise that happens independently of meals.

## 7.7 MA for children and remote-control setups

Many of the challenges of FCL for children apply to MA as well, but to a lesser degree:

- **Sharp sensitivity or circadian changes** — set appropriate temporary or scheduled profile percentages; MA is less demanding on profile accuracy than FCL.
- **24/7 Bluetooth discipline** — giving meal boli (plus reliable profile basal) reduces the stakes of brief connectivity loss. Install an alarm on the caregiver's phone for disconnections.
- **Caregiver coordination** — keep `smb_delivery_ratio` at 0.5 as noted above. Communicate about who is bolusing and when.

For kids, MA is often the realistic destination — not a stepping stone to FCL — because the prerequisites for FCL (site discipline, BT discipline, 24/7 vigilance) are genuinely harder.

## 7.8 Final thoughts

> 💬 **Where the author stands**
>
> I'm genuinely uncertain whether the effort of setting up MA is worth it compared to either (a) a well-tuned vanilla HCL with sloppy carb inputs, or (b) going all the way to full FCL.
>
> MA probably offers a higher safety level than FCL, especially when the full set of FCL prerequisites aren't permanently guaranteed. The reduced daily vigilance may itself be worth it for some users.
>
> Looking at your own situation honestly — what's missing for full FCL, and how long will it take to fix — is the best guide.

Other algorithmic routes that also use Meal Announcement-style workflows are covered in the next chapter (Boost, AIMI, EatingNow, Tsunami).

# Chapter 8 · Other Avenues to Full Closed Loop
This chapter surveys alternatives to autoISF FCL. Each section is intentionally brief — if one of them matches your situation, follow its links for the full story.

## 8.1 FCL with AAPS Master and Automations (the simple FCL)

Since autumn 2023, AAPS Master has supported Full Closed Loop as an official option. It uses personalized Automations to elevate iob when a meal-related rise is detected — no autoISF required.

**Prerequisites** are similar to autoISF FCL (see Chapter 1): fast insulin, excellent CGM, stable technical setup, well-tuned HCL as a starting point. Full details: https://androidaps.readthedocs.io/en/latest/Usage/FullClosedLoop.html

**What you give up vs. autoISF FCL:**

- Less sophisticated meal detection (relies on delta thresholds instead of parabola-fitted acceleration).
- No automatic dura_ISF-style plateau handling (you'd build that manually via Automations).
- Less peak-shaping precision.

**What you gain:**

- Dramatically simpler setup. No 18 tuning parameters.
- Fewer ways things can go wrong.
- Widely published results — a randomized cross-over study (PubMed: *First Use of Open-Source Automated Insulin Delivery AndroidAPS in Full Closed-Loop Scenario; Pancreas4ALL Randomized Pilot Study*) and an ongoing 2025 Australia/NZ study (CLOSE IT trial protocol) both show respectable outcomes.

**A useful hybrid:** run the **autoISF dev variant of AAPS** with `"Enable ISF adaptation by glucose behavior"` OFF. You keep the benefits of `smb_max_range_extension` and `smb_delivery_ratio > 0.5` for stronger SMB boosting, but drive the whole system via Automations rather than autoISF's ISF modulation. See the comparison in Case Study 13.1.

**This method is strongly recommended** for users who want an entry into FCL without the full autoISF set-up project. Many users achieve ~80% time-in-range this way.

## 8.2 FCL with dynamicISF

dynamicISF is available in AAPS (dev variants) and in Trio/iAPS. Unlike autoISF's bgAccel_ISF, it does **not** boost SMBs on detected acceleration — it's a slower, bg-level-driven ISF modulator, conceptually closer to Autosens but with much more dynamic range.

**For FCL use:** dynamicISF can be stretched into an FCL tool, but it has an inherent timing disadvantage — it responds to **bg level**, not to **acceleration or delta**. That means it's late to the party for meal detection.

It may suit users who:

- Have strong sensitivity swings they can't proactively predict.
- Don't want to tune 18 autoISF parameters.
- Are comfortable with an FCL that gets to the right answer a bit late.

**It does not suit users who:**

- Want best-in-class peak height control.
- Have a high-carb, fast-absorbing diet.

Case Study 13.2 would be a valuable addition — if you use dynamicISF for FCL successfully, please submit one with a week of 24h scatter data plus an analyzed meal showing when and how dynamicISF built iob.

Resources:
- AAPS: https://discord.gg/DfvK5HnxXu (search "dynamicISF")
- Trio/iAPS: https://discord.gg/gGKXW5uX3m (section `dynamic-isf-cr`)

## 8.3 Meal-Announcement dev variants: Boost, AIMI, EatingNow, Tsunami

Several AAPS-derived dev branches implement their own meal-handling approaches. All of these are actively evolving; consult their docs for current state.

### Boost

Boost adds code around SMB calculation with a daily "Boost window" during which the extra logic is active.

- Uses a variant of dynamicISF with predicted-bg weighting (40–75%) to mimic higher sensitivity at lower bg.
- Can trigger early boluses from delta and average-delta accelerations when iob is below a user-set threshold — so it can work with or without meal announcement.
- Max "Boost Bolus Cap" set as a percentage of TDD (default 2.5%, up to 5%) for safety.
- The AAPS default 50% `smb_delivery_ratio` can be overwritten with a higher value ("Boost insulin required percent"), suggested ≤75%.
- Automatically stops when delta and average deltas align (steep rise has become a steady rise).

Boost's acceleration-based trigger is conceptually similar to autoISF's bgAccel_ISF route. With an excellent CGM, autoISF detects acceleration slightly earlier and can boost more strongly. Boost is simpler to configure for users who don't want to tune 18 parameters.

See Case Study 13.3 for a Boost-based FCL for a child.

### AIMI

AIMI is another dev variant available for AAPS and ported into Trio. Uses a meal-announcement workflow with its own acceleration-based aggressive response.

- https://discord.gg/tPDQzS3Bq3
- Trio port: https://github.com/mountrcg/Trio#aimi-b30

### EatingNow

EatingNow is another AAPS dev variant with a Meal Announcement workflow. Active development; check the AAPS Discord and associated repos for current status.

### Tsunami

Tsunami is another AAPS dev variant. Also active development; same guidance — check current community resources.

> 💡 **On all these variants:** they're real, legitimate, sometimes excellent — but they're each somebody's active side project. Documentation quality varies. Community support is thinner than for AAPS Master or the autoISF tree. Factor this into your decision.

## 8.4 No-bolus looping with precise carb inputs

A philosophically opposite approach: give **precise** carb inputs (with absorption times) to the loop, but **no boluses** at all. The loop handles everything via SMBs based on the carb information.

This is the traditional iOS Loop approach, and some "pro" iOS Loop users achieve impressive time-in-range (and time-in-tight-range) performance this way — at the cost of meticulous carb accounting.

**Not recommended for casual use.** It demands constant mental load for carb estimation and absorption-time input. It does not eliminate meal-time thinking — it just shifts the work from "what size bolus?" to "how many grams, absorbing how fast?"

## 8.5 Future directions: ML and dual hormones

### Machine Learning / AI

There's ongoing interest in building a self-learning loop. Industry will likely produce a first-generation commercial solution aimed at users with poor HbA1c and weak meal handling — a safe gradual improvement over standard therapy, but not top-tier performance.

**A top-performing self-learning system may be genuinely hard to design**, because:

- Self-learning relies on past data, which breaks down when you do something different today (fasting day after a feast day, new job schedule, travel).
- Self-learning systems don't teach the user how they work, so the user can't intelligently adjust for situations the system hasn't seen.

This is the opposite of the FCL philosophy in this book — here, the user understands the system and adjusts it deliberately.

### Dual hormone systems

Many see dual-hormone (insulin + glucagon) FCL as the ultimate system. The glucagon component would cover the largest current limitation: that zero-temping is a weak tool against impending hypos.

**What dual hormone could enable:**

- More aggressive insulin treatment for highs, because glucagon backs up hypo prevention.
- No weight-gain concerns from roller-coasters (glucagon stimulates glucose release, not caloric intake).
- Potentially dramatically simpler exercise management.

**What's in the way:**

- Extra device complexity (a second cartridge / pump).
- Significant extra cost.
- Unknown real-world handling by typical users.

> 📖 **Off-topic note:** there's also research on adding very small amounts of a glucagon analogue to an insulin cartridge as an *additive* to make Lyumjev act even faster. That would be valuable for FCL even before dual-cartridge systems become mainstream. Background: "Insulins, DIA…" PDF in https://github.com/bernie4375/HCL-Meal-Mgt.-ISF-and-IC-settings

## 8.6 Co-medications that facilitate FCL

### GLP-1 receptor agonists

The drugs most of the world knows as weight-loss medication are also interesting for T1D management, because **slowed gastric emptying makes life much easier for any closed loop.**

Slower carb absorption:

- Reduces peak heights.
- Tolerates slower insulins.
- Reduces tuning sensitivity — a less aggressive FCL still performs well.
- Opens FCL as a viable option for a broader T1D population.

### Emerging evidence in T1D

A small retrospective study of 26 adults with T1D on tirzepatide over 8 months:

- HbA1c reduced by 0.59% at 8 months.
- Body weight reduced by ~10% at 8 months.
- Time-in-range (70–180 mg/dL) increased by ~12.6%.
- Time-in-tight-range (70–140 mg/dL) increased by ~10.7%.
- Time above 180 mg/dL decreased by ~12.6%.
- Well tolerated; only 2 of 26 discontinued.

Source: *Efficacy and Safety of Tirzepatide in Adults With Type 1 Diabetes: A Proof of Concept Observational Study* (J Diabetes Sci Technol 2025;19(2):292–296).

### Access

In most markets, T1D patients are **not currently eligible** for GLP-1 prescriptions — they're approved for T2D and weight management. Access depends heavily on your doctor and region.

Follow the discussion:

- Discord: https://discord.gg/YvrHYmdamc
- Diabettech: https://www.diabettech.com/glp1-ra/glp1-ras-and-type-1-diabetes-a-retrospective-study-of-incretin-based-therapy-use-with-open-source-aid/

If you have experience using a GLP-1 drug with an autoISF FCL, please submit a case study.

## 8.7 Final remark on alternatives

> 🧭 **Choosing your path**
>
> This is an exciting time in the open-source T1D community. You have many viable routes to good looping:
>
> - **Vanilla HCL with sloppy carb inputs** — good for many users, needs only modest tuning.
> - **AAPS Master FCL with Automations** — simple, well-studied, solid time-in-range.
> - **MA with autoISF** (Chapter 7) — middle ground for users missing one or two FCL prerequisites.
> - **Full autoISF FCL** (Chapters 5–8) — highest performance ceiling, biggest setup investment.
> - **Boost, AIMI, EatingNow, Tsunami** — alternative dev branches with their own design tradeoffs.
> - **Dual hormone systems** (future) — potentially transformative, not yet ready.
> - **GLP-1 co-medication** — promising, depends on access.
>
> Pick what fits your life, your temperament, and your access constraints. You don't need to justify your choice to anyone — just have a safe, interesting, and overall enjoyable journey.
>
> And *just eat*.

# Chapter 9 · Performance Monitoring
If you followed the setup chapters, you've earned something important: **the right to let the loop run.** The whole point of FCL is to get there and then stop thinking about it.

This short chapter is about how to keep an eye on the system without slipping back into daily over-tweaking.

## 9.1 Everyday life with your FCL

The bar to clear is not perfection. The bar is *"mostly good, with occasional needs for a small intervention."*

A well-tuned FCL will:

- Handle most meals hands-off, with glucose staying in range (70–180 mg/dL).
- Occasionally run a bit high or a bit low — small deviations are normal.
- Require a small snack every so often when the insulin tail threatens to bring you low.
- Ask for manual help only for truly out-of-spectrum events (unusual snacks, sick days, heavy exercise).

**Resist the urge to fix what isn't broken.** If your weekly time-in-range is holding, leave the settings alone.

### Pre-meal rhythm matters

What your bg and iob look like *before* a meal predicts how well the meal will go.

| State at meal start                                  | Outcome                                           |
|------------------------------------------------------|---------------------------------------------------|
| Glucose rising; iob negative or near zero            | **Bad.** Expect a high peak.                      |
| Glucose flat at target; iob near zero                | OK.                                                |
| Glucose slightly declining; mildly positive iob      | **Good.** Loop is "loaded" for the meal.          |

An EatingSoonTT (§3.5) or the automated low-TT pattern can help produce the third state consistently. Also:

- **A small appetizer** (olives, soup, a handful of nuts) — pushes bg slightly up in a predictable way the loop can respond to early, kicking off SMBs before the main course.
- **A late small dessert** — dark chocolate, a cracker with cheese — uses the insulin tail that's "lurking" from the main meal. Better than letting the tail hypo you.

Over time you'll develop intuition for your own rhythm. A little mindfulness here pays off more than fine-tuning any parameter.

## 9.2 What to watch — and when

Rolling **weekly** data, not daily. Daily data is too noisy to act on.

### The core three views

1. **xDrip 7-day 24-hour scatter diagram.** The single fastest way to spot patterns. If you see a consistent cluster of outliers at a specific time of day, you have something to investigate.
2. **Nightscout Reporter** (or equivalent) — weekly time-in-range, hypo counts, daily curves. Useful for tracking trend direction.
3. **AAPS home screen** — real-time situational awareness during the day. Don't stare at it, but glance.

### When %TIR starts drifting

If your weekly TIR drops, ask in this order:

1. **When are the outliers happening?** Time of day, relation to meals, relation to sleep.
2. **Is a specific meal or snack habit to blame?** Are there "bad" meals and "good" meals?
3. **Is there a pattern with exercise or hormonal/disease cycles?** Period week? A strength training day you added?
4. **Does it correlate with infusion site age, or CGM day 1?** "Bad" cannulas and new sensors can masquerade as a tuning problem.
5. **Have you changed anything recently?** A new Automation, a profile tweak, a diet change? Start by undoing it.

Many "outlier days" trace back to **occlusions, leaky cannulas, or CGM inaccuracy** — nothing to do with your autoISF settings.

Before changing any settings, rule out the prerequisites (Chapter 10, §10.2).

## 9.3 When to tune, when not to

### Do tune when…

- A **lifestyle change** is persistent: new job, new sleep schedule, pregnancy, sustained weight change.
- A **circadian pattern** has genuinely shifted (validated over a couple of weeks, not one noisy week).
- You've identified a **specific profile ISF hour** that's clearly wrong via open-loop testing or emulator analysis.

### Don't tune when…

- You had one bad meal last Tuesday.
- You see a single outlier on the xDrip scatter plot.
- You're curious whether an 8% weight change would improve things.

> ⚠️ **Case Study 8.2 (Futility of tuning based on one extreme meal)** — a negative example where tuning to optimize one unusual meal destroyed performance on normal meals. Read it if you're tempted.

> 💡 **Settings do not have to be great for any one event.** They must suit "good enough" most of what you encounter. Chasing perfection for rare events will cost you time-in-range on the meals you eat every day.

### If you must tune

Change **one thing**. Wait a week. Look at the full spectrum of your meals, not just the one you were worried about. Only then decide whether it helped overall.

The Emulator (Chapter 11) is invaluable for this — it lets you ask "what would last week have looked like with this setting changed?" without actually changing anything.

## 9.4 A sane review cadence

- **Weekly:** glance at xDrip 7-day scatter. If nothing jumps out, you're done.
- **Monthly:** look at weekly %TIR trend. Is it stable, drifting, or improving?
- **Quarterly:** review your Automation list. Shelve what you aren't using. Consider whether any recurring manual intervention should become an Automation.
- **Annually or on major life changes:** re-check that your profile ISFs still match reality via open-loop testing.

That's it. More frequent tuning almost always hurts.

## 9.5 Enjoy

> 💬 If you can develop a mindfulness while remaining relaxed and positive-looking ahead, that may be the best recipe for good success — not every time, but more and more often.

Chapter 10 is for when something does go wrong.

# Chapter 10 · Troubleshooting
When the loop stops behaving, work through this chapter in order. Most problems are not tuning problems — they're prerequisite problems, and you'll find them quickly if you check systematically.

## 10.1 First: know how to get back into HCL

Your escape route is your most important safety tool. You should be able to execute it from muscle memory.

### Turning FCL off

Two paths:

1. **Preferences → OpenAPS SMB → autoISF → "Enable ISF adaptation by glucose behavior" = OFF.** Fastest shutdown.
2. **Tap the loop icon** (violet FCL → green HCL) if your AAPS version supports this UI. Automatically re-enables the overview buttons.

### After turning it off

- **Re-enable the insulin button**: Preferences → Overview → Buttons → Insulin = ON.
- **Start bolusing for meals yourself** again.
- Note that HCL-after-FCL runs **standard oref SMB+UAM without autoISF** — even if your autoISF weights are still tuned. That is the safe default. Re-enabling autoISF for HCL is a separate project.

### Partial fallback

You don't have to go all or nothing. A common arrangement:

- FCL for dinners (when you have time to watch it).
- HCL for breakfast and lunch (where you're rushed anyway).

Use a time-window Automation to control "Enable ISF adaptation by glucose behavior." The loop icon will show the current state (green for HCL, violet for FCL).

## 10.2 Check the prerequisites

Most FCL problems are actually prerequisite problems. Start here.

### Technical prerequisites

- ☐ **Bluetooth stable?** Pump connection alerts firing? Phone always within range?
- ☐ **CGM quality?** Was this sensor fine yesterday and is jumping today? Is it day 1 of a new sensor (often noisier)?
- ☐ **Cannula / pod age?** Is it past your reliable lifetime (often 48h, not the manufacturer stated)?
- ☐ **Were alerts / alarms silenced recently?**

### Data-quality checks

Useful: analyze data **excluding**:

- Sensor day 1.
- Cannula/pod days > 2.

If excluding those "bad" days makes your data look fine, the problem isn't autoISF — it's a prerequisite.

### Did you follow the setup sequence?

It's easy to drift over time. Verify:

- ☐ Your SMB range extension is still wide enough (Chapter 3, §3.1).
- ☐ Your iobTH is set, and the odd/even target logic is enabled (§3.4).
- ☐ Your `bgAccel_ISF_weight` and `pp_ISF_weight` values are what you expect (not accidentally shifted by an Automation with no restore tandem).
- ☐ Autosens is OFF, dynamicISF is OFF (if applicable).

### Profile still correct?

A common failure mode: you built your autoISF on top of a profile that has drifted. Questions:

- When did you last validate your ISFs via open-loop testing?
- Has your body weight, lifestyle, or hormonal pattern changed?
- Were you relying on dynamicISF or Autotune to "cover" the profile before FCL exposed the gap?

If the profile is off, no amount of autoISF tuning will fix it. Go back to HCL, test and fix the profile, then return to FCL.

### Is iobTH set correctly?

iobTH is modulated dynamically (§3.4). In the AUTO ISF tab, check the "effective iobTH" line. Things that silently change it:

- An active TT.
- An active %profile.
- Exercise button yellow.
- Activity Monitor adjustment.
- Recently-run Automation that set a different `iob_threshold_percent` without a restore tandem.

If your effective iobTH doesn't match your expectation, that's the first thing to fix.

## 10.3 Glucose goes too high

### Meals recognized too slowly

Likely causes:

- ☐ **Bluetooth dropouts at meal start** — phone was across the room when you sat down.
- ☐ **CGM quality** — jumpy values confused acceleration detection.
- ☐ **Try an aperitif** — a small appetizer a few minutes before the meal gives the loop time to see an acceleration.

### First SMBs are delayed

- ☐ **Blocked by the 30% jump rule?** (Chapter 2, §2.4.) Check the AUTO ISF tab for "SMB disabled" messages.
- ☐ **Odd-numbered TT or profile target active?** An Automation might have set one.
- ☐ **Pump connection issue** — BT or physical.
- ☐ **Phone proximity** — was the phone near the pump at meal start?

### SMBs are too small

In rough order of likelihood:

- ☐ **Capped by `smb_max_range_extension`** — widen it (Chapter 3, §3.1).
- ☐ **Capped by `autoISF_max`** — widen it (§3.2).
- ☐ **`bgAccel_ISF_weight` set too low** — raise it cautiously.
- ☐ **`pp_ISF_weight` set too low** — raise it cautiously.
- ☐ **CGM smoothing** eating the early acceleration signal — try lighter smoothing.
- ☐ **Sensitivity modulation active** — Activity Monitor, exercise mode, %profile reducing the insulin you'd otherwise get.
- ☐ **ISF adaptation accidentally off** after a Preferences tweak or Automation.

See also: https://github.com/ga-zelle/autoISF → "How to get larger SMBs" for a dedicated troubleshooting PDF.

### Stuck at high bg

- ☐ **dura_ISF not engaging?** Check the AUTO ISF tab during the plateau — is dura contributing?
- ☐ **dura_ISF_weight too low** — raise it in small steps (watch for late hypos).
- ☐ **Fat-related temporary insulin resistance** — consider an Automation that sets elevated %profile at high-FPU meals.
- ☐ **Hypothesis: iobTH too low** — the loop wanted more insulin but was capped.

Often the right fix is not at the stuck-high plateau itself. If bgAccel/pp_ISF had been sharper, the peak would have been lower and shorter, and dura wouldn't need to work as hard. **Look upstream first.**

## 10.4 Glucose goes too low

### Phantom meal triggers

- ☐ **Outside usual meal times?** Set an odd profile target for those hours.
- ☐ **First SMBs too big** — reduce `bgAccel_ISF_weight` (cautiously).
- ☐ **Snacks triggering full meal responses** — set up a snack cockpit button (§5.4).
- ☐ **Compression lows creating false "meal start" signals** — odd-numbered night target or see Case Study 5.3.

### Too much insulin delivered

- ☐ **iobTH too high?** Check the effective iobTH in the AUTO ISF tab.
- ☐ **iobTH-changing Automation ran and didn't restore?** Verify the tandem restore Automation worked (§5.5).
- ☐ **SMB range extension too wide for your needs** — narrow it.
- ☐ **`autoISF_max` too high** — narrow it.
- ☐ **`smb_delivery_ratio` too high** — reduce across the board.
- ☐ **One of the ISF weights too aggressive** — usually `dura_ISF`, which has a cumulative effect. Check the AUTO ISF tab to see which component is dominating.
- ☐ **Temporarily more insulin-sensitive than usual** (e.g., after heavy exercise yesterday)? Use a temp %profile switch rather than changing long-term settings.

### Late hypos after meals

This is the hardest category. Options in order:

1. **Check dura_ISF_weight first.** It's the most common cause of late hypos.
2. **Reduce `bgAccel_ISF_weight`** if early SMBs are too big.
3. **Identify the meal types** where this happens — often low-fibre, low-fat, low-protein meals where the insulin tail outlasts the carb absorption.
4. **Take a small snack** proactively (5–10g) when the loop warns of an imminent hypo. The loop's carb recommendation is often inflated — you usually need much less than it suggests, because the loop doesn't know about fat/protein still digesting.
5. **Adjust your diet** — add more fibre, protein, or fat to balance the carb absorption curve.
6. **Lower iobTH** — if hypos reliably trace to too much iob in the rise phase.
7. **Accept the tradeoff.** Sometimes a small snack is genuinely the right answer — "better a snack than a hypo" — especially for weight-conscious users who can reduce intake at the meal itself to compensate.

## 10.5 Glucose goes too high *and* too low (roller-coasters)

Roller-coasters point to real problems with the setup. They rarely respond to a single parameter tweak.

### Step back and simplify

- Is your lifestyle or diet extreme in some way that's pushing the system past its limits?
- Are your %TIR expectations realistic? The book emphasizes moderate expectations.
- Have you accumulated Automations and workarounds that now interact unpredictably?

### Verify foundations

- ☐ Was your FCL built on true, experimentally-proven ISFs?
- ☐ Did you follow the tuning sequence — Chapter 3 settings, then `bgAccel_ISF` first in Chapter 4?
- ☐ How often have you looked at the AUTO ISF tab or the Emulator to understand what the loop is actually doing?

### When to start over

With many interacting parameters and Automations, you can reach a state where the safest path is not to patch, but to restart:

1. **Full restart of autoISF settings** — go back to Chapter 3 defaults and rebuild. This is not a failure; the book explicitly expects this for some users.
2. **Fall back to HCL** — either vanilla AAPS HCL, or HCL with just dura_ISF active for fatty-meal management.
3. **Switch methods** — try AAPS Master FCL with Automations (Chapter 8, §8.1), which is simpler.
4. **Temporarily switch to a commercial system** — wait for better tools, then re-evaluate.

None of these is a defeat. They're different valid choices for where you are right now.

## 10.6 Staying out of trouble

A few principles that prevent most troubleshooting from ever being needed:

1. **Interference is the enemy.** Let the loop loop. Every user bolus and every additional carb entry distorts the curve autoISF is reading.
2. **Don't optimize for single events.** The goal is "good-enough through nearly all scenarios." (See Case Study 8.2.)
3. **Keep it simple.** Resist the latest trick until you understand how it affects your existing balance.
4. **Use FCL selectively.** It's fine to run FCL only for some meals, or only on certain days. Don't force the loop into situations where you already know it will struggle.
5. **Stay connected to the community.** The Discord channels are where problems get diagnosed fastest: https://discord.gg/tamvhh57Xs
6. **Keep perspective on %TIR expectations.** Many non-looping T1Ds are happy above 60% TIR. A study of 16 AAPS users achieved ~80% TIR on a simpler FCL with no meal announcement. These are reasonable reference points. You don't have to chase 95%.

## 10.7 Just eat

When all else is working — or working well enough — the best thing you can do is stop worrying about it. That's what FCL is for.

---

> 💡 **A note on scope.** The Emulator is optional. You can run a successful FCL without ever installing it. The reason to read these chapters is that the Emulator transforms tuning from "wait two days to see if the change helped" into "watch what last week would have looked like with this change, in 30 seconds." If you like data analysis, it is transformative. If you don't, stick with the AUTO ISF tab and skip this.

# Chapter 11 · The Emulator on Your PC
## 11.1 What the Emulator does

The Emulator is a Python tool that replays your AAPS logfiles on your PC. For any time window you pick, it can:

- Show you **every loop decision** — what autoISF saw, what components contributed, what SMB was requested, whether anything was capped.
- Ask **"what-if" questions** — if I had used `bgAccel_ISF_weight = 0.045` instead of `0.035` last Tuesday, how would each meal's first SMB have been different?
- Produce outputs in multiple formats: a full-detail text log, a dense CSV table, a visual PDF chart, and a "delta" analysis for acceleration-driven decisions.

The key insight: it uses your real, already-recorded CGM and insulin data. Nothing hypothetical. Just "given what actually happened, what would the loop have decided under different settings?"

## 11.2 What it's good for — and what it's not

**Good uses:**

- Finding a better `bgAccel_ISF_weight` by comparing several candidates against the same meal.
- Seeing which autoISF component (acce / pp / dura / bg) was really driving the SMB size at a given moment.
- Confirming that a tuning change would help without committing to it.
- Analyzing a meal retroactively — *why* did that plateau last so long?

**Not good for:**

- Predicting the downstream bg curve after a changed setting. The Emulator can only replay; it cannot simulate how a bigger SMB at 12:30 would have changed the 13:00 bg reading.
- Replacing iteration across multiple meals. One meal "optimized" in the Emulator is still one meal — validate across 2–3 different meal types before committing.
- Tuning from first principles. The Emulator helps you refine hypotheses; it does not generate them.

## 11.3 Installation — high-level

> ⚠️ **Follow the developer's most current instructions.** File names, branches, and Python versions change. The authoritative source is always:
>
> **https://github.com/ga-zelle/APS-what-if**
>
> Look at the latest "Instructions determine_basal emulator" PDF and the "How to run the emulator on the phone" PDF under Documentation in English.

The installation involves four broad steps:

### 1. Set up the folder structure

Suggested layout (names are arbitrary):

```
Logfiles_Emulator/
├── AAPS_logs/        ← copy your phone's AAPS logfiles here
├── Emulator/          ← downloaded Python files live here
└── Emulator_Studies/
    ├── Study_1/       ← one emulation project = one folder
    ├── Study_2/
    └── ...
```

> 💡 **Copy AAPS logfiles from your phone regularly** — they auto-delete after roughly 2 weeks (much faster on 1-minute CGM setups). Keep a month-by-month archive, and alongside each month put a Nightscout Reporter PDF — it makes finding "interesting days" for analysis much easier.

### 2. Download the Python files

Two sources, both on GitHub under `ga-zelle`:

- **`APS-what-if/software`** — the emulator itself (a `.config` and four `.py` files).
- **`Scan-APS-logfiles`** — two more `.py` files (scan helpers).

Match the **branch version** to your AAPS + autoISF version. If you're on AAPS 3.3.3a + autoISF 3.1.0, use the `A3.3.3a+aisf3.1.0` branch. If you can't get the emulator to run, check for a newer file (even with the same name — updates may fix Android-OS-specific issues).

For **1-minute CGM users** (Libre 3 via Juggluco), use `1minute_emulator_std.config`. For standard 5-minute CGMs, use `5minute_emulator_std.config`.

### 3. Create a desktop launcher

Make a shortcut to `emulator_GUI.py` in your Emulator folder, drag it to your desktop, and name it something memorable ("Emulator_start").

### 4. Install supporting software

- **Notepad++** on your PC (for editing `.vdf` files — see §11.4).
- Python — usually already present. If not, see the developer's install guide.

## 11.4 Analyzing a logfile — the "no-change" workflow

This is the simplest mode: replay what happened, with no modifications.

### Create `noChange.vdf`

A `.vdf` file tells the Emulator what to change for a "what-if" run. An **empty** `.vdf` is a `noChange.vdf` — replay as-is.

1. Open Notepad++ and save an empty file as `noChange.vdf`.
2. Keep a copy at the top of your `Emulator_Studies/` folder. For each new study, copy it into the Study_n folder.

> ⚠️ **Every study folder must contain a `noChange.vdf`.** Even for what-if runs, the emulator needs the no-change baseline to compare against.

### Prepare your run

Open the Emulator (from your desktop launcher). A dialog box appears with three paths to fill in:

1. **Project folder** — where results go. Usually `Emulator_Studies/Study_n/`.
2. **VDF file** — for a no-change run, the `noChange.vdf` in that same Study_n folder.
3. **Logfiles** — browse to any logfile from the day you want to analyze. Then:
   - Replace the time in the filename with `*` (asterisk) → this grabs all logfiles from that day.
   - Click **Show matches** to verify.
   - Use the bottom time fields to narrow the window. Times are in UTC; convert from your local time (e.g., for Central EU Summer Time, subtract 2 hours).

### Run the emulation

Click **Run emulation**. If there's a syntax or version error, check the `.log` file first. The Discord channel (https://discord.gg/n3tD5eXExC) is the fastest place to get help.

### The five result formats

The emulation produces multiple output files. Each gives you a different view.

| Output                                | What it contains                                      | Best for                                            |
|---------------------------------------|-------------------------------------------------------|-----------------------------------------------------|
| `noChange.txt`                        | Full AUTO ISF tab content for every loop decision    | Deep-dive investigation — search for "autoISF," "SMB disabled," etc. |
| `noChange.csv`                        | Tabular data for every decision, every 5 minutes      | Looking at trends across hours; copy into Excel     |
| Spreadsheet extract (manual)          | Your annotated and color-coded version of the CSV    | Writing up a case study or comparing multiple runs  |
| `noChange.pdf`                        | Visual chart: bg, iob, iobTH corridor, insulin activity, ISF scatter | Quick eyeball: "did anything weird happen?" |
| `delta` sheet (newer emulator core)   | Short and long average delta analysis                | FCL using Automations (Chapter 8, §8.1) based on delta |

**For most users, the PDF chart + the CSV (in Excel) is the right combination.**

> 📖 **Tips for the CSV workflow in Excel**
>
> - Add a local-time column next to UTC (e.g., `=UTC_cell + 2/24` for Central European Summer Time).
> - Convert time format from hh:mm:ss to hh:mm.
> - Hide columns you don't care about for this analysis; your formulas will still work.
> - Color-code the rows where: an SMB was given, a particular ISF component dominated, iobTH was exceeded, a TT became active.

## 11.5 "What-if" analysis — the `yourChange.vdf` workflow

This is why you installed the Emulator. Ask: "if I had used these settings instead, how would the loop have decided?"

### Writing a `yourChange.vdf`

The file lists parameter changes. Simplest form — one line per parameter, tab-separated:

```
profile   bgAccel_ISF_weight   profile['bgAccel_ISF_weight']*1.2   ### 20% stronger
```

That line says: "for this emulation run, pretend `bgAccel_ISF_weight` was 20% bigger than it actually was."

- **Factor-based syntax** (`* 1.2`, `* 0.8`) is the most common form.
- **Multiple lines** for multiple parameter changes.
- Save the file with a descriptive name like `1.2_bgAccel_2.0_bgBrake_1.2_dura.vdf`.

More complex VDF syntax (e.g., defining circadian `STAIR_ISF` tables for whole-profile experiments) is in the developer's "Guide to VDF Files for the AAPS Emulator" PDF.

### Running it

Same process as the no-change run (§11.4), but point the middle "VDF file" field at your `yourChange.vdf` instead of `noChange.vdf`. The Emulator runs both — you get both sets of results side-by-side in the same Study_n folder.

### Reading the results

Each output type now comes in two versions (noChange and yourChange):

- **`yourChange.txt`** — for every loop decision, exactly how the changed setting would have altered it.
- **`yourChange.csv`** — the tabular version. Compare against `noChange.csv` side-by-side in Excel (either manually, or using the spreadsheet-based tool `autoISF_factors_performa.ods` in the developer's repo).
- **`yourChange.pdf`** — the visual chart, including markers for every decision where the yourChange value differed from noChange.

The visual chart shows "dark green scatter points" for autoISF ISF under `yourChange` and "light green" for `noChange`. Where they diverge is where your setting change mattered.

### What to look for

- The **first place your change made a meaningful difference** is the most informative. Everything after that would have put the bg curve on a different trajectory, so later comparisons become increasingly hypothetical.
- Which meal phases did the change affect — acceleration? plateau? deceleration?
- Did the change run into any safety limit you'd need to widen?

## 11.6 Limitations — important to internalize

> ⚠️ **Each Emulator result is a single-decision calculation, not a simulation.**
>
> If yourChange would have delivered a bigger SMB at 12:30, the Emulator correctly shows that. What it cannot show is: how the extra insulin would have lowered the 12:35 bg reading, and how that would have changed every subsequent decision.
>
> The first meaningful divergence between noChange and yourChange is the most reliable insight. Later divergences are anyone's guess.

This is why:

- **Emulator analysis should focus on early, acceleration-phase decisions** — where the "first big difference" is most cleanly visible.
- **dura_ISF tuning can't be well-emulated** — because it depends on plateaus that would themselves be different under different earlier settings.
- **You still need real-world validation** — the Emulator narrows your hypotheses; the next week of actual meals confirms them.

## 11.7 Where to get help

- **Developer docs:** https://github.com/ga-zelle/APS-what-if (look for PDFs under `Documentation in English`).
- **Discord:** https://discord.gg/n3tD5eXExC (channel: `emulate-aaps`). Fastest place to resolve version or path issues.
- **Case studies:** the book's case studies 4.1 (pizza tuning), 6.2 (biking day), and 8.2 (futility of tuning from one meal) all use the Emulator and show worked examples.

# Chapter 12 · The Emulator on Your Phone
The phone Emulator is a lighter-weight companion to the PC Emulator. It's useful for two things:

1. **Quickly seeing recent loop decisions in tabular form** — a better view than scrolling the AUTO ISF tab.
2. **Real-time "what-if" announcements** — spoken aloud by the phone, when a changed setting would have produced a different SMB.

The second one is genuinely unique. It lets you test a setting idea "in real life" without committing to it.

## 12.1 Why the phone Emulator exists

The PC Emulator is great for retrospective analysis. But for **real-time** tuning — "am I willing to follow this different setting's suggestion, and add this extra SMB manually?" — you need the tool running on the phone that's handling your loop.

The phone Emulator is:

- More limited in output (no PDF charts, simpler CSV).
- Better at real-time feedback.
- The only way to get spoken suggestions (§12.5).

On Android, it runs via QPython 3L. On iPhone (Trio/iAPS), a lighter built-in feature gives you just the tabular view — no full emulator, no speech. See §12.7.

## 12.2 Installation — high-level

> ⚠️ **The developer's installation guide is the authoritative source.** Versions, permissions, and Android OS quirks change. Start there:
>
> **https://github.com/ga-zelle/APS-what-if** → Documentation in English → Installation Guide PDF

The flow:

### 1. Install QPython 3L

- Get it from Google Play Store.
- Put the app icon next to your other looping apps.
- **Long-press the app icon → App info** → exclude it from battery optimization, aggressive app-killing, etc. (Same settings you made for AAPS, NSClient, xDrip, and anything else critical.)

> ⚠️ If QPython gets killed by the OS, the emulator and speech synthesis stop silently. Lock it down like every other critical looping app.

### 2. Copy the .py files

Connect the phone via USB, then copy all the emulator `.py` files from your PC's `Emulator/` folder **into the phone's `QPython/scripts3/` folder**.

Skip `emulator_GUI.py` — that's for the PC desktop launcher only.

### 3. Copy the .config file

Copy `5minute_emulator_std.config` (or `1minute_emulator_std.config` for Libre 3) from your PC to the phone at:

```
Internal memory / AAPS / logs / info.nightscout.androidaps /
```

Not the QPython folder — the AAPS logs folder.

### 4. Copy noChange.vdf

Same location. The phone Emulator reads `.vdf` files from here.

### 5. Optional — more .config variants

You can have multiple config files — e.g., one that announces everything, one that only announces insulin (no carb warnings). More on this in §12.6.

## 12.3 The result table on the phone

Once running, QPython shows a compact table of recent loop decisions. This table is the main passive output. You can consult it at any time to see, for the last N decisions:

- Which autoISF category (acce / pp / bg / dura) contributed how much.
- What the effective ISF was.
- What SMB was requested, delivered, or blocked.

The table is much easier to read than scrolling multiple AUTO ISF tab snapshots, especially when tracking a meal in progress.

### Customization

The output table format is defined in the `.config` file. You can customize which columns appear, reorder them, change decimal separators, etc. See the developer's "How to run the emulator on the phone" PDF for the exact syntax.

## 12.4 What-if analysis on the phone

Same concept as on the PC (§11.5), but running against the current live logfile:

1. Write a `yourChange.vdf` on the PC (§11.5).
2. Copy it to the phone's AAPS logs folder.
3. Select it in the running QPython emulator (via a menu action — see the dev docs).
4. The emulator now runs your change in parallel with the real loop, for each new CGM value.

The results show up in the table and — if you enable it — in spoken announcements.

## 12.5 Real-time speech synthesis — the killer feature

> ⚠️ **iPhone users: this feature is not available.** See §12.7 for what Trio and iAPS offer instead.

When the what-if emulator is running and detects that your experimental setting would produce a **meaningfully different SMB** than the real loop's decision, the phone can speak an announcement:

- *"Extra SMB of 0.8 units recommended."*
- *"Reduce by 0.5 units."*
- *"Carbs required" warnings (useful even without autoISF).*

You can then:

1. Look at your glucose curve and the developing situation.
2. Decide whether to follow the suggestion by **manually adding a bolus** of the suggested size. (You'll need to temporarily re-enable the insulin button in AAPS Preferences → Overview → Buttons → Insulin = ON during test phases.)
3. Watch what happens over the next hour.

After a few days of this, you develop intuition for whether the investigated change really deserves to be folded into your active settings.

> ⚠️ **Your settings must work across a variety of meals.** Don't be seduced by one meal where the what-if suggestion was clearly better — see Case Study 8.2 on the futility of tuning from one extreme meal.

## 12.6 Managing announcements

### Time windows for speech

The `.config` file defines when announcements are allowed. Default: 07:00–23:00 local time (not UTC). Edit `5minute_emulator_std.config` on your PC with Notepad++, then copy the updated file back to the phone's AAPS logs folder.

The config has three independent time windows:

- **Line 1:** when "carbs required" announcements are allowed.
- **Line 2:** when "extra bolus need" announcements are allowed.
- **Line 3:** when "reduce bolus" announcements are allowed.

Set each to match how useful that type of alert is for you.

### Silencing the emulator temporarily

Options, in order of preference:

1. **Switch to `noChange.vdf` as the active VDF.** The emulation continues (you still get the result table), but no what-if comparison runs → no speech.
2. **Use a "silent" custom `.config`** with very narrow time windows for announcements, and switch to it via the emulator's menu.
3. **Silence the phone** (mute + do not disturb) — blunt, shuts off other alerts too.
4. **Kill QPython** (force-stop the app) — emulation stops entirely. No tabular data for that period.

Option 1 is the best default. It keeps you collecting data while silencing the proactive announcements.

## 12.7 iPhone users: Trio and iAPS

iOS-based autoISF variants **cannot run the full emulator** (no QPython equivalent, no Python-based PC tool-chain on iOS). Two lighter options are available instead:

### Built-in table view

Both Trio's and iAPS's autoISF ports integrate a compact table showing the recent loop decisions and the contribution of each autoISF category (acce / pp / bg / dura). Not as powerful as the full emulator, but enough for quick sanity-checks.

**Access:** in Trio, double-click "Statistics." In iAPS, similar — check the current readme for your version.

### No speech synthesis

The real-time "what-if" with spoken announcements is not available on iPhone. Workarounds:

- Do PC-side analysis with the emulator if you have an Android device somewhere (not the looping phone — any Android for analysis work).
- Use the phone's on-screen table view to watch recent decisions during a meal.
- Consult the autoISF Quick Guide and community for guidance.

Future updates may close this gap. Check https://github.com/mountrcg/Trio and https://github.com/mountrcg/iAPS for current status.

## 12.8 Summary

- The phone Emulator extends the PC Emulator with a real-time interface.
- Its best feature is **spoken what-if suggestions** during active meals.
- Installation is more fiddly than the PC emulator (QPython quirks, file placement). Budget an evening.
- On iPhone, you get a compact tabular view but no full emulator or speech.
- The biggest pitfall is letting Android's battery optimizer kill QPython silently.

# Final Remark

This is an exciting time to be part of the open-source T1D community. The tools described in this book — autoISF, the Emulator, the Automations ecosystem — exist because users built them for each other and shared the work freely. If you build something, contribute it back. If you learn something, share it.

Carefully weigh for yourself what your entry point will be. And then — once you've done the work of building a system that handles your meals hands-off — *just eat happily ever after.*

*— The authors*

# Appendix A — Glossary

Key terms used in this book, organized alphabetically. Descriptions are concise; for deeper reading, follow the linked references in the chapters where the terms first appear.

## A

**AAPS (AndroidAPS)** — Open-source Artificial Pancreas System for Android phones. Bluetooth-connected with a pump and a CGM. Supports the broadest choice of pumps and CGMs of any DIY looping option.

**AAPS Client** — Companion app for remote monitoring and limited control of an AAPS phone (e.g., parent → child). iOS equivalent: Loop Caregiver.

**acce_ISF** → see `bgAccel_ISF`.

**acceleration** — Mathematical analysis of the bg curve that detects the earliest signs of a rise. autoISF uses parabola-fitted acceleration; simpler systems use growing bg deltas (which lag by 10–20 minutes).

**Activity Monitor** — autoISF feature that uses phone step count to auto-adjust sensitivity over a ~60-minute window. Capped at +20% (inactivity) / −30% (activity). See §6.6.

**aggressiveness (of the loop)** — How strongly the loop responds to glucose deviations. Modulated by ISF, bg target, %profile, iobTH, and exercise mode settings.

**AIMI** — AAPS-derived dev variant with a Meal Announcement workflow. Also ported into Trio. See §8.3.

**algorithm** — The set of calculations and safety checks a loop performs every 5 minutes (or every minute for 1-minute CGMs) to decide insulin delivery. The oref family (AAPS, Trio, iAPS) and iOS Loop use different algorithms.

**AMA (Advanced Meal Assist)** — Older oref approach to handling meal carbs via increased temp basal, without SMBs. Superseded by SMB+UAM in modern oref.

**Android Studio** — Free developer software needed to build and maintain your personal AAPS installation.

**Anubis** — DIY re-engineered transmitter for the Dexcom G6 CGM. Unlimited lifespan (battery change every ~6 months); won't time out at 10 days.

**apk** — Android application package. The compiled file used to install AAPS on your phone.

**APS** — Artificial Pancreas System. Umbrella term for insulin delivery systems that regulate bg to a target based on CGM data.

**autoCR** — Automated carb-ratio adjustment. Pilot feature in iAPS; not typically useful in advanced oref FCL.

**autoISF** — The version of oref SMB+UAM used in this book. Adapts ISF sharply to the developing glucose curve (acceleration, delta, level, stuck-at-high). Only available in dev variants of AAPS, Trio, and iAPS.

**Auto Bolus / Automatic Bolus** — In iOS Loop terminology, a small automatically-delivered bolus for faster bg correction than TBR alone. Oref equivalent: SMB.

**Automation** — AAPS feature that lets you define patterns in your data (conditions) and actions to take (loop setting changes) when those conditions are met. Automations are how you build a "DIY cockpit."

**Autosens** — Calculation of insulin sensitivity based on deviations over the past 8–24 hours. In FCL with autoISF, **turn Autosens OFF** — the two are incompatible.

**Autotune** — Suggests profile basal, carb ratio, and ISF adjustments based on historical data. **Do not use with autoISF.** Considered controversial.

## B

**basal rate** — The baseline hourly insulin delivery defined in your profile, intended to hold bg stable in the absence of meals or disturbances.

**bg** — Blood glucose. (Technically the tissue glucose that CGMs measure, which lags blood glucose by a few minutes.)

**bg_delta** → see `delta`.

**bg deviation** — Difference between observed bg change and the change expected from insulin effects alone. Used by the loop to estimate carb absorption.

**bg_ISF** — autoISF component that strengthens ISF at high bg and softens it at low bg. Generally unused in FCL (set weights to 0.0). See §4.6.

**bgAccel_ISF (acce_ISF)** — autoISF component that strengthens ISF on detected glucose acceleration (a rising bg curve). The most important component in FCL — drives the first SMBs that replace your meal bolus. Tuned via `bgAccel_ISF_weight`. See §4.2.

**bgBrake_ISF (brake)** — autoISF component active during glucose deceleration (the rise slowing toward the peak). Usually half the weight of bgAccel_ISF. See §4.4.

**bg source** — The software source from which AAPS receives bg values. Typically a CGM app (Dexcom, xDrip+, BYODA, Juggluco for Libre 3).

**Boost** — AAPS-derived dev variant with its own meal-handling algorithm. Uses delta-based acceleration detection. See §8.3.

**bolus calculator** — Tool in AAPS (and equivalent in iOS Loop) that suggests a bolus size based on carbs, IC, ISF, and current iob. Not used in FCL.

**BYODA** — Build Your Own Dexcom App. Lets you build your own Dexcom reader app and pass smoothed bg values to AAPS or xDrip+, while still using Clarity®.

## C

**calculator** → see `bolus calculator`.

**CGM** — Continuous Glucose Monitor. Sensor + transmitter + app that provides bg values to the loop.

**cob** — Carbs On Board. Remaining carbs available for absorption. **Always zero in FCL** (no carb entry).

**connectivity** — Bluetooth or WLAN connections between loop components (phone, pump, CGM, watch). Must be reliable 24/7 for FCL.

**control of bg** — The "boating-like" control problem of balancing carb absorption against insulin activity. Aggressive control risks hypos on turns; too-gentle control misses the target.

**correction factor** — iOS Loop term; analogous to the oref SMB delivery ratio. Scales the size of autoboluses.

**customization for iOS Loop** — Advanced dev features available to iOS Loop users.

## D

**deceleration** — The bg rise slowing as it approaches its peak. Triggers `bgBrake_ISF`.

**delivery limit** — Maximum bolus/basal rates permitted by your AAPS settings.

**delivery ratio** → see `SMB delivery ratio`.

**delta (bg_delta)** — Change in bg over the last 5 minutes. Visible in the AUTO ISF tab.
- `d5` (or "delta") — last 5 minutes.
- `short avg delta (d15)` — average over last 3 deltas (15 minutes).
- `long avg delta (d45)` — average delta between 15 and 45 minutes back.

**dev variant** — Pre-release or side-branch version of AAPS, iAPS, or Trio. Includes experimental features not yet in the main (Master) release. autoISF itself is a dev variant.

**Dexcom** → see `G6`, `G7`, or `Dexcom ONE`.

**DIA (Duration of Insulin Action)** — How many hours your insulin remains active. Set in your profile. Critical for loop accuracy.

**disturbance** — Any factor that pushes bg away from a steady-state baseline — meals, exercise, fever, hormones, stress, and many others. Your profile handles the baseline; disturbances are managed by the loop.

**DIY** — Do It Yourself. Open-source, user-built looping ecosystem.

**DIY cockpit** — The constellation of buttons and Automations a user builds on the AAPS home screen for custom pre-programmed responses. See §5.4.

**Dual Hormone Loop** — Future system that adds a second hormone (glucagon or analogue) alongside insulin. Enables more aggressive insulin treatment without hypo risk. See §8.5.

**dura_ISF** — autoISF component active during persistent high-bg plateaus. Boosts ISF with both duration and height above target. Most relevant for fatty meals. Tuned via `dura_ISF_weight`. See §4.5.

**dynamic carb absorption** — The oref algorithm's continuous calculation of carb absorption based on observed bg deviations and insulin activity. Allows UAM/FCL operation without carb inputs.

**dynamic carb ratio** — Automatic IC adjustment based on bg level and recent TDD. Available in Trio/iAPS. Not used in oref FCL.

**dynamicISF** — Automatic ISF adjustment based on bg level and recent TDD. **Do not use with autoISF.** Covers up profile errors that FCL requires to be correctly set.

**dynamic iobTH** — autoISF's automatic modulation of iobTH based on active TT and exercise mode. See §3.4.

**dynamic bg target** — Loop feature that changes bg target based on detected sensitivity or resistance. Generally disabled in FCL to avoid interaction with the even/odd target logic.

## E

**EatingSoon TT** — A low temporary target (e.g., 74 mg/dL) set before a meal so the loop delivers insulin sooner and the bg has a lower starting point. See §3.5.

**EatingNow** — AAPS-derived dev variant with a Meal Announcement workflow. See §8.3.

**eCarbs** — "Extended Carbs." Carb inputs with an absorption-time tail. Used in iOS Loop; not useful in oref loops.

**Emulator** — Python tool for replaying AAPS logfiles on a PC or phone. Enables retrospective analysis and what-if experimentation. Chapters 13–14.

**even/odd target** → see `odd target`.

**exercise mode** — Loop mode that limits iob and softens ISF during exercise. In autoISF, activated by yellow exercise button + elevated TT above profile target. Tunable via `half_basal_exercise_target`. See §6.2.

## F

**FCL (Full Closed Loop)** — Looping mode where the user gives no bolus and enters no carbs. The loop handles everything automatically. Main subject of this book.

**FPU (Fat-Protein Units)** — Late carb-like insulin need from fat and protein content of a meal. Managed in FCL by dura_ISF (§4.5) or by temporary %profile switches.

## G

**G6 / G7 / Dexcom ONE** — Dexcom CGM variants. G6 is the gold standard for FCL as of early 2026; production ends mid-2026.

**glucagon** — Counterregulatory hormone used in dual-hormone loops to prevent hypos. See §8.5.

**GLP-1 / GIP receptor agonists** — Drugs like Tirzepatide (Mounjaro®) that slow gastric emptying. Make FCL easier. See §8.6.

## H

**half-basal exercise target (HBET)** — AAPS Preferences value that tunes the exercise-mode sensitivity ratio. Lower values produce more aggressive softening. See §6.2.

**HbA1c** — Long-term average blood glucose marker. Reported as %. Medical community commonly targets < 7.0%.

**HCL (Hybrid Closed Loop)** — The loop manages basal and between-meal corrections; the user bolusses for meals. Starting point for transitioning to FCL.

## I

**iAPS** — iPhone-based oref loop (fork of the original iAPS). Has a dev port of autoISF. See Chapter 1 caveats.

**IC (Insulin-to-Carb ratio)** — Grams of carbs covered by 1 unit of insulin. Set in your profile. Critical for HCL; used by the loop in FCL for retrospective carb absorption calculations.

**individualized tuning** — The per-person calibration of all loop parameters based on observed data. The entire setup project in Chapters 3–8 is individualized tuning.

**insulin activity** — Insulin effect in the next 5 minutes, above profile basal supply (can be negative). Shown as the thin yellow line in AAPS.

**insulin counteraction effect (ICE)** — iOS Loop equivalent of bg deviation. Describes how observed bg changes differ from expected.

**insulin kinetics** — The rising-then-falling shape of insulin's activity curve. Varies by insulin type. Represented in AAPS by DIA and peak-time settings.

**insulin required** — The oref algorithm's calculation of how much additional insulin is needed, based on bg, iob, cob, and predictions. Distributed across SMBs and temp basal.

**integral correction effect (IRC)** — iOS Loop feature that adjusts predictions based on historical prediction errors.

**iob** — Insulin On Board. Units of insulin currently available to become active within the DIA window.

**iob delta** — Change in iob over recent minutes. Used by the loop to estimate what was actually absorbed.

**iobTH** — iob threshold. The iob ceiling above which SMBs are blocked. **The most important safety setting in FCL.** See §3.4.

**iOS Loop** — iPhone-based DIY loop using MPC (Model Predictive Control). Requires precise carb inputs — **no UAM or FCL**. Different algorithm from oref.

**ISF (Insulin Sensitivity Factor)** — Expected bg decrease from 1 unit of insulin. The single most important parameter in oref loops. Set in your profile; modulated dynamically by autoISF.

**ISF_weight** — Tunable factor in autoISF that scales each component's effect on profile_ISF. Five weights: `bgAccel_ISF_weight`, `pp_ISF_weight`, `bgBrake_ISF_weight`, `dura_ISF_weight`, and the `bg_ISF` weights.

## J

**Juggluco** — Third-party app that passes Libre 3 raw values to AAPS in 1-minute mode.

## L

**LGS (Low Glucose Suspend)** — AAPS safety feature that reduces basal when bg is dropping. Part of AAPS Objective 6.

**Libre 2 / Libre 3** — Abbott's factory-calibrated CGMs. Alternatives to Dexcom. Libre 3 + Juggluco enables 1-minute mode in autoISF.

**log files** — Record of AAPS actions; used for troubleshooting, debugging, and Emulator replay.

**logarithmic dynamicISF** — Default dynamicISF variant; strengthens ISF logarithmically with rising bg.

**Loop** → see `iOS Loop`.

**Loop Caregiver app** — Remote monitoring/control app for iOS Loop (parent/child scenarios). Android equivalent: AAPS Client.

**Loop Follow** — Remote data viewer for iOS Loop.

## M

**MA** → see `Meal Announcement`.

**MAR (Minimum Absorption Rate)** — iOS Loop carb-absorption floor. Not relevant to oref loops.

**Master** — The latest official release of AAPS (or of other loops). The stable, recommended version for most users. Not the same as dev variants.

**maxIOB** — Hard safety limit. AAPS Preferences setting for the maximum total iob the loop will ever allow.

**MDI (Multiple Daily Injections)** — Traditional insulin-pen therapy (no pump). Fallback if your looping system fails.

**Meal Announcement (MA)** — Closed-looping mode where you give a small pre-bolus at meals but don't count carbs. Middle ground between HCL and FCL. Chapter 7.

**Meal Management** — The art of balancing carb absorption against insulin activity for good post-meal bg control. Can be fully automated (FCL), partially announced (MA), or fully manual (HCL).

**middleware** — Custom-code add-ons for Trio and iAPS that supply the Automation-like functionality these platforms lack natively.

## N

**Nightscout / NSClient** — Open-source web platform for remote bg monitoring, data logging, and remote control of AAPS.

**Nightscout Reporter** — Reporting tool that produces weekly/monthly summaries from Nightscout data. Useful for identifying outlier days and patterns.

**normalTarget** — Hard-coded reference point in AAPS (99 mg/dL from AAPS 4.2.1 onwards; was 100 before). Used in the exercise-mode sensitivity ratio formula.

## O

**occlusion** — Partial or total cannula blockage that slows or stops insulin delivery. Produces hard-to-explain glucose rises and can destroy FCL performance.

**odd target (even/odd target)** — autoISF feature: odd-numbered bg targets (profile or TT) block SMBs entirely; even-numbered allow them. Your emergency SMB brake. See §2.4.

**Open Source** — Transparent, collaboratively-developed software available on GitHub. All DIY loops are open source.

**open loop** — Mode where the loop recommends actions but doesn't enact them — the user must approve each SMB/TBR. AAPS Objective 5.

**oref** — The algorithm family used in AAPS, Trio, and iAPS. Derived from the OpenAPS reference implementation. Distinct from iOS Loop's MPC algorithm.

**override (iOS Loop)** — Temporary %sensitivity change. Oref equivalent: profile switch.

## P

**parabola fit** — Mathematical technique autoISF uses on recent CGM values to detect acceleration. More precise than raw delta thresholds.

**patient type** — AAPS setting that caps maxIOB based on user category (child, teen, adult). Designed to prevent dangerous overrides.

**peak (bg peak)** — Highest bg value reached after a meal. A major tuning target: lower peaks → easier late-meal management.

**pod** — Disposable insulin-delivery module for pod-based pumps (Omnipod, etc.).

**pp_ISF** — autoISF component active during the post-prandial (post-meal) steep linear rise. Second most important weight after bgAccel_ISF. See §4.3.

**pre-bolus** — Meal bolus given 5–20 minutes before eating, to give insulin a head-start against carbs. Used in HCL and MA mode; not in FCL.

**predictions** — Future bg projections calculated by the loop. In oref: eventualBG, IOBpredBG, ZTpredBG, COBpredBG, UAMpredBG (for different scenarios).

**profile** — Basic treatment settings (basal schedule, DIA, IC, ISF schedule, bg target). The foundation on which autoISF builds.

**profile switch (%profile)** — Temporary change of profile (e.g., 80% for exercise, 130% for illness). Multiplies basal, ISF, and iobTH proportionally.

## R

**readthedocs** — Online documentation site for each DIY loop project.

**recommended dose** — iOS Loop equivalent of oref's insulin required.

**remote control** — Parent-operating-child or caregiver-operating-user setups using NSClient or Loop Caregiver.

**resistance (insulin)** — Above-normal insulin need. Common after fatty meals, during illness, with hormonal changes.

**retrospective correction effect** — iOS Loop feature that learns from recent prediction errors to improve future predictions.

**roller-coaster** — Glucose pattern with large swings up and down. Usually indicates over-aggressive ISF or unstable settings.

## S

**sens** — The effective ISF after all modulations, displayed in the AUTO ISF tab.

**sensitivity** — Below-normal insulin need. Common after exercise or on days of high activity.

**sensitivity adaptation** — Methods for tracking and adjusting to sensitivity changes: Autosens, dynamicISF, Activity Monitor, autoISF, or manual temp %profile switches.

**sensitivity detection** — Calculation of sensitivity from bg deviations. Used by Autosens.

**sensor noise** — Unstable or jumpy CGM readings. Problematic for aggressive delivery settings and FCL acceleration detection.

**sigmoid (dynamicISF)** — Dev variant of dynamicISF with S-curve ISF response. Not recommended for Trio/iAPS beginners.

**SMB (Super Micro Bolus)** — Small boluses delivered by the loop, faster than temp basal. In HCL, limited to ~120 min of basal; in FCL, extended via `smb_max_range_extension`. iOS Loop equivalent: autoBolus.

**SMB delivery ratio** — Fraction (0–1) of calculated `insulin required` delivered per SMB cycle. AAPS default 0.5; raised to 0.6–0.7 in FCL. Values > 0.75 not recommended (CGM jitter sensitivity).

**SMB range extension** — Multiplier on the base 120-min-of-basal SMB size limit. Widened in FCL (typically 2.0–3.0) so SMBs can replace meal boluses. See §3.1.

**smoothing** — Algorithms that reduce CGM noise by averaging or interpolating values. Useful but costs you the earliest signs of rises. Configured in AAPS Configuration Builder.

**source code** — The underlying code of a DIY loop. Open source = freely readable, modifiable, and branchable on GitHub.

## T

**TAI** — Trio + autoISF. The autoISF-integrated dev branch of Trio for iPhone.

**TBR (Temp Basal Rate)** — Temporary adjustment to basal, expressed as % of profile. Slower bg control than SMBs but always running.

**TDD (Total Daily Dose)** — Total insulin (bolus + basal) per day. Rough characterization of insulin need. Spikes during occlusions.

**TIR (Time In Range)** — Fraction of time bg is within a target range (typically 70–180 mg/dL). The primary performance metric for looping.

**TITR (Time In Tight Range)** — Time within 70–140 mg/dL. Used for more ambitious %TIR goals; usually requires HCL rather than FCL.

**Tirzepatide / Mounjaro®** → see `GLP-1 receptor agonist`.

**Trio** — iPhone-based oref loop. Has a dev port of autoISF.

**Tsunami** — AAPS-derived dev variant with a Meal Announcement workflow. See §8.3.

**TT (Temporary Target)** — Temporary bg target override. Used for exercise (high TT), EatingSoon (low TT), anti-hypo snack (odd TT for SMB shutoff), and many other cases.

**tuning** → see `individualized tuning`.

## U

**UAM (Un-Announced Meal)** — oref's ability to detect rises without carb inputs and respond with SMBs. The basis of both FCL and the SMB+UAM algorithm in modern AAPS.

**UTC / UTZ / CET** — Time zones. AAPS logfiles use UTC internally; local-time display is a phone setting. For emulator work, subtract your offset from local time to get UTC.

## V

**vanilla** — Informal term for unmodified Master AAPS (or other unmodified loop releases).

**virtual pump** — AAPS test option for running loop logic without a physical pump attached. Used in AAPS Objectives.

## W

**\_weight** → see `ISF_weight`.

**wiki** → see `readthedocs`.

## X

**Xcode** — Apple's developer software needed to build and maintain a personal copy of iAPS or iOS Loop.

**xDrip+** — Open-source CGM reader app that passes (optionally smoothed) values to AAPS. Also a rich alarms platform.

## Y

**YDMV (Your Diabetes May Vary)** — Community reminder that responses to interventions vary person-to-person. Don't treat any single example as universal.

## Z

**zero-tempting** — Temp basal at 0% (no basal insulin delivery). Often applied by the loop after large SMBs or when bg is heading toward target. Limits the loop's ability to respond quickly to new highs — one reason dual-hormone loops are attractive.

# Appendix B — Case Studies Index

The case studies live alongside the source material on the author's GitHub. They're numbered by the section they illustrate. This index lists the case studies referenced throughout this book.

> 📁 **Where to find them:** https://github.com/bernie4375/FCL-potential-autoISF-research — look for files named `case_study_X.Y_*.pdf`.

## Chapter 1 — Prerequisites

| Case Study | Title                                         | What it shows                                                     |
|------------|-----------------------------------------------|-------------------------------------------------------------------|
| 1.1        | Occlusion                                     | 25% TIR loss on a cannula-failure day; why early cannula changes matter |
| 1.2        | Comparing insulins for FCL                    | Modeling comparison of Lyumjev, Fiasp, Apidra, Humalog in FCL    |
| 1.3        | Jumpy CGM                                     | How CGM artefacts can be misinterpreted as meal starts           |
| 1.4        | Lost pump connection                          | Why Bluetooth stability matters around meals                      |
| 1.5        | Permanent CGM values w/ 2× G6                 | Overlapping G6 sensors as the gold-standard CGM setup            |
| 1.6        | When catastrophe strikes                      | Multi-failure scenarios and recovery                              |
| 1.7        | MDI when the loop dies                        | Fallback to pen-based therapy when the loop is unavailable       |
| 1.8        | Libre 3 / 1-minute case                       | **Placeholder** — call for a case study from a Libre 3 user       |

## Chapter 4 — Meals and ISF Weights

| Case Study | Title                         | What it shows                                                       |
|------------|-------------------------------|---------------------------------------------------------------------|
| 4.1        | Pizza                         | Worked example of tuning `_weights` for various autoISF factors   |
| 4.2        | Low carb meals                | Tuning for slow-absorption meals; role of dura_ISF                 |
| 4.3        | Hands-off FCL around Christmas| Real-world holiday week with full FCL                               |

## Chapter 5 — Modulating Loop Aggressiveness

| Case Study | Title                                  | What it shows                                                |
|------------|----------------------------------------|--------------------------------------------------------------|
| 5.2        | Sweet snacks / Glühwein with DIY cockpit | Building a snack-announcement button and related Automations |
| 5.3        | Compression low                        | Night-time CGM artefacts and how to prevent over-reaction    |

## Chapter 6 — Exercise and Activity

| Case Study | Title                                        | What it shows                                                         |
|------------|----------------------------------------------|-----------------------------------------------------------------------|
| 6.2        | Biking day with hi-carb lunch; DIY cockpit   | The 3-Automation pattern for meal-before-exercise (§6.5) in practice |

## Chapter 7 — Advanced HCL with Meal Announcement

| Case Study | Title                          | What it shows                                               |
|------------|--------------------------------|-------------------------------------------------------------|
| 7.1        | Meal Announcement (5 year old) | MA-based setup for a young child                             |

## Chapter 9 — Performance Monitoring

| Case Study | Title                                          | What it shows                                                |
|------------|------------------------------------------------|--------------------------------------------------------------|
| 8.2        | Futility of tuning based on 1 extreme meal     | Negative example — over-optimization for one meal hurts others |

## Chapter 10 — Troubleshooting

| Case Study | Title                                     | What it shows                                   |
|------------|-------------------------------------------|-------------------------------------------------|
| 9.1        | Un-intended loss of loop aggressiveness   | Diagnosing silent aggressiveness regressions    |

## Chapter 8 — Other Avenues to FCL

| Case Study | Title                                                | What it shows                                                |
|------------|------------------------------------------------------|--------------------------------------------------------------|
| 13.1       | Comparison: 1 month FCL, Automation vs. autoISF      | Side-by-side comparison of the two AAPS FCL approaches       |
| 13.2       | FCL using dynamicISF                                 | **Call for submission** — no interpretable data yet           |
| 13.3       | Boost-based FCL for a child                          | Boost in practice for paediatric looping                     |
