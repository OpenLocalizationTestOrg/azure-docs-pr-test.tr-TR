---
title: "aaaFind etkinlik raporları hello Azure portalı | Microsoft Docs"
description: "Nasıl toofind Azure Active Directory etkinliği hello Azure portalında raporları öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Etkinlik raporları hello Azure portal Bul

Azure portalında Azure Klasik portalı toohello hello taşıyorsanız, Azure Active Directory (Azure AD) etkinlik günlükleri yeni göz alın. En son içinde [blog gönderisi](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), etkinlik günlükleri hello kaynak üzerinde çalıştığınız hello Azure portal hello bağlamında nasıl görebilirim açıklanmaktadır. Bu makalede, nasıl toofind hello hello Azure portalında Klasik Azure portalında kullanılan raporları açıklanmaktadır.

## <a name="whats-new"></a>Yenilikler

Merhaba Klasik Azure portalı raporlarında kategoriye ayrılır:

1.  Güvenlik raporları
2.  Etkinlik raporları
3.  Tümleşik uygulama raporları

### <a name="activity-and-integrated-app-reports"></a>Etkinlik ve tümleşik uygulama raporları

Bağlam tabanlı hello Azure portalı raporlama için varolan raporları tek bir görünümde birleştirilir. Bir tek, temel alınan API hello veri toohello görünümü sağlar.

Bu görünümü, üzerinde hello toosee **Azure Active Directory** dikey altında **etkinlik**seçin **denetim günlüklerini**.

![Denetim günlükleri](./media/active-directory-reporting-migration/482.png "Denetim günlükleri")

Raporlar aşağıdaki hello bu görünümde birleştirilir:

-   Denetim raporu
-   Parola sıfırlama etkinliği
-   Parola sıfırlama kaydı etkinliği
-   Self Servis Grup etkinliği
-   Office365 grup adı değişikliği
-   Hesap etkinlik sağlama
-   Parola rollover durumu
-   Hesap hazırlama hataları


Merhaba uygulama kullanım raporu geliştirilmiştir ve hello dahil **oturum açma işlemleri** görünümü. Bu görünümü, üzerinde hello toosee **Azure Active Directory** dikey altında **etkinlik**seçin **oturum açma işlemleri**.

![Oturum açma işlemleri Görünüm](./media/active-directory-reporting-migration/483.png "oturum açma işlemleri görüntüleyin")

Merhaba **oturum açma işlemleri** görünümü, tüm kullanıcı oturum açma işlemleri içerir. Bu bilgileri tooget uygulama kullanım bilgileri kullanabilirsiniz. Hello uygulama kullanım bilgilerini de görüntüleyebilirsiniz **kurumsal uygulamalar** genel bakış, hello **Yönet** bölümü.

![Kuruluş uygulamaları](./media/active-directory-reporting-migration/484.png "kurumsal uygulamalar")

## <a name="access-a-specific-report"></a>Belirli bir rapor erişim

Tek bir görünüm Hello Azure portal sunmasına karşın özel raporları da bakabilirsiniz.

### <a name="audit-logs"></a>Denetim günlükleri

Yanıt toocustomer Geribildiriminizi hello Azure portal, Gelişmiş filtreleme tooaccess istediğiniz hello veri kullanabilirsiniz. Kullanabileceğiniz bir filtredir bir *etkinlik kategorisi*, Azure AD'de oturum hangi hello farklı etkinlik türlerini listeler. Aradığınız toowhat toonarrow sonuçları, bir kategori seçin.

Örneğin, yalnızca etkinlikleri ilgili tooself hizmeti parolasını sıfırlar ilgileniyorsanız hello seçebilirsiniz **Self Servis parola yönetimi** kategorisi. gördüğünüz hello kategorileri çalıştığınız hello kaynak dayanır.  

![Merhaba filtre denetim günlüklerini sayfasındaki Kategori seçenekleri](./media/active-directory-reporting-migration/06.png "hello filtre denetim günlüklerini sayfasındaki Kategori seçenekleri")

Etkinlik kategorileri şunlardır:

- Çekirdek Dizin
- Self Servis Parola Yönetimi
- Self Servis Grup Yönetimi
- Hesap Sağlama

### <a name="application-usage"></a>Uygulama kullanımı

tooview hakkında ayrıntılı uygulama kullanım veya tek bir uygulamayı tüm uygulamalar için altında **etkinlik**seçin **oturum açma işlemleri**. toonarrow hello sonuçları, kullanıcı adı veya uygulama adı filtreleyebilir.

![Filtre oturum açma olayları sayfası](./media/active-directory-reporting-migration/07.png "filtre oturum açma olayları sayfası")

### <a name="security-reports"></a>Güvenlik raporları

#### <a name="azure-ad-anomalous-activity-reports"></a>Azure AD anormal etkinlik raporları

Azure AD anormal bir etkinliğin güvenlik hello Klasik Azure portalı raporlardan birleştirilmiş tooprovide olmuştur, bir merkezi görünümü. Bu görünüm, Azure AD algılamak ve raporlama tüm risk güvenlikle ilgili olayları gösterir.

Aşağıdaki tablonun hello hello Azure AD anormal bir etkinliğin güvenlik raporları ve hello Azure portalında karşılık gelen risk olay türlerini listeler.

| Azure AD anormal Etkinlik Raporu |  Kimlik koruması risk olay türü|
| :--- | :--- |
| Sızan kimlik bilgilerine sahip kullanıcılar | Sızan kimlik bilgileri |
| Düzensiz oturum açma etkinliği | Mümkün olmayan seyahat tooatypical konumları |
| Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri | Virüs bulaşmış cihazlardan oturum açma işlemleri|
| Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri | Anonim IP adreslerinden oturum açma işlemleri |
| Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri | Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri |
| - | Alışılmadık konumlardan oturum açma işlemleri |

Azure AD anormal bir etkinliğin güvenlik aşağıdaki hello raporları olmayan hello Azure portal risk olayları eklendi:

* Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri
* Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri

Bu raporlar hello Klasik Azure portalı hala kullanılabildiği ancak bunların bazı zaman hello gelecekteki kullanım dışı kalacaktır.

Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Algılanan risk olayı

Hello Azure portal, hello algılanan risk olayı hakkında raporlarına erişebilir **Azure Active Directory** dikey altında **güvenlik**. Algılanan risk olayı raporları aşağıdaki hello izlenir:   

- Risk altındaki kullanıcılar
- Riskli Oturum Açma İşlemleri

![Güvenlik raporları](./media/active-directory-reporting-migration/04.png "güvenlik raporları")

Güvenlik raporları hakkında daha fazla bilgi için bkz:

- [Risk güvenlik raporu hello Azure Active Directory portalında kullanıcılar](active-directory-reporting-security-user-at-risk.md)
- [Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Merhaba hello Azure portalı ve Azure Klasik portalı etkinlik raporları

Bu bölümdeki Hello tablo hello Klasik Azure portalı içinde varolan raporları listeler. Ayrıca nasıl erişebileceğini açıklanır hello hello Azure portalı, aynı bilgileri.

tooview tüm veri hello denetim **Azure Active Directory** dikey altında **etkinlik**, çok Git**denetim günlüklerini**.

![Denetim günlükleri](./media/active-directory-reporting-migration/61.png "Denetim günlükleri")

| Klasik Azure portalı                 | hello Azure portal toofind                                                         |
| ---                                  | ---                                                                        |
| Denetim günlükleri                           | İçin **etkinlik kategorisi**seçin **çekirdek dizin**.                       |
| Parola sıfırlama etkinliği              | İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**. |
| Parola sıfırlama kaydı etkinliği | İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**.     |
| Self Servis Grup etkinliği         | İçin **etkinlik kategorisi**seçin **Self Servis Grup Yönetimi**.        |
| Hesap etkinlik sağlama        | İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.         |
| Parola rollover durumu             | İçin **etkinlik kategorisi**seçin **otomatik uygulama parolası Rollover**.      |
| Hesap hazırlama hataları          | İçin **etkinlik kategorisi**seçin **kullanıcı hesabı sağlama**.        |
| Office365 grup adı değişikliği         | İçin **etkinlik kategorisi**seçin **Self Servis parola yönetimi**. İçin **etkinlik kaynak türü**seçin **grup**. İçin **etkinlik kaynağı**seçin **O365 grupları**.|

tooview hello **uygulama kullanımı** raporda hello **Azure Active Directory** dikey altında **Yönet**seçin **kurumsal uygulamalar**ve ardından **oturum açma işlemleri**.


![Kuruluş uygulamaları oturum açma işlemleri raporu](./media/active-directory-reporting-migration/199.png "Kurumsal uygulamaları oturum açma işlemleri raporu")

## <a name="next-steps"></a>Sonraki adımlar

Merhaba raporlama genel bakış için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).
