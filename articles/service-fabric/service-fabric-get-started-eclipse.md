---
title: "Service Fabric Eclipse için eklenti aaaAzure | Microsoft Docs"
description: "Service Fabric eklenti Hello ile Eclipse için kullanmaya başlayın."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Eclipse Java uygulama geliştirmesi için Service Fabric eklentisi
Eclipse en yaygın olarak kullanılan hello biridir Java geliştiriciler için tümleşik geliştirme ortamlarını (IDE). Bu makalede, sizi tanımlamak nasıl tooset, Eclipse geliştirme ortamı toowork Azure Service Fabric ile ayarlama. Tooinstall hello Service Fabric eklentisi, Service Fabric uygulaması oluşturma ve Service Fabric uygulaması tooa yerel veya uzak Service Fabric kümenizdeki Eclipse Neon dağıtmak öğrenin.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Yükleme veya hello Service Fabric Eclipse Neon eklenti güncelleştir
Eclipse'te Service Fabric eklentisi yükleyebilirsiniz. Merhaba eklentisi oluşturma ve Java Hizmetleri dağıtma hello işlemini kolaylaştırmaya yardımcı olabilir.

1.  Eclipse Neon hello en son sürümünü ve en son sürümünü Buildship hello olduğundan emin olun (1.0.17 veya sonraki bir sürümü) yüklü:
    -   Eclipse Neon içinde yüklü bileşenlerin toocheck hello sürümleri Git çok**yardımcı** > **Yükleme ayrıntıları**.
    -   tooupdate Buildship, bkz: [Eclipse Buildship: Eclipse için eklentilerini Gradle][buildship-update].
    -   için toocheck ve güncelleştirmeleri yükleme için Eclipse Neon Git çok**yardımcı** > **Güncelleştirmeleri denetle**.

2.  tooinstall hello Service Fabric Eclipse Neon içinde eklenti Git çok**yardımcı** > **yeni yazılımı yükle**.
  1.    Merhaba, **çalışmak** kutusuna **http://dl.microsoft.com/eclipse**.
  2.    **Ekle**'ye tıklayın.

         ![Eclipse Neon için Service Fabric eklentisi][sf-eclipse-plugin-install]
  3.    Merhaba Service Fabric eklenti seçin ve ardından **sonraki**.
  4.    Merhaba yükleme adımlarını tamamlayın ve hello Microsoft Yazılımı Lisans koşulları kabul edin.

Hello Service yüklü Fabric eklenti zaten varsa, hello en son sürümüne sahip olduğunuzdan emin olun. kullanılabilir güncelleştirmeleri toocheck Git çok**yardımcı** > **Yükleme ayrıntıları**. Yüklü eklentileri listesi Merhaba, Service Fabric seçin ve ardından **güncelleştirme**. Kullanılabilir güncelleştirmeler yüklenir.

> [!NOTE]
> Yükleme veya hello Service Fabric eklenti güncelleştirme yavaşsa, tooan Eclipse ayarı nedeniyle olabilir. Eclipse Eclipse örneğinizle kayıtlı tüm değişiklikleri tooupdate sitelerindeki meta verileri toplar. toospeed denetleniyor ve Service Fabric eklenti güncelleştirmeyi yükleme işlemini hello Git çok**kullanılabilir yazılım siteleri**. Merhaba toohello Service Fabric eklenti konumu (http://dl.microsoft.com/eclipse/azure/servicefabric) işaret eden bir dışında tüm siteler için Hello onay kutularını temizleyin.

## <a name="create-a-service-fabric-application-in-eclipse"></a>Eclipse’te Service Fabric uygulaması oluşturma

1.  Eclipse Neon içinde çok Git**dosya** > **yeni** > **diğer**. **Service Fabric Projesi**’ni seçip **İleri**’ye tıklayın.

    ![Service Fabric Yeni Proje sayfa 1][create-application/p1]

2.  Projeniz için bir ad girip **İleri**’ye tıklayın.

    ![Service Fabric Yeni Proje sayfa 2][create-application/p2]

3.  Şablonları Hello listesinde seçin **hizmet şablonu**. Hizmet şablonu türünüzü (Aktör, Durum Bilgisi Olmayan, Kapsayıcı veya Konuk İkili) seçip **İleri**’ye tıklayın.

    ![Service Fabric Yeni Proje sayfa 3][create-application/p3]

4.  Merhaba hizmet adı girin ve hizmet ayrıntılarını ve ardından **son**.

    ![Service Fabric Yeni Proje sayfa 4][create-application/p4]

5. Hello ilk Service Fabric projenizi oluşturduğunuzda **açık ilişkili perspektif** iletişim kutusu, tıklatın **Evet**.

    ![Service Fabric Yeni Proje sayfa 5][create-application/p5]

6.  Yeni projeniz şöyle görünür:

    ![Service Fabric Yeni Proje sayfa 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Eclips’te Service Fabric uygulaması derleme ve dağıtma

1.  Yeni Service Fabric uygulamanıza sağ tıklayın ve ardından **Service Fabric**’i seçin.

    ![Service Fabric sağ tıklama menüsü][publish/RightClick]

2. Merhaba alt menüde hello seçeneği belirleyin:
    -   Temizleme, olmadan toobuild hello uygulama'yı tıklatın **yapı uygulama**.
    -   toodo hello uygulamasının temiz bir yapı tıklatın **yeniden uygulama**.
    -   Yerleşik yapılarının tooclean hello uygulama'yı tıklatın **temiz uygulama**.

3.  Bu menüden ayrıca uygulamanızı dağıtabilir, dağıtımını kaldırabilir ve yayımlayabilirsiniz:
    -   toodeploy tooyour yerel küme, tıklatın **dağıtmak uygulama**.
    -   Merhaba, **uygulamasını Yayımla** iletişim kutusunda, bir yayımlama profili seçin:
        -  **Local.json**
        -  **Cloud.json**

     Bu JavaScript nesne gösterimi (JSON) dosyaları gerekli tooconnect tooyour yerel veya buluta (Azure'a) küme bilgilerini (örneğin, bağlantı uç ve güvenlik bilgileri) depolar.

  ![Service Fabric Yayımla menüsü][publish/Publish]

Bir alternatif bir yol toodeploy yapılandırmaları Service Fabric uygulamanızı Eclipse kullanılarak çalıştırılır.

  1.    Çok Git**çalıştırmak** > **yapılandırmaları Çalıştır**.
  2.    Altında **Gradle proje**seçin hello **ServiceFabricDeployer** yapılandırma çalıştırın.
  3.    Merhaba üzerinde hello sağ bölmede **bağımsız değişkenleri** sekmesinde için **publishProfile**seçin **yerel** veya **bulut**.  Merhaba varsayılandır **yerel**. Uzak toodeploy tooa veya Bulut küme, select **bulut**.
  4.    Merhaba uygun bilgileri hello doldurulur tooensure yayımlama profillerini, düzenleme **Local.json** veya **Cloud.json** gerektiğinde. Uç nokta bilgilerini ve güvenlik kimlik bilgilerini ekleyebilir ya da güncelleştirebilirsiniz.
  5.    Emin **çalışma dizini** toohello uygulamasıyla toodeploy işaret eder. toochange Merhaba uygulama, hello tıklatın **çalışma** düğmesine tıklayın ve ardından istediğiniz hello uygulamayı seçin.
  6.    **Uygula** ve ardından **Çalıştır** seçeneğine tıklayın.

Uygulamanız birkaç dakika içinde derlenip dağıtılır. Service Fabric Explorer hello dağıtım durumunu izleyebilirsiniz.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Service Fabric hizmeti tooyour Service Fabric uygulaması ekleyin

tooadd bir Service Fabric hizmeti tooan mevcut Service Fabric uygulaması, adımları hello:

1.  Bir hizmete tooadd istediğiniz ve ardından sağ hello proje **Service Fabric**.

    ![Service Fabric Hizmet Ekleme sayfa 1][add-service/p1]

2.  Tıklatın **Service Fabric Hizmet Ekle**, ve tam hello hizmeti toohello projesi adımları tooadd ayarlayın.
3.  Tooadd tooyour proje istediğiniz ve ardından select hello hizmet şablonu **sonraki**.

    ![Service Fabric Hizmet Ekleme sayfa 2][add-service/p2]

4.  Hello hizmet adı (ve diğer ayrıntıları gerektiği gibi) girin ve hello ardından **Hizmet Ekle** düğmesi.  

    ![Service Fabric Hizmet Ekleme sayfa 3][add-service/p3]

5.  Merhaba hizmet eklendikten sonra genel proje yapınızı proje aşağıdaki benzer toohello görünür:

    ![Service Fabric Hizmet Ekleme sayfa 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Service Fabric Java uygulamanızın Bildirim sürümlerini düzenleme

tooedit bildirim sürümleri hello projeye sağ tıklayın, çok Git**Service Fabric** seçip **bildirim sürümleri Düzenle...**  gelen hello menüsü açılır. Başlangıç Sihirbazı'nda hello bildirim uygulama bildirimi, hizmet bildirimi için ve hello sürümleri için güncelleştirebilirsiniz **kod**, **Config** ve **veri** paketler.

Merhaba seçeneğini işaretlerseniz **otomatik olarak uygulama ve hizmet sürümleri güncelleştirme** ve bir sürümüne güncelleştirin, ardından hello bildirim sürümlerini otomatik olarak güncelleştirilir. toogive örnek ilk seçtiğiniz hello onay kutusunu ve ardından güncelleştirme hello sürümü **kod** 0.0.0 sürümünden too0.0.1 ve tıklayarak **son**, bildirimi sürümü ve uygulama bildirimi hizmeti sürümü otomatik olarak güncelleştirilen too0.0.1 olacaktır.

## <a name="upgrade-your-service-fabric-java-application"></a>Service Fabric Java uygulamanızı yükseltme

Bir yükseltme senaryosu için oluşturduğunuz hello söyleyin **App1** hello Service Fabric Eclipse'te eklentisini kullanarak proje. Merhaba eklenti toocreate kullanarak adlı bir uygulama dağıttıktan **fabric: / App1Application**. Merhaba uygulama türü **App1AppicationType**, ve hello uygulama sürümü 1.0. Şimdi, kullanılabilirliğini kesintiye uğratmadan uygulamanızı tooupgrade istiyorsunuz.

İlk olarak, herhangi bir değişiklik tooyour uygulama ve değiştiren hello hizmeti yeniden oluşturun. Güncelleştirme hello hello hizmeti (ve kod, yapılandırma veya ilgili olarak veri) için güncelleştirilmiş hello sürümleri ile hizmetin bildirim dosyası (ServiceManifest.xml) değiştirdi. Ayrıca, güncelleştirilmiş hello sürüm numarasıyla Merhaba uygulaması için hello uygulama bildirimi (ApplicationManifest.xml) değiştirin ve değiştirilen hizmet hello.  

tooupgrade Eclipse Neon kullanarak uygulamanızı yinelenen çalıştırma yapılandırma profili oluşturabilirsiniz. Ardından tooupgrade kullanın uygulamanız gerektiğinde.

1.  Çok Git**çalıştırmak** > **yapılandırmaları Çalıştır**. Hello sol hello küçük oka toohello solundaki bölmesinde **Gradle proje**.
2.  **ServiceFabricDeployer**’a sağ tıklayıp **Yinelenen**’i seçin. Bu yapılandırma için **ServiceFabricUpgrader** gibi yeni bir ad girin.
3.  Merhaba sağ masasındaki hello **bağımsız değişkenleri** sekmesinde, değiştirmek **- Pconfig 'dağıtma' =** çok**- Pconfig 'yükseltme' =**ve ardından **Uygula**.

Bu işlem oluşturur ve bir çalışma yapılandırma profili kaydeder uygulamanız hiçbir zaman tooupgrade kullanabilir. Ayrıca hello en son güncelleştirilen uygulama türü sürümü hello uygulama bildirim dosyasından alır.

Merhaba uygulama yükseltme, birkaç dakika sürer. Service Fabric Explorer'da uygulama yükseltme hello izleyebilirsiniz.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Maven ile kullanılan eski Service Fabric Java uygulamaları toobe geçirme
Service Fabric Java kitaplıkları yakın zamanda Service Fabric Java SDK tooMaven depodan taşınmış. Eclipse, kullanarak Oluştur hello yeni uygulamalar üretir (Maven ile mümkün toowork olacaktır) en son güncelleştirilen projeleri, ancak varolan Service Fabric durum bilgisiz veya hello Service Fabric Java SDK kullanmakta olduğunuz aktör Java uygulamalarını güncelleştirebilirsiniz önceki sürümlerde, toouse hello Service Fabric Java bağımlılıklardan Maven. Lütfen belirtilen hello adımları [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure eski uygulamanızı Maven ile çalışır.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
