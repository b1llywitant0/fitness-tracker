# fitness-tracker
Been hitting the gym for around 6 months and tracking everything manually. This project aims to make fitness data easier to store and document by exploring the path from Telegram logs to dashboards, while incorporating AI coaching to provide personalized fitness recommendations.

## Planned tech stacks
                    ┌─────────────────────┐
                    │     User (You)      │
                    └──────────┬──────────┘
                               │
                     Workout Log Message
                               │
                               ▼
                    ┌─────────────────────┐
                    │ WhatsApp / Telegram │
                    └──────────┬──────────┘
                               │ Webhook
                               ▼
           ┌──────────────────────────────────────┐
           │        Cloud Run (Serverless)        │
           │                                      │
           │  • Receive message                   │
           │  • Store raw workout log             │
           │  • Call Gemini AI                    │
           └──────────┬───────────────────────────┘
                      │
                      ▼
           ┌──────────────────────────────────────┐
           │            Gemini API                │
           │                                      │
           │ Converts:                            │
           │ "Bench 40kg x 6,5,4"                 │
           │ into structured JSON                 │
           └──────────┬───────────────────────────┘
                      │
                      ▼
           ┌──────────────────────────────────────┐
           │             BigQuery                 │
           │                                      │
           │ Raw Layer                            │
           │ • raw_messages                       │
           │                                      │
           │ Parsed Layer                         │
           │ • workout_sessions                   │
           │ • exercise_sets                      │
           └──────────┬───────────────────────────┘
                      │
                dbt Models using Git Actions
                      │
                      ▼
           ┌──────────────────────────────────────┐
           │          Analytics Layer             │
           │                                      │
           │ • Weekly Volume                      │
           │ • Estimated 1RM                      │
           │ • PR Tracking                        │
           │ • Recovery Metrics                   │
           │ • Muscle Group Volume                │
           └──────┬─────────────────┬─────────────┘
                  │                 │
                  ▼                 ▼

     ┌──────────────────┐  ┌──────────────────┐
     │  Looker Studio   │  │    AI Coach      │
     │                  │  │                  │
     │ Dashboards       │  │ Recommendations  │
     │ Trends           │  │ Q&A              │
     └──────────────────┘  └──────────────────┘

### Future ideas
Other than storing the workout performance data, another several improvement that can be implemented later:
1. "Give me workout template to be filled with target weight and reps based on past performance." Don't have to type things from scratch. Input: Split of the day. 
- This way, if not adding movement, then user will only have to fill their RIR to track their set. Since I usually forget which set I am in. lol.
2. Template movement modification based on goal or pain points.
3. Since I also run and swim, will try integrate with my Garmin data as well.