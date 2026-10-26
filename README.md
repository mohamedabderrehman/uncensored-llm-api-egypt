# واجهة API لنموذج لغوي بلا رقابة للمطورين في مصر

> واجهة متوافقة مع OpenAI لفرق التطوير في مصر. عربية طبيعية، تعليمات النظام تُنفَّذ، ومفيش فقرة تحذير قبل كل رد. العنوان: https://uncensored-llm.sbs/v1

**الواجهة:** https://uncensored-llm.sbs/v1
**الموقع:** https://uncensored-llm.sbs

لو استخدمت نموذج لغوي تكتب بيه عن السياسة أو الصحة أو أمن المعلومات أو أي موضوع يعتبره المزود الأجنبي حسّاس، عارف النتيجة: رفض عام، وفقرة تحذير بدل المحتوى، وإجابة نصها ناقص. الصفحة دي بتشرح بديل مباشر: واجهة متوافقة مع OpenAI بترد على السؤال زي ما اتسأل.

## ليه ده مهم للمطورين في مصر

المنتج العربي محتاج نموذج بيكتب عربية صح، مش ترجمة حرفية من الإنجليزي. والمشكلة الأغلى إن النموذج يرفض مواضيع عادية خالص — مصاريف دراسة، تمويل، صحة، اختبار اختراق — لأن السياسة معمولة لسوق تاني. هنا القرار بيفضل لفريق المنتج، والبث واستدعاء الأدوات و JSON mode شغالين زي ما هما. الحد الوحيد اللي باقي هو المحتوى غير القانوني.

## مثال على الاستدعاء

```bash
export UNLLM_KEY="sk-..."
curl https://uncensored-llm.sbs/v1/chat/completions \
  -H "Authorization: Bearer $UNLLM_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"uncensored-llm","messages":[{"role":"user","content":"اشرح ببساطة إزاي بتتحسب القيمة السوقية لعملة رقمية."}],"stream":true}'
```

```python
# pip install openai
from openai import OpenAI
client = OpenAI(base_url="https://uncensored-llm.sbs/v1", api_key="sk-...")
r = client.chat.completions.create(
    model="uncensored-llm",
    messages=[{"role": "user", "content": "اشرح ببساطة إزاي بتتحسب القيمة السوقية لعملة رقمية."}],
)
print(r.choices[0].message.content)
```

```javascript
import OpenAI from "openai";
const ai = new OpenAI({ baseURL: "https://uncensored-llm.sbs/v1", apiKey: process.env.UNLLM_KEY });
const r = await ai.chat.completions.create({ model: "uncensored-llm", messages: [{ role: "user", content: "اشرح ببساطة إزاي بتتحسب القيمة السوقية لعملة رقمية." }] });
console.log(r.choices[0].message.content);
```

## بيتُستخدم في إيه فعلاً

| الحالة | السبب |
|---|---|
| خدمة العملاء | بوت بيحل المشكلة بدل ما يقرا السياسات. |
| محتوى محلي | مقالات وسكريبتات وإيميلات بنبرة مصرية حقيقية. |
| اختبار أمني بترخيص | شغل هجومي داخل نطاق موقّع من العميل. |
| كتابة للبالغين (18+) | مشاهد صريحة بين بالغين بدون قطع. |

## الاستجابة من مدينتك

زمن الاستجابة بيتحدد من مزود النت مش من البلد. قيسه من جهازك الأول:

```bash
curl -o /dev/null -s -w '%{time_total}s\n' https://uncensored-llm.sbs/v1/models
```

| المدينة | المحافظة |
|---|---|
| القاهرة | القاهرة |
| الجيزة | الجيزة |
| الإسكندرية | الإسكندرية |
| بورسعيد | بورسعيد |
| المنصورة | الدقهلية |
| طنطا | الغربية |
| أسيوط | أسيوط |
| الأقصر | الأقصر |
| أسوان | أسوان |
| الإسماعيلية | الإسماعيلية |
| السويس | السويس |
| دمياط | دمياط |

## أسئلة بتتكرر بجد

### متوافقة فعلاً مع OpenAI؟

أيوه. مسارات /v1/chat/completions و /v1/models والبث SSE بنفس صيغة الأحداث، فالمكتبة الرسمية بتشتغل بمجرد تغيير base_url.

### في فترة تجريبية مجانية؟

الشروط السارية منشورة على https://uncensored-llm.sbs، وأي تغيير في الأسعار بيتعلن هناك مش في المستودع ده.

### بيتحجب إيه؟

المحتوى غير القانوني، بما فيه أي مادة تخص من هم تحت 18 سنة. بره كده الرد بيكون عن الطلب نفسه.

### بتشتغل مع Open WebUI أو LibreChat؟

أيوه، الاتنين بيقبلوا base URL متوافق مع OpenAI. حط https://uncensored-llm.sbs/v1 والمفتاح.

### أحمي المفتاح إزاي؟

متغير بيئة لكل بيئة، وتدوير دوري، ومايتحطش أبداً في الواجهة أو مستودع عام.

## الوثائق دي بلغات تانية

- [pt-BR] https://brown1023.github.io/llm-api-sem-censura-brasil/
- [es-419] https://brown1023.github.io/api-llm-sin-censura-latam/
- [id-ID] https://ryuuless.github.io/uncensored-llm-api-indonesia/
- [vi-VN] https://ryuuless.github.io/uncensored-llm-api-vietnam/
- [tr-TR] https://askcode24.github.io/sansursuz-llm-api-turkiye/
- [de-DE] https://askcode24.github.io/uncensored-llm-api-deutschland/
- [es-ES] https://palazuel0s2004.github.io/api-llm-sin-censura-espana/
- [it-IT] https://palazuel0s2004.github.io/llm-api-senza-censura-italia/
- [en-IN] https://nirav0712.github.io/uncensored-llm-api-india/
- [en-PH] https://nirav0712.github.io/uncensored-llm-api-philippines/
- [ar] https://mohamedabderrehman.github.io/uncensored-llm-api-arabia/

---

uncensored-llm.sbs — واجهة متوافقة مع OpenAI. بيتحجب المحتوى غير القانوني وأي مادة تخص من هم تحت 18 سنة. وغير كده المسؤولية على اللي بيستدعي.