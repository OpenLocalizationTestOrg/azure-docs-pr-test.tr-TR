---
title: Active Directory grafik API'si aaaAzure | Microsoft Docs
description: "Bir genel bakış ve Hızlı Başlangıç Kılavuzu hello programlı sağlayan grafik API'si için REST API uç noktaları yoluyla tooAzure AD erişin."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Azure Active Directory Grafik API'si
> [!IMPORTANT]
> Kullanmanız önerilir [Microsoft Graph](https://graph.microsoft.io/) Azure AD Graph API tooaccess Azure Active Directory kaynakları yerine. Geliştirme çalışmalarımız şu anda Microsoft Graph üzerine yoğunlaşmıştır ve Azure AD Grafik API'si için başka bir geliştirme planlanmamaktadır. Senaryolar için Azure AD Graph API hala uygun olabilir, çok sınırlı sayıda vardır; Merhaba daha fazla bilgi için bkz: [Microsoft Graph veya hello Azure AD grafik](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office Geliştirici Merkezi blog postasına.
> 
> 

Hello Azure Active Directory grafik API'si, REST API uç noktaları yoluyla programlı erişim tooAzure AD sağlar. Uygulamalar hello grafik API'si tooperform kullanabilir oluşturma, okuma, güncelleştirme ve (CRUD) işlemleridir dizin verileri ve nesneleri silme. Örneğin, bir kullanıcı nesnesi için genel işlem aşağıdaki hello hello grafik API'si destekler:

* Yeni bir kullanıcı bir dizin oluşturun
* Kendi gruplar gibi bir kullanıcının ayrıntılı özelliklerini alma
* Konum ve telefon numarası gibi bir kullanıcının özelliklerini güncelleştirmek veya parolasını değiştirme
* Rol tabanlı erişim için kullanıcının grup üyeliğini denetleyin
* Bir kullanıcı hesabı devre dışı bırakmak veya tamamen silme

Toplama toouser nesneleri, gruplar ve uygulamalar gibi diğer nesneler üzerinde benzer işlemler gerçekleştirebilirsiniz. Grafik API'si Merhaba uygulaması bir dizin üzerinde Azure AD ile kayıtlı olması gerekir ve olması toocall hello tooallow erişim toohello directory yapılandırılamıyor. Bu, normal bir kullanıcı veya yönetici onayı akışını sağlanır.

hello Azure Active Directory grafik API'si, toobegin kullanarak hello bkz [grafik API'si Hızlı Başlangıç Kılavuzu](active-directory-graph-api-quickstart.md), ya da Görünüm hello [etkileşimli grafik API başvuru belgeleri](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Özellikler
Merhaba grafik API'si hello aşağıdaki özellikleri sağlar:

* **REST API uç noktaları**: hello grafik API'si standart HTTP isteklerini kullanarak erişilen uç noktaları oluşan bir RESTful hizmettir. Merhaba grafik API'si istekleri ve yanıtları için XML veya Javascript nesne gösterimi (JSON) içerik türlerini destekler. Daha fazla bilgi için bkz: [Azure AD Graph REST API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Azure AD ile kimlik doğrulaması**: grafik API'si kimlik doğrulaması gerekir, bir JSON Web Token (JWT) hello isteğinin hello yetkilendirme üstbilgisinde ekleyerek her isteği toohello. Bu belirteç isteği tooAzure Reklamın belirteç uç noktası yapma ve geçerli kimlik bilgilerini sağlayan alınır. Merhaba yetki kodu izin akışı tooacquire belirteci toocall hello grafik veya hello OAuth 2.0 istemci kimlik bilgileri akışının kullanabilirsiniz. Daha fazla bilgi için [OAuth 2.0 Azure AD'de](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Rol tabanlı yetkilendirme (RBAC)**: güvenlik gruplarıdır hello grafik API'si RBAC kullanılan tooperform. Örneğin, bir kullanıcının erişim tooa belirli bir kaynak olup toodetermine istiyorsanız, Merhaba uygulaması hello çağırabilirsiniz [grup üyeliğini denetleyin (Geçişli)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) true veya false döndürür işlemi.
* **Fark sorgu**: grafik API'si sorguları toohello toomake kalmadan iki dönemleri arasında bir dizinde değişiklik sık için toocheck istiyorsanız, bir fark sorgu isteği yapabilirsiniz. Bu istek türü hello önceki fark sorgu isteği ile Merhaba geçerli istek arasında yalnızca hello değişikliklerinin döndürür. Daha fazla bilgi için bkz: [Azure AD Graph API fark sorgu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Dizin genişletmeleri**: tooread veya yazma özellikleri benzersiz dizin nesneleri için gereken bir uygulama geliştiriyorsanız, kaydetme ve hello grafik API'sini kullanarak uzantısı değerleri kullanın. Örneğin, uygulamanızın her kullanıcı için Skype ID özelliği gerektiriyorsa, hello dizininde hello yeni özellik kaydedebilirsiniz ve her kullanıcı nesnesi üzerinde kullanılabilir. Daha fazla bilgi için bkz: [Azure AD Graph API Directory şema uzantıları](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **İzin kapsamları tarafından güvenliği sağlanan**: AAD grafik API'si güvenli ve verdiği erişim tooAAD veri etkinleştirmek ve istemci uygulama türleri dahil olmak üzere, çeşitli destek izin kapsamları gösterir:
  
  * Bu temsilci verilen bir kullanıcı arabirimi ile (temsilci) hello oturum açmış kullanıcıdan toodata yetkilendirme aracılığıyla erişim
  * kullananlar uygulama-rol tabanlı erişim denetimi hizmeti/arka plan programı istemcileri (uygulama rolleri) gibi tanımlama
    
    Her ikisi de devredildi ve uygulama rolü izin kapsamları hello grafik API'si tarafından kullanıma sunulan ayrıcalık temsil eder ve uygulama kayıt izinleri üzerinden istemci uygulamaları tarafından istenen [hello Azure portal özelliklerinde](https://portal.azure.com). İstemcileri izinlere temsilci için hello erişim belirtecini alınan hello kapsamı ("scp") talep inceleyerek toothem hello izin kapsamları verilmiş ve uygulama rolü izinlerini hello rolleri ("rol") talep doğrulayabilirsiniz. Daha fazla bilgi edinmek [Azure AD grafik API'si izin kapsamları](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Senaryolar
Merhaba grafik API'si birçok uygulama senaryolara olanak sağlar. Merhaba en yaygın senaryolar hello şunlardır:

* **(Tek Kiracılı) iş hattı uygulaması**: Bu senaryoda, bir Office 365 aboneliğine sahip bir kuruluş için bir kuruluş Geliştirici çalışır. Merhaba Geliştirici ile Azure AD tooperform görevleri gibi bir lisans tooa kullanıcı atama etkileşimde bulunan bir web uygulaması oluşturma. Bu görev grafik API'si hello Geliştirici Azure AD'de hello tek kiracılı uygulama kaydeder ve yapılandırır, okuma ve yazma izinlerine hello grafik API'si için erişim toohello gerektirir. Uygulama hello yapılandırılmış toouse ya da kendi kimlik bilgilerini ya da bu hello şu anda oturum açma kullanıcı tooacquire belirteci toocall grafik API'si hello.
* **Bir hizmet uygulaması (çok Kiracılı) olarak yazılım**: Bu senaryoda, bağımsız yazılım satıcısı (ISV), Azure AD kullanan başka kuruluşlar için kullanıcı yönetimi özellikleri sağlar barındırılan çok kiracılı web uygulaması geliştirme. Bu özelliklerin erişim toodirectory nesneleri gerekir ve bu nedenle toocall hello grafik API'si Merhaba uygulaması gerekiyor. Merhaba Geliştirici Merhaba uygulaması Azure AD'de kaydeder, toorequire okuma yapılandırır ve yazma izinleri hello grafik API'si için ve böylece diğer kuruluşlardan toouse Merhaba uygulaması directory'lerinde onayı dış erişim sağlar. Bir kullanıcı başka bir kuruluştaki toohello uygulama hello için ilk kez doğruladığında, bunlar bir onay iletişim kutusu hello uygulama istenirken hello izinlerle gösterilir.  Onay sonra Merhaba uygulaması verecektir verme olanlar hello kullanıcının dizininde izinleri toohello grafik API'si istedi. Merhaba izin framework hakkında daha fazla bilgi için bkz: [hello onayı Framework genel bakış](active-directory-integrating-applications.md).

## <a name="see-also"></a>Ayrıca Bkz.
[Azure AD grafik API'si Hızlı Başlangıç Kılavuzu](active-directory-graph-api-quickstart.md)

[AD grafik REST belgeleri](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Azure Active Directory geliştirici kılavuzu](active-directory-developers-guide.md)

