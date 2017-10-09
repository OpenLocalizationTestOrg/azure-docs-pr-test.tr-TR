---
title: "Azure Otomasyonu hesabı aaaManage | Microsoft Docs"
description: "Bu makalede nasıl toomanage hello Otomasyon hesabınızın sertifika yenileme, silme ve yanlış yapılandırılması gibi yapılandırma açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Azure Otomasyonu hesabını yönetme
Belirli bir noktada, Automation hesabınız süresi dolmadan önce toorenew hello sertifika gerekir. Bu farklı çalıştır hesabı hello tehlikeye düşünüyorsanız, silin ve yeniden oluşturun. Bu bölümde ele alınmaktadır nasıl tooperform bu işlemler.

## <a name="self-signed-certificate-renewal"></a>Otomatik olarak imzalanan sertifika yenileme
hello farklı çalıştır hesabı için oluşturulan hello otomatik olarak imzalanan sertifika oluşturma başlangıç tarihinden itibaren bir yıl süresi dolar. Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz. Yenilediğinizde, yukarı veya etkin olarak çalışan sıraya ve bu farklı çalıştır hesabını hello ile kimlik doğrulaması runbook'ları olumsuz etkilenmez tutulan tooensure hello geçerli geçerli sertifika yok. Merhaba sertifika sona erme tarihini kadar geçerli kalır.

> [!NOTE]
> Automation farklı çalıştır hesabı toouse, kuruluş sertifika yetkiliniz tarafından verilen bir sertifika yapılandırdıktan ve bu seçeneği kullanırsanız, hello Kurumsal Sertifika tarafından otomatik olarak imzalanan bir sertifika kullanılacaktır.

toorenew hello sertifika, aşağıdaki hello:

1. Hello Azure portal, hello Automation hesabını açın.

2. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello **hesap özellikleri** bölmesi altında **hesap ayarlarını**seçin **farklı çalıştır hesapları**.

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-manage-account/automation-account-properties-pane.png)
3. Merhaba üzerinde **farklı çalıştır hesapları** ya da hello Çalıştır hesabı veya toorenew hello sertifika için istediğiniz hello Klasik farklı çalıştır hesabı olarak özellikleri dikey penceresinde, seçin.

4. Merhaba üzerinde **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **yenileme sertifika**.

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Merhaba sertifika yenileme sırasında altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme
Bu bölümde açıklanmıştır nasıl toodelete ve bir farklı çalıştır veya Klasik farklı çalıştır hesabını yeniden oluşturun. Bu eylemi gerçekleştirdiğinizde, hello Otomasyon hesabı korunur. Bir farklı çalıştır veya Klasik farklı çalıştır hesabını sildikten sonra hello Azure portalında yeniden oluşturabilirsiniz.

1. Hello Azure portal, hello Automation hesabını açın.

2. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello hesap Özellikler bölmesinde, **farklı çalıştır hesapları**.

3. Merhaba üzerinde **farklı çalıştır hesapları** özellikleri dikey penceresinde, seçin ya da hello Çalıştır hesabı veya Klasik farklı çalıştır hesabı toodelete istiyor. Ardından, hello **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **silmek**.

 ![Farklı Çalıştır hesabını silme](media/automation-manage-account/automation-account-delete-runas.png)

4. Merhaba hesap silindi, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

5. Merhaba hesabı silindikten sonra bunu hello üzerinde yeniden oluşturabilirsiniz **farklı çalıştır hesapları** hello seçerek özellikler dikey penceresini oluşturma seçeneği **Azure farklı çalıştır hesabını**.

 ![Merhaba Automation farklı çalıştır hesabını yeniden oluşturun](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Yanlış yapılandırma
Merhaba Çalıştır veya Klasik farklı çalıştır hesabı toofunction için gereken bazı yapılandırma öğeleri düzgün silinmiş veya yanlış ilk kurulum sırasında oluşturuldu. Merhaba öğeleri içerir:

* Sertifika varlığı
* Bağlantı varlığı
* Farklı Çalıştır hesabı hello katkıda bulunan rolü ' kaldırıldı
* Azure AD'de hizmet sorumlusu veya uygulama

Hello önceki ve diğer örnekleri yanlış hello Otomasyon hesabı hello değiştirir ve durumunu görüntüler algılar *tamamlanmamış* hello üzerinde **farklı çalıştır hesapları** hello özellikleri dikey penceresi hesabı.

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Merhaba farklı çalıştır hesabı seçin, hesap hello **özellikleri** bölmesi hello aşağıdaki hata iletisini görüntüler:

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Bu farklı çalıştır hesabı sorunları hızla, silme ve hello hesabını yeniden oluşturmayı da çözebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Hizmet sorumluları hakkında daha fazla bilgi için çok başvuran[uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).
* Azure automation'da rol tabanlı erişim denetimi hakkında daha fazla bilgi için çok başvuran[Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md).
* Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için çok başvuran[Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).
