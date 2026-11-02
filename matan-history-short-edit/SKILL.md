---
name: מתן היסטור
description: >-
  Use this as the DEFAULT edit for every short (9:16) video of the owner's when no
  other recipe is named: the «מתן היסטור» style (mid-video cold-open hook, fast
  cuts with punch-ins, red slam text, short yellow captions, blue-grid slide,
  archive stills with Ken Burns, CC0 music/SFX, API Hub sponsor + 20MORE bar).
---
# מתן היסטור: עריכת ברירת המחדל לסרטונים קצרים

המתכון המלא, המחייב, נמצא ב-`<YOUR_RECIPE_FOLDER>/RECIPE.md`. צריך לקרוא אותו כולו לפני כל עריכה, והסעיף «נעול» בראש הקובץ גובר על כל השאר.

## מתי משתמשים בו
- בכל סרטון קצר (9:16) כשלא נאמר מתכון אחר. מתכון שהבעלים נוקב בשמו גובר.
- הסטנדרט החזותי הוא סרטון דמו מאושר (Drive `<YOUR_DEMO_FILE>`).

## השלבים
1. לקבל את הגולמי ולתמלל אותו ב-Hub (עברית או אנגלית). לפני כל קריאה ל-Hub לקבל estimate, ומעל 500 קרדיט לעצור ולחכות לאישור.
2. לתכנן עם `scripts/plan.py` ו-`pass1.py`: לבחור הוק cold-open של 1.5–3 שניות מאמצע הסרטון, אף פעם לא המשפט הראשון. לחתוך שקטים, מילות מילוי וגמגומים בלי לחתוך תוכן.
3. לבנות עם `scripts/build.py`, שמריץ את `cap.py`, ולהגדיר `LANG_VID=he` או `LANG_VID=en`. התוצאה:
   - פאנץ'-אין מתחלף בין 1.00 ל-1.12.
   - סלאם אדום (Heebo, ‏150) ושקף כחול עם גריד, רק עם מילים שנאמרו.
   - כתוביות צהובות ‎#FFD400 של 1–3 מילים.
   - B-roll של תמונות סטילס חופשיות מזכויות (PD או CC0) עם Ken Burns, ותמונות ארכיון בשחור-לבן או ספיה.
   - מוזיקת CC0 שמתנמכת מתחת לקול, whoosh ו-impact, ותיקון צבע קל.
4. החסות לפי שפה:
   - בעברית: «בחסות apihub.co.il» למעלה, ובפס התחתון «apihub.co.il · Coupon Code: 20MORE · 20% extra tokens».
   - באנגלית: «Sponsored by apihub.tools» למעלה, ובפס התחתון «apihub.tools · Coupon Code: 20MORE · 20% extra tokens».
   - הקופון תמיד 20MORE.
5. סיום: אם הדובר שואל את הקהל שאלה, הסרטון נגמר עליה. אם אין שאלה, לא להמציא. בסוף חיתוך חד לשחור.
6. לרנדר עם `scripts/final.sh` לקובץ חדש בשם `_rN`, בלי לדרוס קובץ קיים.
   - מפרט: 1080x1920, H.264 High ‏4.1 לכל היותר, yuv420p, bt709, AAC, faststart.
   - עוצמה ‎-16 LUFS, ו-TP לכל היותר ‎-1.5 (המטרה ‎-2.0).
7. QA עצמי:
   - למדוד עם `measure_ass.py` ו-`measure_frames.py` שכל אוברלי נמצא בתוך x 60–1020 ו-y 260–1580.
   - לטשטש מיילים, סכומי כסף, טלפונים ומפתחות. לא לטשטש שמות, וכמות קרדיטים היא לא כסף.
   - לרשום ב-`broll_sources_rN.json` את מקור ורישיון של כל תמונה, מוזיקה ואפקט.
8. לשלוח לבוט ה-QA עם md5 אחרי הרינדור האחרון. אחרי אישור: מוכן (רק MP4, שם הקובץ הוא ההוק), וואטסאפ לבעלים דרך בוט התפעול, ועדכון למנהל הצוות. לא מפרסמים אף פעם.
