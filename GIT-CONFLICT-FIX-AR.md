# 🔧 حل مشكلة: "untracked working tree files would be overwritten"

## المشكلة

```
error: The following untracked working tree files would be overwritten by merge:
	.gitignore
	index.html
	package-lock.json
```

**السبب:** لديك ملفات محلية غير متتبعة (untracked)، وهذه الملفات موجودة أيضاً على GitHub. Git يرفض الدمج خوفاً من استبدالها.

---

## ✅ الحل السريع

### الطريقة 1: إضافة الملفات ثم Pull (موصى بها)

```powershell
# 1. أضف الملفات إلى Git
git add .gitignore index.html package-lock.json

# 2. احفظها
git commit -m "Add local files before merge"

# 3. اجلب التغييرات
git pull origin main

# 4. ارفع كل شيء
git push origin main
```

### الطريقة 2: حذف الملفات المحلية (إذا كانت قديمة)

إذا كانت الملفات المحلية قديمة ولا تحتاجها:

```powershell
# احذف الملفات
Remove-Item .gitignore
Remove-Item index.html
Remove-Item package-lock.json

# اجلب التغييرات
git pull origin main

# ارفع التغييرات
git push origin main
```

### الطريقة 3: نقل الملفات مؤقتاً

إذا أردت الاحتفاظ بنسخة احتياطية:

```powershell
# أنشئ مجلد احتياطي
New-Item -ItemType Directory -Path backup -Force

# انقل الملفات
Move-Item .gitignore backup/
Move-Item index.html backup/
Move-Item package-lock.json backup/

# اجلب التغييرات
git pull origin main

# ارفع التغييرات
git push origin main

# إذا أردت استعادة الملفات لاحقاً
# Move-Item backup/* .
```

---

## 📝 خطوات تفصيلية (الطريقة الموصى بها)

### الخطوة 1: أضف الملفات إلى Git

```powershell
git add .gitignore index.html package-lock.json
```

### الخطوة 2: احفظ التغييرات

```powershell
git commit -m "Add local files before merge"
```

### الخطوة 3: اجلب التغييرات من GitHub

```powershell
git pull origin main
```

**إذا ظهرت نافذة merge:**
- اضغط `Ctrl + C` لإلغائها
- ثم استخدم:
```powershell
git pull origin main --no-edit
```

### الخطوة 4: ارفع كل شيء

```powershell
git push origin main
```

---

## 🔍 إذا ظهرت تعارضات بعد Pull

إذا ظهرت رسالة "CONFLICT":

1. **افتح الملفات المتعارضة** (`.gitignore`, `index.html`, `package-lock.json`)
2. **ابحث عن:**
   ```
   <<<<<<< HEAD
   (تغييراتك)
   =======
   (تغييرات من GitHub)
   >>>>>>> origin/main
   ```
3. **احذف العلامات واختر التغييرات التي تريدها**
4. **احفظ الملفات**
5. **ثم:**
   ```powershell
   git add .
   git commit -m "Resolve merge conflicts"
   git push origin main
   ```

---

## ⚠️ ملاحظات مهمة

### ملف package-lock.json

- هذا الملف مهم لإدارة المكتبات
- عادة ما يكون من الأفضل استخدام النسخة من GitHub
- إذا ظهر تعارض، استخدم النسخة من GitHub

### ملف .gitignore

- هذا الملف يحدد الملفات التي يجب تجاهلها
- تأكد من أن النسخة النهائية تحتوي على جميع القواعد المطلوبة

### ملف index.html

- إذا كان هذا ملف قديم من مشروع سابق، يمكن حذفه
- إذا كان مهم، احتفظ به

---

## 🎯 الحل الأسرع (إذا كنت متأكداً)

إذا كنت متأكداً أن الملفات على GitHub هي الأحدث والأصح:

```powershell
# احذف الملفات المحلية
Remove-Item .gitignore -ErrorAction SilentlyContinue
Remove-Item index.html -ErrorAction SilentlyContinue
Remove-Item package-lock.json -ErrorAction SilentlyContinue

# اجلب التغييرات
git pull origin main

# ارفع التغييرات
git push origin main
```

---

## ✅ بعد حل المشكلة

1. **اذهب إلى Railway Dashboard**
2. **ستجد أن Railway بدأ عملية بناء جديدة تلقائياً**
3. **انتظر حتى ترى "Deploy Succeeded"**
4. **جرب الرابط مرة أخرى**

---

## 📋 ملخص الأوامر (الحل الموصى به)

```powershell
# 1. أضف الملفات
git add .gitignore index.html package-lock.json

# 2. احفظها
git commit -m "Add local files"

# 3. اجلب التغييرات
git pull origin main --no-edit

# 4. ارفع كل شيء
git push origin main
```

---

## 🆘 إذا استمرت المشكلة

1. **تحقق من حالة Git:**
   ```powershell
   git status
   ```

2. **إذا ظهرت ملفات أخرى، أضفها:**
   ```powershell
   git add .
   git commit -m "Add all files"
   git pull origin main --no-edit
   git push origin main
   ```

---

**💡 نصيحة:** دائماً استخدم `git status` قبل `git pull` لمعرفة حالة الملفات!

