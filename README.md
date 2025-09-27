# Terraform + Docker + Ansible + NGINX

- 3 apps Node.js (`app1`, `app2`, `app3`) conectadas a Redis y Postgres  
- Grafana para monitoreo  
- **NGINX como load balancer** (round-robin) entre las 3 apps  
- **Ansible** para automatizar el despliegue de Terraform y NGINX

## Requisitos
- Docker  
- Terraform
- Ansible

## dev 

Grafana → http://localhost:5050  
App1 → http://localhost:5011  
App2 → http://localhost:5012  
App3 → http://localhost:5013  
NGINX → http://localhost:3000

## Uso manual (Terraform)
\`\`\`bash
cd terraform
terraform init
terraform workspace new dev   # primera vez
terraform workspace select dev
terraform apply -auto-approve
\`\`\`

Esto hará automáticamente:  
1. Copiar/templa `nginx.conf` con round-robin  
2. Ejecutar `terraform init`  
3. Crear o seleccionar workspace  
4. Aplicar toda la infraestructura (apps, NGINX, Redis, Postgres, Grafana)

## Verificar round-robin
\`\`\`bash
for i in {1..6}; do curl -s http://localhost:3000; echo; done
\`\`\`
Salida esperada:
Hola, soy la APP2 corriendo en Docker 🚀
Hola, soy la APP3 corriendo en Docker 🚀
Hola, soy la APP1 corriendo en Docker 🚀
Hola, soy la APP2 corriendo en Docker 🚀
Hola, soy la APP3 corriendo en Docker 🚀
Hola, soy la APP1 corriendo en Docker 🚀
  
## Integrantes
Rodríguez Ruiz Alessandro Paul
Kristel Rivera Chamorro
Brad Barrios Capa  
Mc Brenk Ponce Vázques
Darli Manuel Medina Sixce
