---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir


## <a name="task-3-configure-administrative-group"></a>Görev 3: yönetim grubunu yapılandır
Bu yapılandırma görevi, Azure AD dizininde bir yönetim grubu oluşturun. Bu özel yönetim grubu adı *AAD DC Yöneticiler*. Bu grubun üyeleri, etki alanına katılmış toohello yönetilen etki alanı olan makinelere sunucuda yönetici izinleri verilir. Etki alanına katılmış makinelerde toohello Yöneticiler grubunun bu gruba eklenir. Ayrıca, bu grubun üyeleri, Uzak Masaüstü tooconnect uzaktan toodomain katılmış makineler kullanabilirsiniz.

> [!NOTE]
> Azure Active Directory etki alanı Hizmetleri kullanılarak oluşturulan hello yönetilen etki alanındaki etki alanı yöneticisi veya kuruluş yöneticisi izinlerine sahip değil. Yönetilen etki alanlarında, bu izinleri hello hizmeti tarafından ayrılmış ve hello Kiracı içinde kullanılabilir toousers duruma getirilmez. Hello özel yönetim grubu oluşturulan kullanabilirsiniz ancak bu yapılandırma görevi tooperform bazı işlemleri ayrıcalıklı. Bu işlemler, bilgisayarlar toohello etki alanına katılma, etki alanına katılan makineler toohello yönetim grubuna ait ve Grup İlkesi yapılandırma içerir.
>

Başlangıç Sihirbazı otomatik olarak Azure AD dizininizi hello yönetim grubu oluşturur. Bu grubun 'AAD DC Yöneticiler' denir. Bu ada sahip varolan bir grubu Azure AD dizininizi varsa, bu grubun hello Sihirbazı'nı seçer. Grup üyeliği hello kullanarak yapılandırabilirsiniz **yönetici grubuna** sihirbaz sayfası.

1. tooconfigure grup üyeliği tıklatın **AAD DC Yöneticiler**.

    ![Grup üyeliğini Yapılandır](./media/getting-started/domain-services-blade-admingroup.png)

2. Merhaba tıklatın **üye eklemek** düğmesini tooadd kullanıcılar, Azure AD directory toohello yönetici grubundan.

3. İşiniz bittiğinde tıklatın **Tamam** toomove toohello üzerinde **özeti** hello sihirbazın sayfası.

4. Merhaba üzerinde **Özet** hello sihirbazının hello yönetilen etki alanı için gözden geçirme hello yapılandırma ayarları. Merhaba Sihirbazı toomake değişikliklerden tooany adım gerekirse geri dönebilirsiniz. İşiniz bittiğinde tıklatın **Tamam** toocreate hello yeni yönetilen etki alanı.

    ![Özet](./media/getting-started/domain-services-blade-summary.png)

5. Azure AD etki alanı Hizmetleri dağıtımınızın hello ilerleme durumunu gösteren bir bildirim görür. Merhaba bildirime tıklayın toosee ayrıntılı hello dağıtımı devam ediyor.

    ![Bildirim - dağıtımı devam ediyor](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Yönetilen etki alanınızı sağlama
Yönetilen etki alanınızı sağlama işleminin hello tooan saat sürebilir.

1. Dağıtımınızı sürerken ' etki alanı Hizmetleri'nde' hello arayabilirsiniz **arama kaynakları** arama kutusu. Seçin **Azure AD etki alanı Hizmetleri** hello arama sonuç. Merhaba **Azure AD etki alanı Hizmetleri** sağlanmakta hello yönetilen etki dikey penceresinde listelenir.

    ![Yönetilen etki alanı sağlanacak Bul](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Merhaba etki alanı hakkında daha fazla ayrıntı hello yönetilen etki alanı (örneğin, ' contoso100.com') toosee Hello adına tıklayın.

    ![Etki alanı hizmetleri - sağlama durumu](./media/getting-started/domain-services-provisioning-state.png)

3. Merhaba **genel bakış** sekmesi gösterir hello etki şu anda hazırlanır. Tam olarak sağlanana kadar hello yönetilen etki alanı yapılandıramazsınız. Tam olarak sağlanan, yönetilen etki alanı toobe tooan saattir yukarı sürebilir.

    ![Etki alanı hizmetleri - sağlama durumu hello sırasında genel bakış sekmesi ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Merhaba yönetilen etki alanı tam olarak sağlandığında hello **genel bakış** sekmesi gösterir hello etki alanı durumu olarak **çalıştıran**.

    ![Etki Alanı Hizmetleri - Tamamen hazır haldeki Genel Bakış sekmesi](./media/getting-started/domain-services-provisioned.png)

5. Merhaba üzerinde **özellikleri** sekmesine, etki alanı denetleyicileri hello sanal ağı için kullanılabilen iki IP adresi bakın.

    ![Etki Alanı Hizmetleri - tam olarak sağlanan sonra Özellikleri sekmesi](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Sonraki adım
[Görev 4: hello hello Azure sanal ağı için DNS ayarlarını güncelleştirme](active-directory-ds-getting-started-dns.md)
