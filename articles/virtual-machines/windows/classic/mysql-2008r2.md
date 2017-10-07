---
title: "Klasik Azure VM aaaCreate MySQL çalıştıran | Microsoft Docs"
description: "Windows Server 2012 R2 çalıştıran bir Azure sanal makine oluşturma ve MySQL veritabanı hello Klasik dağıtım modeli kullanılarak hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Windows Server 2016 çalıştıran hello Klasik dağıtım modeli kullanılarak oluşturulmuş bir sanal makinede MySQL yükleme
[MySQL](https://www.mysql.com) bir popüler açık kaynak, SQL veritabanı. Bu öğretici şunların nasıl yapıldığını gösterir tooinstall ve Çalıştır hello **5.7.18 MySQL community sürümü** MySQL sunucusu çalıştıran bir sanal makine olarak **Windows Server 2016**. Deneyiminizi MySQL veya Windows Server'ın diğer sürümleri için biraz farklı olabilir.

Linux'ta MySQL yükleme ile ilgili yönergeler için bkz: [nasıl tooinstall Azure üzerinde MySQL](../../linux/mysql-install.md).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Windows Server 2016 çalıştıran bir sanal makine oluşturma
Windows Server 2016 çalıştıran bir VM zaten sahip değilseniz, bu kullanabilirsiniz [öğretici](./tutorial.md) toocreate hello sanal makine.

## <a name="attach-a-data-disk"></a>Veri diski ekleme
Merhaba sanal makine oluşturulduktan sonra isteğe bağlı olarak bir veri diski ekleyebilirsiniz. Bir veri diski üretim iş yükleri ve işletim sistemi sürücünüz (C:) hello üzerinde alana sahip tooavoid için önerilen ekleme, hello işletim sistemi içerir.

Bkz: [nasıl tooattach bir veri diski tooa Windows sanal makine](../attach-managed-disk-portal.md) ve boş disk ekleme hello yönergelerini izleyin. Merhaba konağı önbellek çok ayarlamak**hiçbiri** veya **salt okunur**.

## <a name="log-on-toohello-virtual-machine"></a>Toohello sanal makinede oturum açın
Ardından, artıracaksınız [toohello sanal makinede oturum](./connect-logon.md) MySQL yükleyebilmek için.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Yükleyin ve MySQL Community Server hello sanal makinede çalıştırın
Bu adımları tooinstall izleyin, yapılandırmak ve MySQL Server'ın hello topluluk sürümünü çalıştırın:

> [!NOTE]
> Internet Explorer kullanarak öğeleri indirirken hello IE ayarlayabilirsiniz **Artırılmış Güvenlik Yapılandırması** tooOff ve yükleme işlemi hello basitleştirin. Merhaba Başlat menüsünden Yönetimsel Araçlar/Sunucu Yöneticisi'ni / yerel sunucuya tıklayın ve ardından IE **Artırılmış Güvenlik Yapılandırması** ve hello yapılandırma tooOff ayarlayın).
>
>

1. Uzak Masaüstü kullanarak toohello sanal makineye bağlandıktan sonra tıklatın **Internet Explorer** hello başlangıç ekranından.
2. Select hello **Araçları** hello sağ üst köşesinde (Merhaba cogged tekerleği simgesi) düğmesine tıklayın ve ardından **Internet Seçenekleri**. Hello'ı tıklatın **güvenlik** hello sekmesini ve ardından **Güvenilen siteler** simgesi ve hello ardından **siteleri** düğmesi. Http://*.MySQL.com toohello Güvenilen siteler listesine ekleyin. Tıklatın **Kapat**ve ardından **Tamam**.
3. Merhaba adres çubuğu, Internet Explorer'da https://dev.mysql.com/downloads/mysql/ yazın.
4. Merhaba MySQL site toolocate kullanın ve hello MySQL Yükleyicisi için Windows hello en son sürümünü yükleyin. Merhaba MySQL yükleyici seçerken, dosya kümesi (örneğin, hello mysql-yükleyici-topluluk-5.7.18.0.msi dosya boyutuna 352.8 MB) tamamlamak ve hello yükleyici kaydetmek hello sahip hello sürümünü karşıdan yükleyin.
5. Hello yükleyici, indirme tamamlandığında tıklatın **çalıştırmak** toolaunch kurulumu.
6. Merhaba üzerinde **Lisans Sözleşmesi'ni** sayfasında hello lisans sözleşmesini kabul etmeniz ve tıklayın **sonraki**.
7. Merhaba üzerinde **kurulum türünü seçme** sayfasında, tıklatın ve ardından hello kurulum türünü **sonraki**. Merhaba aşağıdaki adımlarda varsayılmaktadır hello hello seçimi **yalnızca sunucu** kurulum türü.
8. Merhaba, **denetleyin gereksinimleri** sayfasında görüntüler, **yürütme** toolet hello yükleyici eksik tüm bileşenlerini yükleyin. Görüntüleyen, gibi hello C++ yeniden dağıtılabilir çalışma zamanı yönergeleri izleyin.
9. Merhaba üzerinde **yükleme** sayfasında, **yürütme**. Yükleme tamamlandığında tıklatın **sonraki**.

10. Merhaba üzerinde **ürün yapılandırma** sayfasında, **sonraki**.

11. Merhaba üzerinde **türü ve ağ** sayfasında, gerekirse hello TCP bağlantı noktası da dahil olmak üzere, istenen yapılandırma türü ve bağlantı seçeneklerini belirtin. Seçin **Gelişmiş Seçenekleri Göster**ve ardından **sonraki**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Merhaba üzerinde **hesapları ve rolleri** sayfasında, güçlü bir MySQL kök parola belirtin. Gerektiğinde ek MySQL kullanıcı hesaplarını ekleyin ve ardından **sonraki**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Merhaba üzerinde **Windows hizmeti** sayfasında, hello MySQL sunucusu Windows hizmeti olarak gerektiği şekilde çalıştırmak için değişiklikleri toohello varsayılan ayarları belirtin ve ardından **sonraki**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Merhaba hello seçimlerine **eklentileri ve uzantıları** sayfasında isteğe bağlı. Tıklatın **sonraki** toocontinue.
15. Merhaba üzerinde **Gelişmiş Seçenekler** sayfasında, gerektiğinde değişiklikleri toologging seçenekleri belirtin ve ardından **sonraki**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Merhaba üzerinde **geçerli sunucu yapılandırmasını** sayfasında, **yürütme**. Merhaba yapılandırma adımları tamamlandığında tıklatın **son**.
17. Merhaba üzerinde **ürün yapılandırma** sayfasında, **sonraki**.
18. Merhaba üzerinde **yükleme tamamlandı** sayfasında, **kopyalama günlük tooClipboard** tooexamine daha sonra ve ardından isterseniz **son**.
19. Merhaba başlangıç ekranından yazın **mysql**ve ardından **MySQL 5.7 komut satırı istemci**.
20. Adım 12'de belirttiğiniz hello kök parola girin ve komutları tooconfigure MySQL nerede sorun içeren bir istem sunulur. Komutlar ve söz dizimi Hello Ayrıntılar için bkz [MySQL başvuru kılavuzlarına](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Merhaba temel ve veri dizinleri ve sürücüler gibi sunucu yapılandırmasını varsayılan ayarları da yapılandırabilirsiniz. Daha fazla bilgi için bkz: [6.1.2 yapılandırma sunucusu varsayılan olarak](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Uç noktaları yapılandırma

Merhaba Internet üzerinde Hello MySQL hizmeti toobe kullanılabilir tooclient bilgisayarlar için hello TCP bağlantı noktası için bir uç nokta yapılandırmak ve bir Windows Güvenlik duvarı kuralı oluşturmanız gerekir. hangi hello MySQL Server hizmeti için MySQL istemcileri dinler hello varsayılan bağlantı noktası 3306 değerdir. Başlangıç bağlantı noktası tutarlı hello üzerinde sağlanan hello değerine sahip olduğu sürece, başka bir bağlantı noktası belirtebilirsiniz **türü ve ağ** sayfa (Adım 11 hello önceki yordamın).

> [!NOTE]
> Üretim kullanımı için güvenlik etkilerini hello MySQL Server hizmeti kullanılabilir tooall bilgisayarları hello Internet üzerinde hale hello göz önünde bulundurun. Merhaba toouse hello uç noktası erişim denetimi listesi (ACL) ile izin verilen kaynak IP adresleri kümesini tanımlayabilir. Daha fazla bilgi için bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](setup-endpoints.md).
>
>

tooconfigure hello MySQL Server hizmeti için bir uç nokta:

1. Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)**, MySQL sanal makineniz hello adına tıklayın ve ardından **uç noktaları**.
2. Merhaba komut çubuğunda, **Ekle**.
3. Merhaba üzerinde **uç nokta ekleme** sayfasında, için benzersiz bir ad yazın **adı**.
4. Seçin **TCP** hello protokol olarak.
5. Başlangıç bağlantı noktası numarasını yazın **3306**, hem de **genel bağlantı noktası** ve **özel bağlantı noktası**ve ardından **Tamam**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Windows Güvenlik duvarı kuralı tooallow MySQL trafiği ekleme
tooadd komutunda aşağıdaki hello çalıştırmak hello Internet, MySQL trafiğinden izin veren bir Windows Güvenlik duvarı kuralı bir _yükseltilmiş Windows PowerShell komut isteminde_ hello MySQL sunucusu sanal makinesinde.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Uzak bağlantıyı sınayın
tootest, uzak bağlantı toohello Azure VM çalışan hello MySQL Server hizmeti, hello VN içeren hello bulut hizmeti hello DNS adı sağlamanız gerekir.

1. Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)**, MySQL server sanal makinenizi hello adına tıklayın ve ardından **genel bakış**.
2. Merhaba sanal makine panodan hello Not **DNS adı** değeri. Örnek aşağıda verilmiştir:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. MySQL kullanıcı olarak komut toolog içinde aşağıdaki hello MySQL veya hello MySQL istemci çalıştıran yerel bir bilgisayardan çalıştırın.

     MySQL -u <yourMysqlUsername> - p -h<yourDNSname>

   Örneğin, kullanarak izin ver hello MySQL kullanıcı adı _dbadmin3_ ve hello _testmysql.cloudapp.net_ DNS adı hello sanal makine için komutu aşağıdaki hello kullanarak MySQL başlayabilirsiniz:

     MySQL -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Sonraki adımlar
MySQL, çalıştırma hakkında daha fazla toolearn bkz hello [MySQL belgeleri](http://dev.mysql.com/doc/).
