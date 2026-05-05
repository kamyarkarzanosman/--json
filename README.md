لێرەدا تەواوی README.md لەگەڵ نموونەی کۆدی تەواو و لەناو بلۆکی خۆیدا ئامادەیە:
```markdown
# سەحیح موسلیم بە کوردی

ئەم پڕۆژەیە دەقی تەواوی فەرموودەکانی سەحیح موسلیم بە زمانی کوردی و عەرەبی لەخۆ دەگرێت، کە لەلایەن **Kamyar Karzan Osman Aziz**ـەوە ئامادە و پێداچوونەوەی بۆ کراوە بۆ ئەوەی لە پرۆگرامسازیدا بەکاربهێنرێت.

---

## تایبەتمەندییەکان

* **فۆرمات:** JSON
* **زمان:** کوردی و عەرەبی
* **ژمارەی گشتی فەرموودەکان:** ٧٤٥٩ فەرموودە
* **ئامادەکار:** Kamyar Karzan Osman Aziz

---

## پێکهاتەی فایلەکە

فایلەکە بە شێوازێکی ڕێکخراو دروستکراوە بۆ ئەوەی بە ئاسانی لە پڕۆگرامکردندا بەکاربهێنرێت:

```json
{
  "metadata": {
    "id": 2,
    "length": 7459,
    "arabic": {
      "title": "صحيح مسلم",
      "author": "الإمام مسلم بن الحجاج القشيري النيسابوري",
      "introduction": ""
    },
    "kurdish": {
      "title": "صحیح موسلیم",
      "author": "ئیمام موسلیم کوڕی حەجاج النەیسبوری",
      "introduction": ""
    }
  },
  "chapters": [
    {
      "id": 1,
      "arabic": "كتاب الإيمان",
      "kurdish": "کتێبی ئیمان"
    }
  ]
}

```
## چۆنیەتی بەکارهێنان
ئەم پڕۆژەیە دەتوانرێت لە هەموو زمانەکانی پڕۆگرامسازیدا بەکاربهێنرێت. لێرەدا نموونەی بەکارهێنان لە HTML و JavaScript و Python خراوەتە ڕوو.
### ١. نموونەی HTML و JavaScript
دەتوانیت ڕاستەوخۆ داتاکان لە ڕێگەی fetch و بەکارهێنانی ناونیشانی ڕاستەوخۆی فایلەکە لە گیتهەب بخوێنیتەوە و لە پەڕەی وێبدا بە گەڕانی بەشەکان (Chapters) و ژمارەی فەرموودەکان پیشانی بدەیت:
```html
<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>سەحیح موسلیم بە کوردی</title>
   <style>
       body {
           font-family: 'Tahoma', sans-serif;
           background-color: #f0f2f5;
           margin: 0;
           padding: 20px;
           color: #333;
       }
       h2 {
           text-align: center;
           color: #2c3e50;
           margin-bottom: 20px;
       }
       .controls-container {
           max-width: 900px;
           margin: 0 auto 25px auto;
           background: #fff;
           padding: 20px;
           border-radius: 10px;
           box-shadow: 0 4px 15px rgba(0,0,0,0.05);
           display: flex;
           flex-wrap: wrap;
           gap: 15px;
           justify-content: space-between;
       }
       .control-group {
           flex: 1;
           min-width: 200px;
           display: flex;
           flex-direction: column;
           gap: 5px;
       }
       select, input, button {
           padding: 10px;
           border-radius: 5px;
           border: 1px solid #ccc;
           font-size: 1rem;
           font-family: inherit;
       }
       button {
           background-color: #3498db;
           color: #fff;
           border: none;
           cursor: pointer;
           transition: background 0.3s;
           font-weight: bold;
       }
       button:hover {
           background-color: #2980b9;
       }
       .container {
           max-width: 900px;
           margin: 0 auto;
       }
       .hadith-card {
           background-color: #ffffff;
           border-right: 4px solid #e67e22;
           padding: 15px;
           margin-bottom: 15px;
           border-radius: 8px;
           box-shadow: 0 4px 10px rgba(0,0,0,0.05);
       }
       .hadith-info {
           font-size: 0.9rem;
           color: #7f8c8d;
           margin-bottom: 8px;
       }
       .hadith-by {
           font-weight: bold;
           color: #c0392b;
           font-size: 0.95rem;
           margin-bottom: 8px;
       }
       .hadith-text {
           line-height: 1.8;
           font-size: 1.05rem;
       }
       .hadith-arabic {
           direction: rtl;
           font-family: 'Traditional Arabic', serif;
           color: #2c3e50;
           font-size: 1.2rem;
           margin-top: 10px;
           padding-top: 5px;
           border-top: 1px solid #eee;
       }
   </style>
</head>
<body>

   <h2>سەحیح موسلیم بە کوردی</h2>

   <div class="controls-container">
       <div class="control-group">
           <label for="chapter-select">کتێب (بەش):</label>
           <select id="chapter-select">
               <option value="">کتێبێک هەڵبژێرە</option>
           </select>
       </div>
       <div class="control-group">
           <label for="hadith-number">ژمارەی فەرموودە:</label>
           <input type="number" id="hadith-number" placeholder="بۆ نموونە: ١">
       </div>
       <button id="search-btn">گەڕان</button>
   </div>

   <div class="container" id="app-container"></div>

   <script>
       const url = '[https://raw.githubusercontent.com/kamyarkarzanosman/--json/main/sahihmuslimkurdi.json](https://raw.githubusercontent.com/kamyarkarzanosman/--json/main/sahihmuslimkurdi.json)';
       let globalData = {};

       fetch(url)
           .then(response => {
               if (!response.ok) {
                   throw new Error('کێشە لە وەرگرتنی داتاکان هەیە');
               }
               return response.json();
           })
           .then(data => {
               globalData = data;
               populateChapters();
           })
           .catch(error => {
               console.error('هەڵە:', error);
               document.getElementById('app-container').innerText = 'تکایە دڵنیا ببەرەوە لە هێڵی ئینتەرنێت و بوونی فایلەکە.';
           });

       function populateChapters() {
           const chapterSelect = document.getElementById('chapter-select');
           if (globalData && globalData.chapters) {
               globalData.chapters.forEach(chapter => {
                   const option = document.createElement('option');
                   option.value = chapter.id;
                   option.textContent = `${chapter.id} - ${chapter.kurdish}`;
                   chapterSelect.appendChild(option);
               });
           }
       }

       document.getElementById('search-btn').addEventListener('click', function() {
           const selectedChapterId = document.getElementById('chapter-select').value;
           const hNumberInput = document.getElementById('hadith-number').value;

           const container = document.getElementById('app-container');
           container.innerHTML = '';

           if (!globalData || !globalData.chapters) {
               container.innerHTML = '<p style="text-align:center;">داتا بارنەکراوە.</p>';
               return;
           }

           if (selectedChapterId === "") {
               container.innerHTML = '<p style="text-align:center;">تکایە سەرەتا کتێبێک هەڵبژێرە.</p>';
               return;
           }

           if (hNumberInput !== "") {
               const hNumber = parseInt(hNumberInput);
               const foundHadith = globalData.hadiths?.find(h => h.id === hNumber && h.chapterId == selectedChapterId);

               if (foundHadith) {
                   container.innerHTML = createCardHTML(foundHadith);
               } else {
                   container.innerHTML = `<p style="text-align:center;">فەرموودەی ژمارە ${hNumber} لەم کتێبەدا بوونی نییە.</p>`;
               }
           } else {
               const chapterHadiths = globalData.hadiths?.filter(h => h.chapterId == selectedChapterId) || [];
               
               if (chapterHadiths.length > 0) {
                   let html = '';
                   chapterHadiths.forEach(h => {
                       html += createCardHTML(h);
                   });
                   container.innerHTML = html;
               } else {
                   container.innerHTML = '<p style="text-align:center;">هیچ فەرموودەیەک بۆ ئەم کتێبە نەدۆزرایەوە.</p>';
               }
           }
       });

       function createCardHTML(h) {
           return `
               <div class="hadith-card">
                   <div class="hadith-info">ژمارە: ${h.id || ''}</div>
                   <div class="hadith-by">گێڕاوە: ${h.kurdish?.narrator || 'ناڕوون'}</div>
                   <div class="hadith-text">${h.kurdish?.text || ''}</div>
                   <div class="hadith-arabic">${h.arabic || ''}</div>
               </div>
           `;
       }
   </script>

</body>
</html>

```
### ٢. نموونەی Python
بۆ خوێندنەوەی داتا بە زمانی پایسۆن:
```python
import json

# خوێندنەوەی فایلەکە
with open('sahihmuslimkurdi.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# نیشاندانی ناوی کتێبەکان
title = data['metadata']['kurdish']['title']
print(f"ناوی کتێب: {title}")

# نیشاندانی ناوی یەکەم بەش
first_chapter = data['chapters'][0]['kurdish']
print(f"بەشی یەکەم: {first_chapter}")

```
### ٣. نموونەی JavaScript
بۆ بەکارهێنانی داتا لە پرۆژەکانی JavaScript:
```javascript
async function loadHadithData() {
    try {
        const response = await fetch('sahihmuslimkurdi.json');
        const data = await response.json();
        
        console.log(data.metadata.kurdish.title); 
        const firstChapter = data.chapters[0];
        console.log(firstChapter.kurdish); 
    } catch (error) {
        console.error('هەڵە لە خوێندنەوەی داتاکان:', error);
    }
}

loadHadithData();

```
## مۆڵەت (License)
ئەم پڕۆژەیە لەژێر مۆڵەتی کراوەدایە. سەرچاوەی پڕۆژەکە لە گیتهەب:
https://github.com/kamyarkarzanosman/--json/edit/main/sahihmuslimkurdi.json
## SEO Keywords (305 Words)
سەحیح موسلیم, فەرموودەی پێغەمبەر, سەحیح موسلیم بە کوردی, فەرموودەناسی, ژیانی پێغەمبەر, ئیسلام, کتێبی ئیسلامی, فەرموودەی ڕاست, فەرموودەکان, زانستی فەرموودە, ئیسلامناسی, سوننەت, فەرموودەی بوخاری و موسلیم, کتێبی کوردی, خوێندنەوەی ئیسلامی, فەرموودەکانی پێغەمبەر, دەقی فەرموودە, ئیمام موسلیم, ژیاننامەی پێغەمبەر, قورئان و فەرموودە, زانایانی ئیسلام, فەرموودەی سەحیح, پڕۆگرامسازی کوردی, فەرموودەکانی ئیسلام, فەرموودەی صەحیح, کتێبخانەی کوردی, پەڕتووکی ئیسلامی, وەرگێڕانی کوردی, دەقی کوردی, گێڕەرەوەکانی فەرموودە, فەرموودەناسی ئیسلامی, زانستی حەدیس, حەدیسی پێغەمبەر, فەرموودەی قودسی, ژیانی هاوەڵان, ئیسلام لە کوردستان, فەرموودەی بوخاری, سەحیحی بوخاری, سەحیحی موسلیم, کتێبی ئیمان, کتێبی پاککردنەوە, کتێبی سوڕی مانگانە, کتێبی نوێژ, کتێبی مزگەوت, فەرموودەی فەرز, فەرموودەی سوننەت, کۆکردنەوەی فەرموودە, لێکۆڵینەوەی ئیسلامی, ئامادەکردنی کتێب, Kamyar Karzan Osman Aziz, پڕۆژەی ئیسلامی, پڕۆژەی کوردی, گیتھەب کوردی, زمانی کوردی بۆ پڕۆگرامسازی, داتای فەرموودە, داتابەیسی ئیسلامی, فۆرماتی JSON, پڕۆگرامی ئیسلامی, گەشەپێدەری کوردی, بەرنامەی کوردی, فەرموودەی شەو, فەرموودەی ڕۆژ, فەرموودەی زانست, فەرموودەی ئامۆژگاری, فەرموودەی چاکە, فەرموودەی دوعا, فەرموودەی زیکر, فەرموودەی توبە, فەرموودەی دادپەروەری, فەرموودەی هاوڕێیەتی, فەرموودەی کاری چاک, فەرموودەی ماف, فەرموودەی خێزان, فەرموودەی پەروەردە, فەرموودەی ئارامگرتن, فەرموودەی سوپاسگوزاری, فەرموودەی ڕەوشت, فەرموودەی ڕاستگۆیی, فەرموودەی ئەمانەت, فەرموودەی وەفا, فەرموودەی لێخۆشبوون, فەرموودەی یارمەتیدان, فەرموودەی خێرخوازی, فەرموودەی بەخشین, فەرموودەی میهرەبانی, فەرموودەی خۆشەویستی, فەرموودەی یەکتاپەرستی, فەرموودەی باوەڕ, فەرموودەی خواناسی, فەرموودەی نوێژکردن, فەرموودەی زەکات, فەرموودەی ڕۆژوو, فەرموودەی حەج, فەرموودەی عومرە, فەرموودەی قورئانخوێندن, فەرموودەی زانستخواز, فەرموودەی مامۆستا, فەرموودەی خوێندەواری, فەرموودەی ڕێنمایی, فەرموودەی ئاشتی, فەرموودەی کۆمەڵگا, فەرموودەی گەنجان, فەرموودەی منداڵان, فەرموودەی دایک و باوک, فەرموودەی دراوسێ, فەرموودەی میوان, فەرموودەی سەفەر, فەرموودەی بازرگانی, فەرموودەی کرێکاری, فەرموودەی کشتوکاڵ, فەرموودەی تەندروستی, فەرموودەی چارەسەر, فەرموودەی دەرمان, فەرموودەی خەو, فەرموودەی خواردن, فەرموودەی خواردنەوە, فەرموودەی پۆشاک, فەرموودەی جوانکاری, فەرموودەی ماڵ, فەرموودەی ئۆتۆمبێل, فەرموودەی هاتوچۆ, فەرموودەی ژینگەپارێزی, فەرموودەی ئاو, فەرموودەی دارستان, فەرموودەی ئاژەڵان, فەرموودەی باڵندەکان, فەرموودەی مێرووەکان, فەرموودەی کەشوهەوا, فەرموودەی کات, فەرموودەی ڕۆژگار, فەرموودەی مێژوو, فەرموودەی شارستانیەت, فەرموودەی کولتوور, فەرموودەی نەریت, فەرموودەی زمان, فەرموودەی وەرگێڕان, فەرموودەی فەرهەنگ, فەرموودەی زاراوە, فەرموودەی ڕێزمان, فەرموودەی ئەدەب, فەرموودەی شیعر, فەرموودەی پەند, فەرموودەی چیرۆک, فەرموودەی پەندەکانی پێشینان, فەرموودەی ژیر, فەرموودەی دانایی, فەرموودەی سەرکردایەتی, فەرموودەی بەڕێوەبردن, فەرموودەی ئابووری, فەرموودەی سیاسەت, فەرموودەی دادوەری, فەرموودەی سەربازی, فەرموودەی جەنگ, فەرموودەی ئاشتەوایی, فەرموودەی پەیمان, فەرموودەی دراوسێیەتی, فەرموودەی میوانداری, فەرموودەی چاودێری, فەرموودەی بەرپرسیارێتی, فەرموودەی ویژدان, فەرموودەی ڕێز, فەرموودەی خۆشەویستی خودا, فەرموودەی ترسی خودا, فەرموودەی هیوای خودا, فەرموودەی سوپاس, فەرموودەی چاوەڕوانی, فەرموودەی پەلەکردن, فەرموودەی دانبەخۆداگرتن, فەرموودەی ئارامگرتن لەسەر بەڵا, فەرموودەی تاقیکردنەوە, فەرموودەی مردن, فەرموودەی گۆڕ, فەرموودەی ڕۆژی دوایی, فەرموودەی بەهەشت, فەرموودەی دۆزەخ, فەرموودەی حەشر, فەرموودەی پردی سیڕات, فەرموودەی شفاعەت, فەرموودەی پێغەمبەران, فەرموودەی فریشتەکان, فەرموودەی جنۆکە, فەرموودەی شەیتان, فەرموودەی جادوو, فەرموودەی چاوپیسی, فەرموودەی حەسودی, فەرموودەی کینە, فەرموودەی توڕەیی, فەرموودەی ئاگادارکردنەوە, فەرموودەی موژدە, فەرموودەی سەرکەوتن, فەرموودەی شکۆمەندی, فەرموودەی شکاندنی دڵ, فەرموودەی یارمەتی, فەرموودەی هاوکاری, فەرموودەی زانایان, فەرموودەی قوتابخانە, فەرموودەی زانکۆ, فەرموودەی پەڕتووک, فەرموودەی نوسین, فەرموودەی خوێندن, فەرموودەی بیرکردنەوە, فەرموودەی تێڕامان, فەرموودەی ژیرکاری, فەرموودەی بیر, فەرموودەی دڵ, فەرموودەی دەروون, فەرموودەی خۆشەویستی نیشتمان, فەرموودەی خاکی پیرۆز, فەرموودەی مەککە, فەرموودەی مەدینە, فەرموودەی قودس, فەرموودەی کەعبە, فەرموودەی مزگەوتی حەرام, فەرموودەی مزگەوتی پێغەمبەر, فەرموودەی مزگەوتی ئەقسا, فەرموودەی سوننەتی موئەددەبە, فەرموودەی سوننەتی غەیرە موئەددەبە, فەرموودەی نەفل, فەرموودەی قەزا, فەرموودەی کەفارەت, فەرموودەی نەزذر, فەرموودەی قوربانی, فەرموودەی عەقیقە, فەرموودەی میرات, فەرموودەی هاوسەرگیری, فەرموودەی تەڵاق, فەرموودەی مەهر, فەرموودەی شایەت, فەرموودەی گرێبەست, فەرموودەی قەرز, فەرموودەی کار, فەرموودەی کاسبی, فەرموودەی سەرمایە, فەرموودەی باج, فەرموودەی زەوی, فەرموودەی خانووبەرە, فەرموودەی ئاڵتون, فەرموودەی پارە, فەرموودەی دراو, فەرموودەی بانک, فەرموودەی بیمە, فەرموودەی بازاڕ, فەرموودەی مامەڵە, فەرموودەی ڕیبا, فەرموودەی غەش, فەرموودەی فێڵ, فەرموودەی دزی, فەرموودەی تاوان, فەرموودەی سزا, فەرموودەی دادگایی, فەرموودەی شایەتحاڵ, فەرموودەی سوێند, فەرموودەی پەیمانشکێنی, فەرموودەی درۆ, فەرموودەی غەیبەت, فەرموودەی بوختان, فەرموودەی سیخوڕی, فەرموودەی خراپەکاری, فەرموودەی بەزاندنی سنوور, فەرموودەی توندوتیژی, فەرموودەی شەڕانگێزی, فەرموودەی فیتنە, فەرموودەی نەزانین.
```

```
