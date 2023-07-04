---
title: "אנטרופיק, מניקור ומה שביניהם 🤖"
date: 2023-07-20 00:34:00 +0800
categories: [Anthropic, GPT]
tags: [LLMs]
---

שלום!
בבלוג זה ננסה לעקוב אחר ההתפתחויות המהירות בתחום ה- NLP, פוסט אחד בכל פעם!\
הפעם נשתף איך בחרנו את שם הבלוג הזה באמצעות **אנטרופיק**.
## רקע
אנטרופיק היא חברת מחקר שפיתחה מודל שפה גדול הנקרא Claude (**קלוד**), מתחרה ל- ChatGPT, שהוא לכאורה בטיחותי יותר. את נושא הבטיחות עיגנה Anthropic תחת הקונספט של Constitutional AI, ובעברית - "AI חוקתי״. השימוש במינוח ״חוקה״ נועד להדגיש שהמודל צריך להיות כפוף לאוסף עקרונות מסויים.

קלוד תומך ב- context window של 100,000 טוקנים (75,000~ מילים), בערך אורך של ספרון! זה מקנה לו יתרון ביחס ל- ChatGPT.

המודל נגיש לשימוש דרך אפליקציית סלאק, או דרך API באמצעות Access Key.

## איך בחרנו את שם הבלוג?
באמת שניסינו לבד, אבל בסוף פנינו לקלוד. וכך זה נראה שלב אחרי שלב -


הפרומפט הראשון ששלחנו לקלוד היה בנוסח הבא:
```python
blog_naming_prompt = "Please suggest data science blog names for two female data scientists"
```


הפנייה הבסיסית לקלוד באמצעות ה-API מתבצעת באופן הבא:
```python
from anthropic import Anthropic, HUMAN_PROMPT, AI_PROMPT

ANTHROPIC_KEY = <...>

anthropic = Anthropic(api_key=ANTHROPIC_KEY)

completion = anthropic.completions.create(
    model="claude-2.0",
    max_tokens_to_sample=300,
    temperature=1,
    prompt=f"{HUMAN_PROMPT} {blog_naming_prompt}{AI_PROMPT}",
)
print(completion.completion)
```

בקריאה זו מציינים את השם והגרסא של המודל, `claude-2.0`, ואת ה- prompt.\
את ערך הטמפרטורה, אשר משפיעה על מידת האקראיות של התוצאות, קבענו ל- 1 (הערך הדיפולטי).

הופתענו לקבל תשובות מגניבות ומקוריות, מוזמנות להתרשם מהרשימה 🍿

```
 Here are some suggestions for data science blog names for two female data scientists:

• The Data Duo - Simple but captures that it's two data scientists running the blog.

• Algorithm Amazons - Amazons highlights powerful female figures, paired with algorithm shows the data science and machine learning focus.

• Codin' Chicks - Play on coding combined with chicks, could be a lighthearted brand for two female data scientists.

• Binary BFFs - BFFs is a popular acronym for "best friends forever", combined with binary the digital data focus.

• Glamorous Geeks - Blends technical skills of geeks with glamorous to add a feminine twist. 

• AI Allies - Short name showing partnership as allies, with AI highlighting their machine learning capabilities.

Does any of these options resonate with you? I can provide some additional suggestions if those do not quite fit.
```

בהמשך ביצענו prompt engineering כדי שנקבל שמות לבלוג שהם gender-aware

```python
prompt = "Please suggest data science blog names for two female data scientists. Make sure that the names indicate that we are female"
```

כאן קלוד לקח את זה לכיוון של עקבים ומניקור

```
 Here are some suggestions for data science blog names indicating female authors:

• The Data Dolls 
• Data Divas 
• Modeling and Manicures 
• Machine Learning and Mimosas 
• Neural Networks and Nail Polish 
• Algos and Heels

```

אז החלטנו להדגיש את הפן המקצועי בפרומפט. ועשינו שרשרת ניסויים בהן הוספנו בכל פעם מילות מפתח לתחום המקצועי (Machine Learning, NLP וכד׳)


```python
prompt = "Please suggest data science blog names for two female data scientists.\
Make sure that the names has a professional female gender indication"
```

וכך נולד השם - Semantic Sisters! 👯


## הטייקים של Semantic Sisters

.נראה שמדובר במודל שנותן תוצרים ברמת איכות גבוהה והיה קל לשימוש
המודל אמנם בטיחותי, אבל עדיין לוקה בסטריאוטיפיות.
אנחנו היינו מוסיפות לחוקה כמה תיקונים בנושא הזה.

## רפרנסים
[מאמר של חברת Anthropic על Constitutional AI](https://arxiv.org/pdf/2212.08073.pdf)





