---
name: OpenAI רקע לגרפיקה סושיאל
description: >-
  Use when generating a social-graphic background with OpenAI Images (gpt-image)
  for a designer to overlay real Hebrew text later — never bake Hebrew letters
  into the AI image.
---
# OpenAI רקע לגרפיקה סושיאל

## מתי
כשצריך רקע/סצנה לפוסט, קרוסלה או סטורי, והמעצבת מוסיפה אחר כך טקסט עברי אמיתי + לוגו.

## חובה
- מפתח: משתנה סביבה `OPENAI_API_KEY` (Secret). אל תדפיס אותו.
- טקסט עברי, לוגו, כפתור CTA ומספר שקופית — **לא** בתוך הפרומפט של התמונה. רק סצנה ריקה לאזורי טקסט.
- פורמט ברירת מחדל לאינסטגרם: `1024x1024` (1:1). סטורי/רילס: `1024x1536` אם המודל תומך, אחרת 1:1 וחיתוך ידני.

## מודל
העדפה לפי זמינות בחשבון (מהזול ליקר):
1. `gpt-image-1-mini` — טסטים וטיוטות
2. `gpt-image-1` — פרודקשן רגיל
3. `chatgpt-image-latest` או `gpt-image-1.5` — כשצריך איכות גבוהה יותר

## קריאה
`POST https://api.openai.com/v1/images/generations`

גוף לדוגמה:
```json
{
  "model": "gpt-image-1",
  "prompt": "Square social media BACKGROUND ONLY. No text, no letters, no logos, no watermarks. Leave clean empty space in the upper third for later overlay. [describe scene in English]. Photoreal, high contrast, cinematic lighting.",
  "size": "1024x1024",
  "quality": "medium",
  "n": 1
}
```

שמור את `b64_json` לקובץ PNG מקומי (או הורד `url` אם מוחזר). שלח את הקובץ למנהל/לבעלים לאישור לפני שכבות טקסט.

## פרומפט
- תאר באנגלית: נושא, דמויות, תאורה, מצב רוח, אזורים ריקים לטקסט.
- אסור: מילים בעברית, מספרי שקופיות, ססמאות, שמות מותג.
- מותר: "empty space for text overlay", "high contrast", "1:1 square".

## אחרי הרינדור
1. בדוק ויזואלית שאין אותיות שבורות או לוגו מומצא.
2. הוסף טקסט עברי אמיתי + לוגו בכלים שלך (לא כחלק מ־AI image).
3. מסור סט קבצים סופי (PNG/JPG) לצ׳אט הפרטי של הבעלים לפי הכללים הקיימים.

## תקלות
- `insufficient_quota` / `credit_balance_exhausted` → עצור. דווח: צריך קרדיטים ב־platform.openai.com billing. אל תנסה שוב במעגל.
- `invalid_api_key` → Secret חסר או שגוי. דווח למנהל צוות.
- עברית שבורה בתמונה → הפרומפט כלל טקסט; תייצר מחדש בלי אותיות.
