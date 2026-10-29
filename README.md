import qrcode
from PIL import Image

# 1. CONFIGURAÇÃO
# Caminho do seu link/PIX/texto
DADO = "https://instagram.com/grab.ielalves"

# Caminhos no celular - AJUSTA AQUI
CAMINHO_LOGO = "/storage/emulated/0/Download/logo.png"
CAMINHO_SAIDA = "/storage/emulated/0/Download/qr_com_logo.png"

# 2. GERA O QR COM ERRO ALTO (H)
qr = qrcode.QRCode(
    version=1,
    error_correction=qrcode.constants.ERROR_CORRECT_H, # ESSENCIAL pra logo
    box_size=10,
    border=4,
)
qr.add_data(DADO)
qr.make(fit=True)

img_qr = qr.make_image(fill_color="black", back_color="white").convert("RGB")

# 3. ABRE E REDIMENSIONA A LOGO
logo = Image.open(CAMINHO_LOGO).convert("RGBA")

# A logo tem que ter no máximo 25% do QR
tamanho_qr = img_qr.size[0]
tamanho_logo = tamanho_qr // 4
logo = logo.resize((tamanho_logo, tamanho_logo))

# 4. CRIA FUNDO BRANCO ATRÁS DA LOGO (pra não quebrar a leitura)
# Cria um quadrado branco um pouco maior que a logo
fundo_branco_size = int(tamanho_logo * 1.1)
fundo_branco = Image.new("RGB", (fundo_branco_size, fundo_branco_size), "white")

# Posição central
pos_x = (tamanho_qr - fundo_branco_size) // 2
pos_y = (tamanho_qr - fundo_branco_size) // 2

# Cola o fundo branco primeiro
img_qr.paste(fundo_branco, (pos_x, pos_y))

# Agora cola a logo centralizada por cima
pos_logo_x = (tamanho_qr - tamanho_logo) // 2
pos_logo_y = (tamanho_qr - tamanho_logo) // 2

# Usa a própria logo como máscara pra respeitar transparência
img_qr.paste(logo, (pos_logo_x, pos_logo_y), logo)

# 5. SALVA
img_qr.save(CAMINHO_SAIDA)
print(f"Salvo em: {CAMINHO_SAIDA}")
