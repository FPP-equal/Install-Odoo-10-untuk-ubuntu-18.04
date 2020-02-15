# Install-Odoo-10-untuk-ubuntu-18.04
berikut adalah langkah - langkah instalasi odoo 10 di ubuntu 18.04



**1.Update ubuntu**

```sudo apt update && sudo apt dist-upgrade```

```sudo reboot```



**2.Install aplikasi pendukung python**

```sudo apt install python-pip python-dev libevent-dev gcc libxml2-dev node-less python-cups python-dateutil python-decorator python-docutils python-feedparser python-gdata python-geoip python-gevent python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-passlib python-psutil python-psycopg2 python-pychart python-pydot python-pyparsing python-reportlab python-requests python-simplejson python-tz python-unicodecsv python-unittest2 python-vatnumber python-vobject python-werkzeug python-xlwt python-yaml python-babel python-pil```

```sudo pip install pypdf```



**3.Buat akun baru untuk user Odoo**

```sudo adduser --system --home=/opt/odoo --group odoo```



**4. Install wkhtmltopdf (64 bit) untuk keperluan print ke pdf**

```sudo apt install fontconfig fontconfig-config fonts-dejavu-core libfontconfig1 libfontenc1 libjpeg-turbo8 libxrender1 x11-common xfonts-75dpi xfonts-base```

```wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb```

```sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb```

```sudo cp /usr/local/bin/wkhtmltopdf /usr/bin```

```sudo cp /usr/local/bin/wkhtmltoimage /usr/bin```



**6.Install Postgresql dan buat akun user Odoo 10 untuk Postgresql**

```sudo apt install postgresql```

```sudo su - postgres```

```createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo```

```exit```



**7.Ambil Odoo 10 dari sumber repository**

```sudo apt install git```

```sudo su - odoo -s /bin/bash```

```git clone https://www.github.com/odoo/odoo --depth 1 --branch 10.0 --single-branch ```



**8.Pengaturan server odoo**

Ubah kepemilikan ke user odoo
```sudo chown -R odoo: * ```

Instalasi file pengaturan, Copy odoo.conf ke /etc directory:

```sudo cp /opt/odoo/odoo/debian/odoo.conf /etc/odoo-server.conf```

```sudo chown odoo: /etc/odoo-server.conf```

```sudo chmod 640 /etc/odoo-server.conf```



**9.Membuat file log**

```sudo mkdir /var/log/odoo```

```sudo chown odoo:root /var/log/odoo```

```cd /var/log/odoo```

```sudo touch odoo-server.log```



**10.init script**

Buatlah sistem unit 'odoo server' agar aplikasi menjadibersifat service

```cd /lib/systemd/system/```

```sudo wget https://raw.githubusercontent.com/anicetkeric/odoo_v10/master/odoo-server.sh```

```sudo cp odoo-server.sh /lib/systemd/system/odoo-server.service```

Ubah odoo-server service permission dan kepemilikan agar hanya akses root yang dapat mengedit dan untuk user odoo hanya akan bisa membaca atau menjalankannya.

```sudo chmod 755 /lib/systemd/system/odoo-server.service```

```sudo chown root: /lib/systemd/system/odoo-server.service```

Mengaktifkan Odoo pada saat boot:

```sudo systemctl enable odoo-server```

Memulai sistem Odoo

```sudo systemctl start odoo-server```

reload sistem process

```sudo systemctl daemon-reload```

**11.Testing Odoo**

masukan Localhost:8096 atau http://192.168.1.200:8069 ke addres bar pada browser anda, jika instalasi berhasil maka Odoo akan muncul

**Referensi:**

-https://github.com/anicetkeric/odoo_v10

-https://www.grobak.net/id/blog/odoo10-ubuntu/install-odoo-10-di-ubuntu-1804
