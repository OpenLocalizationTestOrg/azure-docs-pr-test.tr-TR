---
title: "Azure AD Connect eşitleme: nasıl toomanage hello Azure AD hizmet hesabı | Microsoft Docs"
description: "Bu konuda nasıl toorestore hello Azure AD hizmet hesabı belgeler."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, tooreset hello nasıl parolasını hello Azure AD Connect eşitleme Bağlayıcısı hizmeti hesabı"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Azure AD Connect eşitleme: nasıl toomanage hello Azure AD hizmet hesabı
Azure AD Bağlayıcısı Hello tarafından kullanılan hello hizmet hesabı toobe hizmet boş varsayılır. Kimlik bilgilerini tooreset gerekiyorsa, bu konu, ilgilidir. Örneğin, bir genel yönetici tarafından hata hello hizmet hesabının PowerShell kullanarak hello parola sıfırlama varsa.

## <a name="reset-hello-credentials"></a>Merhaba kimlik bilgilerini sıfırlama
Hello Azure AD Bağlayıcısı üzerinde tanımlı hello hizmet hesabı Azure AD tooauthentication sorunlar nedeniyle iletişim kuramazsa, hello parolanızı sıfırlayabilir.

1. Toohello Azure AD Connect eşitleme sunucusunda oturum açın ve PowerShell'i başlatın.
2. `Add-ADSyncAADServiceAccount` öğesini çalıştırın.  
   ![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Azure AD genel yönetici kimlik bilgilerini sağlayın.

Bu cmdlet hello hello hizmeti hesabının parolasını sıfırlar ve Azure AD hem de hello eşitleme altyapısı güncelleştirin.

## <a name="known-issues-these-steps-can-solve"></a>Bu adımları çözebilir bilinen sorunlar
Bu bölümde, Azure AD hizmet hesabı hello üzerinde sıfırlama kimlik bilgileri tarafından düzeltilen müşteriler tarafından bildirilen hataları listesidir.

- - -
Olay 6900  
Merhaba sunucu, bir parola değişikliği bildirimi işlenirken beklenmeyen bir hatayla karşılaştı:  
AADSTS70002: Hata doğrulama kimlik bilgileri. AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.

- - -
Olay 659  
Parola İlkesi eşitleme yapılandırması alınırken hata oluştu. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: Hata doğrulama kimlik bilgileri. AADSTS50054: Eski parola kimlik doğrulaması için kullanılır.

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

