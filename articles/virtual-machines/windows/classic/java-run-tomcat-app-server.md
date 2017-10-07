---
title: Klasik Azure VM'de aaaRun Java uygulama sunucusu | Microsoft Docs
description: "Bu öğretici hello Klasik dağıtım modeli ve programlarını nasıl oluşturulacağını kaynakları kullanır toocreate bir Windows sanal makine ve toorun Apache Tomcat uygulama sunucusu yapılandırın."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Nasıl toorun bir Java uygulama sunucusu bir sanal makinede hello Klasik dağıtım modeli kullanılarak oluşturulmuş
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bir Resource Manager şablonu toodeploy için Java 8 ve Tomcat webapp, bkz: [burada](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Azure ile bir sanal makine tooprovide sunucu özelliklerini kullanabilirsiniz. Örnek olarak, Azure üzerinde çalışan bir sanal makine yapılandırılmış toohost Apache Tomcat gibi bir Java uygulama sunucusu olabilir.

Bu kılavuzu tamamladıktan sonra nasıl bir anlayış gerekir toocreate bir sanal makine Azure üzerinde çalışan ve toorun bir Java uygulama sunucusu yapılandırın. Siz öğrenin ve hello aşağıdaki görevleri gerçekleştirin:

* Nasıl toocreate bir sanal makine, bir Java Geliştirme Seti (zaten yüklü JDK) sahiptir.
* Nasıl tooremotely tooyour sanal makinede oturum.
* Nasıl tooinstall bir Java uygulama sunucusu--Apache Tomcat--sanal makinenizde.
* Nasıl toocreate sanal makineniz için bir uç nokta.
* Nasıl tooopen hello bir bağlantı noktası güvenlik duvarı, uygulama sunucusu için.

Merhaba, bir sanal makinede çalışan Tomcat yükleme sonuçlarında tamamlandı.

![Apache Tomcat çalıştıran sanal makine][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate bir sanal makine
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).  
2. ' I tıklatın **yeni**, tıklatın **işlem**, ardından **tümünü görmek** hello içinde **öne çıkan uygulamalar**.
3. Tıklatın **JDK**, tıklatın **JDK 8** hello içinde **JDK** bölmesi.  
   Sanal makine görüntüleri destekleyen **JDK 6** ve **JDK 7** hazır toorun JDK 8 olmayan eski uygulamalarınız varsa kullanılabilir.
4. Merhaba JDK 8 bölmesinde seçin **Klasik**, ardından **oluşturma**.
5. Merhaba, **Temelleri** dikey penceresinde:
   1. Merhaba sanal makine için bir ad belirtin.
   2. Hello Merhaba yönetici adı **kullanıcı adı** alan. Merhaba sonraki alanda izleyen ilişkili parola hello ve bu ad unutmayın. Uzaktan toohello sanal makinede oturum açtığınızda, bunları gerekir.
   3. Hello bir parola girmenizi **yeni parola** alan ve hello girmek **parolayı onayla** alan. Bu parola Merhaba yönetici hesabı değil.
   4. Select hello uygun **abonelik**.
   5. Hello için **kaynak grubu**, tıklatın **Yeni Oluştur** ve yeni bir kaynak grubu hello adını girin. Veya tıklatın **var olanı kullan** bir hello kullanılabilir kaynak gruplarını seçin.
   6. Merhaba sanal makinenin bulunduğu, gibi bir konum seçin **Orta Güney ABD**.
6. **İleri**’ye tıklayın.
7. Merhaba, **sanal makine görüntü boyutu** dikey penceresinde, select **A1 standart** veya başka bir uygun görüntü.
8. **Seç**'e tıklayın.

9. Merhaba, **ayarları** dikey penceresinde tıklatın **Tamam**. Azure tarafından sağlanan hello varsayılan değerleri kullanabilirsiniz.  
10. Merhaba, **Özet** dikey penceresinde tıklatın **Tamam**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely oturum tooyour sanal makineyi açma
1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **sanal makineleri (Klasik)**. Gerekirse, tıklatın **daha fazla hizmet** hello alt sol köşesinde hello Hizmet Kategoriler altında. Merhaba **sanal makineleri (Klasik)** hello listelen giriş **işlem** grubu.
3. Merhaba, toosign istediğiniz içinde hello sanal makine adını tıklatın.
4. Merhaba sanal makine başlatıldıktan sonra hello bölmesini hello üstündeki menü bağlantılara izin verir.
5. **Bağlan**'a tıklayın.
6. Yanıt toohello gerekli tooconnect toohello sanal makine olarak ister. Genellikle, kaydedin veya hello bağlantı ayrıntılarını içeren hello .rdp dosyasını açın. Merhaba son hello .rdp dosyasının ilk satırı hello kapsamında toocopy hello url: bağlantı noktası sahip ve bir uzak oturum açma uygulamasında yapıştırın.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall sanal makinenizde bir Java uygulama sunucusu
Java uygulama sunucusu tooyour sanal makine kopyalayabilir veya bir yükleyici aracılığıyla bir Java uygulama sunucusu yükleyebilirsiniz.

Bu öğretici Tomcat hello Java uygulama sunucusu tooinstall kullanır.

1. Tooyour sanal makinede imzalandığında bir tarayıcı oturumu çok açın[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Merhaba bağlantı için çift **32-bit/64-bit Windows hizmeti yükleyicisini**. Bu yöntemi kullanarak, Tomcat bir Windows hizmeti olarak yükler.
3. İstendiğinde, toorun hello yükleyici seçin.
4. Merhaba içinde **Apache Tomcat Kurulum** Sihirbazı, izleme hello tooinstall Tomcat ister. Bu öğreticinin Hello amaçları hello varsayılan değerleri kabul ederek uygundur. Merhaba ulaştığınızda **Tamamlanıyor hello Apache Tomcat Kurulum Sihirbazı'nı** iletişim kutusu, isteğe bağlı olarak kontrol edebilirsiniz **çalıştırmak Apache Tomcat** toohave şimdi Tomcat Başlat. Tıklatın **son** toocomplete hello Tomcat Kurulum işlemi.

## <a name="toostart-tomcat"></a>toostart Tomcat

Sanal makine ve çalışan hello komutunu bir komut istemi'ni açarak, Tomcat el ile başlatabilirsiniz **net&nbsp;Başlat&nbsp;Tomcat8**.

Tomcat çalışmaya başladıktan sonra Tomcat hello URL'yi girerek erişebileceğiniz <http://localhost: 8080> hello sanal makinenin tarayıcıda.

toosee dış makinelerden çalıştıran Tomcat, toocreate bir uç nokta gerekir ve bir bağlantı noktası açın.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate sanal makineniz için bir uç nokta
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **sanal makineleri (Klasik)**.
3. Java uygulama sunucusu çalışıyor hello sanal makine Hello adına tıklayın.
4. **Uç Noktalar**’a tıklayın.
5. **Ekle**'ye tıklayın.
6. Merhaba, **uç nokta ekleme** iletişim kutusunda:
   1. Merhaba uç noktası için bir ad belirtin; Örneğin, **HttpIn**.
   2. Seçin **TCP** hello protokolü için.
   3. Belirtin **80** hello genel bağlantı noktası için.
   4. Belirtin **8080** hello özel bağlantı noktası.
   5. Seçin **devre dışı** hello kayan IP adresi için.
   6. Merhaba erişim denetim listesi olduğu gibi bırakın.
   7. Merhaba tıklatın **Tamam** düğmesini tooclose hello iletişim kutusu ve hello uç noktası oluşturur.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen hello Güvenlik Duvarı'nda, sanal makine için bir bağlantı noktası
1. Tooyour sanal makinede oturum açın.
2. Tıklatın **Windows Başlangıç**.
3. Tıklatın **Denetim Masası**.
4. Tıklatın **sistem ve güvenlik**, tıklatın **Windows Güvenlik Duvarı**ve ardından **Gelişmiş ayarları**.
5. Tıklatın **gelen kuralları**ve ardından **yeni kural**.  
   ![Yeni gelen kuralı][NewIBRule]
6. Hello için **kural türü**seçin **bağlantı noktası**ve ardından **sonraki**.  
   ![Yeni gelen kuralı bağlantı noktası][NewRulePort]
7. Merhaba üzerinde **protokol ve bağlantı noktaları** ekran, select **TCP**, belirtin **8080** hello olarak **belirli yerel bağlantı noktası**ve ardından **Sonraki**.  
  ![Yeni gelen kuralı][NewRuleProtocol]
8. Merhaba üzerinde **eylem** ekran, select **hello bağlantıya izin verme**ve ardından **sonraki**.
   ![Yeni gelen kuralı eylemi][NewRuleAction]
9. Merhaba üzerinde **profil** ekranında, emin **etki alanı**, **özel**, ve **ortak** seçilir ve ardından **sonraki** .
   ![Yeni gelen kuralı profili][NewRuleProfile]
10. Merhaba üzerinde **adı** ekranında, hello kuralı için bir ad belirtin **HttpIn** (Merhaba kural adı gerekli toomatch hello uç nokta adı değil, ancak) ve ardından **son**.  
    ![Yeni gelen kuralı adı][NewRuleName]

Bu noktada, Tomcat Web sitenizi dış bir tarayıcıdan görüntülenebilir olması gerekir. Merhaba tarayıcının adres penceresinde hello form URL'sini yazın  **http://*,\_DNS\_adı*. cloudapp.net**, burada ***,\_DNS\_adı*** hello sanal makineyi oluşturduğunuzda belirttiğiniz hello DNS adı.

## <a name="application-lifecycle-considerations"></a>Uygulama yaşam döngüsü hakkında dikkat edilecek noktalar
* Kendi web uygulama Arşivi (WAR) oluşturun ve toohello eklemek **webapps** klasör. Örneğin, bir temel Java hizmet sayfa (JSP) dinamik web projesi oluşturun ve bir WAR dosyası olarak dışarı aktarma. Ardından, hello WAR toohello Apache Tomcat kopyalama **webapps** klasörü hello sanal makineye, ardından bir tarayıcıda çalıştırın.
* Merhaba Tomcat hizmeti yüklü olduğunda, varsayılan olarak toostart onu el ile ayarlanır. Bu toostart otomatik olarak hello Hizmetler ek bileşenini kullanarak geçiş yapabilirsiniz. Tıklayarak Hello Hizmetler ek bileşenini başlatın **Windows Başlat**, **Yönetimsel Araçlar**ve ardından **Hizmetleri**. Merhaba çift **Apache Tomcat** ayarlayın ve hizmeti **başlangıç türü** çok**otomatik**.

    ![Bir hizmet toostart otomatik olarak ayarlama][service_automatic_startup]

    Merhaba otomatik olarak Başlat Tomcat sahip olmanın avantaj (örneğin, yeniden başlatma gerektiren yazılım güncelleştirmeleri yüklendikten sonra) hello sanal makine yeniden başlatıldığında çalışmaya başladıktan emin olmalıdır.

## <a name="next-steps"></a>Sonraki adımlar
İsteyebileceğiniz diğer hizmetler hakkında (örneğin, Azure Storage, hizmet veri yolu ve SQL veritabanı) öğrenebilirsiniz tooinclude Java uygulamaları ile. Merhaba kullanılabilir hello bilgileri görüntüleyin [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
