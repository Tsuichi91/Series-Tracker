CSV Import Guide (Movies & Series) — UTF-8, comma-separated

General:
- Leave `id` empty to auto-generate on import; or set your own unique ID.
- Use ISO dates: YYYY-MM-DD (e.g., 2025-08-29) and ISO datetimes: YYYY-MM-DDTHH:MM:SSZ.
- Booleans: true / false
- Decimals use dot: e.g., rating 4.5
- Lists (genres, tags, rewatch_dates) use pipe `|` as separator, e.g.: Action|Sci-Fi
- `type`: use "movie" in movies_template and "series" in series_template (optional but recommended)
- Status values: Watching | Completed | On Hold | Dropped | Plan to Watch
- Series status values: running | completed | paused

Files:
1) movies_template.csv
   Columns: id,type,slug,title_en,title_original,year,poster,backdrop,short_description,genres,age_rating,runtime_min,release_date,franchise,status,rating,favorite,on_watchlist,tags,rewatch_count,rewatch_dates,last_position_seconds,created_at,updated_at
   Required fields for valid movie row: title_en, year, poster (slug recommended). At least one of genres/runtime_min should be filled.

2) series_template.csv
   Columns: id,type,slug,title_en,title_original,year,poster,backdrop,short_description,genres,age_rating,series_status,platform,episode_length_min,status,rating,favorite,on_watchlist,tags,rewatch_count,rewatch_dates,created_at,updated_at
   Required fields for valid series row: title_en, year, poster (slug recommended). At least one of genres/platform/episode_length_min should be filled.

3) series_seasons_template.csv
   Columns: series_id,season_number
   - series_id must match an existing ID in series_template.csv
   - season_number starts at 1

4) series_episodes_template.csv
   Columns: series_id,season_number,code,title,air_date,watched,timestamp_seconds,last_watched_date
   - series_id must match an existing ID in series_template.csv
   - season_number must exist for that series
   - code like S01E03
   - air_date uses ISO date YYYY-MM-DD
   - watched true/false; timestamp_seconds is a number (e.g., 1115), last_watched_date ISO date

Import order suggestion:
1) series_template.csv
2) series_seasons_template.csv
3) series_episodes_template.csv
4) movies_template.csv

Notes:
- Progress bars, next episode, and global progress are computed by the app after import.
- If you don’t need seasons as a separate step, you can have the importer create seasons on-the-fly from the `season_number` values in episodes.
