# NDCODFWEB 開發環境建立
20200716

### 一、在Windows上使用VirtualBox安裝CentOS 7，並更新所有的套件、關掉selinux、防火牆。

1. 至[國發會](https://www.ndc.gov.tw/cp.aspx?n=32A75A78342B669D&s=68798FA6FAE753EC)→首頁→主要業務數位發展規劃基礎服務開放文件格式(Open Document Format, ODF)→支援ODF文件格式軟體工具，參考並下載「[ODFWEB伺服器佈署說明書-1.6.pdf](https://ws.ndc.gov.tw/Download.ashx?u=LzAwMS9hZG1pbmlzdHJhdG9yLzEwL3JlbGZpbGUvNTU2Ni85MzAwL2Y5NTAzOWY1LTU5MjMtNDY1ZS1hZDc2LTI5YWQ1ZWFkM2RlYS5wZGY%3d&n=T0RGV0VC5Ly65pyN5Zmo5L2I572y6Kqq5piO5pu4LTEuNi5wZGY%3d&icon=..pdf)」
2. CentOS 7安裝完畢，開啟終端機執行`sudo yum update -y`更新所有套件。
3. 執行`systemctl disable firewalld.service`關閉防火牆。
4. 執行``` yum remove `rpm -qa|grep libreoffice` ```移除原LibreOffice。


### 二、關閉 selinux

```
yum install vim -y
yum install net-tools unzip -y
vim /etc/selinux/config 
```

### 三、下載 GitHub ndcodfweb 原始碼
```
git clone https://github.com/NDCODF/ndcodfweb.git

```

### 四、安裝 nvm

1. 使用 curl 或 wget 安裝 nvm
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
or

```
wget -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

2. 刪除在 home 目錄下產生的 install.sh
```
rm install.sh
```

### 五、安裝 nodejs
```
nvm install v10
nvm use v10
```

### 六、安裝編譯套件
```
yum install libtool libpng-devel libcap-devel cppunit-devel -y
```


### 七、手動編譯 Poco library

```
wget http://pocoproject.org/releases/poco-1.9.0/poco-1.9.0-all.tar.gz
tar zxvf poco-1.9.0-all.tar.gz
yum install openssl-devel -y
cd poco-1.9.0-all/
yum install gcc-c++ -y
./configure --prefix=/opt/poco
sudo make -j4
sudo make install
```


### 八、安裝 ndcodfsys http://free.nchc.org.tw/ndc.odf/NDCODFWEB-V1.4.zip
```
unzip NDCODFWEB-V1.4.zip
cd NDCODFWEB-V1.4/ndcodfsys
yum localinstall gumbo* -y
yum localinstall ndcodfsys* -y
```


### 九、執行 autogen

```
cd ndcodfweb
./autogen.sh
```


### 十、編譯前端 loleaflet
```
cd ndcodfweb/loleaflet
npm install -g jake
make
```


### 十一、安裝pip2
```
sudo easy_install pip
pip2 install --user polib
```


### 十二、編譯 ndcodfweb
```
cd ndcodfweb
./configure --enable-silent-rules --with-lokit-path=./bundled/include --with-lo-path=/opt/ndcodfsys --enable-debug --disable-werror --disable-ssl --with-poco-includes=/opt/poco/include --with-poco-libs=/opt/poco/lib
make
mkdir /etc/loolwsd
make run
```
