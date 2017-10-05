---
title: "Azure RemoteApp koleksiyonunuzun kullanıcı ekleme | Microsoft Docs"
description: "Kullanıcıların Azure RemoteApp koleksiyonunuzun eklemeyi öğrenin"
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>Azure RemoteApp koleksiyonunuzun kullanıcı ekleme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Kullanıcılarınızın bakın ve uygulamalarınızı Azure RemoteApp kullanmaya başlamadan önce koleksiyonunuzu erişim vermek sahip. Bu kolay bir parçasıdır: üzerinde **kullanıcı erişimini** sekmesinde, kullanıcı hesabı bilgilerini girin ve ardından onay işaretine tıklayın.

Hangi hesap bilgileri gerekiyor? Oluşturduğunuz (Bulut veya karma) ve Office 365 ProPlus koleksiyonda kullanıp koleksiyon türüne göre değişir.

## <a name="supported-user-identities"></a>Desteklenen kullanıcı kimlikleri
Uygulamalara erişimi için farklı kullanıcı kimliklerini kullanarak farklı koleksiyon türleri (karma ve bulut) destekler.  

RemoteApp karma koleksiyonu için şirket içi ve Azure Active Directory Kiracı dizin Tümleştirmesi ile bir Active Directory etki alanı altyapısını ayarlamak için (ve isteğe bağlı olarak çoklu oturum açmayı) gerekir. Ayrıca, bazı Active Directory nesnelerini şirket içi dizinini oluşturmanız gerekir.  

RemoteApp bulut koleksiyonu için Azure Active Directory kimlikleri destek sahip herhangi bir kullanıcı RemoteApp Microsoft Accounts dahil etmek için kullanıcı erişimini verilebilir.  Aşağıdaki tabloya bakın.

Office 365, Azure Active Directory Kullanıcıları kullanıcılardır. Azure Active Directory karma varsa, dizin eşitlenen hesapları, bunlar bir RemoteApp karma dağıtımında kullanıcı erişimi verilebilir.   

Bu tablo kimliği, koleksiyon ve Active Directory gereksinimleri nelerdir desteklenmektedir hızlı başvuru olarak kullanabilirsiniz.

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
> Azure Active Directory kullanıcıları, aboneliğinizle ilişkili kiracıya ait olmalıdır. (Aboneliğinizi, portalın **Ayarlar** sekmesinde görüntüleyebilir ve değiştirebilirsiniz. Daha fazla bilgi için bkz. [RemoteApp tarafından kullanılan Azure Active Directory kiracısını değiştirme](remoteapp-changetenant.md).)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus kullanıcı hesabı bilgileri
Koleksiyonunuzda Office 365 ProPlus şablon görüntüsü kullanıyorsanız *veya* Office 365 kullanan özel bir görüntü oluşturduysanız, yalnızca aboneliğinizin varsayılan etki alanı için Office 365 aboneliğine sahip Azure Active Directory Kullanıcıları eklemek için izin verilir. Bkz: [Azure RemoteApp ile Office 365'ı kullanarak](remoteapp-o365.md) daha fazla bilgi için.

