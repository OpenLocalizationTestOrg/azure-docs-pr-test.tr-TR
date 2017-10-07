---
title: "aaaInstall Azure Windows VM üzerinde MongoDB | Microsoft Docs"
description: "Windows Server 2012 R2 çalıştıran bir Azure VM üzerinde MongoDB tooinstall hello Resource Manager dağıtım modeli ile nasıl oluşturulacağını öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Yükleme ve Azure Windows VM üzerinde MongoDB yapılandırma
[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır. Bu makalede yükleme ve bir Windows Server 2012 R2 sanal makinede (VM) Azure MongoDB yapılandırma sırasında size kılavuzluk eder. Ayrıca [MongoDB azure'da bir Linux VM yüklemek](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Ön koşullar
Yükleyip MongoDB yapılandırmadan önce toocreate VM gerekir ve, ideal olarak, bir veri diski tooit ekleyin. Aşağıdaki makaleleri toocreate VM hello görmek ve bir veri diski ekleyin:

* Kullanarak bir Windows Server VM oluşturma [Azure portal hello](quick-create-portal.md) veya [Azure PowerShell](quick-create-powershell.md).
* Bir veri diski tooa Windows Server VM kullanarak attach [Azure portal hello](attach-managed-disk-portal.md) veya [Azure PowerShell](attach-disk-ps.md).

Yükleme ve yapılandırma MongoDB, toobegin [tooyour Windows Server VM üzerinde oturum](connect-logon.md) Uzak Masaüstü kullanarak.

## <a name="install-mongodb"></a>MongoDB'yi yükleme
> [!IMPORTANT]
> Kimlik doğrulaması ve IP adresi bağlama gibi MongoDB güvenlik özellikleri varsayılan olarak etkin değildir. Güvenlik özellikleri, MongoDB tooa üretim ortamına dağıtmadan önce etkinleştirilmelidir. Daha fazla bilgi için bkz: [MongoDB güvenlik ve kimlik doğrulama](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Uzak Masaüstü kullanarak VM tooyour bağlandıktan sonra Internet Explorer hello açın **Başlat** hello VM menüsünde.
2. Seçin **kullanım önerilen güvenlik, gizlilik ve uyumluluk ayarları** zaman Internet Explorer ilk açar ve tıklatın **Tamam**.
3. Internet Explorer Artırılmış Güvenlik Yapılandırması, varsayılan olarak etkindir. Merhaba MongoDB Web sitesi toohello izin verilen siteler listesine ekleyin:
   
   * Select hello **Araçları** hello sağ üst köşesinde simgesi.
   * İçinde **Internet Seçenekleri**seçin hello **güvenlik** sekmesini tıklatın ve ardından hello seçin **Güvenilen siteler** simgesi.
   * Merhaba tıklatın **siteleri** düğmesi. Ekleme *https://\*. mongodb.org* Güvenilen siteler ve ardından Kapat hello iletişim kutusu toohello listesi.
     
     ![Internet Explorer güvenlik ayarlarını yapılandırın](./media/install-mongodb/configure-internet-explorer-security.png)
4. Toohello Gözat [MongoDB - indirmeleri](http://www.mongodb.org/downloads) sayfa (http://www.mongodb.org/downloads).
5. Gerekirse, hello seçin **Community Server** edition ve ardından hello en son kararlı sürümü geçerli Windows Server 2008 R2 64-bit ve daha sonra. toodownload yükleyici Merhaba, tıklatın **yükleme (MSI)**.
   
    ![MongoDB yükleyici indirin](./media/install-mongodb/download-mongodb.png)
   
    Merhaba yükleme tamamlandıktan sonra hello yükleyiciyi çalıştırın.
6. Okuma ve hello lisans sözleşmesini kabul edin. İstendiğinde, seçin **tam** yükleyin.
7. Merhaba son ekranında tıklatın **yükleme**.

## <a name="configure-hello-vm-and-mongodb"></a>Merhaba VM ve MongoDB yapılandırın
1. Merhaba yol değişkenleri hello MongoDB yükleyici tarafından güncelleştirilmez. Merhaba MongoDB olmadan `bin` path değişkeniniz bir konumda ihtiyacınız toospecify hello tam yolu MongoDB yürütülebilir her kullanışınızda. tooadd hello konumu tooyour path değişkeni:
   
   * Sağ hello **Başlat** menü ve select **sistem**.
   * Tıklatın **Gelişmiş Sistem ayarları**ve ardından **ortam değişkenleri**.
   * Altında **sistem değişkenleri**seçin **yolu**ve ardından **Düzenle**.
     
     ![Yol değişkenleri yapılandırın](./media/install-mongodb/configure-path-variables.png)
     
     Merhaba yolu tooyour MongoDB ekleme `bin` klasör. MongoDB yüklü genellikle *C:\Program Files\MongoDB*. VM Hello yükleme yolu doğrulayın. Merhaba aşağıdaki örnek, hello varsayılan MongoDB yükleme konumu toohello `PATH` değişkeni:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Emin tooadd hello başında noktalı virgül olması (`;`) konumu tooyour eklediğiniz tooindicate `PATH` değişkeni.

2. MongoDB veri ve günlük dizinleri veri diskinizde oluşturun. Merhaba gelen **Başlat** menüsünde, select **komut istemi**. Örnek hello hello dizinler F: sürücüde oluşturun.
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Aşağıdaki komut, hello yolu tooyour verilerini ayarlama hello ile bir MongoDB örneği başlatın ve dizinleri uygun şekilde oturum:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Merhaba günlük dosyaları MongoDB tooallocate için birkaç dakika sürer ve bağlantıları dinlemeyi Başlat. Tüm günlük iletilerini yönlendirilmiş toohello olan *F:\MongoLogs\mongolog.log* olarak dosya `mongod.exe` sunucu başlar ve günlük dosyalarını ayırır.
   
   > [!NOTE]
   > MongoDB örneğinizin çalışırken hello komut istemi bu görevde odaklanmış kalır. Merhaba komut istemi penceresini açık toocontinue MongoDB çalışan bırakın. Veya hello sonraki adımda ayrıntılı olarak hizmet olarak Mongodb'yi yükleyin.

4. Merhaba daha sağlam bir MongoDB deneyimi için yükleme `mongod.exe` bir hizmet olarak. Bir hizmet oluşturma toouse MongoDB her istediğinizde çalışan bir komut istemi tooleave gerekmeyen anlamına gelir. Merhaba, yol tooyour veri ve günlük dizinleri uygun şekilde ayarlama Hello hizmeti aşağıdaki gibi oluşturun:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Merhaba yukarıdaki komut MongoDB, "Mongo VT" açıklaması ile adlı bir hizmette oluşturur. şu parametreler hello da belirtilir:
   
   * Merhaba `--dbpath` seçeneği hello hello veri dizininin konumunu belirtir.
   * Merhaba `--logpath` seçeneği hello çalışan hizmetin bir komut penceresi toodisplay çıkışını olmadığı için kullanılan toospecify bir günlük dosyası olması gerekir.
   * Merhaba `--logappend` seçeneği belirtir hello hizmetinin yeniden başlatma çıkış tooappend toohello mevcut günlük dosyası neden olur.
   
   toostart MongoDB hizmet Merhaba, hello aşağıdaki komutu çalıştırın:
   
    ```
    net start MongoDB
    ```
   
    Merhaba MongoDB hizmet oluşturma hakkında daha fazla bilgi için bkz: [MongoDB için bir Windows hizmeti yapılandırma](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Test hello MongoDB örneği
Tek bir örneği olarak çalışan veya bir hizmet olarak yüklü MongoDB ile oluşturma ve kullanma, veritabanlarınızı şimdi başlayabilirsiniz. toostart hello MongoDB Yönetim Kabuğu hello başka bir komut istemi penceresi açın **Başlat** menüsünde ve hello aşağıdaki komutu girin:

```
mongo  
```

Merhaba hello veritabanlarıyla listeleyebilirsiniz `db` komutu. Bazı verileri aşağıdaki şekilde ekleyin:

```
db.foo.insert( { a : 1 } )
```

Verileri gibi arayabilirsiniz:

```
db.foo.find()
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Çıkış hello `mongo` gibi konsolu:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Güvenlik Duvarı ve ağ güvenlik grubu kurallarını yapılandırma
MongoDB yüklü ve çalışır durumda, uzaktan tooMongoDB bağlanabilmesi için bir bağlantı noktası Windows Güvenlik Duvarı'nı açın. toocreate yeni gelen kuralı tooallow TCP bağlantı noktası 27017, yönetici bir PowerShell komut istemini açın ve hello aşağıdaki komutu girin:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Hello kullanarak hello kuralı da oluşturabilirsiniz **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı** grafik yönetim aracıdır. Yeni gelen kuralı tooallow TCP bağlantı noktası 27017 oluşturun.

Gerekirse, bir ağ güvenlik grubu kural tooallow erişim tooMongoDB gelen hello mevcut Azure sanal ağ alt dışında oluşturun. Hello kullanarak ağ güvenlik grubu kuralları hello oluşturabilirsiniz [Azure portal](nsg-quickstart-portal.md) veya [Azure PowerShell](nsg-quickstart-powershell.md). Merhaba Windows Güvenlik duvarı kurallarıyla olarak, TCP bağlantı noktası 27017 toohello sanal ağ arabirimi, MongoDB VM izin verir.

> [!NOTE]
> TCP bağlantı noktası 27017 MongoDB tarafından kullanılan hello varsayılan bağlantı noktasıdır. Hello kullanarak bu bağlantı noktasını değiştirebilirsiniz `--port` başlatırken parametresi `mongod.exe` el ile veya bir hizmet. Hello bağlantı noktasını değiştirirseniz, önceki adımları hello emin tooupdate hello Windows Güvenlik Duvarı ve ağ güvenlik grubu kuralları olun.


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen tooinstall ve MongoDB, Windows VM yapılandırabilirsiniz. Artık MongoDB, Windows VM göre hello konularında Gelişmiş hello aşağıdaki erişebilirsiniz [MongoDB belgelerine](https://docs.mongodb.com/manual/).

