# GapGPT Chatbot

یک کلاینت وب ساده، برای اتصال به API خدمات GapGPT با پشتیبانی کامل از قابلیت حفظ مکالمه (Context) و قابلیت‌های پیشرفته.

دمو: https://behnamonline.github.io/gapgpt-chatbot

## ویژگی‌ها
- پشتیبانی از ادامه گفتگو (Multi-turn Chat) با ارسال خودکار `previous_response_id`.
- ریست خودکار تاریخچه گفتگو به محض تغییر مدل.

---

## نحوه کار با API (مثال‌های cURL)

### ۱. ارسال پیام اول (شروع گفتگو)
```bash
curl https://api.gapgpt.app/v1/responses\
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "deepseek-v4-flash",
    "input": "عدد ۱۸ را به خاطر بسپار"
  }'
```
خروجی اینشکلی هست

```json
{"created_at":1792503932,"error":null,"id":"resp_990b65876e74fdf370174674732d96d6","incomplete_details":null,"instructions":null,"max_output_tokens":null,"metadata":{},"model":"deepseek/deepseek-v4-flash","object":"response","output":[{"content":[{"annotations":[],"text":"باشه، عدد ۱۸ رو به خاطر دارم. 😊\n\nاگر سوال یا کاری با این عدد داری، خوشحال میشم کمک کنم.","type":"output_text"}],"id":"msg_5c527d9926ab61b4bccdda7a6323c907","role":"assistant","status":"completed","type":"message"}],"parallel_tool_calls":true,"previous_response_id":null,"reasoning":null,"status":"completed","store":true,"temperature":1,"text":{"format":{"type":"text"}},"tool_choice":"auto","tools":[],"top_p":1,"truncation":"disabled","usage":{"input_tokens":14,"input_tokens_details":{"cached_tokens":0},"output_tokens":38,"output_tokens_details":{"reasoning_tokens":0},"total_tokens":52},"user":null}
```
و آی دی پیام در مثال بالا مثلا میشه resp_990b65876e74fdf370174674732d96d6

### ۲. ارسال پیام بعدی (ادامه گفتگو با استفاده از previous_response_id)

```bash
curl https://api.gapgpt.app/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "deepseek-v4-flash",
    "input": "خب حالا با ۱۰ جمع کن و بگو",
    "previous_response_id": "resp_990b65876e74fdf370174674732d96d6"
  }'
```
