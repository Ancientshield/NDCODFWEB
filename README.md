# OxOffice 開發環境建立
20200716

### 一、在Windows上使用VirtualBox安裝CentOS 7，並更新所有的套件、關掉selinux、防火牆。

1. 至[國發會](https://www.ndc.gov.tw/cp.aspx?n=32A75A78342B669D&s=68798FA6FAE753EC)→首頁→主要業務數位發展規劃基礎服務開放文件格式(Open Document Format, ODF)→支援ODF文件格式軟體工具，參考並下載「[ODFWEB伺服器佈署說明書-1.6.pdf](https://ws.ndc.gov.tw/Download.ashx?u=LzAwMS9hZG1pbmlzdHJhdG9yLzEwL3JlbGZpbGUvNTU2Ni85MzAwL2Y5NTAzOWY1LTU5MjMtNDY1ZS1hZDc2LTI5YWQ1ZWFkM2RlYS5wZGY%3d&n=T0RGV0VC5Ly65pyN5Zmo5L2I572y6Kqq5piO5pu4LTEuNi5wZGY%3d&icon=..pdf)」
2. CentOS 7安裝完畢，開啟終端機執行`yum update -y`更新所有套件。
3. 執行``` systemctl disable firewalld.service` ```關閉防火牆。
4. 執行yum remove `rpm -qa|grep libreoffice`移除原LibreOffice。

### 二、至GutHub下載程式碼並編譯OxOffice所需的套件


安裝nvm
```
wget -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

安裝nodejs
```
nvm install v10
nvm use v10
```

手動編譯Poco library

```
wget http://pocoproject.org/releases/poco-1.9.0/poco-1.9.0-all.tar.gz
tar zxvf poco-1.9.0-all.tar.gz
yum install openssl-devel -y
cd poco-1.9.0-all/
yum install gcc-c++ -y
./configure --prefix=/opt/poco && make install
```

git clone oxool-community

```
git clone https://github.com/OSSII/oxool-community.git
cd oxool-community

```