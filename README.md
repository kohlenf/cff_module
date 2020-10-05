Steps:

Need install dev tools and libs

apt install -y build-essential && apt -y install libpcre3 libssl-dev libpcre3-dev libssl-dev libxml2-dev libxslt-dev libgd-dev libgeoip-dev
Download module and source code 

sudo mkdir -p /opt/develop
cd /opt/develop
sudo git clone https://github.com/kohlenf/cff_module.git
sudo wget http://nginx.org/download/nginx-1.14.2.tar.gz
sudo tar -xf nginx-1.14.2.tar.gz
cd /opt/develop/nginx-1.14.2
sudo ./configure --prefix=/etc/nginx --add-dynamic-module=/opt/develop/cff_module --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --with-cc-opt='-g -O2 -fdebug-prefix-map=/build/nginx-GkiujU/nginx-1.14.2=. -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_geoip_module=dynamic --with-http_gunzip_module --with-http_gzip_static_module --with-http_image_filter_module=dynamic --with-http_sub_module --with-http_xslt_module=dynamic --with-stream=dynamic --with-stream_ssl_module --with-mail=dynamic --with-mail_ssl_module --with-http_secure_link_module
sudo make
sudo make install
#If nginx installed , replace bin file from build
sudo cp /opt/develop/nginx-14.1.2/objs/nginx /usr/sbin/nginx
echo "load_module /usr/lib/nginx/modules/ngx_http_cookie_flag_filter_module.so;" >> /etc/nginx/nginx.conf
And than true add set_cookie_flag to site-enables config file

set_cookie_flag HttpOnly secure SameSite=None;

NOTE:

Also you can check nginx arguments with nginx -V

for example with nginx installed from repo

CONFARGS=$(nginx -V 2>&1 | sed -n -e 's/^.*arguments: //p')
echo $CONFARGS
