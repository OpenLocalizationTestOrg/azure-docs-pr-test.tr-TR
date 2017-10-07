---
title: "Azure Application Insights aaaResources, rolleri ve erişim denetimi | Microsoft Docs"
description: "Sahipleri, Katkıda Bulunanlar ve okuyucular, kuruluşunuzun Öngörüler."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Kaynaklar, rolleri ve erişim denetimi Application Insights
Kim okuma ve güncelleştirme erişim tooyour verilerini azure'da denetleyebilirsiniz [Application Insights][start], kullanarak [Microsoft Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Merhaba, erişim toousers atamak **kaynak grubuna veya aboneliğe** uygulama kaynağınızı ait - değil hello kaynağında kendisini toowhich. Merhaba atamak **Application Insights bileşen katkıda bulunan** rol. Bu erişim tooweb testleri ve uygulama kaynağınızı birlikte uyarıları Tekdüzen denetim sağlar. [Daha fazla bilgi edinin](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Kaynaklar, gruplar ve abonelikleri
İlk olarak, bazı tanımları:

* **Kaynak** - Microsoft Azure hizmet örneğini bir. Application Insights kaynağınıza toplar, çözümler ve uygulamanızdan gönderilen hello telemetri verilerini görüntüler.  Web uygulamaları, veritabanları ve VM'ler Azure kaynaklarını diğer türleri içerir.
  
    Kaynaklarınızın toosee açmak hello [Azure Portal][portal], oturum açın ve tüm kaynaklar'ı tıklatın. toofind bir kaynak türü adını hello filtre alanına parçası.
  
    ![Azure kaynak listesi](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Kaynak grubu** ] [ group] -tooone grubun her kaynağa ait. Bir grup kullanışlı olduğu şekilde toomanage ilgili erişim denetimi için özellikle kaynakları. Örneğin, tek bir kaynak grubu bir Web uygulaması, bir Application Insights kaynağı toomonitor hello uygulama ve depolama kaynak tookeep koyabilirsiniz verileri dışarı.

    ![Gözat, kaynak grupları belirtin, sonra bir grup seçin](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Abonelik** ](https://manage.windowsazure.com) -toouse Application Insights veya diğer Azure kaynaklarına, oturum tooan Azure aboneliği. Her kaynak grubu tooone fiyat paketinizi seçin ve burada, bir kuruluşun abonelik ise hello üyeleri ve bunların erişim izinlerini seçmeniz Azure aboneliği aittir.
* [**Microsoft hesabı** ] [ account] -hello kullanıcı adı ve parola tooMicrosoft Azure toosign kullanmak abonelikler, XBox Live, Outlook.com ve diğer Microsoft Hizmetleri.

## <a name="access"></a>Merhaba kaynak grubunda erişimi denetleme
Toplama toohello kaynak uygulamanız için oluşturduğunuz olduğunu da uyarıları ve web testleri için gizli kaynaklar ayrı önemli toounderstand olur. Ekli toohello oldukları aynı [kaynak grubu](#resource-group) uygulamanız. Ayrıca diğer Azure hizmetleriyle gibi Web sitesi ya da depolama burada konumuna.

![Application Insights kaynakları](./media/app-insights-resources-roles-access-control/00-resources.png)

toocontrol erişim toothese kaynaklar için önerilir:

* Denetim hello erişim **kaynak grubuna veya aboneliğe** düzeyi.
* Merhaba atamak **uygulama Öngörüler bileşeni katkıda bulunan** rol toousers. Bu tooedit web testleri, uyarılar ve Application Insights kaynaklara erişim tooany hello grubundaki diğer hizmetler sağlamadan sağlar.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide tooanother kullanıcıya erişim
Sahibi hakları toohello abonelik veya hello kaynak grubu olması gerekir.

Merhaba kullanıcı olmalıdır bir [Microsoft Account][account], veya tootheir erişim [kuruluş Microsoft Account](../active-directory/sign-up-organization.md). Erişim tooindividuals ve toouser grupları Azure Active Directory'de tanımlı sağlayabilir.

#### <a name="navigate-toohello-resource-group"></a>Toohello kaynak grubuna gidin
Merhaba kullanıcı ekleyin.

![Uygulamanızın kaynak dikey penceresinde, Essentials'ı açın, hello kaynak grubu açın ve var. ayarları/kullanıcılar'ı seçin. Ekle'ye tıklayın.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Veya başka düzeyi gidin ve hello kullanıcı toohello abonelik ekleyin.

#### <a name="select-a-role"></a>Rol seçin
![Merhaba yeni kullanıcı için bir rol seçin](./media/app-insights-resources-roles-access-control/03-role.png)

| Rol | Merhaba kaynak grubunda |
| --- | --- |
| Sahip |Kullanıcı erişim dahil her şeyi değiştirebilir |
| Katılımcı |Tüm kaynaklar da dahil olmak üzere her şeyi düzenleyebilirsiniz |
| Uygulama Öngörüler bileşen katkıda bulunan |Application Insights kaynaklara, web testleri ve Uyarıları düzenleyebilirsiniz |
| Okuyucu |Görüntüleyebilir, ancak değişikliği değil |

'Düzenleme' oluşturma, silme ve güncelleştirme içerir:

* Kaynaklar
* Web testleri
* Uyarılar
* Sürekli dışarı aktarma

#### <a name="select-hello-user"></a>Merhaba kullanıcıyı seçin

İstediğiniz hello kullanıcı hello dizininde değilse, bir Microsoft hesabı olan herkes davet edebilirsiniz.
(Bunlar Outlook.com, OneDrive, Windows Phone veya XBox LIVE gibi hizmetleri kullanıyorsanız, bunlar bir Microsoft hesabınız vardır.)

## <a name="related-content"></a>İlgili içerik

* [Rol tabanlı erişim denetimi Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
