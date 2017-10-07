---
title: "aaaAdd kullanıcı tooyour Azure RemoteApp koleksiyonu | Microsoft Docs"
description: "Bilgi nasıl tooadd kullanıcılar tooyour Azure RemoteApp koleksiyonu"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Nasıl tooadd kullanıcı tooyour Azure RemoteApp koleksiyonu
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Kullanıcılarınızın bakın ve uygulamalarınızı Azure RemoteApp kullanmaya başlamadan önce tooyour koleksiyonuna erişmek toogrant sahip. Bu hello kolay bir parçasıdır: hello üzerinde **kullanıcı erişimini** sekmesinde, hello hello kullanıcısı için hesap bilgilerini girin ve ardından hello onay işaretine tıklayın.

Hangi hesap bilgileri gerekiyor? Oluşturduğunuz (Bulut veya karma) ve Office 365 ProPlus koleksiyonda kullanıp hello koleksiyon türüne göre değişir.

## <a name="supported-user-identities"></a>Desteklenen kullanıcı kimlikleri
Merhaba farklı koleksiyon türleri (karma ve bulut) kullanarak farklı bir kullanıcı kimlikleri için erişim tooapplications destekler.  

RemoteApp karma koleksiyonu, şirket içi ve Azure Active Directory Kiracı dizin Tümleştirmesi ile Active Directory etki alanı altyapısı yukarı tooset gerekir (ve isteğe bağlı olarak çoklu oturum açmayı). Ayrıca, bazı Active Directory nesneleri hello şirket içi dizin toocreate gerekir.  

RemoteApp bulut koleksiyonu için Azure Active Directory kimlikleri destek sahip herhangi bir kullanıcı, kullanıcı erişim tooRemoteApp tooinclude Microsoft Accounts verilebilir.  Merhaba tabloya bakın.

Office 365, Azure Active Directory Kullanıcıları kullanıcılardır. Azure Active Directory karma varsa, dizin eşitlenen hesapları, bunlar bir RemoteApp karma dağıtımında kullanıcı erişimi verilebilir.   

Bu tablo kimliği, koleksiyon ve hello Active Directory gereksinimleri nelerdir desteklenmektedir hızlı başvuru olarak kullanabilirsiniz.

| Kullanıcı hesapları | Bulut | Karma |
| --- | --- | --- |
| Microsoft Hesabı |Evet |Hayır |
| Azure Active Directory (Azure AD) | | |
| Yalnızca Azure AD bulut |Evet |Hayır |
| Parola Eşitleme ile ADsync |Evet |Evet |
| Parola Eşitleme olmadan ADsync |Evet |Hayır |
| AD FS ile ADsync |Evet |Evet |
| [3. taraf Azure desteklenen kimlik sağlayıcıları](https://msdn.microsoft.com/library/azure/jj679342.aspx) (örnek: Ping) |Evet |Evet |
| Multi-Factor Authentication |Evet |Evet |

Kullanıma [daha fazla bilgi](remoteapp-ad.md) RemoteApp için Active Directory yapılandırma hakkında daha fazla.

> [!NOTE]
> Hello Azure Active Directory Kullanıcıları, aboneliğinizle ilişkili hello Kiracı olmalıdır. (Görüntülemek ve aboneliğinizi hello değiştirmek **ayarları** hello portal sekmesindedir. Bkz: [RemoteApp tarafından kullanılan değişiklik hello Azure Active Directory Kiracı](remoteapp-changetenant.md) daha fazla bilgi için.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus kullanıcı hesabı bilgileri
Koleksiyonunuzda hello Office 365 ProPlus şablon görüntüsü kullanıyorsanız *veya* Office 365 kullanan özel bir görüntü oluşturduysanız, hello için Office 365 aboneliğine sahip tooadd Azure Active Directory Kullanıcıları yalnızca izin verilir aboneliğiniz için varsayılan etki alanı. Bkz: [Azure RemoteApp ile Office 365'ı kullanarak](remoteapp-o365.md) daha fazla bilgi için.

