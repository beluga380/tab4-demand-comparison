# Tab 4 (Demand Comparison): what to do, recording script, submission

## 1. Get Tab 4 into the live app

1. Send Sanika your GitHub username and accept the collaborator invite (check your email).
2. Clone the repo: `git clone https://github.com/sanikawankhade87/ai-data-centre-expansion` then `cd ai-data-centre-expansion`
3. Unzip `Tab4_Demand_Comparison.zip` and copy into the repo root:
   - `tab4_demand.py`
   - `data/monthly-spending-data-center-us.csv` (byte-for-byte the same as the OWID download of 23 Oct 2026. If the Tab 1 owner already added a file with this exact name, keep theirs.)
4. Download the two Census files and save them into `data/` **without renaming them**:
   - National.xlsx: https://www.census.gov/hfp/btos/downloads/National.xlsx
   - AI Core Questions.xlsx: https://www.census.gov/hfp/btos/downloads/AI%20Core%20Questions.xlsx
     (on the BTOS Downloads page it sits under "Historical Data" → "AI Core Questions (Original)")
5. Open `requirements.txt` and add one line: `openpyxl` (it reads the .xlsx files). Leave the other lines alone.
6. Test on your laptop: `pip install -r requirements.txt` then `streamlit run app.py`. Open Tab 4. You should see "AI use kept pace" and "Building ran ahead" on the two cards, and the trace should say **row 16**.
7. Push it:
   ```
   git add tab4_demand.py requirements.txt "data/National.xlsx" "data/AI Core Questions.xlsx" data/monthly-spending-data-center-us.csv
   git commit -m "Add Tab 4: demand comparison"
   git pull --rebase
   git push
   ```
8. Wait 2 to 5 minutes, open https://ai-data-centre-expansion.streamlit.app/ and check Tab 4 loads. If it shows an error about `openpyxl`, step 5 was missed. If the app is stuck, open the app's "Manage app" menu (bottom right, only visible to the repo owner) and reboot, or ask Sanika to.
9. Front page answer. `app.py` still says "To be written from Tab 4's comparison." It's a shared file, so message Sanika first, then replace that line with:
   ```python
   ANSWER = (
       "Partly. From 2023 to late 2025, the share of US firms using AI grew as fast as data centre "
       "construction spending. Since November 2025, construction spending has grown clearly faster "
       "than AI use, so the newest wave of building is running ahead of measured demand (Tab 4)."
   )
   ```
   This matters for your recording too, because you start on the front page.
10. Tell the group in one message: Tab 4 is live, it uses the Census BTOS series only (Epoch training compute left out, reason is in the tab), and the Census changed its AI question in Nov 2025 so the tab has two comparison windows.

**Version note.** Census updates National.xlsx every two weeks (the copy checked here was updated 22 Oct 2026). If you download a newer release, the app recalculates on its own but the numbers below may move a little. Always read numbers off your own screen when recording.

## 2. Numbers you will trace (files of 22–23 Oct 2026)

| What | Where | Value |
|---|---|---|
| AI use, base month Nov 2025 | National.xlsx → sheet "Response Estimates" → row 16, cells AB16 and AA16 | 17.3% and 17.2% → mean 17.25 |
| AI use, end month Aug 2026 | same row, cells I16 and H16 | 22.4% and 23.2% → mean 22.80 |
| AI use index | 22.80 ÷ 17.25 × 100 | **132.2** |
| Construction, Nov 2025 | monthly-spending-data-center-us.csv, line 144 | 3189271464 |
| Construction, Aug 2026 | same file, line 153 | 5371310412 |
| Build index | 5371310412 ÷ 3189271464 × 100 | **168.4** |
| Verdict ratio | 132.2 ÷ 168.4 | **0.78** (below 0.90, so "building ran ahead") |

Period codes are two-week survey periods: 202524 = 3–16 Nov 2025, 202525 = 17–30 Nov 2025, 202617 = 27 Jul–9 Aug 2026, 202618 = 10–23 Aug 2026 (sheet "Collection and Reference Dates"). Each period counts in the month its reference period ends, and the periods in a month are averaged.

Two things you might get asked:
- The 2026 Census file words the question as "Super Intelligence or SI (formerly referred to as Artificial Intelligence or AI)". That is the Census Bureau's own wording in the file, same question as the November 2025 revision.
- The 10% "too close to call" band is our addition. The proposal says "clearly faster" without a number, so the tab sets it at 10% and says so in the trace.

## 3. Recording script (about 4:15 at a normal pace)

Before recording: browser zoom 125% or more, the live app open on the front page, National.xlsx open in Excel at sheet "Response Estimates", the CSV open in Excel or Notepad, a calculator open. Turn off notifications. Use a headset mic if you have one. Do one test recording of 20 seconds and play it back.

**0:00–0:25, question and persona** (front page on screen)
"Hi, I'm Aaron. Our group's question is: Is the rapid expansion of AI data centres justified by the actual demand for AI? Our app is for Dana Reyes, an energy policy analyst deciding whether her state should build grid capacity for data centres as permanent demand."

**0:25–1:25, my contribution** (click Tab 4, scroll slowly, then flash the file on GitHub for 3 seconds)
"I built Tab 4, Demand Comparison, which is this file, tab4_demand.py, in our repository. Tabs 1 to 3 show how much is being built. My tab checks that against how many US businesses actually use AI. I compare two Census Bureau series: monthly construction spending on data centres, in constant 2021 dollars, and the Business Trends and Outlook Survey, which asks firms every two weeks whether they used AI.
The survey changed its AI question in November 2025, so I split the comparison into two windows. From September 2023 to September 2025, AI use grew faster than construction: index 269 against 236. Since November 2025 it's the other way round: construction reached 168 but AI use only 132. So for Dana, the newest building is running ahead of measured use, and part of that load may not be permanent."

**1:25–2:30, design decision** (point at the chart)
"The visual task is comparing the growth rate of two things measured in different units, dollars and percent of firms. I put both on one axis as an index, with the first month of each window set to 100, so the steeper line is the one growing faster.
The alternative I rejected was a dual-axis chart, with dollars on the left and percent on the right. I rejected it because the two scales can be stretched independently, so you can make the lines cross wherever you like. The chart would be deciding the answer instead of the data.
A second decision: I didn't join the two AI lines into one. Between the two question wordings the share jumps from about 10% to 17%, and that jump comes from the new definition, not new users. Joining them would show fake growth, so the panels are kept separate."

**2:30–4:00, trace a number** (open the trace expander in the app, then switch to Excel and the CSV)
"Now I'll trace the AI use index of 132 back to the source. In National.xlsx, sheet Response Estimates, row 16 is question 7, answer Yes. The base month is November 2025, which has two survey periods: cell AB16 is 17.3% and AA16 is 17.2%, average 17.25. The end month is August 2026: I16 is 22.4% and H16 is 23.2%, average 22.8. 22.8 divided by 17.25, times 100, is 132.2, which is the 132 on the chart.
For the build line, in the construction CSV, line 144, November 2025, is 3,189,271,464 dollars. Line 153, August 2026, is 5,371,310,412. Divided and times 100 gives 168.4. Then 132.2 divided by 168.4 is 0.78. That's below our 0.9 threshold, so the verdict is 'building ran ahead'."
(Type each division into the calculator on screen as you say it.)

**4:00–4:30, AI use and the check**
"I used Claude, an AI assistant, to help find the Census survey files, write the Python code for this tab, and draft this script. To check it, I recalculated the August 2026 index by hand from the Excel cells and the CSV, which is what I just showed, and it matched the app. I also read the Census Bureau's note on the November 2025 question change before deciding to keep the two windows apart. Thanks for watching."

## 4. Submit

1. Record with screen and voice (OBS, Zoom "record to computer", Xbox Game Bar with Win+Alt+R, or PowerPoint's screen recording). Face is optional.
2. Check the length is **under 5:00** (aim for 4:30). Assessors stop at 5:00.
3. Watch it once at normal speed: voice clear, chart labels and Excel cells readable.
4. Canvas → Assignment 3 Part 1: Recorded presentation → upload the file, or paste an **unlisted** YouTube/OneDrive link (check the link opens in a private window).
5. Deadline: your extension to 26 Oct. Don't leave the upload to the last hour.

## 5. Peer feedback (the other 5 marks, due Fri 6 Nov)

For **every** other group member's recording on Canvas:
- Tick the 8 checklist items honestly (ticks are spot-checked against the videos).
- Fill **both** boxes: what worked, and the one change that would most improve it.
- Name moments with rough times, for example "At 2:40 the trace showed the CSV row clearly."
- Make the improvement note something they can change, for example "Zoom the browser so the axis labels are readable at 1:15."
