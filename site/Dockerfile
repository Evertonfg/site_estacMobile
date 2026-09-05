# SITE INSTITUCIONAL — nginx servindo arquivo estático.
#
# Dockerfile e não "static site" do painel: assim o deploy é o MESMO em
# EasyPanel, Coolify, Render ou numa VPS crua. Sem ele, o EasyPanel tenta
# adivinhar como servir a pasta — e HTML solto, sem package.json, é justamente
# o caso em que a detecção automática falha.
#
# Imagem alpine: 40 MB, sobe em segundos, sem Node nenhum. O site não tem
# build — é um arquivo.
FROM nginx:1.27-alpine

# A configuração vem antes do conteúdo: mudando só o HTML, o Docker reaproveita
# esta camada e o deploy fica mais rápido.
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY . /usr/share/nginx/html

# O Dockerfile e o nginx.conf não são página: dentro do html eles seriam
# servidos como arquivo, e a configuração do servidor ficaria pública.
RUN rm -f /usr/share/nginx/html/Dockerfile \
          /usr/share/nginx/html/nginx.conf \
          /usr/share/nginx/html/.dockerignore

EXPOSE 80

# HEALTHCHECK: o EasyPanel usa isto pra saber se o contêiner subiu de verdade,
# em vez de assumir que sim porque o processo existe.
# HEALTHCHECK --interval=30s --timeout=3s \
 #  CMD wget -q --spider http://localhost/ || exit 1
