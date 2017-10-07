---
title: "Azure AD Connect eşitleme: dizin uzantıları | Microsoft Docs"
description: "Bu konu, Azure AD CONNECT'te hello dizin uzantıları özelliğini açıklar."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Azure AD Connect eşitleme: dizin uzantıları
Dizin uzantıları sağlar. tooextend hello şema şirket içi Active Directory'den kendi özniteliklerle Azure ad'deki. Bu özellik toomanage şirket içi devam öznitelikleri kullanma toobuild LOB uygulamalarını sağlar. Bu öznitelikler aracılığıyla tüketilebilir [Azure AD grafik dizin uzantıları](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) veya [Microsoft Graph](https://graph.microsoft.io/). Merhaba öznitelikleri kullanılabilir kullanarak görebilirsiniz [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net) ve [Microsoft Graph Explorer'a](https://graphexplorer2.azurewebsites.net/) sırasıyla.

Şu anda hiçbir Office 365 iş yükü bu öznitelikler tüketir.

Hangi ek öznitelikleri yapılandırabilirsiniz hello Yükleme Sihirbazı'nı hello özel ayarları yolunda toosynchronize istiyor.
![Şema genişletme Sihirbazı](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
Geçerli adaylar öznitelikleri aşağıdaki hello Hello yüklemesini göstermektedir:

* Kullanıcı ve grup nesne türleri
* Tek değerli öznitelikler: dize, Boolean, tamsayı, ikili
* Birden çok değerli öznitelikleri: dize, ikili

Azure AD Connect yüklemesi sırasında oluşturulan hello şema önbelleğinden Hello özniteliklerinin listesini okuyun. Ek öznitelikler ile Merhaba Active Directory şemasını genişlettiyseniz, ardından hello [şema yenileneceğini](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) önce bu yeni öznitelikler görünür.

Azure AD'de bir nesne too100 dizin uzantıları nitelikler olabilir. Merhaba uzunluk üst sınırı 250 karakterdir. Bir öznitelik değeri uzunsa hello eşitleme altyapısı tarafından kesilir.

Azure AD Connect yüklemesi sırasında bir uygulama bu öznitelikler kullanılabildiği kaydedilir. Bu uygulamada hello Azure portal görebilirsiniz.  
![Şema uzantısı uygulama](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Bu öznitelikler artık grafik kullanılabilir:  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Merhaba öznitelikleri uzantısıyla önekli\_{AppClientId}\_. Merhaba AppClientId aynı Azure AD kiracınızdaki tüm öznitelikleri değeri hello sahiptir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
