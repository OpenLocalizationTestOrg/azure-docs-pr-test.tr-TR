---
title: "aaaCreate ve karma bağlantılar yönetme | Microsoft Docs"
description: "Nasıl toocreate karma bir bağlantı hello bağlantıyı yönetmek ve hello karma Bağlantı Yöneticisi'ni yüklemek öğrenin. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Karma Bağlantıları Oluşturma ve Yönetme

> [!IMPORTANT]
> BizTalk Karma Bağlantılar kullanımdan kalktı ve yerine App Service Karma Bağlantılar kullanıma sunuldu. Daha fazla bilgi için mevcut BizTalk karma bağlantılar nasıl toomanage bakın dahil olmak üzere [Azure App Service karma bağlantılar](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Merhaba adımlara genel bakış
1. Karma bağlantı hello girerek oluşturabilirsiniz **ana bilgisayar adı** veya **FQDN** özel ağınızda hello şirket içi kaynağının.
2. Azure web uygulamaları veya Azure mobil uygulamalar toohello karma bağlantı bağlayın.
3. Şirket içi kaynakta Hello karma Bağlantı Yöneticisi'ni yükleyin ve toohello bağlanmak belirli karma bağlantı. Hello Azure portalında bir tek tıklamalı deneyimi tooinstall sağlar ve bağlanın.
4. Karma bağlantılar ve bağlantı anahtarları yönetin.

Bu konu, aşağıdaki adımları listeler. 

> [!IMPORTANT]
> Bu, olası tooset bir karma bağlantı uç noktası tooan IP adresi olur. Bir IP adresi kullanırsanız, olabilir veya hello şirket içi kaynağa bağlı olarak, istemci ulaşabilir değil. Merhaba karma bağlantı DNS araması yaparsanız hello istemcide bağlıdır. Çoğu durumda, hello **istemci** uygulama kodunuz. Merhaba, istemci DNS araması gerçekleştirmez, (bir etki alanı adı (x.x.x.x) değilmiş gibi onu tooresolve başlangıç IP adresi denemez), trafik hello karma bağlantı gönderilmez.
> 
> Sahte (kod) örneğin tanımladığınız **10.4.5.6** , şirket içi ana bilgisayarı olarak:
> 
> **Senaryo works aşağıdaki hello:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **Senaryo aşağıdaki hello çalışmıyor:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Karma bağlantı oluşturma
Web uygulamaları kullanarak Azure portalında karma bağlantı hello oluşturulabilmesi için **veya** BizTalk Services'ı kullanarak. 

**toocreate Web uygulamalarını kullanarak karma bağlantılar**, bkz: [bağlanmak Azure Web Apps tooan şirket içi kaynağa](../app-service-web/web-sites-hybrid-connection-get-started.md). Ayrıca, tercih edilen hello yöntemi olan web uygulamasından hello karma Bağlantı Yöneticisi (HCM) yükleyebilirsiniz. 

**Karma bağlantılar BizTalk Services toocreate**:

1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Merhaba sol gezinti bölmesinde seçin **BizTalk Services** ve BizTalk hizmetinizi seçin. 
   
    Mevcut bir BizTalk hizmetini yoksa, şunları yapabilirsiniz [BizTalk hizmeti oluşturma](biztalk-provision-services.md).
3. Select hello **karma bağlantılar** sekmesi:  
   ![Karma bağlantılar sekmesi][HybridConnectionTab]
4. Seçin **karma bir bağlantı oluşturmak** veya select hello **ekleme** hello görev çubuğu düğmesini. Merhaba aşağıdakileri girin:
   
   | Özellik | Açıklama |
   | --- | --- |
   | Ad |Merhaba karma adı benzersiz olmalıdır ve hello olamaz bağlantı aynı BizTalk hizmeti hello adlandırın. Herhangi bir ad girin, ancak amacı ile belirli. Örneklere şunlar dahildir:<br/><br/>Bordro*SQLServer*<br/>SupplyList*SharepointServer*<br/>Müşteriler*OracleServer* |
   | Ana bilgisayar adı |Merhaba tam ana bilgisayar adı, yalnızca hello ana bilgisayar adını girin veya hello şirket içi kaynağa IPv4 adresini hello. Örneklere şunlar dahildir:<br/><br/>(sqlsunucum)<br/>*(sqlsunucum)*. *Etki alanı*. corp.*şirketiniz*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*. *Şirketiniz*.com<br/>10.100.10.10<br/><br/>Başlangıç IPv4 adresi kullanırsanız, istemci veya uygulama kodunuz hello IP adresi çözebilir değil olduğunu unutmayın. Merhaba önemli bkz, bu konunun hello üstünde Not. |
   | Bağlantı noktası |Merhaba şirket içi kaynağa Hello bağlantı noktası numarasını girin. Örneğin, Web uygulamaları kullanıyorsanız, bağlantı noktası 80 veya 443 numaralı bağlantı noktasını girin. SQL Server kullanıyorsanız, 1433 numaralı bağlantı noktasını girin. |
5. Merhaba onay işareti toocomplete hello Kurulumu öğelerini seçin. 

#### <a name="additional"></a>Ek
* Birden çok karma bağlantılar oluşturulabilir. Merhaba bkz [BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md) hello izin verilen bağlantı sayısı. 
* Her bir karma bağlantı için bağlantı dizeleri bir çift oluşturulur: uygulama anahtarları DİNLEME, gönderme ve şirket içi anahtarları. Her bir çifti birincil ve ikincil anahtar vardır. 

## <a name="LinkWebSite"></a>Azure App Service Web uygulaması veya mobil uygulama bağlama
Karma bağlantı, mevcut Azure App Service tooan içinde toolink bir Web uygulaması veya mobil uygulama seçin **varolan karma bağlantıyı kullan** hello karma bağlantılar dikey penceresinde. Bkz: [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>İçi karma Bağlantı Yöneticisi Hello yükleyin
Karma bağlantı oluşturulduktan sonra hello şirket içi kaynağa hello karma Bağlantı Yöneticisi'ni yükleyin. Azure web uygulamaları ya da BizTalk hizmetinizi indirilebilir. BizTalk Services adımlar: 

1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Merhaba sol gezinti bölmesinde seçin **BizTalk Services** ve BizTalk hizmetinizi seçin. 
3. Select hello **karma bağlantılar** sekmesi:  
   ![Karma bağlantılar sekmesi][HybridConnectionTab]
4. Merhaba görev çubuğunda seçin **şirket içi Kurulum**:  
   ![Şirket içi Kurulumu][HCOnPremSetup]
5. Seçin **yükleme ve yapılandırma** toorun ya da indirme hello karma Bağlantı Yöneticisi hello şirket içi sistem. 
6. Merhaba onay işareti toostart hello yüklemeyi seçin. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Ek
* Karma Bağlantı Yöneticisi üzerinde işletim sistemleri aşağıdaki hello yüklenebilir:
  
  * Windows Server 2008 R2 (.NET Framework 4.5 + ve Windows Management Framework 4.0 + gerekli)
  * Windows Server 2012 (Windows Management Framework 4.0 + gerekli)
  * Windows Server 2012 R2
* Merhaba karma Bağlantı Yöneticisi'ni yükledikten sonra hello şunlar olur: 
  
  * Hello karma Azure üzerinde barındırılan bağlantı otomatik olarak yapılandırılan toouse hello birincil uygulama bağlantı dizesi değil. 
  * Merhaba şirket içi kaynak otomatik olarak yapılandırılan toouse hello birincil şirket içi bağlantı dizesi değil.
* Merhaba karma Bağlantı Yöneticisi geçerli şirket içi bağlantı dizesi yetkilendirme için kullanmanız gerekir. Geçerli uygulama bağlantı dizesi, Hello Azure Web uygulaması veya mobil uygulama yetkilendirme için kullanmanız gerekir.
* Karma bağlantılar, başka bir sunucuya başka bir örneği hello karma Bağlantı Yöneticisi'ni yükleyerek ölçeklendirebilirsiniz. Aynı adresi hello şirket içi dinleyici toouse hello hello ilk şirket içi dinleyicisi olarak yapılandırın. Bu durumda, hello rastgele dağıtılmış (hepsini bir kez) arasında hello etkin şirket içi dinleyicileri trafiğidir. 

## <a name="ManageHybridConnection"></a>Karma bağlantılar yönetme
toomanage, karma bağlantılar şunları yapabilirsiniz:

* Hello Azure portal kullanın ve tooyour BizTalk hizmeti gidin. 
* Kullanım [REST API'leri](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Kopyala/yeniden hello karma bağlantı dizeleri
1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Merhaba sol gezinti bölmesinde seçin **BizTalk Services** ve BizTalk hizmetinizi seçin. 
3. Select hello **karma bağlantılar** sekmesi:  
   ![Karma bağlantılar sekmesi][HybridConnectionTab]
4. Merhaba karma bağlantıyı seçin. Merhaba görev çubuğunda seçin **bağlantıyı Yönet**:  
   ![Seçeneklerini yönetin][HCManageConnection]
   
    **Bağlantıyı Yönet** listeleri hello uygulama ve şirket içi bağlantı dizeleri. Hello bağlantı dizeleri kopyalama veya erişim tuşu hello bağlantı dizesinde kullanılan hello yeniden oluşturun. 
   
    **Yeniden seçerseniz**, paylaşılan erişim bağlantı dizesi değiştirildiğinde hello içinde kullanılan anahtar hello. Aşağıdaki hello:
   
   * Hello Klasik Azure portalı, seçin **anahtarları Eşitle** hello Azure uygulamanızı içinde.
   * Merhaba yeniden Çalıştır **şirket içi Kurulum**. Hello yeniden çalıştırdığınızda, şirket içi kurulumu, otomatik olarak şirket içi kaynaktır hello toouse güncelleştirilmiş hello birincil bağlantı dizesi yapılandırıldı.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Grup İlkesi toocontrol hello içi karma bağlantı tarafından kullanılan kaynakları
1. Merhaba karşıdan [karma Bağlantı Yöneticisi Yönetim Şablonları](http://www.microsoft.com/download/details.aspx?id=42963).
2. Merhaba dosyaları ayıklayın.
3. Grup İlkesi değiştirir hello bilgisayarda aşağıdaki hello:  
   
   * Merhaba kopyalayın. ADMX dosyalarını toohello *%WINROOT%\PolicyDefinitions* klasör.
   * Merhaba kopyalayın. ADML dosyaları toohello *%WINROOT%\PolicyDefinitions\en-us* klasör.

Kopyalandıktan sonra Grup İlkesi Düzenleyicisi'ni toochange hello İlkesi kullanabilirsiniz.

## <a name="next"></a>Sonraki
[Azure Web Apps tooan bağlanmak şirket içi kaynak](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Azure Web uygulamaları tooon içi SQL Server'a bağlanma](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Karma bağlantılara genel bakış](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Microsoft Azure BizTalk hizmetlerinin yönetilmesi için REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[BizTalk Services: Sürümler Grafiği](biztalk-editions-feature-chart.md)  
[Klasik Azure portalını kullanarak BizTalk hizmeti oluşturma](biztalk-provision-services.md)  
[BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
