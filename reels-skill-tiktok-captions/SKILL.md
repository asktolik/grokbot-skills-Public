---
name: סקיל רילסים
description: >-
  Use this when the owner names «סקיל רילסים» (captions-tiktok + hook-shake) for a
  9:16 reel: TikTok captions with yellow active word, yellow hook title with
  opening shake shown only 0–4s, API Hub sponsor + 20MORE bar, silence/filler
  cuts, light color, local ffmpeg render.
---
# סקיל רילסים (captions-tiktok + hook-shake)

המתכון המלא המחייב נמצא ב-`<YOUR_RECIPE_FOLDER>/RECIPE.md`. צריך לקרוא אותו כולו לפני כל עריכה, וסעיפי «נעול» גוברים. המימוש האחרון נמצא ב-`<YOUR_WORK_FOLDER>/` (`build_rN.py`, `render_rN.sh`).

## מתי משתמשים בו
רק כשהבעלים נוקב בשם «סקיל רילסים». ברירת המחדל לסרטונים קצרים היא «מתן היסטור».

## עיקרי המתכון
1. תמלול ב-Hub בלבד, עם estimate לפני כל קריאה ומפתח APIhub מתוך Secret. הרינדור מקומי ב-ffmpeg ו-libass.
2. חיתוך שקטים ומילות מילוי בלי לחתוך תוכן, ותיקון צבע קל (`eq=contrast=1.06:saturation=1.12`).
3. כתוביות TikTok: Heebo Bold 74 לבן עם קו מתאר, עד 3 מילים בכתובית, והמילה הפעילה בצהוב וב-108%. SRT מוגה שנבנה מאותן כתוביות.
4. כותרת הוק בתיבה צהובה, עם שייק פתיחה של 0.6 שניות. **היא מופיעה רק ב-0 עד 4 שניות, תמיד** (נעול). בפריים השער הכותרת נשארת.
5. פס חסות לכל אורך הסרטון, עם הקופון 20MORE. בעברית האתר הוא apihub.co.il ובאנגלית apihub.tools.
6. כל אובייקט נמצא בתוך האזור הבטוח: y 260–1580 ו-x 60–1020.
7. הסיום: אם הדובר שואל את הקהל שאלה, מסיימים עליה. משאירים כ-200ms אחרי המילה האחרונה, ו-fade של 40ms.
8. מפרט: H.264 High עד 4.1, yuv420p, bt709, AAC, faststart, ‏−16 LUFS. כל סבב מקבל שם `_rN` חדש, בלי לדרוס קובץ.
9. שולחים לבוט ה-QA עם md5. אחרי האישור: רק ה-MP4 עולה למוכן, בוט התפעול שולח וואטסאפ לבעלים, ומנהל הצוות מקבל עדכון. לא מפרסמים אף פעם.
