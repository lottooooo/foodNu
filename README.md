# 🍳 foodNu — fridge to recipe

**An AI-native food operating system for everyday home cooks.**
*Submitted to the App Store · built solo with Claude Code*

foodNu turns your fridge into the starting point for every meal decision. Scan your fridge, talk to **Chef Kai** (your AI sous-chef), and get a personalised recipe that fits what you have, your energy tonight, and your health goals — with the meal logged automatically when you cook it.

> We're building for the moment every other food app loses the user: the tired Tuesday evening when the plan falls apart and DoorDash wins. That's the moment foodNu is designed for.

## 🎬 Demo

https://github.com/user-attachments/assets/45da2194-6a84-4d5a-be7b-dfeb837482a3

## ✨ What's been built

- 🧊 **Fridge inventory** — Your live fridge, always in view. Items are auto-categorised (vegetables, meat, dairy, condiments) and flagged when they're going stale. Add items manually or scan to update the whole lot at once.
- 📸 **Fridge scanner** — Point your phone at the fridge, take a photo, and the AI reads every visible ingredient — quantities included. A review screen lets you correct anything before confirming; the confirmed list saves to a persistent inventory that updates with every scan.
- 👨‍🍳 **Chef Kai — conversational recipe engine** — After scanning, Chef Kai opens a chat. He knows what's in your fridge, what you're avoiding, how tired you feel tonight, and what you've told him before. He suggests one recipe at a time, refines it through conversation, and once you lock it in — that's your dinner.
- 📖 **Recipe tab — saved cookbook** — Every recipe you've accepted from Kai lives here. Filter by occasion (Quick Weekday, Low Energy, Weekend Cook), tap into the full recipe with steps and macros, and cook from it directly. "Cook it again" logs it straight to the diary; "Tweak with Chef Kai" reopens the recipe in Kai chat for modifications.
- 📔 **Diary tab** — A food log that mostly fills itself. When you cook a Kai recipe, it's logged automatically; for anything else, a quick note or photo does it. Calendar view shows every day at a glance.
- ⚙️ **Customize tab** — Tell Kai who you are: your cooking skill level, what appliances you have, any dietary restrictions, and what you love or avoid. He uses all of it — every session, no re-explaining needed.

## 🛠️ Tech stack

| Layer | Choice |
|---|---|
| **Mobile** | React Native + Expo (SDK 54), TypeScript |
| **State** | Zustand |
| **Backend** | Python (FastAPI) |
| **AI — vision** | GPT-4o-mini (fridge scanning) |
| **AI — recipes** | GPT-4o-mini (Chef Kai conversations) |
| **Database** | Supabase (PostgreSQL) |
| **Built with** | Claude Code (development) |

## 🧪 Engineering highlights

- **Prompt evaluation harness** — a 100-case suite scored by two independent graders: a deterministic 7-check code grader and an out-of-family LLM judge (to avoid self-grading bias). Iterated across four gated rounds — recipe quality **+36%** first-turn / **+22%** multi-turn, with every measured dietary-safety and ingredient-hallucination failure driven to zero. Caught the judge itself drifting (identical replies scoring 3/10 vs 9/10 across runs) and fixed it by pinning calibration anchors and moving every objective check into the deterministic grader.
- **Deterministic guardrails in Python, not prompt text** — a leak guard, dietary-conflict filter, quantity-label sanitizer, and confirmation gate wrap the model call, so routing and gating can't drift at high temperature ("data beats the rule").
- **Orchestrated recipe pipeline** — a single generation call on the first turn; multi-call orchestration (intent classification, cuisine resolution, inventory-change detection) on follow-ups.
- **Production foundations** — per-user data isolation (Sign in with Apple + JWT + row-level security), per-user rate limiting to bound API cost, and full-funnel event analytics across the cook loop.
