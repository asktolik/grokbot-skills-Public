---
name: 'אינפוגרפיקה ממותגת 16:9'
description: >-
  Use this when making a branded 16:9 Hebrew infographic or explainer image
  (headline with highlighted word, hub diagram with connected cards, 3 info
  cards, branded bottom bar) in one of several color themes.
---
# אינפוגרפיקה ממותגת 16:9

## תבנית
- תיקייה: `<YOUR_TEMPLATE_FOLDER>/` (תבנית `infographic-template.html`, `render.py`, `README.md`, `assets/` עם אווטאר, לוגו ופונטים מקומיים).
- גודל 1920x1080. כל הטקסט HTML אמיתי. אסור טקסט מתוך תמונת AI.

## מבנה קבוע
1. תג עליון קטן (למשל `APIHUB · GROK BOT`).
2. כותרת עברית עבה, מילה אחת עטופה ב־`<mark>` (מרקר בצבע הנושא).
3. תת־כותרת שורה אחת.
4. תרשים: מרכז `.hub` + עד 4 כרטיסים `.bot` מחוברים בקווים.
5. שלושה כרטיסים תחתונים: תווית אנגלית קטנה, כותרת ושלוש נקודות.
6. פס מיתוג תחתון קבוע: תמונה, שם ותואר, קישורים, לוגו. לא משנים בלי בקשה.

## צבעים
- משתני CSS בראש הקובץ: `--a1` `--a2` `--marker` `--bar1` `--bar2` `--bar-link` `--bg` `--ink` `--muted` `--label` `--hub-ink`.
- ערכות קיימות: ברירת מחדל כחול־סגול, `body.teal`, `body.orange`. ערכה חדשה = העתקת בלוק `body.xxx{}`.
- ניגודיות טקסט לפחות 4.5:1 (טקסט לבן על כתום נכשל בעבר).

## הפקה
1. עדכן טקסט בעותק של התבנית (לא בקובץ המקור).
2. `python3 render.py` (Playwright). לא `chrome --screenshot`.
3. בדוק ויזואלית: אין חיתוך, אין עברית שבורה, אין מלבן לבן.
4. QA לפני מסירה, ואז מסירה לבעלים. בלי פרסום בלי אישור.

## אסור
- להמציא מספרים, ציטוטים או טענות. כל טענה מהבעלים או ממקור אמיתי.
- להחליף לוגו או מיתוג בלי הוראה.
