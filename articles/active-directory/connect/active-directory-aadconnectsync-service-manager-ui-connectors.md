---
title: "hello Azure AD eşitleme hizmeti Yöneticisi kullanıcı Arabirimi aaaConnectors | Microsoft Docs"
description: "Merhaba bağlayıcılar sekmesinde hello Synchronization Service Manager için Azure AD Connect anlayın."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Bağlayıcıları hello Azure AD Connect Eşitleme Hizmeti Yöneticisi ile kullanma

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

Merhaba bağlayıcılar sekmesi tüm sistemler hello eşitleme altyapısı bağlı kullanılan toomanage aynıdır.

## <a name="connector-actions"></a>Bağlayıcı Eylemler
| Eylem | Açıklama |
| --- | --- |
| Oluştur |Kullanmayın. Tooadditional AD ormanına bağlanmak için hello Yükleme Sihirbazı'nı kullanın. |
| Özellikler |Etki alanı ve OU filtreleme için kullanılır. |
| [Silme](#delete) |Kullanılan tooeither hello veri hello bağlayıcı alanı veya ormanda toodelete bağlantı tooa silin. |
| [Çalıştırma profillerini Yapılandır](#configure-run-profiles) |Filtreleme, hiçbir şey etki alanı dışındaki tooconfigure burada. Bu eylemi kullanabilirsiniz zaten yapılandırılmış toosee farklı çalıştır profili. |
| Çalıştırın |Bir kerelik Çalıştır profilini toostart kullanılır. |
| Durdur |Çalışmakta olan bir profili bir bağlayıcı durdurur. |
| Bağlayıcı dışarı aktarma |Kullanmayın. |
| İçeri aktarma Bağlayıcısı |Kullanmayın. |
| Güncelleştirme Bağlayıcısı |Kullanmayın. |
| Şema Yenile |Merhaba önbellekteki şema yeniler. Bu tercih edilen toouse hello hello Yükleme Sihirbazı'nda bunun yerine, bu yana, aynı zamanda güncelleştirmeleri kuralları eşitleme seçenektir. |
| [Bağlayıcı alanı arama](#search-connector-space) |Kullanılan toofind nesneleri ve çok[bir nesne ve verileri hello sistemi aracılığıyla izleyin](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Sil
Merhaba silme eylemi iki farklı işlemler için kullanılır.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Merhaba seçeneği **silme yalnızca bağlayıcı alanı** Koru hello yapılandırma ancak tüm verileri kaldırır.

Merhaba seçeneği **bağlayıcı silin ve bağlayıcı alanı** hello verileri ve hello yapılandırma kaldırır. Tooconnect tooa orman artık istemediğinizde bu seçenek kullanılır.

Her iki seçenek, tüm nesneleri eşitlemek ve hello meta veri deposu nesne güncelleştirin. Bu işlem uzun süren bir işlemdir.

### <a name="configure-run-profiles"></a>Çalıştırma profillerini Yapılandır
Bu seçenek çalıştırma profili için bir bağlayıcı yapılandırılmış toosee hello sağlar.

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Bağlayıcı alanı arama
Merhaba arama bağlayıcı alanı eylemi yararlı toofind nesneleri ve veri sorunlarını giderme.

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Başlangıç seçerek bir **kapsam**. Bağlı veri (RDN, DN, bağlayıcı, alt ağacı), arama yapabilirsiniz veya durum hello nesnesinin (tüm diğer seçenekleri için).  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Örneğin bir alt ağacı arama yaparsanız, bir OU'daki tüm nesneleri alın.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
Bu kılavuzdan nesneyi seçin, seçin **özellikleri**, ve [izleyerek](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) hello meta veri deposu, aracılığıyla hello kaynak bağlayıcı alanı ve toohello hedef bağlayıcı alanı.

### <a name="changing-hello-ad-ds-account-password"></a>Merhaba AD DS hesap parolasını değiştirme
Merhaba hesap parolasını değiştirmek, hello eşitleme hizmeti artık mümkün tooimport/dışarı aktarma değişiklikleri tooon içi olacaktır AD.   Merhaba aşağıdakileri görebilirsiniz:

- Merhaba içeri/dışarı aktarma adım hello AD Bağlayıcısı için "-start-kimlik bilgileri yok" hatası ile başarısız olur.
- "Windows Olay Görüntüleyicisi altında hello uygulama olay günlüğüne olay kimliği 6000 ve ileti hatayla Merhaba kimlik bilgileri geçersiz olduğundan yönetim"Aracısı contoso.com başarısız oldu"toorun. Hello ifadesini" içerip

tooresolve hello vermek, hello aşağıdakileri kullanarak güncelleştirme hello AD DS kullanıcı hesabı:


1. Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.
</br>![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Toohello Git **Bağlayıcılar** sekmesi.
3. Merhaba yapılandırılmış toouse hello AD DS hesabı olan AD Bağlayıcısı seçin.
4. Eylemler altında seçin **özellikleri**.
5. Merhaba açılan iletişim kutusunda Bağlan tooActive Directory ormanı seçin:
6. Merhaba orman adı gösterir hello karşılık gelen şirket içi AD.
7. Eşitleme için kullanılan hello AD DS hesap Hello kullanıcı adı gösterir.
8. Yeni bir parola Hello hello AD DS hesabının hello parola metin kutusuna girin ![Azure AD Connect eşitleme şifreleme anahtarı yardımcı programı](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Tamam toosave hello yeni parola ve hello eşitleme hizmeti tooremove hello eski parola bellek önbelleğinden yeniden başlatın.



## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
