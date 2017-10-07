---
title: "Uygulama proxy'si uygulama oluşturma aaaProblem | Microsoft Docs"
description: "Nasıl tootroubleshoot hello Azure AD yönetim portalında uygulama proxy'si uygulama oluşturmayı sorunları"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>Uygulama proxy'si uygulama oluşturma sorunu 

Aşağıda bazı hello yaygın sorunların çoğunu kişiler yüz yeni bir uygulama proxy'si uygulama oluştururken verilmiştir.

## <a name="recommended-documents"></a>Önerilen belgeler 

Merhaba Yönetici portalı üzerinden uygulama proxy'si uygulama oluşturma hakkında daha fazla toolearn bkz [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Belge hello adımlarını izleyerek ve Merhaba uygulaması oluşturulurken bir hata alma, hello hata ayrıntıları için bilgi ve öneriler nasıl toofix hello uygulama için bkz. Çoğu hata iletileri önerilen bir düzeltmeyi içerir. 

## <a name="specific-things-toocheck"></a>Belirli bir işlemi toocheck

tooavoid sık karşılaşılan doğrulayın:

-   Bir yönetici izni toocreate uygulama proxy'si uygulama ile

-   Merhaba İç URL benzersizdir

-   Merhaba dış URL benzersizdir

-   http veya https URL'leri başlangıcı hello ve sonunda bir "/"

-   Merhaba URL bir etki alanı adı ve IP adresi olmalıdır

Merhaba uygulaması oluşturduğunuzda hello sağ üst köşedeki hello hata iletisi görüntülenmelidir. Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.

   ![Bildirim istemi](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>Sonraki adımlar
[Hello Azure portalında uygulama ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md)
