# 📚 Manga Metadata Scraper & Organizer: The Sequel Nobody Asked For

> *"It's for research purposes," I whisper to my hard drive as it weeps. Again.*

## 🤔 What Even Is This? (The Director's Cut)

Look, I didn't just scrape 594,346 entries once. I scraped them *multiple times* using different methods because apparently I hate sleep and love redundancy. This is what happens when a data scientist discovers that one scraper is good, but THREE scrapers is a personality disorder.

This is a collection of Python scripts that scrape, organize, convert, merge, and generally abuse manga metadata from some hentai website into every format known to mankind. Think of it as a digital librarian that works way too hard, asks zero questions, and has developed a concerning dependency on async/await.

**TL;DR:** I turned procrastination into a data pipeline, then turned that pipeline into a HYDRA. Your FBI agent is now filing for overtime.

## 🛠️ The Arsenal (AKA: Tools I Built Instead of Having a Social Life)

### Scrapers (The Data Hunters - Now With Flavors!)

- **`faster_scraper.py`** - The speed demon. Uses the `doujin-api.onrender.com` API endpoint. 8 concurrent workers. Async. Chunked processing. Goes brrr. 🏎️💨 *The "I found a shortcut" edition.*
- **`scraper_for_linux.py`** - Same speed demon, but it directly hits `some hentai website.net/g/{id}/` like a madlad. Async. Chunked. Probably gets rate-limited more. *The "I do things the hard way" edition.*
- **`mangascraper.py`** - The OG boomer scraper. Now with command-line arguments (`--start` and `--end`). Includes image optimization and PDF generation (disabled by default because your hard drive is already crying). Like your dad's old Camry—reliable but embarrassing. *The "I learned from my mistakes" edition.*

### Data Wranglers (The Format Shapeshifters - Now With More Options!)

- **`jsonl_to_csv.py`** - Converts JSONL to CSV because some people still use Excel in 2026. Outputs `manga_all_2.csv`. We don't judge. (We do judge.)
- **`jsonl_to_db.py`** - Shoves JSONL into SQLite. Now with 100% more SQL and 0% more social life!
- **`csv_to_db.py`** - NEW: Converts CSV directly to SQLite. For when you already have CSV and don't want to deal with JSONL. Lazy? Yes. Efficient? Also yes.
- **`csv_to_parquet.py`** - Makes your data files smol and FAST. Parquet gang rise up. 📦✨
- **`merge_csvs.py`** - NEW: Merges multiple CSV files with automatic deduplication. Because apparently I scraped the same data twice and needed a way to fix it without admitting I'm an idiot.

### Utility Belt (The "I Forgot Something" Collection)

- **`clearner.py`** - Fixes those pesky string IDs that should've been integers from the start. Converts recommendation IDs too. Past me was an idiot. Current me is still an idiot, just a more organized one.
- **`sorter.py`** - Sorts your ID lists. Groundbreaking. Revolutionary. Nobel Prize pending. (It literally just sorts numbers. I'm not proud.)
- **`custom.py`** - A mysterious API caller that does... something? Even I forgot. It's like that drawer in your kitchen where you keep things "just in case."

## 🚀 Quick Start (Or: How to Explain This to Your IT Department)

### Scraping (The "I'm Doing Data Science" Phase)

```bash
# The fast way (API endpoint, fewer rate limits)
python faster_scraper.py

# The hard way (Direct some hentai website, more rate limits, more pain)
python scraper_for_linux.py

# The old-school way (with arguments, for people who like control)
python mangascraper.py --start 1 --end 10000
```

**Pro tip:** Run this at 3 AM so your roommate doesn't ask questions. Run it at 4 AM if you want to explain why your WiFi is dead.

### Converting Your Loot (The "Making It Look Professional" Phase)

```bash
# JSONL to CSV (for the normies)
python jsonl_to_csv.py

# JSONL to SQLite (for the SQL nerds)
python jsonl_to_db.py

# CSV to SQLite (for the lazy SQL nerds)
python csv_to_db.py

# CSV to Parquet (for the "I use Pandas" flex)
python csv_to_parquet.py

# Merge multiple CSVs (for the "oops I scraped twice" moment)
python merge_csvs.py
```

### Image Optimization & PDF Generation (The "I Have Too Much Time" Phase)

The `mangascraper.py` now includes:
- **Image optimization** - Converts body pages to grayscale (60% size reduction), keeps cover in color
- **PDF generation** - Packs optimized images into PDFs (disabled by default because your SSD is already screaming)

## 📦 What You'll Need (Besides Therapy and a Better Life)

```bash
pip install aiohttp beautifulsoup4 requests pandas pyarrow sqlite3
```

*(Also img2pdf and Pillow if you're feeling nostalgic and want PDFs. But let's be real, nobody uses those anymore.)*

**Optional (for the masochists):**
```bash
pip install curl-cffi  # For the mangascraper.py if you want to use it
```

**System Requirements:**
- Python 3.7+ (because we're not animals)
- A stable internet connection (and an unstable life)
- Approximately 2GB of disk space (and 0GB of shame)
- A good explanation ready for when someone asks what you're downloading
- Patience. Lots of patience. Like, therapy-level patience.

## 🎯 Features That Slap (Harder Than Your Mom Finding Your Browser History)

- **Multiple scraping methods** - API endpoint, direct site, or old-school. Pick your poison.
- **Async scraping** - Because waiting is for chumps and people with patience
- **Auto-retry logic** - Handles rate limits like a champ. Gets rejected, tries again. Unlike your dating life.
- **Duplicate prevention** - Tracks good/bad IDs so you don't waste time. Unlike this entire project.
- **Chunked processing** - Processes IDs in batches. Smarter than my first attempt.
- **UTF-8 support** - Japanese characters? ✓ Chinese? ✓ Emojis? ✓ Your dignity? ✗
- **Multiple export formats** - CSV, SQLite, Parquet. More formats than your ex had excuses.
- **CSV merging** - Combines multiple CSVs with deduplication. For when you realize you scraped the same data twice.
- **Image optimization** - Grayscale conversion for body pages. Saves space. Looks terrible. Worth it.
- **Sleep prevention** - Your PC won't doze off mid-scrape (Windows only). Someone should stay awake for this.
- **Error handling** - Fails gracefully, unlike my life choices
- **Progress tracking** - Watch numbers go up. It's like dopamine, but sadder.
- **Consecutive failure detection** - Stops when it realizes there's nothing left to scrape. Smart enough to quit.

## 📊 Data Schema (AKA: What Did I Even Scrape? Twice?)

Each entry includes:
- **ID** - A unique number, like your social security but less useful
- **Title** - Usually in Japanese. Google Translate is your friend. Or enemy. Depends.
- **Upload Date** - When this blessed content graced the internet
- **Artists, Groups, Parodies, Characters** - The who's who of... art
- **Tags** - Oh boy. So many tags. Too many tags. Tags you didn't know existed. Tags that make you question humanity.
- **Categories** - For organizational purposes (lying to ourselves is free)
- **Language** - Mostly Japanese. Some English. All questionable.
- **Page count** - How long your "research" will take
- **Favorites** - Community popularity metric (yes, there's a community, and yes, they're judging you)
- **Cover image URL** - For thumbnails. And science. Definitely science.
- **Recommendations** - Because algorithms know you better than you know yourself. Scary, right?

## 📈 The Dataset (Or: My Magnum Opus of Questionable Decisions - Now With Sequels)

The `manga_all.csv` file contains **594,346 entries** spanning IDs from 1 to 629,832.

Yes, you read that right. **HALF A MILLION ENTRIES.** That's more entries than:
- Books in a small library
- Days you've been alive (probably)
- Reasons this was a good idea (definitely)
- Times I've questioned my life choices (ongoing)

I spent more time scraping this than I've spent on my actual job. My therapist has a therapist now.

**Columns (14 total):**
- `id` - Unique identifier (like a social security number for "art")
- `title` - Full title (often longer than a CVS receipt)
- `date` - Upload date (YYYY-MM-DD format, because ISO 8601 is the only standard I respect)
- `parodies`, `charecters`, `groups`, `categories`, `language`, `tags`, `artists` - JSON arrays of metadata (yes I misspelled "characters" in the code, no I'm not fixing it now, it's a feature)
- `favorites` - How many people publicly admitted to liking this
- `num_pages` - Page count (for time management purposes)
- `recommendations` - "If you liked this, you'll love..." (the algorithm is judging you harder than I am)
- `cover_image` - Direct URL to cover art (SFW-ish... depends on your workplace and your life choices)

**Sample entry:**
```
ID: 1
Title: (C71) [Arisan-Antenna (Koari)] Eat The Rich! (Sukatto Golf Pangya)
Date: 2014-06-28
Pages: 14
Favorites: 3,029
```
*Ah yes, ID #1. The beginning of a beautiful disaster. The first of many poor decisions.*

All text fields support full UTF-8 (Japanese, Chinese, emojis, hieroglyphics, ancient Sumerian, your browser history, you name it) thanks to `ensure_ascii=False` in the export scripts.

**File sizes:**
- CSV: Too thicc for GitHub (that's what she said)
- Parquet: Smol and spicy
- SQLite: Compact and queryable
- JSONL: Raw and unfiltered

**Solution:** Uploaded to HuggingFace because they don't judge → [Dataset Link](https://huggingface.co/datasets/NoobEngineere/NSFW_Manga)

*Warning: Downloading this dataset will raise questions from your ISP, your IT department, your cat, and your therapist.*

## ⚠️ Legal Disclaimer (The "Please Don't Sue Me" Section - Now With More Desperation)

This is for **educational purposes**. And by educational, I mean you'll learn:
- How web scraping works
- How async Python works
- How to disappoint your parents
- How to explain your GitHub activity to recruiters
- How to merge CSVs when you realize you scraped the same data twice
- How to optimize images for PDFs nobody will use

**Rules of Engagement:**
- Don't be weird (weirder than this already is)
- Respect rate limits (the site has feelings too, apparently)
- Don't DDoS anyone (that's just rude and illegal)
- Be cool (unlike this project)
- If you get caught, you don't know me
- This is public data (I checked... twice... okay three times... maybe four)
- Use the API endpoint if possible (it's nicer to the servers)

**Disclaimer:** I am not responsible for:
- Your browser history
- Your hard drive contents
- Your IT department's questions
- Your significant other's concerns
- Your therapist's notes
- Whatever the FBI thinks this is
- Your electricity bill
- Your PC's fan noise
- Your roommate's questions
- Your life choices

## 🤷 FAQ (Frequently Avoided Questions - Now With Sequels)

**Q: Why does this exist?**  
A: Bold of you to assume I have a good reason. Data hoarding is a perfectly valid hobby, okay? Don't judge me. Also, I apparently needed to do it THREE times.

**Q: Is this legal?**  
A: Scraping public data is generally fine. What you do with it is between you, your conscience, your browser's incognito mode, and the FBI.

**Q: How long did this take?**  
A: Long enough that I've forgotten what sunlight looks like. The scraper ran for days. DAYS. My electricity bill is crying. My hard drive is crying. I'm crying.

**Q: Why are there multiple scrapers?**  
A: Because I'm an idiot who discovered that different methods work differently. One uses an API, one uses direct scraping. They're like Pokémon, but sadder and more illegal.

**Q: Why is there a merge script?**  
A: Because I scraped the same data twice and needed a way to fix it without admitting I'm an idiot. Spoiler: I'm an idiot.

**Q: Can I use this for other sites?**  
A: Sure, but you'll need to rewrite like... everything. Also, please get better hobbies. Seriously. Go outside.

**Q: Why are there so many scraper files?**  
A: Evolution, baby. Each one is slightly less terrible than the last. It's like Pokémon, but sadder and more ethically questionable.

**Q: Did you actually scrape 594K entries?**  
A: Yes. Yes I did. Multiple times. Do I regret it? Ask me after therapy. And after my electricity bill arrives.

**Q: What's your GitHub streak?**  
A: Longer than my last relationship, thanks for asking. Also longer than my attention span.

**Q: Should I put this on my resume?**  
A: Depends. Are you applying to work at a data company or explaining yourself to HR? Also, maybe don't mention the "scraped it three times" part.

**Q: Are you okay?**  
A: Define "okay." Also, no.

**Q: Why is there image optimization?**  
A: Because I realized PDFs were huge and decided to make them less huge. Grayscale manga looks terrible but saves space. It's a trade-off I'm not proud of.

**Q: What's the difference between the scrapers?**  
A: `faster_scraper.py` uses an API (faster, fewer rate limits). `scraper_for_linux.py` hits some hentai website directly (slower, more rate limits). `mangascraper.py` is the old one with arguments and PDF support. Pick your poison.

## 🎓 Pro Tips (From Someone Who Learned The Hard Way - Multiple Times)

- **Start small.** Don't scrape 500k IDs on your first run like I did. Learn from my mistakes (and my therapist's notes).
- **The site has rate limits.** The scripts handle it, but don't be greedy. We're pirates, not monsters. Also, use the API endpoint if possible.
- **Use `faster_scraper.py`** unless you need PDFs. And let's be honest, nobody needs PDFs in 2026.
- **Run it overnight.** Your PC will sound like a jet engine. Your roommate will ask questions. Your electricity bill will cry. Have lies prepared.
- **SQLite is great for querying.** CSV is great for sharing. Parquet is great for flexing on data scientists. Merge CSVs when you realize you scraped twice.
- **Back up your data.** Losing 594K entries after days of scraping will make you cry. I know. I cried. Multiple times.
- **Use a VPN.** Not for legal reasons. Just for peace of mind. And plausible deniability.
- **Clear your terminal history.** Trust me on this one. Your future self will thank you.
- **Don't tell your friends.** They won't understand. They'll judge. They're not ready. They'll never be ready.
- **Check for duplicates.** Use `merge_csvs.py` if you accidentally scraped the same data twice. Not that I would know anything about that.

## 🐛 Known Issues (AKA: It's Not A Bug, It's A Feature)

- Sometimes the site just... doesn't respond. That's life. That's web scraping. That's depression.
- PDF generation is slow and disabled by default. Because I value your time more than I value mine.
- The code has comments like "Be polite" and "Don't let the user be stupid." Past me was optimistic.
- `clearner.py` is misspelled. It should be `cleaner.py`. I'm not fixing it. We live with our mistakes.
- The scraper sometimes gets rate limited. It's like getting rejected, but by a server.
- UTF-8 encoding issues if you're on Windows. Because Windows hates fun.
- Your antivirus might flag this. It's not malware. It's just... misunderstood.
- Running this will make your PC fans sound like a Boeing 747 taking off.
- The dataset is too large for GitHub. Even GitHub said "nah fam."
- My code style is inconsistent. Some files have docstrings. Some have existential crisis comments.
- I scraped the same data multiple times. Yes, I know. Yes, I'm aware. Yes, I have the merge script.
- Image optimization makes manga look like it's from 1995. But it saves space!
- The API endpoint might go down. The direct scraper is slower but more reliable. Pick your poison.

## 📝 License

MIT License, which means:
- You can use this
- You can modify this
- You can distribute this
- You can't sue me
- You can't blame me for your life choices
- You definitely can't put this on your LinkedIn
- You probably shouldn't tell anyone you used this

**In other words:** Do whatever you want, just don't tell anyone I helped. And definitely don't tell them I scraped it three times.

---

## 🏆 Achievements Unlocked

- ✅ Scraped 594,346 entries
- ✅ Scraped them again (because I'm an idiot)
- ✅ Scraped them a third time (using a different method)
- ✅ Learned async Python the hard way
- ✅ Maxed out my hard drive
- ✅ Disappointed my parents
- ✅ Created a dataset larger than my future
- ✅ Spent more time on this than my actual job
- ✅ Made my FBI agent's job interesting
- ✅ Questioned my life choices (ongoing)
- ✅ Built a merge script to fix my own mistakes
- ✅ Optimized images that nobody will see
- ✅ Generated PDFs that nobody will use
- ✅ Wrote a README that's longer than the actual code

---

## 🙏 Acknowledgments

- **Stack Overflow** - For every error message I Googled at 3 AM
- **My therapist** - For listening to me explain this project (multiple times)
- **Coffee** - For making this possible (and for my addiction)
- **My sleep schedule** - RIP, you will be missed (and not missed)
- **some hentai website** - For not IP banning me (yet)
- **The doujin-api** - For existing and making my life easier
- **My FBI agent** - Sorry for the weird search history (and the redundant scraping)
- **My electricity bill** - I'm sorry
- **My hard drive** - I'm sorry
- **You** - For reading this far. Are you okay? Do you need to talk? Should we start a support group?

---

*Made with ☕, Python, and a concerning amount of free time.*

*"It's not a phase, mom. It's data science. Also, I scraped it three times."*

---

**P.S.** If you're a recruiter reading this: I also do normal projects. Please hire me. I have bills to pay. And a hard drive to replace.

**P.P.S.** If you're my mom reading this: It's for school, I swear. (It's not for school.)

**P.P.P.S.** If you're my FBI agent: I can explain. (I can't explain.)

**P.P.P.P.S.** If you're my therapist: We need to talk about my life choices.

**P.P.P.P.P.S.** If you're my hard drive: I'm sorry. I'll buy you a replacement. Eventually.
