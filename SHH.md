🔑 SSH (Private vs Public Key)

Private Key – Sizning maxfiy kalitingiz. Faqat sizda bo‘ladi, hech kimga bermang. ~/.ssh/id_rsa yoki ~/.ssh/id_ed25519.

Public Key – Serverga qo‘yiladigan kalit. ~/.ssh/id_rsa.pub yoki ~/.ssh/id_ed25519.pub.

Kalit yaratish:

ssh-keygen -t ed25519 -C "you@example.com"


Serverga public key qo‘yish:

ssh-copy-id -i ~/.ssh/id_ed25519.pub ubuntu@server_ip


Keyin parolsiz ulanishingiz mumkin:

ssh -i ~/.ssh/id_ed25519 ubuntu@server_ip

🔒 SSL Certificate

SSL (HTTPS) xavfsiz ulanishni ta’minlaydi.

Eng ko‘p ishlatiladigani: Let’s Encrypt (bepul).

O‘rnatish:

sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx -d domain.uz -d www.domain.uz


Har 3 oyda avtomatik yangilanadi:

sudo certbot renew --dry-run

🔥 Firewall

Ubuntu UFW:

sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status


AWS Security Group:

22 (SSH) → faqat sizning IP manzilingizga ruxsat.

80 (HTTP), 443 (HTTPS) → 0.0.0.0/0.

🌐 Portlar va Protokollar

TCP – bog‘lanishli, ishonchli (HTTP, HTTPS, SSH).

UDP – bog‘lanishsiz, tezroq (DNS, video, VOIP).

Muhim portlar:

22/tcp → SSH

80/tcp → HTTP

443/tcp → HTTPS

53/tcp/udp → DNS

⚙️ NGINX

Reverse Proxy: tashqi so‘rovlarni ichki serverlarga yo‘naltiradi.

Konfiguratsiya fayllari:

/etc/nginx/sites-available/

/etc/nginx/sites-enabled/

Misol:

server {
    listen 80;
    server_name project.uz;
    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
    }
}


Tekshirish:

sudo nginx -t
sudo systemctl restart nginx

📦 PM2 (Node.js Process Manager)

O‘rnatish:

sudo npm install -g pm2


Ishga tushirish:

pm2 start dist/main.js --name app1
pm2 save
pm2 startup


Ko‘rish:

pm2 ls
pm2 logs app1

🐧 Ubuntu va Terminal

root foydalanuvchi → to‘liq huquqlarga ega. Tavsiya: oddiy user + sudo.

File access:

ls -l → fayl huquqlarini ko‘rish

chmod → ruxsatlarni o‘zgartirish

chown → egasini o‘zgartirish

systemctl → xizmatlarni boshqarish:

sudo systemctl status nginx
sudo systemctl restart nginx


nano → matnli fayllarni tahrirlash (Ctrl+O saqlash, Ctrl+X chiqish).

curl → HTTP so‘rov yuborish:

curl -I https://domain.uz

👨‍💻 Rollar

Cloud Engineer → AWS, GCP, Azure’da infratuzilma quradi. Networking, VM, storage, scaling.

DevOps Engineer → CI/CD, Docker, Kubernetes, monitoring, deploy pipeline.

Backend Developer (BE) → API, DB, autentifikatsiya, biznes logika.

Frontend Developer (FE) → UI, brauzer qismi, React/Vue/Angular.
