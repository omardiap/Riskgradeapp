import streamlit as st

st.set_page_config(page_title="Risk Grade App")

st.title("Risk Grade Calculator")

st.markdown("احسب درجة الخطر للعميل بناءً على العوامل التالية:")

income = st.number_input("الدخل الشهري (جنيه)", min_value=0)
credit_score = st.slider("درجة الـ Credit Score", 0, 900)
employment_years = st.slider("عدد سنوات العمل", 0, 40)
has_default = st.selectbox("هل العميل تأخر في سداد قرض قبل كده؟", ["لا", "نعم"])

risk_score = (
    income / 1000 +
    credit_score / 100 +
    employment_years * 2 -
    (50 if has_default == "نعم" else 0)
)

if st.button("احسب"):
    if risk_score > 70:
        grade = "منخفض المخاطر ✅"
    elif risk_score > 50:
        grade = "متوسط المخاطر ⚠️"
    else:
        grade = "مرتفع المخاطر ❌"

    st.subheader(f"النتيجة: {grade}")
    st.caption(f"الدرجة الرقمية: {risk_score:.2f}") Riskgradeapp
