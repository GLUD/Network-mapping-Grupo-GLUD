# Pentesting-Red-Grupo-GLUD

ESTE TUTORIAL ESTA HECHO CON FINES EDUCATIVOS Y DE ENSEÑANZA. EL USO NO ADECUADO DEL MATERIAL ES BAJO SU RESPONSABILIDAD.
https://glud.org/2017/03/03/pentesting-red-grupo-glud/

# Recursos

- https://nmap.org/
- https://www.kali.org/penetration-testing/openvas-vulnerability-scanning/

Hay que instalar OpenVAS en la distro a utilizar ya que no se encuentra en las herramientas de Kali Linux.

# Instalación
## Instalar dependencias

```bash
sudo apt-get install build-essential bison flex cmake pkg-config  libglib2.0-dev libgnutls-dev  libpcap0.8-dev libgpgme11 libgpgme11-dev doxygen libuuid1 uuid-dev sqlfairy xmltoman sqlite3 libxml2-dev libxslt1.1 libxslt1-dev xsltproc libmicrohttpd-dev libsqlite3-dev
```

## Descargar y descomprimir OpenVAS

```bash
mkdir openvas
cd openvas/
wget http://wald.intevation.org/frs/download.php/1638/openvas-libraries-7.0.1.tar.gz
wget http://wald.intevation.org/frs/download.php/1640/openvas-scanner-4.0.1.tar.gz
wget http://wald.intevation.org/frs/download.php/1637/openvas-manager-5.0.0.tar.gz
wget http://wald.intevation.org/frs/download.php/1639/greenbone-security-assistant-5.0.0.tar.gz
wget http://wald.intevation.org/frs/download.php/1633/openvas-cli-1.3.0.tar.gz
tar xvfz  openvas-libraries-7.0.1.tar.gz
tar xvfz  openvas-scanner-4.0.1.tar.gz
tar xvfz  openvas-manager-5.0.0.tar.gz
tar xvfz  openvas-cli-1.3.0.tar.gz
```

## Compilar e instalar OpenVAS

```bash
cd openvas-libraries-7.0.1/
mkdir source
cd source
cmake ..
make
make install
cd openvas-scanner-4.0.1/
mkdir source
cd source
cmake ..
make
make install
cd openvas-manager-5.0.0/
mkdir source
cd source
cmake ..
make
make install
cd openvas-cli-1.3.0/
mkdir source
cd source
cmake ..
make
make install
cd greenbone-security-assistant-5.0.0/
mkdir source
cd source
cmake ..
make
make install
```

## Creación de certificado e inicio de servicio

```bash
openvas-mkcert
ldconfig
openvassd
```

## Tendremos que verificar que el servicio aya iniciado con

```bash
ps -ef | grep openvas
```

## Descarga de Firmas de Vulnerabilidades

```bash
openvas-nvt-sync
openvas-scapdata-sync
openvas-certdata-sync
```

## Recargar procesos y finalizar configuración.

```bash
openvas-mkcert-client -n -i
openvasmd –rebuild –progress
openvasmd
gsad
```

## Crear el usuario de administración.

```bash
openvasad -c add_user -u your_new_login_here -r Admin
```

Ingresaremos con el usuario “admin” y la contraseña generada en el paso anterior.
