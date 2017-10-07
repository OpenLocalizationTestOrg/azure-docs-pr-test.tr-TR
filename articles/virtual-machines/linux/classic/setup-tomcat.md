---
title: "bir Linux sanal makine üzerinde Apache Tomcat yukarı aaaSet | Microsoft Docs"
description: "Bilgi nasıl Linux çalıştıran Azure sanal makineler kullanarak tooset Apache tomcat7'yi ayarlama."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Azure ile Linux sanal makine tomcat7'yi ayarlayın
Apache Tomcat (veya yalnızca Cakarta Tomcat adıysa ayrıca Tomcat) bir açık kaynak web sunucusu ve hello Apache yazılım Foundation (ASF) tarafından geliştirilmiş servlet kapsayıcı değil. Tomcat hello Java Servlet ve Sun Microsystems hello JavaServer sayfaları (JSP) belirtimlerine uygular. Tomcat hangi toorun Java kod içinde saf Java HTTP web sunucusu ortamı sağlar. Merhaba basit yapılandırmada, Tomcat tek işletim sistemi işleminde çalışır. Bu işlem, Java sanal makinesi (JVM) çalışır. Her bir tarayıcı tooTomcat HTTP isteğinden hello Tomcat işleminde ayrı bir iş parçacığı olarak işlenir.  

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, nasıl toouse hello Klasik dağıtım modeli yer almaktadır. En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz. toouse bir Resource Manager şablonu toodeploy bir Ubuntu VM açık JDK ve Tomcat, bkz: [bu makalede](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

Bu makalede, Linux görüntüde tomcat7'yi yükleyin ve Azure'da dağıtın.  

Şunları öğreneceksiniz:  

* Nasıl toocreate azure'da bir sanal makine.
* Nasıl tooprepare hello sanal makine için tomcat7'yi.
* Nasıl tooinstall tomcat7'yi.

Bir Azure aboneliği zaten sahip olduğunuz varsayılır.  Ücretsiz deneme için kaydolabilirsiniz değil, varsa [Azure Web sitesi hello](https://azure.microsoft.com/). Bir MSDN aboneliğiniz varsa, bkz: [Microsoft Azure özel fiyatlandırma: MSDN, MPN ve BizSpark avantajları](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). Azure, hakkında daha fazla toolearn bkz [Azure nedir?](https://azure.microsoft.com/overview/what-is-azure/).

Bu makalede, Tomcat ve Linux temel bilgiye sahip olduğunuz varsayılmaktadır.  

## <a name="phase-1-create-an-image"></a>1. Aşama: görüntü oluşturma
Bu aşamada, Azure'da bir Linux görüntüsü kullanarak bir sanal makine oluşturur.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>1. adım: bir SSH kimlik doğrulama anahtarı oluştur
SSH, sistem yöneticileri için önemli bir araçtır. Ancak, insan tarafından belirlenen bir parola tabanlı erişim güvenlik yapılandırma önerilmez. Kötü niyetli kullanıcılar, bir kullanıcı adı ve zayıf bir parolaya göre sisteminizi içine bozulabilir.

Merhaba iyi haber tooleave uzaktan erişim açın ve parolalar hakkında endişelenmeniz olmayan bir yolu yoktur. Bu yöntem, asimetrik şifreleme ile kimlik doğrulaması oluşur. Merhaba kullanıcının özel hello hello kimlik doğrulaması veren bir anahtardır. Merhaba kullanıcının hesabı bile kilitleyebilirsiniz toonot izin parola kimlik doğrulaması.

Bu yöntemin başka bir avantajı, farklı parolalar toosign toodifferent sunucularında gerekmez ' dir. Merhaba kişisel özel anahtarı tüm sunucularda, tooremember birkaç parolaların önleyen kullanılarak doğrulanabilir.



Bu adımları toogenerate hello SSH kimlik doğrulama anahtarı izleyin.

1. PuTTYgen konumu aşağıdaki hello yükleyip: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Puttygen.exe çalıştırın.
3. Tıklatın **Generate** toogenerate hello anahtarları. Merhaba işleminde hello penceresinde hello boş alanı üzerinden taşıma hello fareyle rastgele artırabilir.  
   ![Yeni anahtar düğmesi hello gösteren puTTY anahtar Oluşturucu ekran görüntüsü oluştur][1]
4. İşlem Hello oluşturduktan sonra yeni bir ortak anahtar Puttygen.exe gösterir.  
   ![Merhaba yeni ortak anahtar ve özel anahtar düğmesi kaydetme hello gösteren puTTY anahtar Oluşturucu ekran görüntüsü][2]
5. Seçin ve hello ortak anahtarı kopyalayın ve publicKey.pem adlı bir dosyaya kaydedin. Tıklamayın **ortak anahtarı Kaydet**, ortak anahtarın dosya biçimi kaydedilmiş hello istiyoruz hello ortak anahtarından farklı olduğu için.
6. Tıklatın **özel anahtarı Kaydet**ve privateKey.ppk adlı bir dosyaya kaydedin.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>2. adım: hello Azure portal hello görüntü oluşturma
1. Merhaba, [portal](https://portal.azure.com/), tıklatın **yeni** hello toocreate görüntüyü görev. Ardından gereksinimlerinize göre hello Linux görüntü seçin. Merhaba aşağıdaki örnek hello Ubuntu 14.04 görüntüyü kullanır.
![Merhaba portalının hello yeni düğmesini gösteren ekran görüntüsü][3]

2. İçin **ana bilgisayar adı**, tooaccess ve Internet istemcileri bu sanal makine kullanır hello URL için hello adı belirtin. Merhaba DNS adı, örneğin, tomcatdemo son parçası Hello tanımlayın. Azure, ardından tomcatdemo.cloudapp.net hello URL oluşturur.  

3. İçin **SSH kimlik doğrulama anahtarı**, PuTTYgen tarafından oluşturulan hello ortak anahtarı içeren hello publicKey.pem dosyasından hello anahtar değerini kopyalayın.  
![SSH kimlik doğrulama anahtarı hello Portalı'nda kutusu][4]

4. Diğer ayarları gerektiği gibi yapılandırın ve ardından **oluşturma**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>2. Aşama: sanal makineniz tomcat7'yi için hazırlayın.
Bu aşamada, Tomcat trafiği için bir uç nokta yapılandırmak ve tooyour yeni bir sanal makine bağlayın.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>1. adım: hello HTTP bağlantı noktası tooallow web erişimi'ni açın
Azure uç noktaları ile birlikte bir ortak ve özel bağlantı noktası TCP veya UDP protokolünü oluşur. Merhaba özel bağlantı noktası hello hizmetinin tooon hello sanal makine dinlediğini hello bağlantı noktasıdır. tooexternally gelen, Internet tabanlı trafiği için Azure bulut hizmeti hello hello bağlantı noktasını dinler Hello genel bağlantı noktasıdır.  

TCP bağlantı noktası 8080 Tomcat toolisten kullandığını hello varsayılan bağlantı noktası numarasıdır. Bu bağlantı noktası ile Azure bir uç nokta açıldıysa, sizin ve diğer Internet istemcileri Tomcat sayfalarına erişebilirsiniz.  

1. Hello Portalı'nda tıklatın **Gözat** > **sanal makineler**ve ardından oluşturduğunuz hello sanal makineyi'ı tıklatın.  
   ![Merhaba sanal makineleri dizininin ekran görüntüsü][5]
2. tooadd bir uç nokta tooyour sanal makine tıklatın hello **uç noktaları** kutusu.
   ![Merhaba uç noktaları kutusunu gösteren ekran görüntüsü][6]
3. **Ekle**'ye tıklayın.  

   1. Merhaba uç noktası için bir hello uç adı **Endpoint**ve 80 enter **genel bağlantı noktası**.  

      Too80 ayarlarsanız tooinclude hello bağlantı noktası numarası kullanılan tooaccess Tomcat hello URL gerekmez. Örneğin, http://tomcatdemo.cloudapp.net.    

      81 gibi tooanother değerini ayarlarsanız tooadd hello bağlantı noktası numarası toohello URL tooaccess Tomcat gerekir. Örneğin, http://tomcatdemo.cloudapp.net:81 /.
   2. İçinde 8080 girin **özel bağlantı noktası**. Varsayılan olarak, TCP bağlantı noktası 8080 Tomcat dinler. Merhaba varsayılan dinleme Tomcat bağlantı noktasını değiştirdiyseniz, güncelleştirmelidir **özel bağlantı noktası** toobe hello Tomcat dinleme bağlantı noktası hello aynı.  
      ![Ekran görüntüsü, Ekle komutu, genel bağlantı noktası ve özel bağlantı noktası gösteren kullanıcı Arabirimi][7]
4. Tıklatın **Tamam** tooadd hello uç nokta tooyour sanal makine.

### <a name="step-2-connect-toohello-image-you-created"></a>2. adım: oluşturduğunuz toohello görüntü Bağlan
SSH aracı tooconnect tooyour sanal makine seçebilirsiniz. Bu örnekte, PuTTY kullanın.  

1. Sanal makinenizin Hello DNS adı hello portaldan alın.
    1. Tıklatın **Gözat** > **sanal makineleri**.
    2. Merhaba, sanal makinenin adını seçin ve ardından **özellikleri**.
    3. Merhaba, **özellikleri** döşeme, hello bakın **etki alanı adı** kutusunu tooget hello DNS adı.  

2. Merhaba SSH bağlantılarında Hello bağlantı noktası numarası alma **SSH** kutusu.  
![Merhaba SSH bağlantı noktası gösteren ekran görüntüsü][8]

3. Karşıdan [PuTTY](http://www.putty.org/).  

4. İndirdikten sonra hello yürütülebilir dosya Putty.exe'ı tıklatın. PuTTY yapılandırması hello ana bilgisayar adıyla hello temel seçeneklerini yapılandırmak ve bağlantı noktası, sanal makinenize hello özelliklerinden elde sayısını.   
![Merhaba PuTTY yapılandırması ana bilgisayar adı ve bağlantı noktası seçeneklerini gösteren ekran görüntüsü][9]

5. Merhaba sol bölmede **bağlantı** > **SSH** > **Auth**ve ardından **Gözat** toospecify Merhaba privateKey.ppk dosyasının başlangıç konumu. Hello privateKey.ppk dosyasını önceki hello PuTTYgen tarafından oluşturulan hello özel anahtarı içeren "1. Aşama: görüntü oluşturma" bölümünde bu makalenin.  
![Merhaba bağlantı dizin hiyerarşisi ve Gözat düğmesini gösteren ekran görüntüsü][10]

6. Tıklatın **açık**. Bir ileti kutusu tarafından uyarı. Yapılandırılan hello DNS adı ve bağlantı noktası numarası doğru değilse, tıklatın **Evet**.
![Merhaba bildirim gösteren ekran görüntüsü][11]

7. Kullanıcı adınızı istendiğinde tooenter şunlardır.  
![Where gösteren ekran görüntüsü tooenter kullanıcı adı][12]

8. Hello toocreate hello sanal makine kullanılan hello kullanıcı adı girin "1. Aşama: görüntü oluşturma" bölümünde bu makalenin. Merhaba aşağıdaki gibi bir şey görürsünüz:  
![Merhaba kimlik doğrulama onay gösteren ekran görüntüsü][13]

## <a name="phase-3-install-software"></a>3. Aşama: Yazılımı yükleme
Bu aşamada hello Java Çalışma zamanı ortamı, tomcat7'yi ve diğer tomcat7'yi bileşenlerini yükler.  

### <a name="java-runtime-environment"></a>Java Çalışma zamanı ortamı
Tomcat Java'da yazılmış olmalıdır. Java geliştirme setleri (JDKs), OpenJDK ve Oracle JDK iki tür vardır. Merhaba istediğinizi seçebilirsiniz.  

> [!NOTE]
> Hem JDKs neredeyse aynı hello sınıflarda hello Java API için kod hello sahip, ancak hello kod hello sanal makine için farklıdır. OpenJDK toouse açık kitaplıkları eğilimlidir, Oracle JDK eğilimlidir sırada toouse olanları kapalı. Oracle JDK sahip daha sınıfları ve bazı düzeltilen hatalar ve Oracle JDK OpenJDK daha fazla kararlı.

#### <a name="install-openjdk"></a>OpenJDK yükleyin  

Aşağıdaki komut toodownload OpenJDK hello kullanın.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate dizin toocontain JDK dosyaları hello:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK dosyalarıyla hello/usr/lib/jvm/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Oracle JDK yükleyin


Komut toodownload Oracle JDK hello Oracle Web sitesinden aşağıdaki hello kullanın.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate dizin toocontain JDK dosyaları hello:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK dosyalarıyla hello/usr/lib/jvm/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* Oracle varsayılan Java sanal makinesi hello gibi JDK tooset:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Java yüklemenin başarılı olduğunu onaylayın
Merhaba Java Çalışma zamanı ortamı düzgün yüklenmediyse tootest aşağıdaki hello gibi bir komutu kullanabilirsiniz:  

    java -version  

OpenJDK yüklediyseniz, hello aşağıdaki gibi bir ileti görürsünüz: ![başarılı OpenJDK yükleme iletisi][14]

Oracle JDK yüklediyseniz, hello aşağıdaki gibi bir ileti görürsünüz: ![başarılı Oracle JDK yükleme iletisi][15]

### <a name="install-tomcat7"></a>Tomcat7'yi yükleme
Komut tooinstall tomcat7'yi aşağıdaki hello kullanın.  

    sudo apt-get install tomcat7  

Tomcat7'yi kullanmıyorsanız, bu komutun uygun varyasyonunu hello kullanın.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Tomcat7'yi yükleme işleminin başarılı olduğunu doğrulayın
toocheck tomcat7'yi başarıyla yüklediyseniz, tooyour Tomcat sunucusunun DNS adı gözatın. Bu makalede, http://tomcatexample.cloudapp.net/ hello örnek URL'dir. Merhaba aşağıdaki gibi bir ileti görürseniz, tomcat7'yi doğru bir şekilde yüklendi.
![Başarılı tomcat7'yi yükleme iletisi][16]

### <a name="install-other-tomcat7-components"></a>Diğer tomcat7'yi bileşenlerini yükle
Yükleyebileceğiniz isteğe bağlı diğer Tomcat bileşenleri vardır.  

Kullanım hello **sudo önbellek apt arama tomcat7'yi** komutu toosee hello kullanılabilir bileşenlerinin tümünü. Aşağıdaki komutları tooinstall hello bazı yararlı bileşenlerini kullanın.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>4. Aşama: Tomcat7'yi yapılandırma
Bu aşamada, Tomcat yönetin.

### <a name="start-and-stop-tomcat7"></a>Tomcat7'yi durdurup başlatın
Merhaba tomcat7'yi sunucusu yüklediğinizde otomatik olarak başlatır. Bu komutu aşağıdaki hello ile de başlatabilirsiniz:   

    sudo /etc/init.d/tomcat7 start

toostop tomcat7'yi:

    sudo /etc/init.d/tomcat7 stop

tomcat7'yi tooview hello durumu:

    sudo /etc/init.d/tomcat7 status

toorestart Tomcat Hizmetleri: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Tomcat7'yi Yönetim
Yönetici kimlik bilgilerinizi hello Tomcat kullanıcı yapılandırma dosyası tooset düzenleyebilirsiniz. Merhaba aşağıdaki komutu kullanın:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Örnek aşağıda verilmiştir:  
![Merhaba sudo VI komut çıktısı gösteren ekran görüntüsü][17]  

> [!NOTE]
> Merhaba yönetici kullanıcı adı için güçlü bir parola oluşturun.  

Bu dosyasını düzenledikten sonra tomcat7'yi Hizmetleri hello değişiklikler etkili komutu tooensure aşağıdaki hello ile yeniden başlatmanız:  

    sudo /etc/init.d/tomcat7 restart  

Tarayıcınızı açın ve girin **http://<your tomcat server DNS name>/Yöneticisi/html** URL hello gibi. Bu makalede Hello örneğin hello http://tomcatexample.cloudapp.net/manager/html URL'dir.  

Bağlandıktan sonra benzeri toohello aşağıdaki görmeniz gerekir:  
![Merhaba Tomcat Web Uygulama Yöneticisi ekran görüntüsü][18]

## <a name="common-issues"></a>Genel sorunlar
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Merhaba sanal makineyle Tomcat ve Moodle Internet hello erişemiyor
#### <a name="symptom"></a>Belirti  
  Tomcat çalışıyor ancak tarayıcınızla hello Tomcat varsayılan sayfa göremez.
#### <a name="possible-root-cause"></a>Olası temel nedeni   

  * Merhaba Tomcat dinleme bağlantı noktası olan değil hello hello sanal makinenizin uç noktasının Tomcat trafiği için özel bağlantı noktası ile aynı.  

     Genel bağlantı noktası ve özel bağlantı noktası bitiş noktası ayarları ve hello özel bağlantı noktası aynı Tomcat hello hello olduğundan emin olun onay bağlantı noktasını dinler. Bkz: "1. Aşama: görüntü oluşturma" uç noktaları, sanal makine için yapılandırma hakkında yönergeler için bu makalenin.  

     toodetermine hello Tomcat dinleme bağlantı noktası, /etc/httpd/conf/httpd.conf (Red Hat sürüm) veya /etc/tomcat7/server.xml (Debian sürüm) açın. Varsayılan olarak, hello Tomcat dinleme bağlantı noktası 8080'dir. Örnek aşağıda verilmiştir:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Toochange hello varsayılan bağlantı noktası, Tomcat dinleme (örneğin 8081) Debian ve Ubuntu ve istediğiniz gibi bir sanal makine kullanıyorsanız, hello işletim sistemi için başlangıç bağlantı noktası açmanız gerekir. İlk olarak, hello profil açın:  

        sudo vi /etc/default/tomcat7  

     Ardından hello son satırı açıklamadan çıkarın ve "Hayır" çok "Evet" değiştirin.  

        AUTHBIND=yes
  2. Merhaba dinleme bağlantı noktası, Tomcat Hello Güvenlik Duvarı'nı devre dışı.

     Yalnızca hello Tomcat varsayılan hello yerel ana sayfasından da görebilirsiniz. Merhaba sorunudur büyük olasılıkla kulak tooby Tomcat olan, başlangıç bağlantı noktası hello güvenlik duvarı tarafından engellenir. Merhaba w3m aracı toobrowse hello Web sayfasını kullanabilirsiniz. Merhaba aşağıdaki komutları w3m yükleyin ve toohello Tomcat varsayılan sayfasına göz atın:  


        sudo yum yükleme w3m w3m-img


        w3m http://localhost: 8080  
#### <a name="solution"></a>Çözüm

  * Merhaba Tomcat dinleme bağlantı noktası hello değil, aynı hello hello uç noktasının trafiği toohello sanal makine için özel bağlantı noktası olarak hello özel bağlantı noktası değiştirmek toobe hello Tomcat dinleme bağlantı noktası hello aynı.   
  2. Güvenlik Duvarı/iptables tarafından Hello sorunu neden olursa, aşağıdaki satırları çok/etc/sysconfig/iptables hello ekleyin. Merhaba ikinci satır yalnızca https trafiği için gereklidir:  

      -A -p tcp -m tcp--dport 80 -j kabul giriş

      -A -p tcp -m tcp--dport 443 -j kabul giriş  

     > [!IMPORTANT]
     > Merhaba önceki satırları hello aşağıdaki gibi erişim genel kısıtlar satırları yukarıda konumlandırıldığı emin olun: - bir giriş -j--Reddet-with ICMP konak yasaklanmış REDDET



tooreload hello iptables, hello aşağıdaki komutu çalıştırın:

    service iptables restart

Bu CentOS 6.3 test edilmiştir.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Proje yüklediğinizde reddedildi dosyaları çok/var/lib/tomcat7'yi / webapps /
#### <a name="symptom"></a>Belirti
  Ne zaman bir SFTP (örneğin, FileZilla) istemci tooconnect tooyour sanal makine kullanmanız ve çok/var/lib/tomcat7'yi / webapps gidin/toopublish, sitenizi bir hata iletisi benzer toohello aşağıdaki alın:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Olası temel nedeni
  Hiçbir izinleri tooaccess hello /var/lib/tomcat7/webapps klasör sahip.  
#### <a name="solution"></a>Çözüm  
  Merhaba kök hesap tooget izni gerekir. Bu klasör hello sahipliğini hello makine sağladığında, kullanılan kök toohello kullanıcı adından değiştirebilirsiniz. Merhaba azureuser hesap adı ile örnek aşağıda verilmiştir:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Merhaba -R seçeneği tooapply hello izinleri çok bir dizin içinde tüm dosyalar için kullanın.  

  Bu komut, dizinler için de çalışır. Merhaba -R seçeneği değişiklikleri tüm dosyaları ve dizinleri hello dizin içinde izinlerini hello. Örnek aşağıda verilmiştir:  

     sudo chown -R username:group directory  

  Bu komut, tüm dosyaları ve hello dizini içinde olan dizinleri (kullanıcı ve grup) sahipliği değiştirir.  

  Merhaba aşağıdaki komut yalnızca hello izni hello klasörü dizininin değiştirir. Merhaba dosya ve klasörleri hello dizin içinde değiştirilmez.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
