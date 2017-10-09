---
title: "aaaView Azure etkinlik günlükleri toomonitor kaynakları | Microsoft Docs"
description: "Merhaba etkinlik günlükleri tooreview kullanıcı eylemleri ve hataları kullanın. Azure Portal PowerShell, Azure CLI ve REST gösterir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Etkinliği Görüntüle kaynaklardaki tooaudit eylemlerini günlüğe kaydeder
Etkinlik günlükleri, belirleyebilirsiniz:

* hangi işlemlerin aboneliğinizde hello kaynaklar üzerinde gerçekleştirilen
* (bir arka uç hizmeti tarafından başlatılan işlemleri bir kullanıcı olarak hello çağıran döndürmeyen rağmen) hello işlemi kimin başlattığını
* Ne zaman hello işlemi oluştu
* Merhaba işlem Hello durumu
* Merhaba işlemi yardımcı olabilecek diğer özelliklerin değerlerine Hello araştırma

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Merhaba portal, PowerShell, Azure CLI, Öngörüler REST API'si aracılığıyla hello etkinlik günlüklerindeki bilgi almak veya [Öngörüler .NET kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portal
1. tooview hello etkinlik günlükleri hello portal üzerinden seçin **İzleyici**.
   
    ![etkinlik günlükleri seçin](./media/resource-group-audit/select-monitor.png)

   Veya, tooautomatically filtre hello etkinlik günlüğü belirli kaynak veya kaynak grubu, select **etkinlik günlüğü** bu kaynak dikey penceresinden. Bu hello etkinlik günlüğü seçili hello kaynak tarafından otomatik olarak filtrelenir dikkat edin.
   
    ![Kaynağa göre filtrele](./media/resource-group-audit/filtered-by-resource.png)
2. Merhaba, **etkinlik günlüğü** dikey penceresinde, son işlemleri özetini bakın.
   
    ![Eylemler Göster](./media/resource-group-audit/audit-summary.png)
3. toorestrict hello görüntülenen işlemlerinin sayısı farklı koşullar seçin. Örneğin, hello aşağıdaki görüntüde hello gösterir **Timespan** ve **olayı başlatan tarafından** alanları belirli kullanıcı veya uygulamanın hello geçen ay tarafından yapılan tooview hello Eylemler değiştirildi. Seçin **Uygula** tooview hello Sorgunuzun sonuçlarını.
   
    ![filtre seçeneklerini ayarlama](./media/resource-group-audit/set-filter.png)

4. Toorun hello sorgu daha sonra yeniden gereksinim duyarsanız, seçin **kaydetmek** ve hello sorgu bir ad verin.
   
    ![Sorgu kaydetme](./media/resource-group-audit/save-query.png)
5. bir sorgu çalıştırın tooquickly dağıtımları başarısız gibi hello yerleşik sorguları birini seçebilirsiniz.

    ![seçme sorgusu](./media/resource-group-audit/select-quick-query.png)

   Merhaba seçili sorgu gerekli hello filtre değerleri otomatik olarak ayarlar.

    ![Dağıtım hataları görüntüleme](./media/resource-group-audit/view-failed-deployment.png)   

6. Merhaba işlemleri toosee hello olay özetini birini seçin.

    ![Görünüm işlemi](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. Merhaba çalıştırmak tooretrieve günlük girişlerini **Get-AzureRmLog** komutu. Ek parametreler toofilter hello girişlerinin listesini sağlar. Bir başlangıç ve bitiş zamanı belirtmezseniz hello son bir saat girişlerinde döndürülür. Örneğin, bir kaynak grubu için tooretrieve hello işlemleri sırasında hello son bir saat çalıştırın:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Aşağıdaki örneğine hello nasıl toouse hello etkinlik oturum belirtilen süre boyunca gerçekleştirilecek tooresearch işlemleri gösterir. Merhaba başlangıç ve bitiş tarihleri tarih biçiminde belirtilir.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Ya da son 14 gün tarih işlevleri toospecify hello tarih aralığı, hello gibi kullanabilirsiniz.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. Belirttiğiniz hello başlangıç saati bağlı olarak hello önceki komutları işlemleri hello kaynak grubu için uzun bir listesi döndürebilir. Ne arama ölçütlerini sağlayarak aradığınız için hello sonuçları filtreleyebilirsiniz. Örneğin, bir web uygulaması nasıl durduruldu tooresearch çalışıyorsanız, komutu aşağıdaki hello çalıştırabilirsiniz:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    Bu örneğin gösterir durdurma eylemi tarafından gerçekleştirilen someone@contoso.com. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. Hatta artık mevcut bir kaynak grubu için belirli bir kullanıcı tarafından yapılan hello Eylemler arayabilir.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Başarısız işlemler için filtre uygulayabilirsiniz.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Bu girişi için hello durum iletisini bakarak bir hatada odaklanabilirsiniz.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Hangi döndürür:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Azure CLI
* tooretrieve günlük girişlerini, çalıştırdığınız hello **azure Grup günlük Göster** komutu.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>REST API
Merhaba etkinlik günlüğü ile çalışmaya yönelik hello REST işlemlerini hello parçası olan [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx). tooretrieve etkinlik günlüğü olaylarını görme [listesinde bir abonelikte hello Yönetimi olayları](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* Azure etkinlik günlükleri, Power BI toogain fazla öngörü aboneliğinizde hello eylemler hakkında ile kullanılabilir. Bkz: [Görünüm ve Power BI ve daha fazla Azure etkinlik günlüklerini analiz edin](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).
* güvenlik ilkelerini ayarlama hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).
* toolearn dağıtım işlemlerini görüntülemek için hello komutlar hakkında bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
* tooprevent silme tüm kullanıcılar için bir kaynakta nasıl görürüm toolearn [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).

