---
title: "aaaAzure Active Directory denetim API Başvurusu | Microsoft Docs"
description: "Tooget hello Azure Active Directory denetim API'si ile çalışmaya nasıl"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Azure Active Directory denetim API Başvurusu
Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.  
Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess denetim veri sağlayan bir API ile sağlar.
Bu konunun Hello kapsamı olan tooprovide hello hakkında başvuru bilgileri sizinle **API denetim**.

Bkz.:

* [Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için

* [Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.


İçin:

- Sık sorulan sorular, okuma bizim [SSS](active-directory-reporting-faq.md) 

- Sorunları, lütfen [bir destek bileti dosya](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Merhaba veri erişebilecek mi?
* Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar
* Genel Yöneticiler
* Yetkilendirme tooaccess hello API sahip herhangi bir uygulama (app yetkilendirme olabilir Kurulum genel yöneticinin iznine dayanılarak yalnızca)

## <a name="prerequisites"></a>Ön koşullar
Bu rapor aracılığıyla sipariş tooaccess içinde raporlama API'si Merhaba, sahip olmanız gerekir:

* Bir [Azure Active Directory ücretsiz ya da daha iyi edition](active-directory-editions.md)
* Tamamlanan hello [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Merhaba API'sine erişim
Bu API hello erişebilirsiniz [Graph Explorer'a](https://graphexplorer2.cloudapp.net) veya program aracılığıyla, örneğin, PowerShell kullanarak. Sırayla PowerShell toocorrectly yorumlamak için AAD grafik REST çağrılarında kullanılan hello OData filtresi sözdizimi hello backtick kullanmanız gerekir (diğer adıyla: Vurgu) çok "kaçış karakteri" Merhaba $ karakteri. Merhaba backtick karakter görür [PowerShell'in kaçış karakteri](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo hello $ karakteri değişmez değer yorumu izin verme ve PowerShell değişken adı olarak kafa karıştırıcı kaçının (IE: $filter).

Bu konunun Hello odak Graph Explorer'a hello üzerinde noktasıdır. Bu PowerShell örnek için bkz [PowerShell Betiği](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>API uç noktası
Bu API URI aşağıdaki hello kullanarak erişebilirsiniz:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

(OData sayfalandırma kullanarak) hello Azure AD denetim API'si tarafından döndürülen kayıt hello sayısına bir sınır yoktur.
Bekletme sınırları veri raporlama, kullanıma [raporlama bekletme ilkeleri](active-directory-reporting-retention.md).

Bu çağrı hello verileri toplu olarak döndürür. Her toplu işlem en fazla 1000 kaydı var.  
tooget hello sonraki toplu kayıt, kullanım hello sonraki bağlantı. Merhaba skiptoken bilgi hello ilk döndürülen kayıt kümesinden alın. Merhaba Atla belirteci hello hello sonuç kümesinin sonunda olacaktır.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Desteklenen filtreler
Bir API tarafından döndürülen kayıt sayısını hello daraltabilirsiniz bir filtre formda çağırın.  
Oturum açma için API ilgili veriler, filtreleri aşağıdaki hello desteklenir:

* **$top =\<döndürülen kayıt toobe sayısı\>**  -toolimit hello döndürülen kayıt sayısı. Bu pahalı bir işlemdir. Nesnelerin tooreturn binlerce istiyorsanız bu filtre kullanmamanız gerekir.     
* **$filter =\<filtre ifadesi\>**  -desteklenen filtre alanlarının önem verdiğiniz kayıtların hello türünü hello temelinde toospecify

## <a name="supported-filter-fields-and-operators"></a>Desteklenen filtre alanları ve işleçleri
İlgilendiğiniz kayıtları toospecify hello türü, bir veya filtre alanları aşağıdaki hello bir birleşimini içerebilir bir filtre ifadesi oluşturabilirsiniz:

* [Tarihi](#activitydate) -bir tarih veya tarih aralığı tanımlar
* [Kategori](#category) -üzerinde toofilter istediğiniz hello kategorisini tanımlar.
* [activityStatus](#activitystatus) -bir etkinlik hello durumunu tanımlar
* [activityType](#activitytype) -bir etkinlik hello türünü tanımlar
* [Etkinlik](#activity) -dize olarak hello etkinlik tanımlar  
* [Aktör/adı](#actorname) -hello aktör'ın adı biçiminde hello aktör tanımlar
* [Aktör/objectID](#actorobjectid) -hello aktör'ın kimliği biçiminde hello aktör tanımlar   
* [Aktör/upn](#actorupn) -hello aktör'ın kullanıcı asıl adı (UPN) biçiminde hello aktör tanımlar 
* [Hedef/adı](#targetname) -hello aktör'ın adı biçiminde hello hedef tanımlar
* [Hedef/objectID](#targetobjectid) -hello hedefin kimliği biçiminde hello hedef tanımlar  
* [Hedef/upn](#targetupn) -hello aktör'ın kullanıcı asıl adı (UPN) biçiminde hello aktör tanımlar   

- - -
### <a name="activitydate"></a>Tarihi
**İşleçler desteklenen**: eq, ge, le, gt, lt

**Örnek**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Notlar**:

DateTime UTC biçiminde olmalıdır

- - -
### <a name="category"></a>category

**Desteklenen değerler**:

| Kategori                         | Değer     |
| :--                              | ---       |
| Çekirdek Dizin                   | Dizin |
| Self Servis Parola Yönetimi | SSPR      |
| Self Servis Grup Yönetimi    | SSGM      |
| Hesap Sağlama             | Sync      |
| Otomatik Parola Geçişi      | Otomatik Parola Geçişi |
| Kimlik Koruması              | IdentityProtection |
| Davetli Kullanıcılar                    | Davetli Kullanıcılar |
| MIM Hizmeti                      | MIM Hizmeti |



**İşleçler desteklenen**: eq

**Örnek**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>ActivityStatus

**Desteklenen değerler**:

| Etkinlik durumu | Değer |
| :--             | ---   |
| Başarılı         | 0     |
| Hata         | - 1   |

**İşleçler desteklenen**: eq

**Örnek**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=activityType eq 'User'    

**Notlar**:

büyük küçük harfe duyarlı

- - -
### <a name="activity"></a>Etkinlik
**İşleçler desteklenen**: eq, içerir, startsWith

**Örnek**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Notlar**:

büyük küçük harfe duyarlı

- - -
### <a name="actorname"></a>Aktör/adı
**İşleçler desteklenen**: eq, içerir, startsWith

**Örnek**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Notlar**:

Büyük küçük harfe duyarsızdır

- - -
### <a name="actorobjectid"></a>Aktör/objectID
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>Hedef/adı
**İşleçler desteklenen**: eq, içerir, startsWith

**Örnek**:

    $filter=targets/any(t: t/name eq 'some name')    

**Notlar**:

Büyük küçük harfe duyarsızdır

- - -
### <a name="targetupn"></a>Hedef/upn
**İşleçler desteklenen**: eq, startsWith

**Örnek**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Notlar**:

* Büyük küçük harfe duyarsızdır
* Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity sorgulanırken tooadd hello tam ad alanı gerekir

- - -
### <a name="targetobjectid"></a>Hedef/objectID
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>Aktör/upn
**İşleçler desteklenen**: eq, startsWith

**Örnek**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Notlar**:

* Büyük küçük harfe duyarsızdır 
* Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity sorgulanırken tooadd hello tam ad alanı gerekir

- - -
## <a name="next-steps"></a>Sonraki Adımlar
* Filtrelenmiş sistem etkinlikler için toosee örnekler istiyor musunuz? Merhaba denetleyin [Azure Active Directory denetim API'si örnekleri](active-directory-reporting-api-audit-samples.md).
* Tooknow hello Azure AD raporlama API'si hakkında daha fazla istiyor musunuz? Bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).

