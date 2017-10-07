---
title: "Apache Phoenix aaaUse ve Windows tabanlı Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Bilgi nasıl toouse, hdınsight'ta Apache Phoenix ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Hdınsight'ta Windows tabanlı HBase kümeleriyle Apache ve SQuirreL kullanma
Bilgi nasıl toouse [Apache Phoenix](http://phoenix.apache.org/) , hdınsight'ta ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın. Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Hello Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Hello hdınsight'ta Phoenix sürüm bilgileri için bkz: [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Bu belge yalnızca iş için Windows tabanlı Hdınsight kümeleri Hello adımları. Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Phoenix Linux tabanlı Hdınsight kullanma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı HBase ile kullanım Apache Phoenix kümeleri](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>SQLLine kullanın
[SQLLine](http://sqlline.sourceforge.net/) bir komut satırı yardımcı programı tooexecute SQL değil.

### <a name="prerequisites"></a>Ön koşullar
SQLLine kullanmadan önce hello şunlara sahip olmanız gerekir:

* **Hdınsight'ta HBase kümesi**. Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].
* **Toohello HBase kümesi hello Uzak Masaüstü Protokolü aracılığıyla bağlanma**. Yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri hello Klasik Azure portalı kullanarak][hdinsight-manage-portal].

**toofind hello ana bilgisayar adı çıkışı**

1. Açık **Hadoop komut satırı** hello masaüstünden.
2. Komut tooget hello DNS soneki aşağıdaki hello çalıştırın:

        ipconfig

    Yazma **bağlantıya özgü DNS soneki**. Örneğin, *myhbasecluster.f5.internal.cloudapp.net*. Tooan HBase kümesi bağlandığınızda, FQDN kullanarak hello Zookeepers, tooconnect tooone gerekir. Her Hdınsight kümesi 3 Zookeepers sahiptir. Bunlar *zookeeper0*, *zookeeper1*, ve *zookeeper2*. Merhaba FQDN şöyle olacaktır *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Açık **Hadoop komut satırı** hello masaüstünden.
2. Aşağıdaki komutları tooopen SQLLine hello çalıştırın:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![Hdınsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    Merhaba örnekte kullanılan hello komutlar:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>SQuirreL kullanma
[SQL istemci sQuirreL](http://squirrel-sql.sourceforge.net/) tooview hello yapısı JDBC uyumlu bir veritabanına izin, tablolardaki hello verileri göz atın, sorunu SQL komutlarını vb. grafik bir Java programdır. Kullanılan tooconnect tooApache hdınsight'ta Phoenix olabilir.

Bu bölümde, nasıl gösterilir tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta VPN aracılığıyla yapılandırın.

### <a name="prerequisites"></a>Ön koşullar
Merhaba yordamları izlemeden önce hello şunlara sahip olmanız gerekir:

* Bir HBase kümesi tooan bir DNS sanal makineye sahip Azure sanal ağı dağıtıldı.  Yönergeler için bkz: [oluşturma HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet].

* Merhaba HBase kümesi küme bağlantıya özgü DNS soneki alın. tooget, hello küme halinde RDP ve ipconfig komutunu çalıştırmak.  Merhaba DNS soneki benzer:

        myhbase.b7.internal.cloudapp.net
* İndirme ve yükleme [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) istasyonunuzda. Sertifikanızı hello paket toocreate gelen makecert gerekir.  
* İndirme ve yükleme [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) istasyonunuzda.  SQL istemci sürüm 3.0 ve daha yüksek sQuirreL JRE 1.6 veya sonraki sürümünü gerektirir.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Bir noktadan siteye VPN bağlantısı toohello Azure sanal ağı yapılandırma
Bir noktadan siteye VPN bağlantısı yapılandırma söz konusu 3 adım vardır:

1. [Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Sertifikalarınızı oluşturma](#Create-your-certificates)
3. [VPN istemcinizi yapılandırma](#Configure-your-VPN-client)

Bkz: [bir noktadan siteye VPN bağlantısı tooan Azure Virtual Network yapılandırma](../vpn-gateway/vpn-gateway-point-to-site-create.md) daha fazla bilgi için.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Bir sanal ağ ve dinamik yönlendirme ağ geçidi yapılandırma
Bir Azure sanal ağındaki bir HBase kümesi sağlanan güvence altına almak (Bu bölümün hello önkoşullara bakın). Merhaba sonraki tooconfigure bir noktadan siteye bağlantı adımdır.

**tooconfigure hello noktadan siteye bağlantı**

1. İçinde toohello oturum [Klasik Azure portalı][azure-portal].
2. Hello solda tıklatın **ağlar**.
3. Oluşturduğunuz hello sanal ağa tıklayın (bkz [sağlama HBase kümeleri Azure sanal ağı][hdinsight-hbase-provision-vnet]).
4. Tıklatın **yapılandırma** hello üstten.
5. Merhaba, **noktadan siteye bağlantı** bölümünde, select **noktadan siteye bağlantı yapılandırma**.
6. Yapılandırma **başlangıç IP** ve **CIDR** bağlıyken toospecify hello IP adresi aralığı, VPN istemcilerinizin alır bir IP adresi. Merhaba aralığı aralıklar, şirket içi üzerinde bulunan Ağ ve Azure sanal ağı için bağlanırsınız hello hello biriyle çakışamaz. Örneğin. Merhaba sanal ağ için 10.0.0.0/20 seçtiyseniz 10.1.0.0/24 hello istemci adres alanı için seçebilirsiniz. Merhaba bkz [noktadan siteye bağlantı] [ vnet-point-to-site-connectivity] daha fazla bilgi için.
7. Merhaba sanal ağ adres alanları bölümünde tıklayın **ağ geçidi alt ağı eklemek**.
8. Tıklatın **KAYDETMEK** hello sayfanın hello üzerinde.
9. Tıklatın **Evet** tooconfirm hello değiştirin. Merhaba sistem hello toohello sonraki yordama devam etmeden önce değiştirme yapmadan tamamlanana kadar bekleyin.

**toocreate dinamik yönlendirme ağ geçidi**

1. Merhaba Klasik Azure Portalı ' tıklatın **PANO** hello sayfasının hello üstten.
2. Tıklatın **ağ geçidi Oluştur** hello sayfasının hello Alttan.
3. Tıklatın **Evet** tooconfirm. Merhaba ağ geçidi oluşturulana kadar bekleyin.
4. Tıklatın **PANO** hello üstten.  Merhaba sanal ağ visual diyagramı görürsünüz:

    ![Azure sanal ağı noktadan siteye sanal diyagramı][img-vnet-diagram]

    Merhaba diyagramı 0 istemci bağlantılarını gösterir. Bir bağlantı toohello sanal ağ yaptıktan sonra hello numarası güncelleştirilmiş tooone olacaktır.

#### <a name="create-your-certificates"></a>Sertifikalarınızı oluşturma
Bir X.509 sertifikası olan kullanarak tek yönlü toocreate hello ile birlikte sertifika oluşturma Aracı (makecert.exe) [Microsoft Visual Studio Express için Windows Masaüstü](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate otomatik olarak imzalanan sertifika**

1. İstasyonunuzdan, bir komut istemi penceresi açın.
2. Toohello Visual Studio Araçları klasörüne gidin.
3. Aşağıdaki hello örnek komutta aşağıdaki hello oluşturur ve istasyonunuzda hello kişisel sertifika deposunda kök sertifikasını yükleyin ve ayrıca toohello Klasik Azure portalı daha sonra yükleyeceğiniz karşılık gelen bir .cer dosyası oluşturun.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Bulunan, HBaseVnetVPNRootCertificate toouse hello sertifika için istediğiniz hello adı olduğu .cer dosyasını toobe hello istediğiniz toohello dizini değiştirin.

    Merhaba komut istemi kapatmayın.  Merhaba sonraki yordamda gerekir.

   > [!NOTE]
   > İstemci sertifikaları oluşturulacak bir kök sertifikası oluşturduğunuzdan, bu sertifikayı ve özel anahtarını tooexport istediğiniz ve burada kurtarılabilir tooa güvenli konuma kaydedin.
   >
   >

**toocreate bir istemci sertifikası**

* Hello aynı komut istemi (Merhaba üzerinde toobe sahip hello kök sertifikanın oluşturulduğu aynı bilgisayar. Merhaba istemci sertifikası oluşturulmalıdır hello kök sertifikasından), çalışma hello komutu aşağıdaki:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate hello kök sertifika adıdır.  Toomatch hello kök sertifika adı vardır.  

    Merhaba kök sertifikasını ve hello istemci sertifikası, bilgisayarınızdaki kişisel sertifika deposunda depolanır. Certmgr.msc tooverify kullanın.

    ![Azure sanal ağı noktadan siteye VPN sertifikası][img-certificate]

    Bir istemci sertifikası tooconnect toohello sanal ağ istediğiniz her bilgisayara yüklenmelidir. Benzersiz istemci sertifikaları tooconnect toohello sanal ağ istediğiniz her bilgisayar için oluşturmanızı öneririz. tooexport hello istemci sertifikaları, certmgr.msc kullanın.

**tooupload hello kök sertifika toohello Klasik Azure portalı**

1. Merhaba Klasik Azure Portalı ' tıklatın **ağ** hello soldaki.
2. HBase kümesi dağıtıldığı hello sanal ağ'ı tıklatın.
3. Tıklatın **SERTİFİKALARI** hello üstten.
4. Tıklatın **karşıya** hello gelen alt ve son önce hello yordamda oluşturduğunuz hello kök sertifika dosyasını belirtin. Merhaba sertifika içeri kadar bekleyin.
5. Tıklatın **PANO** hello üstte.  Merhaba sanal diyagramı hello durumunu gösterir.

#### <a name="configure-your-vpn-client"></a>VPN istemcinizi yapılandırma
**Merhaba istemci VPN paketini toodownload ve yükle**

1. Merhaba Hızlı Bakış bölümünde hello sanal ağın hello PANO sayfasından öğelerinden birini tıklatın **indirme hello 64-bit istemci VPN paketini** veya **indirme hello 32 bit istemci VPN paketini** göre İş istasyonu işletim sistemi sürümü.
2. Tıklatın **çalıştırmak** tooinstall hello paket.
3. Merhaba güvenlik isteminde tıklatın **daha fazla bilgi**ve ardından **yine de çalıştırmaya**.
4. Tıklatın **Evet** iki kez.

**tooconnect tooVPN**

1. İş istasyonunuzu Hello masaüstünde hello görev çubuğunda hello ağları simgesine tıklayın. Bir VPN bağlantısı, sanal ağ adıyla göreceksiniz.
2. Merhaba VPN bağlantısı adını tıklatın.
3. **Bağlan**'a tıklayın.

**tootest hello VPN bağlantısı ve etki alanı ad çözümlemesi**

* Merhaba iş istasyonundan, bir komut istemi açın ve hello hello HBase kümesi'nin DNS soneki verilen adlarından birini ping myhbase.b7.internal.cloudapp.net ise:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Yükleme ve SQuirreL iş istasyonunuza yapılandırma
**tooinstall SQuirreL**

1. Merhaba SQuirreL SQL istemci jar dosyasını indirin [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Açma/çalıştırma hello jar dosyasını. Merhaba gerektirir [Java Çalışma zamanı ortamı](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Tıklatın **sonraki** iki kez.
4. Yazma izni ve ardından hello sahip olduğu bir yol belirtin **sonraki**.

  > [!NOTE]
  > Merhaba C:\Program Files\squirrel-sql-3.6 klasöründe Hello varsayılan yükleme klasörüdür.  Sipariş toowrite toothis yolunda hello yükleyici hello Yöneticisi ayrıcalığı verilmelidir. Yönetici olarak bir komut istemi açın, tooJava'nın bin klasörüne gidin ve ardından çalıştırın:
  >
  >     Java.exe-jar [hello SQuirreL jar dosyasını hello yolu]
5. Tıklatın **Tamam** tooconfirm hello hedef dizin oluşturma.
6. Merhaba tooinstall hello temel ve standart paketleri varsayılandır.  **İleri**’ye tıklayın.
7. Tıklatın **sonraki** iki kez tıkladıktan sonra **Bitti**.

**tooinstall hello Phoenix sürücüsü**

Merhaba phoenix sürücü jar dosyasını hello HBase kümesi üzerinde bulunur. Merhaba yolu hello sürümlerine bağlı benzer toohello aşağıda verilmiştir:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Toocopy gerekir, tooyour iş istasyonu hello [SQuirreL yükleme klasörü] altında / lib yolu.  Merhaba kolay hello küme ve Kullan, dosyayı kopyalayıp yapıştırın (CTRL + C ve CTRL + V) toocopy tooRDP yoludur, tooyour iş istasyonu.

**Phoenix sürücü tooSQuirreL tooadd**

1. SQuirreL SQL istemci istasyonunuzdan açın.
2. Merhaba tıklatın **sürücü** hello sol sekmesinde.
3. Merhaba gelen **sürücüleri** menüsünde tıklatın **yeni sürücü**.
4. Aşağıdaki bilgilerle hello girin:

   * **Ad**: Phoenix
   * **Örnek URL**: jdbc:phoenix:zookeeper2.contoso hbase eu.f5.internal.cloudapp.net
   * **Sınıf adı**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Kullanıcı hello örnek URL tüm alt durumda. Kullanabileceğiniz bunlar tam zookeeper çekirdek bunlardan birini çalışmıyor durumda.  Merhaba konak zookeeper0, zookeeper1 ve zookeeper2 adları.
     >
     >

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-driver]
5. **Tamam** düğmesine tıklayın.

**toocreate bir diğer ad toohello HBase kümesi**

1. Merhaba SQuirreL tıklatın **diğer adlar** hello sol sekmesinde.
2. Merhaba gelen **diğer adlar** menüsünde tıklatın **yeni diğer**.
3. Aşağıdaki bilgilerle hello girin:

   * **Ad**: Merhaba HBase kümesi veya tercih ettiğiniz herhangi bir ad hello adı.
   * **Sürücü**: Phoenix.  Bu hello son yordamda oluşturduğunuz hello sürücü adı eşleşmelidir.
   * **URL**: hello URL sürücü yapılandırmasından kopyalanır. Tüm küçük toouser emin olun.
   * **Kullanıcı adı**: herhangi bir metin olabilir.  VPN bağlantısı burada kullandığından, hello kullanıcı adı hiç kullanılmaz.
   * **Parola**: herhangi bir metin olabilir.

     ![Hdınsight HBase Phoenix SQuirreL sürücüsü][img-squirrel-alias]
4. Tıklatın **Test**.
5. **Bağlan**'a tıklayın. Merhaba bağlantı yaptığında, SQuirreL şuna benzer:

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun test**

1. Merhaba tıklatın **SQL** sağ sonraki toohello sekmesinde **nesneleri** sekmesi.
2. Kopyalayın ve hello aşağıdaki kodu yapıştırın:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Merhaba çalıştırma düğmesine tıklayın.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Geçiş geri toohello **nesneleri** sekmesi.
5. Merhaba diğer adı'nı genişletin ve ardından genişletin **tablo**.  Merhaba yeni tablo altında listelenen görürsünüz.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl toouse hdınsight'ta Apache Phoenix.  toolearn daha bakın

* [HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.
* [Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar ile iletişim kurabilir Doğrudan HBase.
* [Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): öğrenin nasıl tooconfigure HBase çoğaltmayı iki Azure veri merkezleri arasında.
* [Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: öğrenin nasıl toodo gerçek zamanlı [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
