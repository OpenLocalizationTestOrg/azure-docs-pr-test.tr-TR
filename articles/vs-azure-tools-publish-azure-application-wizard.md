---
title: "Visual Studio Azure uygulaması Yayımlama Sihirbazı aaaUsing hello | Microsoft Docs"
description: "Nasıl tooconfigure hello hello Visual Studio Azure uygulaması Yayımlama Sihirbazı çeşitli ayarlarında öğrenin"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Merhaba Visual Studio Azure uygulaması Yayımlama Sihirbazı kullanma
Visual Studio'da bir web uygulaması geliştirme sonra hello kullanarak bu uygulama tooan Azure bulut hizmeti yayımlayabilirsiniz **Azure uygulamasını Yayımla** Sihirbazı. 

> [!NOTE]
> Bu konu, toocloud Hizmetleri, değil tooweb siteleri dağıtma hakkında ' dir. Tooweb siteleri dağıtma hakkında daha fazla bilgi için bkz: [nasıl tooDeploy bir Azure Web sitesi](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Hello Azure uygulamasını Yayımla Sihirbazı'na erişim

Sahip olduğunuz Visual Studio projesi hello türüne bağlı olarak iki yolla hello Azure uygulamasını Yayımla Sihirbazı erişebilir.

**Bir Azure bulut hizmeti projesi varsa:**

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **Yayımla**.

**Azure için etkinleştirilmemiş bir web uygulaması projesi varsa:**

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **Dönüştür** > **tooAzure bulut hizmeti projesini Dönüştür**. 

1. İçinde **Çözüm Gezgini**, yeni oluşturulan hello Azure projesine sağ tıklayın ve, hello bağlam menüsünden seçin **Yayımla**.

## <a name="sign-in-page"></a>Oturum açma sayfası

![Oturum açma sayfası](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Hesap** - bir hesap seçin veya seçin **Hesap Ekle** hello hesap açılır listesinde.

**Aboneliğinizi seçin** -hello abonelik toouse dağıtımınız için seçin.
   
## <a name="settings-page---common-settings-tab"></a>Ayarları Sayfası - Genel Ayarları sekmesi   

![Genel ayarları](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Bulut hizmeti** -hello açılır kullanarak ya da var olan bir bulut hizmeti ya da seçin seçin  **&lt;Yeni Oluştur >**ve bir bulut hizmeti oluşturun. Her bir bulut hizmeti için parantez içinde Hello veri merkezi görüntüler. Merhaba veri merkezinin konumu hello bulut hizmeti için aynı hello depolama hesabı (Gelişmiş) için hello veri merkezinin konumu olarak hello olduğunu önerilir.  

**Ortam** -seçin **üretim** veya **hazırlama**. Toodeploy istiyorsanız ortam hazırlama hello bir test ortamında uygulamanızı seçin. 

**Derleme Yapılandırması** -seçin **hata ayıklama** veya **sürüm**.

**Hizmet yapılandırması** -seçin **bulut** veya **yerel**.
   
**Tüm roller için Uzak Masaüstü'nü etkinleştirin** -onay toobe mümkün tooremotely istiyorsanız bu seçeneği connect toohello hizmeti. Bu seçenek, öncelikle sorun giderme amacıyla kullanılır. Bu onay kutusunu seçtiğinizde, hello **uzak masaüstü yapılandırması** iletişim kutusu görüntülenir. Merhaba seçin **ayarları** bağlantı toochange hello yapılandırması.
   
**Tüm web rolleri için Web dağıtımı etkinleştirmek** -bu seçenek, tooenable web dağıtımı hello hizmeti denetleyin. Merhaba seçmelisiniz **tüm roller için Uzak Masaüstü'yi etkinleştirmek** bu özellik toouse seçeneği. Daha fazla bilgi için bkz: [ [yayımlama Visual Studio kullanarak bir Azure bulut hizmeti](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Ayarları sayfası - Gelişmiş Ayarları sekmesi

![Gelişmiş ayarlar](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Dağıtım etiketi** -hello varsayılan adı kabul edin veya seçtiğiniz bir ad girin. tooappend hello tarih toohello dağıtım etiketi, bırakın hello onay kutusu seçili. 
   
**Depolama hesabı** - seçin bu dağıtım için depolama hesabı toouse hello **&lt;Yeni Oluştur > toocreate bir depolama hesabı. Her Depolama hesabı için parantez içinde Hello veri merkezi görüntüler. Merhaba veri merkezinin konumu hello depolama hesabı için aynı hello bulut hizmeti (ortak ayarları) için hello veri merkezinin konumu olarak hello olduğunu önerilir.  
   
Hello Azure depolama hesabı hello paket hello uygulama dağıtımı için depolar. Merhaba uygulama dağıtıldıktan sonra hello paket hello depolama hesabından kaldırılır.

**Hata durumunda dağıtımı Sil** -yayımlama sırasında hatalarla karşılaşılırsa silinen bu seçeneği toohave hello dağıtımını seçin. Bulut hizmetiniz için toomaintain sabit bir sanal IP adresi istiyorsanız bu işaretinin kaldırılması gerekir.

**Dağıtım güncelleştirme** -toodeploy yalnızca güncelleştirilmiş bileşenleri istiyorsanız bu seçeneği belirleyin. Bu dağıtım türünde tam bir dağıtıma göre daha hızlı olabilir. Bulut hizmetiniz için toomaintain sabit bir sanal IP adresi istiyorsanız bu denetlenmesi. 

**Dağıtım güncelleştirmesi - ayarları** -bu iletişim kutusunu kullanılan toofurther nasıl güncelleştirilmiş hello rolleri toobe istediğinizi belirtin. Seçerseniz **Artımlı güncelleştirme**, o hello uygulama her zaman kullanılabilir olacak şekilde her uygulamanızın ardına, güncelleştirilmiş bir örneğidir. Seçerseniz **eşzamanlı güncelleştirme**, uygulamanız tüm örneklerini hello güncelleştirilir aynı anda. Eşzamanlı güncelleştirme hızlıdır ancak hizmetinizi hello güncelleştirme işlemi sırasında kullanılamayabilir. 

![Dağıtım ayarları](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**IntelliTrace'i etkinleştirme** -tooenable IntelliTrace isteyip istemediğinizi belirtin. IntelliTrace ile Azure içinde çalıştığında bir rol örneği için kapsamlı hata ayıklama bilgileri oturum açabilir. Toofind hello bir sorunun nedenini gerekiyorsa, Azure'da çalışıyormuş gibi hello IntelliTrace günlüklerini toostep Visual Studio kodunuzdan aracılığıyla kullanabilirsiniz. IntelliTrace'i kullanma hakkında daha fazla bilgi için bkz: [yayımlanan Azure bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Profil oluşturma etkinleştir** -tooenable performans profili oluşturma isteyip istemediğinizi belirtin. Merhaba Visual Studio profil oluşturucu tooget bulut hizmetinizin nasıl çalışacağını hello hesaplama yönlerini ayrıntılı analizini sağlar. Hello Visual Studio profil oluşturucu kullanma hakkında daha fazla bilgi için bkz: [bir Azure bulut hizmeti hello performansını Test](./vs-azure-tools-performance-profiling-cloud-services.md).

**Uzaktan hata ayıklayıcı tüm roller için etkinleştirme** -tooenable uzaktan hata ayıklama isteyip istemediğinizi belirtin. Visual Studio kullanarak bulut hizmetlerinde hata ayıklama ile ilgili daha fazla bilgi için bkz: [bir Azure bulut hizmeti ya da sanal makineye Visual Studio'da hata ayıklama](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Tanılama Ayarları sayfası

![Tanılama ayarları](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Tanılama tootroubleshoot Azure bulut hizmeti (veya Azure sanal makine) sağlar. Tanılama hakkında daha fazla bilgi için bkz: [yapılandırma tanılama Azure Cloud Services ve sanal makineler için](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Application Insights hakkında daha fazla bilgi için bkz: [Application Insights nedir?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Özet sayfası

![Özet](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Hedef profil** -bir yayımlama profili toocreate seçmiş olduğunuz hello ayarları arasından seçim yapabilirsiniz. Örneğin, bir test ortamı için bir profil ve üretim için başka oluşturabilirsiniz. toosave bu profil, hello seçin **kaydetmek** simgesi. Merhaba Sihirbazı hello profili oluşturur ve hello Visual Studio projesinde kaydeder. toomodify hello profili adı, açık hello **hedef profil** listeleyin ve ardından **< Yönet... >**.
   
   > [!NOTE]
   > Visual Studio'da Çözüm Gezgini'nde yayımlama Hello profili görüntülenir ve hello profil ayarları tooa .azurePubxml uzantılı bir dosyaya yazılır. Ayarları XML etiketleri öznitelik olarak kaydedilir.
   > 
   > 

## <a name="publishing-your-application"></a>Uygulamanızı yayımlama

Projenizin dağıtımı için tüm hello ayarlarını yapılandırdıktan sonra Seç **Yayımla** hello iletişim hello sonundaki. Merhaba hello işlem durumunu izleyebilirsiniz **çıkış** Visual Studio'daki.

## <a name="next-steps"></a>Sonraki adımlar
- [Geçiş ve bir Web uygulaması tooan Visual Studio'dan Azure bulut hizmeti yayımlama](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Nasıl toouse Visual Studio toopublish bir Azure bulut hizmeti öğrenin](./vs-azure-tools-publishing-a-cloud-service.md)
- [Yayımlanan Azure bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Bir Azure bulut hizmeti Hello performansını test etme](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Azure bulut Hizmetleri ve sanal makineler için tanılama yapılandırma](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [Application Insights nedir?](./application-insights/app-insights-overview.md)