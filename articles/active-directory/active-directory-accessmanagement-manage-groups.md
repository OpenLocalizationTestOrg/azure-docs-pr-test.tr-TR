---
title: "Azure Active Directory'de aaaManaging gruplarını | Microsoft Docs"
description: "Nasıl toocreate ve grupları toomanage Azure yönetmek kullanıcıları Azure Active Directory kullanarak."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Azure Active Directory içinde grupları yönetme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Azure Active Directory (Azure AD) kullanıcı yönetimi hello özelliklerini hello özelliği toocreate gruplarını biridir. Lisans veya izinleri tooa sayısı, kullanıcı aynı anda atama gibi bir grup tooperform yönetim görevleri kullanın. Grupları tooassign erişim izni de kullanabilirsiniz

* Merhaba directory içindeki nesneleri gibi kaynakları
* SaaS uygulamaları, Azure Hizmetleri, SharePoint siteleri veya şirket içi kaynaklar gibi kaynakları dış toohello dizini

Ayrıca, bir kaynak sahibi başka birisi tarafından sahip olunan erişim tooa kaynak tooan Azure AD grubuna atayabilirsiniz. Bu atama hello üyeleri bu Grup erişim toohello kaynağın verir. Ardından, hello grubunun hello sahibi hello grubu üyeliği yönetir. Etkili bir şekilde hello kaynak sahibi temsilciler toohello hello Grup hello izin tooassign kullanıcılar tootheir kaynağın sahibi.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Toomanage hello Azure AD Yönetim Merkezi'nde nasıl gruplar için bkz: [bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Nasıl grup oluşturulur?
Kuruluşunuzun abone olduğu hello Hizmetleri toowhich bağlı olarak hello aşağıdakilerden birini kullanarak bir grup oluşturabilirsiniz:

* Merhaba Klasik Azure portalı
* Merhaba Office 365 hesap portalı
* Merhaba Windows Intune hesap portalı

Görevleri hello Klasik Azure portalında gerçekleştirilen gibi açıklar. Azure AD dizininizi Azure olmayan Portal toomanage kullanma hakkında daha fazla bilgi için bkz: [Azure AD dizininizi yönetme](active-directory-administer.md).

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.
2. Select hello **grupları** sekmesi.
3. **Grup Ekle**'yi seçin.
4. Merhaba, **Grup Ekle** penceresinde hello adı belirtin ve hello bir grubun açıklaması.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Güvenlik grubuna bireysel kullanıcıları nasıl eklerim veya kaldırırım?
**tooadd tek tek kullanıcı tooa grubu**

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.
2. Select hello **grupları** sekmesi.
3. Merhaba Grup toowhich tooadd üyelerinin istediğiniz açın. Açık hello **üyeleri** hello sekmesinde seçtiyseniz grubu, zaten görüntüleme.
4. **Add Members (Üye Ekle)** seçeneğini belirleyin.
5. Merhaba üzerinde **Add Members** sayfası, hello kullanıcı veya bu grubun bir üyesi olarak tooadd istediğiniz bir grup seçin hello adı. Bu ad toohello eklendiğinden emin olun **seçili** bölmesi.

**tooremove tek bir kullanıcı bir gruptan**

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.
2. Select hello **grupları** sekmesi.
3. Tooremove üyelerinin istediğiniz hello grubu açın.
4. Select hello **üyeleri** sekmesi, bu gruptan tooremove istediğiniz ve ardından hello üyenin adını seçin hello **kaldırmak**.
5. Merhaba isteminde hello gruptan bu üye tooremove istediğinizi onaylayın.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Merhaba bir grubun üyeliğini dinamik olarak nasıl yönetebilirim?
Azure AD içinde hangi kullanıcıların toobe hello grubunun üyesi olan bir basit kural toodetermine kolayca ayarlayabilirsiniz. Basit bir kural yalnızca tek bir karşılaştırma yapan kuraldır. Örneğin, bir grup tooa SaaS uygulamasına atandıysa, iş unvanına "Satış Temsilcisi" sahip olan bir kural tooadd kullanıcıları ayarlayabilirsiniz Bu kural, dizininizdeki bu iş unvanına sahip toothis SaaS uygulama tooall kullanıcılar daha sonra erişim verir.

Herhangi bir kullanıcı değişiklik özniteliklerini hello sistem değerlendirildiğinde hello öznitelik değişikliği hello kullanıcının herhangi bir grup tetikleyecek varsa bir dizin toosee tüm dinamik Grup kurallarında ekler veya kaldırır. Bir kullanıcı bir grupta kuralı uymazsa, bunlar üye toothat grup olarak eklenir. Bunlar artık üyesi olan bir grup hello kuralı karşılamak varsa, bunlar bir üye olarak, bu gruptan kaldırılır.

> [!NOTE]
> Güvenlik gruplarında veya Office 365 gruplarında dinamik üyelik için bir kural ayarlayabilirsiniz. İç içe geçmiş grup üyelikleri grup tabanlı atama tooapplications için şu anda desteklenmiyor.
>
> Atanmış bir Azure AD Premium lisansı toobe gruplara yönelik dinamik üyelikler gerektirir
>
> * Merhaba grupta kuralı yöneten hello Yöneticisi
> * Merhaba grubunun tüm üyeleri
>
>

**bir grup için tooenable dinamik üyeliği**

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.
2. Select hello **grupları** sekme ve açık hello Grup tooedit istiyor.
3. Select hello **yapılandırma** sekmesini tıklatın ve ardından **dinamik üyelikleri etkinleştir** çok**Evet**.
4. Merhaba Grup toocontrol için tek bir basit kural ayarlayın bu grubun işlevleri için dinamik üyeliği. Hello emin olun **kullanıcıları ekleme yeri** seçeneği seçilir ve ardından kullanıcı özelliği (örneğin, departman, iş unvanı, vb.), hello listeden seçin
5. Ardından, bir koşul (Eşit Değildir, Eşittir, İle Başlamaz, İle Başlar, İçermez, İçerir, Eşleşmez, Eşleşir) seçin.
6. Seçili hello kullanıcı özelliği için bir karşılaştırma değer belirtin.

konusunda toolearn toocreate *Gelişmiş* kuralları (birden çok karşılaştırma içeren kurallar) dinamik grup üyeliği için bkz: [öznitelikleri toocreate kullanarak gelişmiş kurallar](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Ek bilgiler
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
