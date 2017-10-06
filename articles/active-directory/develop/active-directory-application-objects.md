---
title: "aaaAzure Active Directory uygulaması ve hizmet sorumlusu nesneleri | Microsoft Docs"
description: "Uygulama ve Azure Active Directory hizmet asıl nesneleri arasındaki ilişki hello tartışması"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Uygulama ve hizmet asıl nesneler Azure Active Directory'de (Azure AD)
Bazen "uygulama" hello Azure AD bağlamında kullanıldığında yanlış hello terim anlamını hello. Merhaba, bu makalenin hedeftir toomake bunu Azure AD uygulama tümleştirmesi, kavramsal ve somut yönlerini kaydı ve onay için bir çizimi ile açıklığa kavuşturan NET bir [çok kiracılı uygulama](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Genel Bakış
Azure AD ile tümleşik bir uygulama hello yazılım boy gidin etkilere sahiptir. "Uygulama" toonot yalnızca hello hello uygulama yazılımı, ancak aynı zamanda kendi Azure AD kaydını ve kimlik doğrulama/yetkilendirme çalışma zamanında "görüşmeleri" rolünde başvuran kavramsal bir terim sık kullanılır. Tanımı gereği, bir uygulama içinde çalışabilmesi için bir [istemci](active-directory-dev-glossary.md#client-application) (kaynak kullanma), rol bir [kaynak sunucusu](active-directory-dev-glossary.md#resource-server) rol (sunan API'leri tooclients) veya her ikisi de bile. Merhaba konuşma protokolü tarafından tanımlanan bir [OAuth 2.0 yetkilendirme verme akış](active-directory-dev-glossary.md#authorization-grant), hello istemci/kaynak tooaccess/korumak kaynağın veri sırasıyla izin verme. Şimdi edelim daha derin bir düzeyi ve nasıl hello Azure AD uygulama modeli bir uygulamayı tasarım zamanı ve çalışma zamanı temsil eden bakın. 

## <a name="application-registration"></a>Uygulama kaydı
Azure AD uygulaması hello kaydettiğinizde [Azure portal][AZURE-Portal], iki nesne, Azure AD kiracınız oluşturulur: uygulama nesnesi ve bir hizmet sorumlusu nesnesi.

#### <a name="application-object"></a>Uygulama nesnesi
Azure AD uygulaması, bir ve Merhaba uygulaması kaydedildiği hello Azure AD kiracısında bulunduğu uygulama nesnesi tarafından hello uygulamanın "home" Kiracı olarak bilinen tanımlanır. Hello Azure AD grafik [uygulama varlığı] [ AAD-Graph-App-Entity] hello şema uygulama nesnenin özellikler için tanımlar. 

#### <a name="service-principal-object"></a>Hizmet sorumlusu nesnesi
Merhaba hizmet sorumlusu nesnesi bir güvenlik sorumlusu toorepresent hello uygulama çalışma zamanında hello temel sağlayan belirli bir kiracı hello İlkesi ve bir uygulamanın kullanmak için izinler tanımlar. Hello Azure AD grafik [ServicePrincipal varlık] [ AAD-Graph-Sp-Entity] hello şema için bir hizmet asıl nesnenin özelliklerini tanımlar. 

#### <a name="application-and-service-principal-relationship"></a>Uygulama ve hizmet asıl ilişkisi
Merhaba uygulama nesnesi hello olarak göz önünde bulundurun *genel* uygulamanızı hello olarak kullanmak üzere tüm kiracılar ve hello hizmet sorumlusu arasında gösterimini *yerel* kullanılmak üzere belirli bir gösterimi Kiracı. Merhaba hangi ortak şablondan ve varsayılan özellikleri gibi hello uygulama nesnesi hizmet *türetilmiş* karşılık gelen hizmet asıl nesneleri oluşturulurken kullanılacak. Uygulama nesnesi bu nedenle 1:1 ilişki hello yazılım uygulamayla ve onun karşılık gelen hizmet asıl nesneleri ile 1:many ilişkisi vardır.

Bir hizmet sorumlusu her bir kiracı tooestablish oturum açma için bir kimlik etkinleştirme Merhaba uygulaması kullanılacak olduğunda ve/veya hello Kiracı tarafından güvenli hale getirilmiş erişim tooresources oluşturulmuş olması gerekir. Tek kiracılı uygulama (kendi giriş kiracısı içinde), genellikle oluşturulur ve uygulama kaydı sırasında kullanılmak üzere rıza yalnızca bir hizmet sorumlusu sahip olur. Kiracı kullanıcıdan tooits kullanım burada seçtiği bir çok kiracılı Web uygulaması/API ayrıca her bir kiracı oluşturulan bir hizmet sorumlusu vardır.  

> [!NOTE]
> Tooyour uygulama nesnesi, yaptığınız tüm değişiklikler de yansıtılır hello uygulamanın giriş Kiracı yalnızca (burada kaydedildiği hello Kiracı) kendi hizmet sorumlusu nesnesi. Çok kiracılı uygulamalar için değişiklikleri toohello uygulama nesnesi değil yansıtılır hiçbir tüketici Kiracı hizmet asıl nesneleri, hello erişim hello kaldırılana kadar [uygulama erişim Paneli'ne](https://myapps.microsoft.com) ve yeniden verilir.
><br>  
> Ayrıca, yerel uygulamalar varsayılan olarak çok Kiracı olarak kaydedilen unutmayın.
> 
> 

## <a name="example"></a>Örnek
Merhaba Aşağıdaki diyagramda gösterilmektedir hello arasındaki ilişki bir uygulamanın uygulama nesnesi karşılık gelen hizmet asıl nesneleri hello örnek bir çok kiracılı uygulama bağlamında adlı **ik uygulama**. Bu senaryoda üç Azure AD kiracılarıyla vardır: 

* **Adatum** - hello hello geliştirilen hello şirket tarafından kullanılan Kiracı **ik uygulama**
* **Contoso** - hello hello tüketicisidir Contoso kuruluşundaki hello tarafından kullanılan Kiracı **ik uygulama**
* **Fabrikam** - hello hello ayrıca hello tüketir Fabrikam kuruluş tarafından kullanılan Kiracı **ik uygulama**

![Uygulama nesnesi ve bir hizmet sorumlusu nesnesi arasındaki ilişki](./media/active-directory-application-objects/application-objects-relationship.png)

Merhaba önceki diyagramda, adım 1 hello uygulama ve hizmet asıl nesneleri hello uygulamanın giriş Kiracı oluşturma hello işlemidir.

Onay, contoso ve Fabrikam Yöneticiler tamamladığınızda, adım 2'de bir hizmet sorumlusu nesnesi şirketlerinin Azure AD kiracısı ve atanan hello izinleri verilen o hello yönetici oluşturulur. Ayrıca bu hello HR uygulama tek başına kullanım için kullanıcılar tarafından yapılandırılan ve tasarlanmış tooallow izin olabilir unutmayın.

Adım 3'te hello tüketici kiracılar hello HR uygulama (Contoso ve Fabrikam) her biri kendi hizmet sorumlusu nesnesi vardır. Her kullanımlarını izin verdiği hello hello ilgili yönetici tarafından yönetilen zamanında hello uygulama örneği temsil eder.

## <a name="next-steps"></a>Sonraki adımlar
Bir uygulamanın uygulama nesnesi hello Azure AD grafik API'si hello erişilebilir [Azure portal'ın] [ AZURE-Portal] uygulama bildirim Düzenleyicisi veya [Azure AD PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), OData tarafından temsil edilen [uygulama varlığı][AAD-Graph-App-Entity].

Bir uygulamanın hizmet sorumlusu nesnesi hello Azure AD grafik API'si erişilebilir veya [Azure AD PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), OData tarafından temsil edilen [ServicePrincipal varlık] [ AAD-Graph-Sp-Entity].

Merhaba [Azure AD Graph Explorer'a](https://graphexplorer.azurewebsites.net/) hello uygulama ve hizmet asıl nesneleri sorgulamak için yararlıdır.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
