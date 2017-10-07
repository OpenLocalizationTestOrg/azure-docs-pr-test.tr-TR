---
title: "roller, izinleri ve güvenlik Azure İzleyicisi ile aaaGet kullanmaya | Microsoft Docs"
description: "Nasıl toouse Azure monitörün yerleşik rolleri ve izinleri toorestrict toomonitoring kaynaklara öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Roller, izinleri ve güvenlik Azure İzleyicisi ile kullanmaya başlama
Birçok ekip toostrictly gerek toomonitoring verilere erişmek ve ayarları düzenlemek. Örneğin, özel olarak (destek mühendisleri, devops mühendisleri) izleme üzerinde çalışan takım üyeleri varsa veya bir yönetilen hizmet sağlayıcısı kullanıyorsanız, bunların özelliği toocreate kısıtlama sırasında izleme verilerini tooonly erişmesine toogrant isteyebilirsiniz değiştirebilir veya kaynakları silin. Bu makalede nasıl tooquickly azure'da yerleşik izleme RBAC rolü tooa kullanıcı uygulamak veya kendi özel rol sınırlı izleme izinleri gereken kullanıcılar için yapı gösterilmektedir. Ardından Azure İzleyici ilgili kaynaklarınız için güvenlik konuları açıklanır ve erişim toohello verileri sınırlayabilirsiniz nasıl içerirler.

## <a name="built-in-monitoring-roles"></a>Yerleşik izleme roller
Azure monitörün yerleşik roller tasarlanmış toohelp sınırı erişim tooresources hala olanlar etkinleştirme sırasında bir abonelikte altyapı tooobtain izlemekten sorumlu ve ihtiyaç duydukları hello verilere yapılandırın. Azure İzleyicisi, iki Giden kutusu rolleri sağlar: bir izleme okuyucu ve izleme katılımcı.

### <a name="monitoring-reader"></a>Okuyucu izleme
Merhaba izleme okuyucu rolüne atanan kişi bir Abonelikteki tüm izleme verilerini görüntülemek ancak herhangi bir kaynağa değiştiremez veya tüm ayarları ilgili toomonitoring kaynakları düzenleyin. Bu rol, toobe yapabileceksiniz isteyen desteği veya işlem mühendisleri gibi bir kuruluştaki kullanıcılar için uygundur:

* Merhaba Portalı'nda izleme panoları görüntülemek ve kendi özel izleme panolar oluşturun.
* Sorgu hello kullanarak ölçümünün [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlet'leri](insights-powershell-samples.md), veya [platformlar arası CLI](insights-cli-samples.md).
* Sorgu hello etkinlik günlüğü hello portalı, Azure İzleyici REST API'si, PowerShell cmdlet'leri veya platformlar arası CLI kullanarak.
* Görünüm hello [tanılama ayarlarını](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) bir kaynak için.
* Görünüm hello [oturum profili](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) aboneliği.
* Otomatik ölçeklendirme ayarlarını görüntüleyin.
* Uyarı etkinliği görüntüle ve ayarlar.
* Application Insights verilere erişmek ve veri AI analizleri görüntüleyin.
* Günlük analizi (OMS) çalışma veri hello çalışma alanı için kullanım verilerini de dahil olmak üzere arayın.
* Günlük analizi (OMS) yönetim grupları görüntüleyin.
* Merhaba günlük analizi (OMS) arama şemasını alın.
* Günlük analizi (OMS) Intelligence paketlerini listeler.
* Almak ve günlük analizi (OMS) kayıtlı aramalar yürütün.
* Merhaba günlük analizi (OMS) depolama yapılandırmasını alır.

> [!NOTE]
> Bu rol, akış tooan olay hub'ı veya bir depolama hesabında depolanan okuma erişimi toolog veri sağlamaz. [Aşağıya bakın](#security-considerations-for-monitoring-data) toothese kaynaklarına erişim yapılandırma hakkında bilgi için.
> 
> 

### <a name="monitoring-contributor"></a>Katkıda bulunan izleme
Atanan kişi hello izleme katkıda bulunan rolü için bir Abonelikteki tüm izleme verilerini görüntülemek ve oluşturmak veya izleme ayarlarını değiştirmek, ancak diğer kaynakları değiştiremezsiniz. Bu rolü hello izleme okuyucu rolüne bir üst kümesidir ve kuruluşun izleme takım veya isteyen, ayrıca yukarıdaki toohello izinleri de toobe için Yönetilen hizmet sağlayıcıları üyeleri için uygundur:

* İzleme panoları paylaşılan Pano olarak yayımlayın.
* Ayarlama [tanılama ayarlarını](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) bir resource.* için
* Set hello [oturum profili](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) bir subscription.* için
* Uyarı etkinliği ve ayarları ayarlayın.
* Application Insights web testleri ve bileşenleri oluşturun.
* Günlük analizi (OMS) paylaşılan çalışma alanı anahtarlarının listesi.
* Etkinleştirmek veya devre dışı günlük analizi (OMS) Intelligence paketleri.
* Oluşturma ve silme ve günlük analizi (OMS) kayıtlı aramalar çalıştırın.
* Oluşturun ve hello günlük analizi (OMS) depolama yapılandırması silin.

* Kullanıcı ayrıca hello hedef kaynak (depolama hesabı veya olay hub'ad alanı) tooset günlük profili veya tanılama ayarını ListKeys iznine sahip olmanız gerekir.

> [!NOTE]
> Bu rol, akış tooan olay hub'ı veya bir depolama hesabında depolanan okuma erişimi toolog veri sağlamaz. [Aşağıya bakın](#security-considerations-for-monitoring-data) toothese kaynaklarına erişim yapılandırma hakkında bilgi için.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>İzinler ve özel RBAC rolleri izleme
Yerleşik roller yukarıda Hello hello tam ekibinizin ihtiyaçlarını karşılamıyorsa, aşağıdakileri yapabilirsiniz [özel RBAC rolü oluşturma](../active-directory/role-based-access-control-custom-roles.md) daha ayrıntılı izinlere sahip. Aşağıda hello açıklamalarının ortak Azure İzleyici RBAC işlemleriyle verilmiştir.

| İşlem | Açıklama |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, yazma, silme] |Okuma/yazma/silme uyarı kuralları. |
| Microsoft.Insights/AlertRules/Incidents/Read |Olaylar (Merhaba uyarı kuralı tetiklenen geçmişini) için uyarı kuralları listesi. Bu, yalnızca toohello portal geçerlidir. |
| Microsoft.Insights/AutoscaleSettings/[Read, yazma, silme] |Okuma/yazma/silme otomatik ölçeklendirme ayarları. |
| Microsoft.Insights/DiagnosticSettings/[Read, yazma, silme] |Okuma/yazma/silme tanılama ayarları. |
| Microsoft.Insights/eventtypes/digestevents/Read |Bu izin, tooActivity günlükleri hello Portalı aracılığıyla erişen kullanıcılar için gereklidir. |
| Microsoft.Insights/eventtypes/values/Read |Bir abonelikte etkinlik günlüğü olayları (Yönetim olayları) listeler. Bu izni geçerli tooboth programlı ve portal erişim toohello etkinlik günlüğü yok. |
| Microsoft.Insights/LogDefinitions/Read |Bu izin, tooActivity günlükleri hello Portalı aracılığıyla erişen kullanıcılar için gereklidir. |
| Microsoft.Insights/MetricDefinitions/Read |Ölçüm tanımlarını (bir kaynak için kullanılabilir ölçüm türlerinin listesi) okuyun. |
| Microsoft.Insights/Metrics/Read |Bir kaynak için ölçümleri okuyun. |

> [!NOTE]
> Erişim tooalerts, tanılama ayarlarını ve ölçümleri bir kaynak için okuma erişimi toohello kaynak türü ve bu kaynağın kapsamını hello kullanıcının sahip gerektirir. ("Yazma") oluşturma arşivler tooa depolama hesabı veya akışları tooevent hub hello kullanıcı tooalso gerektiren bir tanılama ayarı ya da günlük profili ListKeys izninizin olması hello hedef kaynak üzerindeki.
> 
> 

Örneğin, yukarıdaki tabloda hello kullanarak bir "etkinlik günlüğü okuyucusu" şöyle için özel bir RBAC rolü oluşturabilirsiniz:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Verilerin izlenmesi için güvenlik konuları
İzleme verilerini — özellikle günlük dosyalarını — IP adresleri veya kullanıcı adları gibi gizli bilgiler içerebilir. İzleme verilerini Azure üç temel formlarında gelir:

1. Merhaba, Azure aboneliğinizde tüm denetim düzlemi eylemleri açıklar etkinlik günlüğü.
2. Tanılama günlükleri, bir kaynak tarafından gösterilen günlükleri.
3. Kaynaklar tarafından gösterilen ölçümleri.

Bu veri türlerini üç bir depolama hesabında depolanan veya tooEvent Hub, her ikisi de genel amaçlı Azure kaynaklardır akışı. Bu genel amaçlı kaynaklar olduğundan, oluşturma, silme ve bunlara erişmek için bir yönetici genellikle ayrılmış ayrıcalıklı bir işlemdir. İzleme ile ilgili kaynaklara tooprevent kötüye kullanılması için yöntemler aşağıdaki hello kullanmanızı öneririz:

* Bir tek, özel bir depolama hesabı verileri izlemek için kullanın. Birden çok depolama hesaplarına veri izleme verilerini tooseparate ihtiyacınız varsa, hiçbir zaman izleme arasında bir depolama hesabı kullanımı paylaşabilir ve bu olarak izleme olmayan veri yanlışlıkla yalnızca (ör. toomonitoring veri erişimi olanlar verebilir bir üçüncü taraf SIEM) toonon izleme veri erişim.
* Tek ve özel bir hizmet veri yolu veya olay hub'ın ad tüm tanılama ayarları arasında aynı yukarıdaki neden hello için kullanın.
* Sınırlamak erişim toomonitoring ilgili depolama hesapları veya olay hub'ları farklı bir kaynak grubunda tutarak ve [kapsamı kullan](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) izleme rollerinizi toolimit erişim tooonly bu kaynak grubu.
* Hiçbir zaman bir kullanıcı yalnızca erişim toomonitoring verilere ihtiyaç duyduğunda depolama hesapları veya olay hub'ları abonelik kapsamında hello ListKeys izni verin. (Ayrılmış bir izleme kaynak grubu varsa) Bu izinler toohello kullanıcı bir kaynak veya kaynak grubu, bunun yerine, vermek kapsamı.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Sınırlama erişim toomonitoring ilgili depolama hesapları
Bir kullanıcı veya uygulama toomonitoring veri depolama hesabındaki erişim oluştururken, aşağıdakileri yapmalısınız [bir hesap SAS oluşturmak](https://msdn.microsoft.com/library/azure/mt584140.aspx) hizmet düzeyi salt okunur erişim tooblob depolama ile izleme verileri içeren hello depolama hesabı üzerinde. PowerShell'de, bunu aşağıdaki gibi görünmelidir:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Bu depolama hesabından tooread gereken hello belirteci toohello varlık sonra verebilirsiniz ve listelemek ve o depolama hesabındaki tüm BLOB'lar okuma.

Alternatif olarak, bu izne sahip RBAC toocontrol gerekiyorsa, bu varlık hello bu belirli depolama hesabındaki Microsoft.Storage/storageAccounts/listkeys/action izni verebilirsiniz. Bu, toobe mümkün tooset tanılama ayarı ya da günlük profili tooarchive tooa depolama hesabı olması gereken kullanıcılar için gereklidir. Örneğin, bir kullanıcı veya bir depolama hesabından tooread yeterlidir uygulama için özel RBAC rolü aşağıdaki hello oluşturabilirsiniz:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Merhaba ListKeys izni hello kullanıcı toolist hello birincil ve ikincil depolama hesabı anahtarları sağlar. Bu anahtarları hello kullanıcı tüm imzalı izinleri verin (okuma, yazma, BLOB'ları oluşturmak, silmek BLOB'lar vb.) tüm hizmetleri (blob, kuyruk, tablo, dosya), depolama hesabındaki imzalanmış. Mümkün olduğunda yukarıda açıklanan bir hesap SAS kullanılmasını öneririz.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Sınırlama erişim toomonitoring ilgili olay hub'ları
Event hubs ile benzer bir desen izlenebilir ancak ilk toocreate bir adanmış dinleme yetkilendirme kuralı gerekir. Toolisten toomonitoring ilgili olay hub'ları yeterlidir toogrant erişim tooan uygulama istiyorsanız, aşağıdaki hello:

1. Yalnızca dinleme talepleri ile izleme verilerini akış için oluşturulan hello olay ölçeklendirecek bir paylaşılan erişim ilkesi oluşturun. Bu hello Portalı'nda yapılabilir. Örneğin, "monitoringReadOnly." çağırabilirsiniz Mümkünse, doğrudan toohello tüketici anahtarı ve hello sonraki adımı atlayın toogive isteyeceksiniz.
2. Merhaba tüketici toobe mümkün tooget hello anahtar geçici gerekiyorsa, bu olay hub'ın hello kullanıcı hello ListKeys eylemi verin. Bu ayrıca toobe mümkün tooset tanılama ayarını gerekir veya profil toostream tooevent hub oturum kullanıcılar için gereklidir. Örneğin, bir RBAC kuralı oluşturabilirsiniz:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Sonraki adımlar
* [RBAC ve izinlerini Kaynak Yöneticisi'ni okuyun](../active-directory/role-based-access-control-what-is.md)
* [Azure'da izleme okuma hello genel bakış](monitoring-overview.md)

