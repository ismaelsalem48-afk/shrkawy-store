# Shrkawy Store

متجر إلكترونيات تجريبي كامل يدعم العربية وRTL، ويحتوي على صفحات المنتجات والتفاصيل والسلة وCheckout ومحاكي دفع تعليمي وصفحات النجاح والفشل والإلغاء.

> **تنبيه:** المشروع تعليمي، ولا يخصم أموالًا حقيقية. لا تُدخل بيانات بطاقة حقيقية.

## التقنيات
- HTML5
- CSS3 (Grid وFlexbox وتصميم متجاوب)
- JavaScript عادي
- localStorage لحفظ السلة والطلب
- Node.js/Express اختياري لربط Stripe Test Mode

## هيكل الملفات
- `index.html`: الصفحة الرئيسية
- `products.html`: قائمة المنتجات
- `product-details.html`: التفاصيل
- `cart.html`: السلة
- `checkout.html`: بيانات العميل والدفع
- `payment.html`: محاكي الدفع
- `success.html`, `failed.html`, `cancel.html`: نتائج الدفع
- `style.css`, `script.js`, `products.js`, `checkout.js`, `payment.js`, `result.js`
- `server/payment-server.js`: خادم اختياري لـStripe Test Mode

## التشغيل محليًا
من داخل مجلد المشروع:
```bash
python -m http.server 5500
```
ثم افتح `http://localhost:5500`.

## تجربة الشراء
1. افتح الصفحة الرئيسية.
2. اختر منتجًا وافتح تفاصيله.
3. أضفه إلى السلة وعدّل الكمية.
4. انتقل إلى Checkout وأدخل بيانات تجريبية.
5. اختر البطاقة التجريبية.
6. في محاكي الدفع استخدم:
   - نجاح: `4242 4242 4242 4242`
   - رفض: `4000 0000 0000 0002`
   - تاريخ: `12/30`
   - CVV: `123`
7. يمكن كذلك اختيار النتيجة يدويًا من القائمة.

## Stripe Test Mode الاختياري
المشروع لا يحتوي على أي Secret Key. لإنشاء حساب Stripe Test واستخدام Hosted Checkout:
1. أنشئ حسابًا واستخدم وضع الاختبار.
2. انسخ `server/.env.example` إلى `server/.env`.
3. أضف `STRIPE_SECRET_KEY` داخل ملف البيئة فقط.
4. نفّذ:
```bash
cd server
npm install
npm start
```
5. توثيق بطاقات Stripe الرسمية: https://docs.stripe.com/testing

**مهم:** الواجهة الحالية تستخدم المحاكي التعليمي افتراضيًا؛ ربط مسار Stripe يتطلب تعديل حدث الإرسال في `checkout.js` لاستدعاء `/api/create-checkout-session` ثم التوجيه إلى `url` الناتج.

## النشر
### Netlify أو GitHub Pages (المحاكي فقط)
ارفع جميع الملفات كما هي، واجعل مجلد المشروع هو Publish Directory. لا يحتاج المحاكي إلى Backend.

### Render/Vercel للـBackend الاختياري
ارفع مجلد `server`، واضبط `STRIPE_SECRET_KEY` و`CLIENT_URL` في Environment Variables. لا ترفع ملف `.env` إلى المستودع.

## الفرق بين الدفع الحقيقي والتجريبي
- الحقيقي يتصل بشبكات الدفع ويجري تسوية مالية فعلية.
- التجريبي أو المحاكي يختبر تجربة المستخدم وحالات النجاح والرفض والإلغاء دون تحريك أموال.
