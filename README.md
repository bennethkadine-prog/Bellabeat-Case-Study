# Bellabeat-Case-Study: What Fitness-Tracker Habits Say About Engagement
A consumer-insights analysis of 35 smart-device users, built in Python (pandas, matplotlib)

This case study uses Fitbit activity and sleep data as a proxy to explore questions relevant to Bellabeat membership behavior. The analysis examines recording coverage, weekday and weekend activity, peak activity hours, and the relationship between sleep and activity. Fitbit users are not Bellabeat members, so findings may not represent Bellabeat customers.

TL;DR
Engagement is moderate and no one is fully engaged. The most engaged user wore the device on 79% of days; most sit near two-thirds.
Activity peaks twice a day (midday and 6-7 pm), with a dip at 3 pm. Weekends look different: one broad afternoon peak and a later start.
Sleep tracking is a habit split. 24 of 35 users logged sleep, and those who did were either near-daily or barely at all.
Heavy sleep-loggers also move more (median about 8,460 vs 5,860 daily steps). This is an association in a small sample, and it likely reflects general device engagement more than anything about sleep.

1. Business task
Bellabeat is a wellness-technology company focused on women's health. This analysis asks how people use a smart tracker day to day, and what that suggests for marketing the Bellabeat app and its wearables.

Stakeholders: marketing and product teams. Guiding question: which usage patterns could shape engagement and messaging strategy?

2. Data
Public Fitbit tracker data (Kaggle), covering March 12 to May 12, 2016 (62 days). Three tables:

Table	|Grain|	Window|	Users|
----------------------------
Daily activity	|user x day|	62 days|	35
Hourly steps	|user x hour	|62 days	|35
Sleep	|user x night	|April 12 to May 12 (31 days)	|24

Activity and steps arrived as two files each (one per collection period), which I combined

3. Cleaning
Step	Result
Combined split files	Activity 1,397 rows; hourly steps 46,183 rows
Standardized column names	Lowercase across all tables
Removed duplicates	24 activity, 3 sleep, 175 hourly rows
Checked nulls	None in any table
Parsed dates	Sleep and hourly timestamps converted to datetime
Verified user IDs	All 35 users appear in both activity and steps
The key catch: sleep data covers only the second half of the study period. Any comparison involving sleep had to be restricted to the matching dates, or the two sources would measure different windows.

4. Analysis
4.1 How engaged are users?
A day counted as "worn" if it had any steps or fewer than 1,440 sedentary minutes (an all-sedentary, zero-step day looks like a device sitting on a shelf). Share of days worn per user:

Mean 57.5%, median 64.5%, max 79%.
Two users recorded almost nothing (under 10 days).
I grouped users by share of days worn: High (over 65%): 17, Medium (45-65%): 13, Low (under 45%): 5. These cut-offs are a judgment call, not natural breaks in the data.

[add image]

4.2 What does everyday movement look like?
On days the device was worn, the average user recorded about 949 sedentary minutes, 203 lightly active, 15 fairly active and 22 very active. Most worn days are close to full-day recordings: 97% logged at least 10 hours and 88% at least 15.

Engagement group	Sedentary	Lightly	Fairly	Very
Low	1,192	108	26	13
Medium	991	209	13	17
High	899	210	15	25
Low-engagement users have very high sedentary time and little light activity. Some of that is likely partial wear (the device records "sedentary" by default), so I treat the Low row with caution.

4.3 When are users active?
[add image]
Activity follows a two-peak day: a midday peak (12-2 pm) and a higher evening peak (6-7 pm), with a short dip around 3 pm and near-zero movement from 1 to 4 am.

[addimage]
Weekdays show both peaks and a sharp 3 pm dip. Weekends show one broad early-afternoon peak, a morning start about an hour later and lower evening activity.

4.4 Sleep tracking and activity
24 of 35 users (69%) logged sleep. Nights logged per user (mean 17.1, median 20.5, range 1-31) form a U-shape: many near-daily loggers, a cluster of light loggers and a thin middle.
[addimage]
I grouped loggers as Low (1-7 nights), Mid (8-21), High (22+) and compared average daily steps over the shared April 12 to May 12 window:

Group	Users	Mean steps	Median steps
Low	8	6,289	5,861
Mid	4	4,941	4,519
High	12	8,575	8,463
[addimage]

High loggers have a median about 2,600 steps above Low loggers, and their middle half is much tighter (roughly 8,000 to 9,900 steps, versus about 2,500 to 8,400 for Low). Mid has only four users, so I report it but do not interpret it.

5. Recommendations
Treat wear habit as the core engagement problem. No user reached 80% of days. Onboarding and reminder strategy that builds a daily wearing routine likely matters more than adding features.
Time nudges to real behavior. Evening (6-7 pm) and midday (12-2 pm) are when users already move; the 3 pm dip is a natural window for a prompt. Use a later, single-peak schedule on weekends.
Segment sleep-feature messaging. Light sleep-loggers and non-loggers (11 users never logged) are a distinct audience from near-daily loggers. Test prompts aimed at converting the light group into a routine.
Use engagement as the segmentation variable. Heavy loggers are both more active and more consistent, which makes engagement a practical way to tailor messaging.
