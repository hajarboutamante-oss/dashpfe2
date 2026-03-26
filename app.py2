import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# ==============================
# CONFIGURATION PAGE
# ==============================
st.set_page_config(page_title="Dashboard Aéraulique", layout="wide")

# ==============================
# TITRE
# ==============================
st.title("📊 Dashboard PFE - Réseau Aéraulique")

# ==============================
# SIDEBAR (PARAMÈTRES)
# ==============================
st.sidebar.header("⚙️ Paramètres")

Q_ref = st.sidebar.slider("Débit de référence (m3/h)", 1000, 50000, 20000)
DP_ref = st.sidebar.slider("Perte de charge (Pa)", 100, 2000, 800)

p_lin = st.sidebar.number_input("Pertes linéaires (Pa)", value=500)
p_sing = st.sidebar.number_input("Pertes singulières (Pa)", value=300)

st.sidebar.subheader("Caissons")
C1 = st.sidebar.number_input("C1 (Pa)", value=1036)
C2 = st.sidebar.number_input("C2 (Pa)", value=706)
C3 = st.sidebar.number_input("C3 (Pa)", value=1002)

# ==============================
# RÉSULTATS
# ==============================
st.header("📌 Résultats")

col1, col2 = st.columns(2)

with col1:
    st.metric("Débit", f"{Q_ref} m³/h")

with col2:
    st.metric("Perte de charge", f"{DP_ref} Pa")

# Analyse automatique
if DP_ref < 700:
    st.success("✔️ Réseau performant")
elif 700 <= DP_ref <= 1000:
    st.warning("⚠️ Réseau acceptable")
else:
    st.error("❌ Perte de charge élevée")

# ==============================
# 1. COURBE ΔP = f(Q)
# ==============================
st.subheader("📈 Courbe ΔP = f(Q)")

Q = np.linspace(1000, 50000, 100)
DP = DP_ref * (Q / Q_ref)**2

fig1, ax1 = plt.subplots()
ax1.plot(Q, DP, linewidth=2)
ax1.scatter(Q_ref, DP_ref)  # point actuel

ax1.set_xlabel("Débit (m³/h)")
ax1.set_ylabel("Perte de charge (Pa)")
ax1.set_title("Évolution de la perte de charge")

st.pyplot(fig1)

# ==============================
# 2. RÉPARTITION DES PERTES
# ==============================
st.subheader("🥧 Répartition des pertes")

fig2, ax2 = plt.subplots()
ax2.pie(
    [p_lin, p_sing],
    labels=["Linéaires", "Singulières"],
    autopct='%1.1f%%'
)

st.pyplot(fig2)

# ==============================
# 3. COMPARAISON DES CAISSONS
# ==============================
st.subheader("📊 Comparaison des caissons")

labels = ["C1", "C2", "C3"]
values = [C1, C2, C3]

fig3, ax3 = plt.subplots()
ax3.bar(labels, values)

ax3.set_ylabel("Perte de charge (Pa)")
ax3.set_title("Comparaison des pertes par caisson")

st.pyplot(fig3)

# ==============================
# 4. AFFICHAGE TOTAL
# ==============================
st.subheader("📌 Synthèse")

total = p_lin + p_sing

st.write(f"**Pertes totales : {total} Pa**")
