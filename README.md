# N
Vendedor fantasma 
streamlit
google-generativeai
ibm-cloud-sdk-core
ibm-secrets-manager-sdk
import streamlit as st
import google.generativeai as genai
from ibm_cloud_sdk_core.security import IamAuthenticator
from ibm_secrets_manager_sdk.secrets_manager_v2 import SecretsManagerV2
from streamlit.components.v1 import html

# --- SEUS DATOS OFICIAIS ---
IBM_API_KEY = "ApiKey-b2fd4100-96f7-4ecb-894e-9e9cdd4a45f0"
INSTANCE_URL = "https://6061c436-358a-4d3d-8c50-5bbd7765c9da.br-sao.secrets-manager.appdomain.cloud"
GEMINI_KEY = "AIzaSyDpDVBS7G41MHSu-6i0cwTRp4QxFgmSYIU"
PAYPAL_ID = "2E9XQDPX2XYJG"

# --- INICIALIZAÇÃO ---
genai.configure(api_key=GEMINI_KEY)
model = genai.GenerativeModel('gemini-1.5-flash')

try:
    auth = IamAuthenticator(IBM_API_KEY)
    sm = SecretsManagerV2(authenticator=auth)
    sm.set_service_url(INSTANCE_URL)
except:
    pass

# --- INTERFACE QUÂNTICA ---
st.set_page_config(page_title="Vendedor Fantasma IBM", page_icon="⚛️")

st.markdown("""
    <style>
    .stApp { background-color: #00050a; color: #00f2ff; font-family: 'Courier New', monospace; }
    .stButton>button { 
        background: linear-gradient(45deg, #00f2ff, #0072ff); 
        color: white; border: none; border-radius: 8px; width: 100%; font-weight: bold; height: 3.5em;
    }
    .quantum-card { border: 1px solid #00f2ff; padding: 20px; border-radius: 10px; background: rgba(0, 242, 255, 0.05); }
    </style>
    """, unsafe_allow_html=True)

st.title("⚛️ VENDEDOR FANTASMA QUÂNTICO")
st.write("### Conectado à IBM Cloud São Paulo")
st.markdown("---")

perfil = st.text_input("INSIRA O @ PARA ANÁLISE DE LUCRO:", placeholder="@seu_perfil")

if perfil:
    if st.button("EXECUTAR DIAGNÓSTICO IBM"):
        with st.status("🌀 Processando em Cluster Quântico...", expanded=True) as s:
            st.write("Autenticando IBM IAM...")
            st.write("Acessando Secrets Manager br-sao...")
            
            prompt = f"Analise o perfil {perfil}. Dê 2 dicas de marketing de elite e venda o serviço 'Vendedor Fantasma' de R$ 5.000. Seja magnético."
            response = model.generate_content(prompt)
            s.update(label="✅ PROCESSAMENTO CONCLUÍDO!", state="complete")

        st.markdown(f'<div class="quantum-card">{response.text}</div>', unsafe_allow_html=True)

        # --- FECHAMENTO PAYPAL ---
        st.markdown("---")
        st.subheader("💎 DESBLOQUEAR ESTRATÉGIA (PLANO OURO)")
        st.write("Receba o setup completo e a consultoria individual.")
        
        col1, col2 = st.columns(2)
        with col1:
            st.info("### VALOR: R$ 5.000,00\n(Pagamento Seguro via PayPal)")
            st.write("- Tecnologia IBM Cloud\n- Escala Garantida")

        with col2:
            paypal_html = f"""
            <div style="display: flex; justify-content: center;">
                <script src="https://www.paypal.com"></script>
                <div id="paypal-container-{PAYPAL_ID}"></div>
                <script>
                  paypal.HostedButtons({{ hostedButtonId: "{PAYPAL_ID}" }}).render("#paypal-container-{PAYPAL_ID}")
                </script>
            </div>
            """
            html(paypal_html, height=350)

st.sidebar.write("🔒 **IBM STATUS: PROTECTED**")
st.sidebar.write("Region: **br-sao**")
st.sidebar.write("🚀 **Meta: R$ 200.000,00**")
