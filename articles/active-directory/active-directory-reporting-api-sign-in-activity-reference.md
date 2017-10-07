---
title: "aaaAzure Active Directory oturum açma etkinliği raporu API Başvurusu | Microsoft Docs"
description: "Hello Azure Active Directory oturum açma etkinliği raporu API Başvurusu"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Azure Active Directory oturum açma etkinliği raporu API Başvurusu
Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.  
Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess oturum açma etkinliği raporu veri sağlayan bir API ile sağlar.
Bu konunun Hello kapsamı olan tooprovide hello hakkında başvuru bilgileri sizinle **oturum açma etkinliği raporu API işleminde**.

Bkz.:

* [Oturum açma etkinliklerini](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için
* [Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.


## <a name="who-can-access-hello-api-data"></a>Merhaba API veri erişebilecek mi?
* Kullanıcı ve hizmet asıl adı hello Güvenlik Yöneticisi veya güvenlik okuyucu rolü
* Genel Yöneticiler
* Yetkilendirme tooaccess hello API sahip herhangi bir uygulama (app yetkilendirme olabilir Kurulum genel yöneticinin iznine dayanılarak yalnızca)

bir uygulama tooaccess API'leri gibi güvenlik oturum açma olayları, PowerShell tooadd hello uygulamaları hizmet sorumlusu hello güvenlik okuyucu rolüne aşağıdaki kullanım hello tooconfigure erişim

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Ön koşullar
Bu rapor aracılığıyla tooaccess raporlama API Merhaba, sahip olmanız gerekir:

* Bir [Azure Active Directory Premium P1 veya P2 edition](active-directory-editions.md)
* Tamamlanan hello [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Merhaba API'sine erişim
Bu API hello erişebilirsiniz [Graph Explorer'a](https://graphexplorer2.cloudapp.net) veya program aracılığıyla, örneğin, PowerShell kullanarak. Sırayla PowerShell toocorrectly yorumlamak için AAD grafik REST çağrılarında kullanılan hello OData filtresi sözdizimi hello backtick kullanmanız gerekir (diğer adıyla: Vurgu) çok "kaçış karakteri" Merhaba $ karakteri. Merhaba backtick karakter görür [PowerShell'in kaçış karakteri](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo hello $ karakteri değişmez değer yorumu izin verme ve PowerShell değişken adı olarak kafa karıştırıcı kaçının (IE: $filter).

Bu konunun Hello odak Graph Explorer'a hello üzerinde noktasıdır. Bu PowerShell örnek için bkz [PowerShell Betiği](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>API uç noktası
Bu API taban URI aşağıdaki hello kullanarak erişebilirsiniz:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Veri hacmi toohello, bu API bir milyon kayıtları döndürülen bir sınıra sahiptir. 

Bu çağrı hello verileri toplu olarak döndürür. Her toplu işlem en fazla 1000 kaydı var.  
tooget hello sonraki toplu kayıt, kullanım hello sonraki bağlantı. Merhaba alma [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello ilk döndürülen kayıt kümesi bilgileri. Merhaba Atla belirteci hello hello sonuç kümesinin sonunda olacaktır.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Desteklenen filtreler
Bir API tarafından döndürülen kayıt sayısını hello daraltabilirsiniz bir filtre formda çağırın.  
Oturum açma için API ilgili veriler, filtreleri aşağıdaki hello desteklenir:

* **$top =\<döndürülen kayıt toobe sayısı\>**  -toolimit hello döndürülen kayıt sayısı. Bu pahalı bir işlemdir. Nesnelerin tooreturn binlerce istiyorsanız bu filtre kullanmamanız gerekir.  
* **$filter =\<filtre ifadesi\>**  -desteklenen filtre alanlarının önem verdiğiniz kayıtların hello türünü hello temelinde toospecify

## <a name="supported-filter-fields-and-operators"></a>Desteklenen filtre alanları ve işleçleri
İlgilendiğiniz kayıtları toospecify hello türü, bir veya filtre alanları aşağıdaki hello bir birleşimini içerebilir bir filtre ifadesi oluşturabilirsiniz:

* [signinDateTime](#signindatetime) -bir tarih veya tarih aralığı tanımlar
* [UserId](#userid) -belirli kullanıcı tabanlı hello kullanıcının kimliği tanımlar
* [userPrincipalName](#userprincipalname) -belirli kullanıcı tabanlı hello kullanıcının kullanıcı asıl adı (UPN) tanımlar
* [AppID](#appid) -göre belirli uygulama hello uygulamanın Kimliğini tanımlar
* [appDisplayName](#appdisplayname) -göre belirli uygulama hello uygulamanın görünen adı tanımlar
* [loginStatus](#loginStatus) -hello oturumları hello durumunu tanımlar (başarı / hata)

> [!NOTE]
> Grafik Gezgini'ni kullanırken, hello toouse hello filtre alanlarınızı durumdur her harfi için doğru gerekir.
> 
> 

toonarrow döndürülen veriler hello hello kapsamını aşağı desteklenen hello filtreleri ve filtre alanları birleşimlerini oluşturabilirsiniz. Örneğin, hello aşağıdaki ifadeyi hello 1 Temmuz 2016 Temmuz 6 2016 arasındaki üst 10 kayıtları döndürür:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**İşleçler desteklenen**: eq, ge, le, gt, lt

**Örnek**:

Belirli bir tarih kullanma

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Bir tarih aralığı kullanma    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Notlar**:

Merhaba datetime parametresi hello UTC biçiminde olmalıdır 

- - -
### <a name="userid"></a>Kullanıcı Kimliği
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Notlar**:

UserId Hello değeri bir dize değeridir

- - -
### <a name="userprincipalname"></a>userPrincipalName
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Notlar**:

userPrincipalName Hello değeri bir dize değeridir

- - -
### <a name="appid"></a>AppID
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Notlar**:

AppID Hello değeri bir dize değeridir

- - -
### <a name="appdisplayname"></a>appDisplayName
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Notlar**:

appDisplayName Hello değeri bir dize değeridir

- - -
### <a name="loginstatus"></a>loginStatus
**İşleçler desteklenen**: eq

**Örnek**:

    $filter=loginStatus+eq+'1'  


**Notlar**:

Merhaba loginStatus için iki seçenek vardır: 0 - başarılı, 1 - hata

- - -
## <a name="next-steps"></a>Sonraki adımlar
* Oturum açma filtrelenmiş etkinlikler için toosee örnekler istiyor musunuz? Merhaba denetleyin [Azure Active Directory oturum açma etkinliği raporu API örnekleri](active-directory-reporting-api-sign-in-activity-samples.md).
* Tooknow hello Azure AD raporlama API'si hakkında daha fazla istiyor musunuz? Bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).

