# مخطط البيانات

نستخدم JSON UTF-8 في البداية لتسهيل المراجعة والمساهمة. أسماء الحقول مستقرة بالإنجليزية، والنصوص متعددة اللغات داخل كائنات اللغة. عند اتساع البيانات يمكن بناء فهرس/API من دون تغيير معنى السجلات.

## الحقول المشتركة

```json
{
  "id": "stable-kebab-case-id",
  "type": "institution|pathway|credential|subject|resource|announcement",
  "status": "proposed|verified|needs_review|archived",
  "sources": [{
    "url": "https://example.dz/",
    "publisher": "اسم الجهة الناشرة",
    "source_type": "official|institution|educator|community|library",
    "accessed_at": "2026-10-28",
    "published_at": null,
    "license": "اسم الترخيص أو unknown"
  }],
  "created_at": "2026-10-28",
  "updated_at": "2026-10-28",
  "reviewed_at": null,
  "review_notes": "ما الذي تم التحقق منه؟"
}
```

التواريخ بصيغة ISO 8601. استخدم `null` عند غياب معلومة بدل اختلاقها. لا تعتبر `unknown` ترخيصًا يسمح بإعادة النشر.

## المؤسسة التعليمية

```json
{
  "id": "dz-example-school-001",
  "type": "institution",
  "status": "proposed",
  "names": {"ar": "اسم المؤسسة", "fr": null, "ber": null},
  "institution_kind": "primary|middle|secondary|university|faculty|institute|vocational|other",
  "education_levels": ["primary"],
  "location": {"wilaya_code": null, "wilaya": null, "municipality": null, "address": null},
  "official_urls": [],
  "program_ids": [],
  "sources": [],
  "created_at": "2026-10-28",
  "updated_at": "2026-10-28",
  "reviewed_at": null
}
```

لا تحفظ معلومات شخصية للموظفين أو الطلبة ضمن سجل المؤسسة.

## المسار والشهادة

المسار يربط المرحلة السابقة واللاحقة، متطلبات الانتقال، المواد والاختيارات. الشهادة تسجل الاسم الرسمي، الجهة المانحة، المستوى، شروطها، السنة التي تنطبق عليها المعلومة، ومصدرها. بيانات القبول والمواعيد متغيرة وتحتاج `valid_from` و`valid_until` عند توفرهما وتاريخ تحقق حديث.

## المادة أو الوحدة

تتضمن الاسم والمرحلة والشعبة والمستوى والسنة والوحدة/الكفاءة واللغات ومراجع البرنامج الرسمي. اربطها بمعرف ثابت كي يمكن للتطبيق تصفية الموارد تبعًا لها.

## المورد التعليمي

```json
{
  "id": "resource-example-001",
  "type": "resource",
  "status": "proposed",
  "title": {"ar": "عنوان المورد", "fr": null, "ber": null},
  "resource_kind": "lesson|summary|exercise|exam|research|book|video|channel|reference|template|other",
  "description": {"ar": "وصف موجز أصلي", "fr": null, "ber": null},
  "education_level": "secondary",
  "grade": null,
  "track": null,
  "subject_id": null,
  "unit": null,
  "language": ["ar"],
  "provider": "الجهة أو المؤلف",
  "url": "https://example.dz/resource",
  "license": "unknown",
  "redistribution_allowed": false,
  "published_at": null,
  "last_verified_at": null,
  "tags": [],
  "sources": [],
  "created_at": "2026-10-28",
  "updated_at": "2026-10-28",
  "reviewed_at": null
}
```

ابدأ بفهرسة الروابط والبيانات الوصفية. لا ترفع الملف نفسه إلا إذا كان الترخيص أو الإذن يسمح صراحة بالتوزيع.

## إعلان ومعلومة زمنية

إعلان المنحة أو التسجيل أو المسابقة يحفظ الجهة الرسمية والرابط وتاريخ النشر وبداية/نهاية الصلاحية والمنطقة/الفئة المعنية. عند انتهاء الصلاحية يصبح مؤرشفًا، ولا يظهر كفرصة مفتوحة.

## التحقق

- `proposed`: لم يعتمد بعد.
- `verified`: راجعه مساهم مخول واستند إلى مصدر صالح.
- `needs_review`: قديم أو تغيّر مصدره أو ورد بلاغ عنه.
- `archived`: انتهت صلاحيته أو لم يعد صالحًا للعرض النشط.

بيانات الطالب الشخصية وتقدمه ونتائجه لا تنتمي إلى هذا المخطط ولا تحفظ في المستودع.
