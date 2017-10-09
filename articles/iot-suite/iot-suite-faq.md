---
title: aaaAzure IOT paketi ile ilgili SSS | Microsoft Docs
description: "IoT Paketi için sık sorulan sorular"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>IoT Paketi için sık sorulan sorular

Ayrıca bkz.: hello bağlı Fabrika özel [SSS](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Merhaba önceden yapılandırılmış çözümleri hello kaynak kodu nereden bulabilirim?

Merhaba kaynak kodu, GitHub depolarının aşağıdaki hello depolanır:
* [Önceden yapılandırılmış Uzaktan izleme çözümü][lnk-remote-monitoring-github]
* [Önceden yapılandırılmış Tahmine dayalı bakım çözümü][lnk-predictive-maintenance-github]
* [Bağlı Fabrika önceden yapılandırılmış çözümü](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Toohello en son sürümünü kullanan IOT Hub cihaz yönetimi özellikleri hello hello Uzaktan izleme önceden yapılandırılmış çözümün nasıl güncelleştiririm?

* Önceden yapılandırılmış bir çözüm hello https://www.azureiotsuite.com/ sitesinden dağıtırsanız, her zaman hello hello çözümü en son sürümü yeni bir örneğini dağıtır.
* Önceden yapılandırılmış bir çözüm hello komut satırını kullanarak dağıtırsanız, yeni kodu ile var olan bir dağıtıma güncelleştirebilirsiniz. Bkz: [bulut dağıtımı] [ lnk-cloud-deployment] hello GitHub içinde [deposu][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Bir yeni cihaz yöntemi toohello Uzaktan izleme çözümü desteği nasıl ekleyebilir miyim?

Merhaba bölümüne bakın [yeni bir yöntem toohello simulator desteği eklemek] [ lnk-add-method] hello içinde [önceden yapılandırılmış çözümü özelleştirme] [ lnk-customize] makalesi.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>Merhaba sanal cihaz my istenen özellik değişiklikleri neden yoksayılıyor?
Hello çözüm önceden yapılandırılmış Uzaktan izleme, benzetimli hello aygıt kodu yalnızca hello kullanır **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** özellikleri istenen tooupdate hello özellikleri bildirdi. Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Cihazımı hello çözüm panosunda, cihazların Merhaba listesi görünmez neden?

cihazların Merhaba çözüm panosunda Hello listesi sorgu tooreturn hello aygıtların listesini kullanır. Şu anda bir sorgu en fazla 10 K aygıtları döndüremez. Sorgunuzu Hello arama ölçütlerini daha kısıtlayıcı yapmayı deneyin.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Azure portal ve tıklatmak silme azureiotsuite.com önceden yapılandırılmış bir çözüm üzerinde hello kaynak grubunda silinmesi arasındaki hello fark nedir?

* Merhaba önceden yapılandırılmış çözümü silerseniz [azureiotsuite.com][lnk-azureiotsuite], hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm hello kaynakları silin. Ek kaynaklar toohello kaynak grubu eklediyseniz, bu kaynakları da silinir. 
* Merhaba hello kaynak grubunu silerseniz [Azure portal][lnk-azure-portal], yalnızca bu kaynak grubundaki hello kaynakları silin. Hello hello önceden yapılandırılmış çözümde ilişkili toodelete hello Azure Active Directory Uygulama etmeniz [Klasik Azure portalı][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Bir abonelikte kaç IoT Hub örneği sağlayabilirim?

Varsayılan olarak, sağlayabilirsiniz [10 IOT hub'ları abonelik başına][link-azuresublimits]. Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] tooraise bu sınırı. Sağlama too10 yukarı önceden yapılandırılmış çözümleri herhangi bir abonelikte yalnızca bir sonucu olarak, her önceden yapılandırılmış çözüm sağlarken bu yana yeni bir IOT Hub'nı kullanabilirsiniz. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Bir abonelikte kaç Azure Cosmos DB örneği sağlayabilirim?

Elli. Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] tooraise bu sınırlama, ancak varsayılan olarak, abonelik başına 50 Cosmos DB örnekleri yalnızca sağlayabilirsiniz. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Bir abonelikte kaç tane Ücretsiz Bing Haritaları API'si sağlayabilirim?

İki. Bir Azure aboneliğinde Enterprise planları için yalnızca iki adet İç İşlemler Düzey 1 Bing Haritası oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü, varsayılan hello iç işlemleri düzey 1 planıyla tarafından sağlanır. Sonuç olarak, herhangi bir değişiklik yapılmadıysa bir abonelikte çözümlerini izleme uzak tootwo yukarı yalnızca sağlayabilirsiniz.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Statik haritaya sahip bir uzaktan izleme çözümü dağıtımım var; etkileşimli bir Bing haritasını nasıl eklerim?

1. Kurumsal QueryKey için Bing haritaları API'nizi almak [Azure portal][lnk-azure-portal]: 
   
   1. Toohello Kurumsal için Bing haritaları API'nizi hello olduğu kaynak grubu gidin [Azure portal][lnk-azure-portal].
   2. Tıklatın **tüm ayarları**, ardından **anahtar yönetimi**. 
   3. İki anahtar görebilirsiniz: **MasterKey** ve **QueryKey**. Merhaba değerini kopyalayın **QueryKey**.
      
      > [!NOTE]
      > Kurumsal için Bing Haritaları API'si hesabınız yok mu? Merhaba oluşturun [Azure portal] [ lnk-azure-portal] tıklatarak + yeni, Enterprise ve izleme için Bing haritaları API'si arama toocreate ister.
      > 
      > 
2. Merhaba son hello koddan aşağı çekmek [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].
3. Hello deposu hello /docs/ klasöründe hello komut satırı dağıtım rehberini izleyerek dağıtım Bulut veya yerel çalıştırın. 
4. Yerel çalıştırdıktan veya dağıtım, arama, kök klasörünüzde hello için bulut sonra *. user.config file dosyanızı dağıtımı sırasında oluşturulan. Bu dosyayı bir metin düzenleyicisinde açın. 
5. Değişiklik hello aşağıdaki satır kopyaladığınız tooinclude hello değeri, **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>DreamSpark için Microsoft Azure'a sahipsem önceden yapılandırılmış bir çözüm oluşturabilir miyim?

Şu anda önceden yapılandırılmış bir çözüm oluşturamazsınız bir [DreamSpark için Microsoft Azure] [ lnk-dreamspark] hesabı. Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Önceden yapılandırılmış bir çözüm, bulut çözümü sağlayıcısı (CSP) aboneliğiniz varsa oluşturabilir miyim?

Şu anda bir bulut çözümü sağlayıcısı (CSP) aboneliğiyle önceden yapılandırılmış bir çözüm oluşturamazsınız. Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.

### <a name="how-do-i-delete-an-aad-tenant"></a>Bir AAD kiracısını nasıl silerim?

Bkz. Eric Golpe'un blog gönderisi [bir Azure AD Kiracısını silme Kılavuzu][lnk-delete-aad-tennant].

### <a name="next-steps"></a>Sonraki adımlar

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]
* [Önceden yapılandırılmış bağlı Fabrika çözümüne genel bakış](iot-suite-connected-factory-overview.md)
* [Merhaba IOT güvenlikten plan][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
