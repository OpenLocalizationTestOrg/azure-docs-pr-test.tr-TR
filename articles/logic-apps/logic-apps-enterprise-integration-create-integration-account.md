---
title: "aaaCreate, bağlantı, silmek veya bir tümleştirme hesap Azure logic apps içinde taşımak | Microsoft Docs"
description: "Nasıl toocreate bir tümleştirme hesap ve tooyour logic apps Bağla"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Bir tümleştirme hesabı nedir?

Bir tümleştirme hesabı toomanage yapıları, şemalar, haritalar, sertifikalar, iş ortakları ve anlaşmaları dahil olmak üzere Kurumsal tümleştirme uygulamalarını sağlar. Oluşturduğunuz herhangi bir tümleştirme uygulama bu şemaları, haritalar, sertifikalar ve benzeri bir tümleştirme hesap tooaccess kullanır.

## <a name="create-an-integration-account"></a>Bir tümleştirme hesabı oluşturma

1.  İçinde toohello oturum [Azure portal](http://portal.azure.com "Azure portal"). Merhaba sol menüden seçin **daha fazla hizmet**.

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Merhaba hello sayfanın en üstünde, seçin **Ekle**.

    ![Seçin ekleme](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Ad tümleştirme hesabını ve select hello toouse istediğiniz Azure aboneliği. Oluşturabilir ya da yeni bir **kaynak grubu** veya varolan bir kaynak grubu seçin. Ardından bir **konumu** tümleştirme hesabınızı barındırmak için ve bir **fiyatlandırma katmanı**. 

    Hazır olduğunuzda, seçin **oluşturma**.

    ![Tümleştirme hesabının ayrıntılarını verin](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure tümleştirme hesabınızı 1 dakika içinde tamamlanmalıdır hello seçili konumda sağlar.

5. Merhaba sayfayı yenileyin. Yeni tümleştirme hesabınızı bakın.

    ![Yeni tümleştirme hesabınız görüntülenir](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Ardından, bu, oluşturulan tooyour mantıksal uygulama hello tümleştirme hesabı bağlayın. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Bir tümleştirme hesap tooa mantıksal uygulama bağlantı

toogive mantıksal uygulamalarınızı erişim toomaps, şemalar, anlaşmalar ve diğer yapıları tümleştirme hesabınızda, bağlantı hello tümleştirme hesap tooyour mantıksal uygulama.

### <a name="prerequisites"></a>Ön koşullar

* Bir tümleştirme hesabı
* Bir mantıksal uygulama

> [!NOTE] 
> Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun *aynı Azure konumuna* başlamadan önce.


1. Hello Azure portal, mantıksal uygulamanızı seçin ve mantığı uygulamanızın konumunu denetleyin.

    ![Mantıksal uygulamanızı seçin, konumunu denetleyin](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. Altında **ayarları**seçin **tümleştirme hesabını**.

    !["Tümleştirme hesabı" seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Merhaba gelen **tümleştirme hesabı seçin** listesinde, select hello tümleştirme hesap toolink tooyour mantıksal uygulama istiyorsanız. bağlama, toofinish seçin **kaydetmek**.

    ![Tümleştirme hesabınızı seçin](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Tümleştirmenize bağlantılı tooyour mantıksal uygulama hesabıdır ve tümleştirme hesabınızdaki tüm yapıları artık kullanılabilir tooyour mantıksal uygulama olduğunu gösteren bir bildirim alır.

    ![Mantıksal uygulamanızı bağlı tooyour tümleştirme hesabı](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Tümleştirme hesabınızın bağlantılı tooyour mantıksal uygulama olduğundan, mantıksal uygulamalarınızı hello B2B bağlayıcılar kullanabilirsiniz. XML doğrulaması ve düz dosya kodlama/kod çözme bazı ortak B2B bağlayıcıları içerir.  

## <a name="delete-your-integration-account"></a>Tümleştirme hesabınızı silme

1. Seçin **daha fazla hizmet**.

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Merhaba tümleştirme hesabı toodelete istediğinizi seçin.

    ![Tümleştirme hesap toodelete seçin](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Başlangıç menüsünde, **silmek**.

    !["Sil"'i seçin](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Seçim toodelete hello tümleştirme hesabınızı onaylayın.

## <a name="move-your-integration-account"></a>Tümleştirme hesabınızı taşıma

toomove tümleştirme hesap tooanother Azure abonelik veya kaynak grubu, şu adımları izleyin.

> [!IMPORTANT]
> Bir tümleştirme hesap taşıdıktan sonra tüm betikler toouse hello yeni kaynak kimlikleri güncelleştirmeniz gerekir.

1. Seçin **daha fazla hizmet**.

    !["Daha fazla Hizmetleri" seçin](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Merhaba tümleştirme hesabı toomove istediğinizi seçin. Altında **ayarları**, seçin **özellikleri**.

    ![Tümleştirme hesap toomove seçin. Ayarlarda, Özellikler'i seçin.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Merhaba kaynak grubu veya tümleştirme hesabınızla ilişkili Azure abonelik değiştirin.

    ![Kaynak grubu Değiştir veya değişiklik abonelik seçin](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Sonraki Adımlar
* [Anlaşmaları hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  

