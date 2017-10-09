---
title: 'Azure AD Connect: Zaten varsa Azure AD | Microsoft Docs'
description: "Bu konu, nasıl toouse bağlandığınız zaman açıklar mevcut Azure AD kiracısı vardır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: Mevcut bir kiracı olduğunda
Nasıl toouse Azure AD Connect varsayılmaktadır hello konuları çoğunu Başlat ile yeni bir Azure AD Kiracı ve hiçbir kullanıcı ya da diğer nesneleri vardır. Ancak bir Azure AD kiracısı ile başlamış olması durumunda kullanıcılar ve diğer nesneleri ile doldurulur ve şimdi toouse bağlan, istediğiniz sonra bu konuda size göre.

## <a name="hello-basics"></a>Merhaba temelleri
Azure AD'de bir nesne ya da hello bulutta (Azure AD) veya şirket içinde yönetilir. Tek bir nesne için Azure AD içinde bazı öznitelikler şirket içi ve bazı diğer öznitelikleri yönetemez. Her nesnenin hello nesne yönetildiği belirten bir bayrak vardır.

Bazı kullanıcılar şirket içi ve diğer hello bulutta yönetebilirsiniz. Bu yapılandırma için yaygın bir senaryo bir kuruluş hesap çalışanları ve Satış çalışanları karışımını içeren ' dir. Merhaba hesap çalışanları sahip bir şirket içi AD hesabının ancak hello Satış çalışanları yapmak için bunlar Azure AD'de bir hesabınız yok. Bazı kullanıcılar şirket içi ve bazı Azure AD'de yönetmek.

Toomanage kullanıcılar başlattıysanız, ayrıca, Azure AD şirket içi AD ve tooconsider gereken bazı ek sorunları sonra toouse Connect, daha sonra istediğiniz.

## <a name="sync-with-existing-users-in-azure-ad"></a>Mevcut kullanıcıların Azure AD'de eşitleme
Azure AD Connect yüklediğinizde ve Eşitlemeyi Başlat hello Azure AD eşitleme hizmeti (Azure AD'de) her yeni nesne üzerinde bir denetimi yapar ve toofind var olan bir nesne toomatch deneyin. Bu işlem için kullanılan üç öznitelikleri vardır: **userPrincipalName**, **proxyAddresses**, ve **sourceAnchor**/**İmmutableıd**. Bir eşleşme **userPrincipalName** ve **proxyAddresses** olarak bilinen bir **yumuşak eşleşme**. Bir eşleşme **sourceAnchor** olarak bilinen **sabit eşleşme**. Hello için **proxyAddresses** yalnızca hello değerle özniteliği **SMTP:**, hello birincil e-posta adresi, hello değerlendirmesi için kullanılır.

Merhaba eşleşme yalnızca Bağlan gelen yeni nesneler için değerlendirilir. Varolan bir nesne, bu özelliklerden herhangi birini eşleşen şekilde değiştirirseniz, daha sonra bir hata yerine bakın.

Azure AD hello öznitelik değerleri hello olduğu bir nesneyi bulursa gelen bir nesne için aynı Connect ve, bunu Azure AD içinde zaten sonra hello nesnesinde Azure AD Connect tarafından ele alınır. Merhaba önceden bulut Yönetilen Nesne yönetilen şirket içi işaretlenir. Tüm öznitelikleri şirket içi bir değere sahip Azure AD'de AD yazılır hello şirket içi değerle. Merhaba özel bir öznitelik olduğunda bir **NULL** şirket içi değer. Bu durumda, Azure AD kalır, ancak hello değeri hala yalnızca şirket içi toosomething başka değiştirebilirsiniz.

> [!WARNING]
> Azure AD'de tüm öznitelikleri hello şirket içi değeriyle üzerine toobe kalacaklarını beri iyi verileri şirket içinde olduğundan emin olun. Örneğin, e-posta adresi Office 365'te yalnızca yönetilen ve değil tutulan içinde güncelleştirilmiş AD DS, AD DS'de mevcut Azure AD/Office 365'te herhangi bir değeri kaybetmek sonra şirket içi.

> [!IMPORTANT]
> Her zaman hızlı ayarları tarafından kullanılır, Parola Eşitleme'yi kullanmaya sonra Azure AD'de hello parola şirket hello parolayla yazılır AD. Yeniden tooinform gerekiyor kullanılan toomanage farklı parolalar, kullanıcılarınız varsa Bağlan yüklendiğinde kullanması gereken bunları şirket içi parola hello.

Merhaba önceki bölümde ve uyarı planlamanızda dikkate alınmalıdır. Yansıtılan değil Azure AD'de birçok değişiklik yaptıysanız, AD DS, yeniden nesnelerinizi Azure AD Connect ile eşitleme önce nasıl toopopulate AD DS ile Merhaba güncelleştirilmiş değerleri için tooplan gerekiyor şirket içi.

Nesnelerinizi yazılımla eşleşen eşleşen, ardından hello **sourceAnchor** sabit bir eşleşme daha sonra kullanılabilmesi için Azure AD'de toohello nesne eklenir.

### <a name="hard-match-vs-soft-match"></a>Vs Soft-match sabit eşleşmiyor
Connect yeni yükleme için arasındaki soft - eşleşme sabit pratik fark yoktur. Merhaba, bir olağanüstü durum kurtarma durumda farktır. Azure AD Connect sunucunuzla kaybettiyseniz, hiçbir veri kaybı olmadan yeni bir örneğini yeniden yükleyebilirsiniz. Bir sourceAnchor sahip bir nesne tooConnect ilk yükleme sırasında gönderilir. Merhaba eşleşme sonra yapılması daha çok daha hızlı olan hello istemci (Azure AD Connect) tarafından değerlendirilebilir aynı Azure AD içinde hello. Sabit bir eşleşme hem Bağlan ve Azure AD tarafından değerlendirilir. Geçici bir eşleşme yalnızca Azure AD tarafından değerlendirilir.

### <a name="other-objects-than-users"></a>Kullanıcılar daha başka nesneler
Kullanıcılar genellikle userPrincipalName ve proxyAddresses, hello eşleşme kolaylaşır sahiptir. Ancak, güvenlik grupları gibi diğer nesneler bu yoktur. Bu durumda, yalnızca bir sabit eşleşme hello sourceAnchor kullanarak eşleştirebilirsiniz. Merhaba sourceAnchor olduğu her zaman Base64 dönüştürülen hello **objectGUID** iki nesneleri toomatch gerektiğinde Azure AD içinde hello değerini güncelleştirmeniz gerekir böylece şirket. Merhaba sourceAnchor/İmmutableıd yalnızca PowerShell ile ve hello portalı üzerinden değil güncelleştirilebilir.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Yeni bir şirket içi Active Directory verilerini Azure AD oluşturma
Azure AD ile yalnızca bulut çözümü olan bazı müşteriler başlatmak ve şirket içi olmayan AD. Daha sonra bunlar tooconsume şirket kaynaklarına ve şirket içi toobuild istiyorsanız AD tabanlı Azure AD verileri. Azure AD Connect bu senaryo için yardımcı olamaz. Kullanıcıların şirket içi oluşturmaz ve tüm özelliği tooset hello parola şirket içi toohello yoksa Azure AD olduğu gibi aynı.

Merhaba tek nedeni tooadd planladığınız neden AD olduğu toosupport LOB'lar (satır iş kolu uygulamaları), ardından toouse göz önünde bulundurmalısınız belki de şirket içi ise [Azure AD etki alanı Hizmetleri](../../active-directory-domain-services/index.md) yerine.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
