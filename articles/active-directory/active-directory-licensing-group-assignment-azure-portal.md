---
title: "Azure Active Directory'de aaaAssign lisansları tooa grubunun | Microsoft Docs"
description: "Azure Active Directory Grup lisans yoluyla tooassign toousers nasıl lisansları"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Azure Active Directory'de Grup üyeliğiyle lisansları toousers atayın

Bu makalede, Azure Active Directory'de (Azure AD) kullanıcı ürün lisansları tooa grubu atama ve bunlar doğru lisansa sahip emin doğrulama anlatılmaktadır.

Bu örnekte, hello Kiracı adlı bir güvenlik grubu içeren **ik departmanı**. Bu grubun tüm üyelerini hello İnsan Kaynakları departmanı (yaklaşık 1.000 kullanıcı) içerir. Office 365 Kurumsal E3 tooassign lisansları toohello tüm departman istiyor. Hello departmanı kullanmaya hazır toostart kadar hello hello ürüne dahil Yammer Kurumsal hizmeti geçici olarak devre dışı bırakılması gerekir. Ayrıca toodeploy Enterprise Mobility istediğiniz + güvenlik lisansları toohello aynı kullanıcı grubunu.

> [!NOTE]
> Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Bir lisans tooa kullanıcı atanabilmesi için önce Merhaba yönetici hello kullanıcı toospecify hello kullanım konumu özelliği sahip.

> Grup lisans atama için belirtilen bir kullanım konumu olmayan tüm kullanıcılar hello dizininin hello konumu devralır. Birden çok konumda kullanıcılar varsa, her zaman kullanım konumu, kullanıcı oluşturma akışının bir parçası, lisans atamasını hello sonucu her zaman doğru olduğundan ve kullanıcıların almadığınız sağlayacak Azure AD'de (örneğin AAD Connect yapılandırması aracılığıyla) - ayarlamanızı öneririz izin verilmeyen konumlarda Hizmetleri.

## <a name="step-1-assign-hello-required-licenses"></a>1. adım: gerekli hello lisansları atama

1. İçinde toohello oturum [ **Azure portal** ](https://portal.azure.com) bir yönetici hesabıyla. toomanage lisansları, hello hesap genel yönetici rolü veya kullanıcı hesabının yönetici olması gerekir.

2. Seçin **daha fazla hizmet** sol gezinti bölmesinde hello ve ardından **Azure Active Directory**. Bu dikey tooFavorites ekleyebilir veya toohello portalı panosunun sabitleyin.

3. Merhaba üzerinde **Azure Active Directory** dikey penceresinde, select **lisansları**. Burada görmek ve hello kiracıdaki tüm lisanslanabilir ürünlerini yönetmek bir dikey pencere açılır.

4. Altında **tüm ürünleri**, Office 365 Kurumsal E3 ve Enterprise Mobility + Security hello ürün adları işaretleyerek seçin. toostart hello atama, select **atamak** hello dikey penceresinde hello üstünde.

   ![Tüm ürünlerin lisans atayın](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Merhaba üzerinde **Ata lisans** dikey penceresinde tıklatın **kullanıcılar ve gruplar** tooopen hello **kullanıcılar ve gruplar** dikey. Merhaba grup adı arayın *ik departmanı*hello grubu seçin ve ardından tıklayarak emin tooconfirm olması **seçin** hello dikey penceresinde hello sonundaki.

   ![Bir grup seçin](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Merhaba üzerinde **Ata lisans** dikey penceresinde tıklatın **atama seçenekleri (isteğe bağlı)**, hello daha önce seçilen iki ürün dahil olan tüm hizmet planlarını görüntüler. Bul **Yammer Kurumsal** ve açıp **devre dışı** hello ürün lisansıyla hizmet toodisable. Tıklayarak onaylayın **Tamam** hello altındaki **atama seçenekleri**.

   ![Atama seçenekleri](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. Merhaba de toocomplete hello atamada **Ata lisans** dikey penceresinde tıklatın **atamak** hello dikey penceresinde hello sonundaki.

8. Bir bildirim hello durumunu ve hello işleminin sonucunu gösteren hello sağ üst köşesinde içinde görüntülenir. Merhaba atama toohello grubu (örneğin, nedeniyle önceden var olan lisans hello grubundaki) tamamlanamadı, hello hatanın hello bildirim tooview Ayrıntılar'ı tıklatın.

Biz şimdi hello ik departmanı grubu için bir lisans şablonu belirlediniz. Azure AD'de bir arka plan işlemi başlatıldı tooprocess tüm varolan grubun üyesi olmuştur. Bu ilk işlemi hello grubunun geçerli boyutunu hello bağlı olarak biraz zaman alabilir. Hello sonraki adımda, biz tooverify hello işlem nasıl bitirdi açıklamakta ve başka ilgilenilmesi gereken tooresolve sorunları olup olmadığını.

> [!NOTE]
> Başlatmak için alternatif bir konum aynı atama hello: **kullanıcılar ve gruplar** Azure AD'de. Çok Git**Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm grupları**. Hello grup bulmak, seçmek ve Git toohello **lisansları** sekmesini hello **atamak** düğme hello dikey üstünde hello lisans atama dikey penceresinde açar.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>2. adım: hello ilk atama tamamlandığını doğrulama

1. Çok Git**Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm grupları**. Hello bulur **ik departmanı** lisansı atanmış olan grup.

2. Merhaba üzerinde **ik departmanı** grubu dikey penceresi, select **lisansları**. Bu, hızlı bir şekilde lisansları toousers tam olarak atanmışsa ve içine toolook gereken herhangi bir hata varsa doğrulamanıza olanak tanır. Aşağıdaki bilgilerle hello kullanılabilir:

   - Şu anda ürün lisansları listesi toohello grubuna atanmış. Etkinleştirilmiş bir giriş tooshow hello belirli hizmetleri seçin ve toomake değiştirir.

   - Toohello grubu (Merhaba değişiklikleri işlenmekte olan veya tüm kullanıcı üyeler için işlemeyi bitirdikten varsa) yapılan hello en son lisans değişiklikler durumu.

   - Lisansları toothem atanamıyor çünkü bir hata durumunda olan kullanıcılar hakkında bilgi.

   ![Atama seçenekleri](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Daha ayrıntılı lisans altında işleme hakkında bilgi **Azure Active Directory** > **kullanıcılar ve gruplar** > *grup adı*  >  **Denetim günlüklerini**. Etkinlikleri izleyerek hello dikkat edin:

   - Etkinliği: **göre grubundaki lisans toousers uygulama Başlat**. Merhaba sistem hello lisans atamasını değişiminde hello grubu ve tooall kullanıcı üyeleri uygulama başlatıldığında seçer bu günlüğe kaydedilir. Yapıldığı hello değiştirme hakkında bilgi içerir.

   - Etkinliği: **göre grubundaki lisans toousers uygulama son**. Merhaba sistem hello gruptaki tüm kullanıcılar işlemeyi tamamladığında bu günlüğe kaydedilir. Kaç kullanıcı başarıyla işlendi ve kaç kullanıcı grubu lisansları atanamıyor özetini içerir.

   [Bu bölümde okuma](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn denetim günlüklerini grup tabanlı lisans tarafından kullanılan tooanalyze değişikliklerinin nasıl olabilir hakkında daha fazla bilgi.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>3. adım: lisans sorunlarını denetleyin ve çözümleyin

1. Çok Git**Azure Active Directory** > **kullanıcılar ve gruplar** > **tüm grupları**, hello bulun **ik departmanı**lisansı atanmış olan grup.
2. Merhaba üzerinde **ik departmanı** grubu dikey penceresi, select **lisansları**. Merhaba bildirim hello dikey üstünde lisansları için atanamıyor 10 kullanıcıları gösterir. Tıklatarak bu grup için bir lisans hatası durumunda tüm kullanıcıların listesini açar.
3. Merhaba **başarısız atamalar** sütun söyler bize her iki ürün lisansları toohello kullanıcılar atanamıyor. Merhaba **üst başarısızlık nedeni** sütun hello hatanın nedenini hello içerir. Bu durumda, sahip **çakışan hizmet planları**.

   ![Başarısız atamalar](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Bir kullanıcı tooopen hello seçin **lisansları** dikey. Bu dikey toohello kullanıcı şu anda atanmış olan tüm lisanslar gösterir. Bu örnekte, hello kullanıcının hello devralındı hello Office 365 Kurumsal E1 lisans sahip **bilgi noktası kullanıcılar** grubu. Bu çalıştı sistem tooapply hello gelen hello hello E3 lisans çakışıyor **ik departmanı** grubu. Sonuç olarak, bu gruptan hello lisansları hiçbiri toohello kullanıcıya atandı.

   ![Bir kullanıcı için Görünüm lisansları](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve Kaldır hello hello kullanıcıdan bu çakışma **bilgi noktası kullanıcılar** grubu. Azure AD hello değişiklik işledikten sonra hello **ik departmanı** lisansları doğru atanır.

   ![Lisansı doğru atandı](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Sonraki adımlar

toolearn hello özelliği hakkında daha fazla lisans Yönetim grupları, üzerinden için ayarlanmış makaleler hello bakın:

* [Grup tabanlı Azure Active Directory lisanslaması nedir?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory'deki bir gruba lisans sorunlarını tanımlama ve](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate tek tek kullanıcılar toogroup tabanlı Azure Active Directory'de lisanslama nasıl lisanslı](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory grup tabanlı ilave senaryolar lisanslama](active-directory-licensing-group-advanced.md)
