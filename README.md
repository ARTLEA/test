import React, { useState } from "react";

export default function MadeByMeOnboarding() {
  const [step, setStep] = useState(1);
  const [formData, setFormData] = useState({
    email: "",
    password: "",
    plan: "",
    role: "",
    designerInfo: {
      productTypes: "",
      experience: "",
      tools: "",
    },
    marketerInfo: {
      channels: "",
      targetAudience: "",
      experience: "",
    },
    storeName: "",
    storeDescription: "",
    products: [],
  });

  const handleChange = (e) => {
    const { name, value } = e.target;

    if (step === 3 && formData.role === "designer" && ["productTypes", "experience", "tools"].includes(name)) {
      setFormData({
        ...formData,
        designerInfo: { ...formData.designerInfo, [name]: value },
      });
    } else if (step === 3 && formData.role === "marketer" && ["channels", "targetAudience", "experience"].includes(name)) {
      setFormData({
        ...formData,
        marketerInfo: { ...formData.marketerInfo, [name]: value },
      });
    } else {
      setFormData({ ...formData, [name]: value });
    }
  };

  const nextStep = () => setStep((s) => Math.min(s + 1, 7));
  const prevStep = () => setStep((s) => Math.max(s - 1, 1));

  return (
    <div className="min-h-screen bg-gradient-to-tr from-indigo-400 via-purple-500 to-pink-500 flex items-center justify-center p-6">
      <div className="bg-white rounded-xl shadow-lg w-full max-w-2xl p-8">
        {step === 1 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">التسجيل في منصة MADE BY ME</h2>
            <input
              type="email"
              name="email"
              placeholder="البريد الإلكتروني"
              value={formData.email}
              onChange={handleChange}
              className="border rounded p-3 mb-4 w-full"
            />
            <input
              type="password"
              name="password"
              placeholder="كلمة المرور"
              value={formData.password}
              onChange={handleChange}
              className="border rounded p-3 mb-4 w-full"
            />
            <button
              disabled={!formData.email || !formData.password}
              onClick={nextStep}
              className="bg-purple-600 text-white py-3 px-6 rounded w-full disabled:opacity-50"
            >
              التالي
            </button>
          </>
        )}

        {step === 2 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">اختر خطتك</h2>
            <div className="space-y-4 text-lg">
              <label className={`block p-4 border rounded cursor-pointer ${formData.plan === "free" ? "bg-purple-100 border-purple-500" : ""}`}>
                <input
                  type="radio"
                  name="plan"
                  value="free"
                  checked={formData.plan === "free"}
                  onChange={handleChange}
                  className="mr-3"
                />
                التجربة المجانية - 15 يوم
              </label>
              <label className={`block p-4 border rounded cursor-pointer ${formData.plan === "monthly" ? "bg-purple-100 border-purple-500" : ""}`}>
                <input
                  type="radio"
                  name="plan"
                  value="monthly"
                  checked={formData.plan === "monthly"}
                  onChange={handleChange}
                  className="mr-3"
                />
                الاشتراك الشهري - 9.99 دولار
              </label>
              <label className={`block p-4 border rounded cursor-pointer ${formData.plan === "yearly" ? "bg-purple-100 border-purple-500" : ""}`}>
                <input
                  type="radio"
                  name="plan"
                  value="yearly"
                  checked={formData.plan === "yearly"}
                  onChange={handleChange}
                  className="mr-3"
                />
                الاشتراك السنوي - 29.99 دولار
              </label>
            </div>
            <div className="flex justify-between mt-8">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100">عودة</button>
              <button disabled={!formData.plan} onClick={nextStep} className="bg-purple-600 text-white py-3 px-6 rounded disabled:opacity-50">
                التالي
              </button>
            </div>
          </>
        )}

        {step === 3 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">هل أنت مصمم أم مسوّق؟</h2>
            <select
              name="role"
              value={formData.role}
              onChange={handleChange}
              className="border rounded p-3 w-full mb-6"
            >
              <option value="">اختر دورك</option>
              <option value="designer">مصمم</option>
              <option value="marketer">مسوّق</option>
            </select>

            {formData.role === "designer" && (
              <div className="space-y-4">
                <input
                  type="text"
                  name="productTypes"
                  placeholder="أنواع المنتجات التي تصممها"
                  value={formData.designerInfo.productTypes}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
                <input
                  type="text"
                  name="experience"
                  placeholder="خبرتك في التصميم"
                  value={formData.designerInfo.experience}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
                <input
                  type="text"
                  name="tools"
                  placeholder="أدوات التصميم المفضلة (مثلاً Canva, Figma)"
                  value={formData.designerInfo.tools}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
              </div>
            )}

            {formData.role === "marketer" && (
              <div className="space-y-4">
                <input
                  type="text"
                  name="channels"
                  placeholder="قنوات التسويق التي تستخدمها (مثلاً Instagram, TikTok)"
                  value={formData.marketerInfo.channels}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
                <input
                  type="text"
                  name="targetAudience"
                  placeholder="الجمهور المستهدف"
                  value={formData.marketerInfo.targetAudience}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
                <input
                  type="text"
                  name="experience"
                  placeholder="خبرتك في التسويق"
                  value={formData.marketerInfo.experience}
                  onChange={handleChange}
                  className="border rounded p-3 w-full"
                />
              </div>
            )}

            <div className="flex justify-between mt-8">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100">
                عودة
              </button>
              <button disabled={!formData.role} onClick={nextStep} className="bg-purple-600 text-white py-3 px-6 rounded disabled:opacity-50">
                التالي
              </button>
            </div>
          </>
        )}

        {step === 4 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">إنشاء المتجر والبروفايل</h2>
            <input
              type="text"
              name="storeName"
              placeholder="اسم المتجر"
              value={formData.storeName}
              onChange={handleChange}
              className="border rounded p-3 w-full mb-4"
            />
            <textarea
              name="storeDescription"
              placeholder="وصف المتجر"
              value={formData.storeDescription}
              onChange={handleChange}
              className="border rounded p-3 w-full mb-4"
              rows={4}
            />
            <div className="flex justify-between mt-8">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100">
                عودة
              </button>
              <button
                disabled={!formData.storeName || !formData.storeDescription}
                onClick={nextStep}
                className="bg-purple-600 text-white py-3 px-6 rounded disabled:opacity-50"
              >
                التالي
              </button>
            </div>
          </>
        )}

        {step === 5 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">رفع المنتجات</h2>
            <p className="mb-4 text-gray-600">ميزة بسيطة لإضافة منتج (تطوير لاحق)</p>
            {/* هنا يمكن إضافة فورم رفع منتجات حقيقي مستقبلاً */}
            <button onClick={nextStep} className="bg-purple-600 text-white py-3 px-6 rounded w-full">
              متابعة (تخطي الرفع مؤقتًا)
            </button>
            <div className="mt-4">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100 w-full">
                عودة
              </button>
            </div>
          </>
        )}

        {step === 6 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">التسويق الذكي باستخدام الذكاء الاصطناعي</h2>
            <p className="mb-4 text-gray-700">
              التكامل مع Canva، Figma، وAdobe لإنشاء محتوى تسويقي تلقائي للمنتجات.
            </p>
            <button onClick={nextStep} className="bg-purple-600 text-white py-3 px-6 rounded w-full">
              متابعة
            </button>
            <div className="mt-4">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100 w-full">
                عودة
              </button>
            </div>
          </>
        )}

        {step === 7 && (
          <>
            <h2 className="text-3xl font-bold mb-6 text-purple-700">وسائل الدفع</h2>
            <p className="mb-4 text-gray-700">سيتم إضافة خيارات الدفع لاحقًا.</p>
            <button
              onClick={() => alert("تم إتمام التسجيل بنجاح!")}
              className="bg-green-600 text-white py-3 px-6 rounded w-full"
            >
              إكمال
            </button>
            <div className="mt-4">
              <button onClick={prevStep} className="py-3 px-6 border rounded hover:bg-gray-100 w-full">
                عودة
              </button>
            </div>
          </>
        )}
      </div>
    </div>
  );
}
