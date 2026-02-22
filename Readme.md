# 📚 Manga Metadata Scraper & Organizer

> *"It's for research purposes," I whisper to my hard drive as it weeps.*

## 🤔 What Even Is This?

Look, I'm not saying I scraped 594,346 entries of "cultural artifacts" from the internet, but I'm also not NOT saying that. This is basically what happens when a data scientist has too much free time and questionable priorities.

This is a collection of Python scripts that scrape, organize, and convert manga metadata from nhentai into various formats. Think of it as a digital librarian that works way too hard, asks zero questions, and definitely needs therapy.

**TL;DR:** I turned procrastination into a data pipeline. Your FBI agent is judging both of us right now.

## 🛠️ The Arsenal (AKA: Tools I Built Instead of Going Outside)

### Scrapers (The Data Hunters)

- **`faster_scraper.py`** - The speed demon. Async scraping with 8 concurrent workers. Goes brrr faster than your excuses. 🏎️💨
- **`scraper_for_linux.py`** - Same speed demon, but it showered, uses Arch btw, and won't shut up about it.
- **`mangascraper.py`** - The OG boomer scraper. Slow, steady, and has PDF download capabilities. Like your dad's old Camry—reliable but embarrassing.

### Data Wranglers (The Format Shapeshifters)

- **`jsonl_to_csv.py`** - Converts JSONL to CSV because some people still use Excel in 2026. We don't judge. (We do judge.)
- **`jsonl_to_db.py`** - Shoves everything into SQLite. Now with 100% more SQL and 0% more social life!
- **`csv_to_parquet.py`** - Makes your data files smol and FAST. Parquet gang rise up. 📦✨

### Utility Belt (The "I Forgot Something" Collection)

- **`clearner.py`** - Fixes those pesky string IDs that should've been integers from the start. Past me was an idiot.
- **`sorter.py`** - Sorts your ID lists. Groundbreaking. Revolutionary. Nobel Prize pending.
- **`custom.py`** - A mysterious API caller that does... something? Even I forgot. It's like that drawer in your kitchen.

## 🚀 Quick Start (Or: How to Explain This to Your IT Department)

### Scraping (The "I'm Doing Data Science" Phase)

```bash
# The fast way (for people with places to be)
python faster_scraper.py

# The old-school way (for people who like watching progress bars)
python mangascraper.py --start 1 --end 10000
```

**Pro tip:** Run this at 3 AM so your roommate doesn't ask questions.

### Converting Your Loot (The "Making It Look Professional" Phase)

```bash
# To CSV (for the normies)
python jsonl_to_csv.py

# To SQLite (for the SQL nerds)
python jsonl_to_db.py

# To Parquet (for the "I use Pandas" flex)
python csv_to_parquet.py
```

## 📦 What You'll Need (Besides Therapy)

```bash
pip install aiohttp beautifulsoup4 requests pandas pyarrow sqlite3
```

*(Also img2pdf and Pillow if you're feeling nostalgic and want PDFs. But let's be real, nobody uses those anymore.)*

**System Requirements:**
- Python 3.7+ (because we're not animals)
- A stable internet connection (and an unstable life)
- Approximately 2GB of disk space (and 0GB of shame)
- A good explanation ready for when someone asks what you're downloading

## 🎯 Features That Slap (Harder Than Your Mom Finding Your Browser History)

- **Async scraping** - Because waiting is for chumps and people with patience
- **Auto-retry logic** - Handles rate limits like a champ. Gets rejected, tries again. Unlike your dating life.
- **Duplicate prevention** - Tracks good/bad IDs so you don't waste time. Unlike this entire project.
- **UTF-8 support** - Japanese characters? ✓ Chinese? ✓ Emojis? ✓ Your dignity? ✗
- **Multiple export formats** - CSV, SQLite, Parquet. More formats than your ex had excuses.
- **Sleep prevention** - Your PC won't doze off mid-scrape (Windows only). Someone should stay awake for this.
- **Error handling** - Fails gracefully, unlike my life choices
- **Progress tracking** - Watch numbers go up. It's like dopamine, but sadder.

## 📊 Data Schema (AKA: What Did I Even Scrape?)

Each entry includes:
- **ID** - A unique number, like your social security but less useful
- **Title** - Usually in Japanese. Google Translate is your friend. Or enemy. Depends.
- **Upload Date** - When this blessed content graced the internet
- **Artists, Groups, Parodies, Characters** - The who's who of... art
- **Tags** - Oh boy. So many tags. Too many tags. Tags you didn't know existed.
- **Categories** - For organizational purposes (lying to ourselves is free)
- **Language** - Mostly Japanese. Some English. All questionable.
- **Page count** - How long your "research" will take
- **Favorites** - Community popularity metric (yes, there's a community)
- **Cover image URL** - For thumbnails. And science.
- **Recommendations** - Because algorithms know you better than you know yourself

## 📈 The Dataset (Or: My Magnum Opus of Questionable Decisions)

The `manga_all.csv` file contains **594,346 entries** spanning IDs from 1 to 629,832. 

Yes, you read that right. **HALF A MILLION ENTRIES.** That's more entries than:
- Books in a small library
- Days you've been alive (probably)
- Reasons this was a good idea (definitely)

I spent more time scraping this than I've spent on my actual job. My therapist is very interested.

**Columns (14 total):**
- `id` - Unique identifier (like a social security number for "art")
- `title` - Full title (often longer than a CVS receipt)
- `date` - Upload date (YYYY-MM-DD format, because ISO 8601 is the only standard I respect)
- `parodies`, `charecters`, `groups`, `categories`, `language`, `tags`, `artists` - JSON arrays of metadata (yes I misspelled "characters" in the code, no I'm not fixing it now)
- `favorites` - How many people publicly admitted to liking this
- `num_pages` - Page count (for time management purposes)
- `recommendations` - "If you liked this, you'll love..." (the algorithm is judging you)
- `cover_image` - Direct URL to cover art (SFW-ish... depends on your workplace)

**Sample entry:**
```
ID: 1
Title: (C71) [Arisan-Antenna (Koari)] Eat The Rich! (Sukatto Golf Pangya)
Date: 2014-06-28
Pages: 14
Favorites: 3,029
```
*Ah yes, ID #1. The beginning of a beautiful disaster.*

All text fields support full UTF-8 (Japanese, Chinese, emojis, hieroglyphics, ancient Sumerian, you name it) thanks to `ensure_ascii=False` in the export scripts.

**File size:** Too thicc for GitHub (that's what she said)
**Solution:** Uploaded to HuggingFace because they don't judge → [Dataset Link](https://huggingface.co/datasets/NoobEngineere/NSFW_Manga)

*Warning: Downloading this dataset will raise questions from your ISP, your IT department, and your cat.*

## ⚠️ Legal Disclaimer (The "Please Don't Sue Me" Section)

This is for **educational purposes**. And by educational, I mean you'll learn:
- How web scraping works
- How async Python works  
- How to disappoint your parents
- How to explain your GitHub activity to recruiters

**Rules of Engagement:**
- Don't be weird (weirder than this already is)
- Respect rate limits (the site has feelings too)
- Don't DDoS anyone (that's just rude)
- Be cool (unlike this project)
- If you get caught, you don't know me
- This is public data (I checked... twice... okay three times)

**Disclaimer:** I am not responsible for:
- Your browser history
- Your hard drive contents  
- Your IT department's questions
- Your significant other's concerns
- Your therapist's notes
- Whatever the FBI thinks this is

## 🤷 FAQ (Frequently Avoided Questions)

**Q: Why does this exist?**  
A: Bold of you to assume I have a good reason. Data hoarding is a perfectly valid hobby, okay? Don't judge me.

**Q: Is this legal?**  
A: Scraping public data is generally fine. What you do with it is between you, your conscience, and your browser's incognito mode.

**Q: How long did this take?**  
A: Long enough that I've forgotten what sunlight looks like. The scraper ran for days. DAYS. My electricity bill is crying.

**Q: Can I use this for other sites?**  
A: Sure, but you'll need to rewrite like... everything. Also, please get better hobbies.

**Q: Why are there so many scraper files?**  
A: Evolution, baby. Each one is slightly less terrible than the last. It's like Pokémon, but sadder.

**Q: Did you actually scrape 594K entries?**  
A: Yes. Yes I did. Do I regret it? Ask me after therapy.

**Q: What's your GitHub streak?**  
A: Longer than my last relationship, thanks for asking.

**Q: Should I put this on my resume?**  
A: Depends. Are you applying to work at a data company or explaining yourself to HR?

**Q: Are you okay?**  
A: Define "okay."

## 🎓 Pro Tips (From Someone Who Learned The Hard Way)

- **Start small.** Don't scrape 500k IDs on your first run like I did. Learn from my mistakes (and my therapist's notes).
- **The site has rate limits.** The scripts handle it, but don't be greedy. We're pirates, not monsters.
- **Use `faster_scraper.py`** unless you need PDFs. And let's be honest, nobody needs PDFs in 2026.
- **Run it overnight.** Your PC will sound like a jet engine. Your roommate will ask questions. Have lies prepared.
- **SQLite is great for querying.** CSV is great for sharing. Parquet is great for flexing on data scientists.
- **Back up your data.** Losing 594K entries after days of scraping will make you cry. I know. I cried.
- **Use a VPN.** Not for legal reasons. Just for peace of mind. And plausible deniability.
- **Clear your terminal history.** Trust me on this one.
- **Don't tell your friends.** They won't understand. They'll judge. They're not ready.

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

## 📝 License

MIT License, which means:
- You can use this
- You can modify this  
- You can distribute this
- You can't sue me
- You can't blame me for your life choices
- You definitely can't put this on your LinkedIn

**In other words:** Do whatever you want, just don't tell anyone I helped.

---

## 🏆 Achievements Unlocked

- ✅ Scraped 594,346 entries
- ✅ Learned async Python the hard way
- ✅ Maxed out my hard drive
- ✅ Disappointed my parents
- ✅ Created a dataset larger than my future
- ✅ Spent more time on this than my actual job
- ✅ Made my FBI agent's job interesting
- ✅ Questioned my life choices (ongoing)

---

## 🙏 Acknowledgments

- **Stack Overflow** - For every error message I Googled at 3 AM
- **My therapist** - For listening to me explain this project
- **Coffee** - For making this possible
- **My sleep schedule** - RIP, you will be missed
- **nhentai** - For not IP banning me (yet)
- **My FBI agent** - Sorry for the weird search history
- **You** - For reading this far. Are you okay? Do you need to talk?

---

*Made with ☕, Python, and a concerning amount of free time.*

*"It's not a phase, mom. It's data science."*

---

**P.S.** If you're a recruiter reading this: I also do normal projects. Please hire me. I have bills to pay.

**P.P.S.** If you're my mom reading this: It's for school, I swear.

**P.P.P.S.** If you're my FBI agent: I can explain.
