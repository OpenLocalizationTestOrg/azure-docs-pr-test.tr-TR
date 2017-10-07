---
title: "tek tek lisanslı kullanıcılar tooa Azure Active Directory'de Grup aaaHow toomigrate | Microsoft Docs"
description: "Nasıl toogroup tabanlı Azure Active Directory'yi kullanarak lisans tooswitch tek tek kullanıcı lisansları"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Azure Active Directory'de lisans için tooadd kullanıcılar tooa grubunun nasıl lisanslı

Varolan dağıtılmış lisansları toousers hello kuruluşlar "doğrudan atama"; aracılığıyla olabilir diğer bir deyişle, PowerShell komut dosyaları veya diğer araçlar tooassign tek tek kullanıcı lisansları kullanıyor. Grup tabanlı lisans toomanage kuruluşunuzda lisanslarla toostart isterseniz, bir geçiş gerekir planı tooseamlessly var olan çözümler grup tabanlı lisanslama ile değiştirin.

Burada, geçirme toogroup tabanlı lisans geçici olarak, şu anda atanmış lisansları kaybetme kullanıcılar neden olacak bir durum kaçınmalısınız Hello en önemli şey tookeep aklınızda olur. Lisansları kaldırılmasına neden herhangi bir işlem olmalıdır tooremove hello kullanıcıların erişim tooservices ve kendi veri kaybetme riskini engellendi.

## <a name="recommended-migration-process"></a>Önerilen geçiş işlemi

1. Lisans atama ve kullanıcılar için temizleme yönetme var olan Otomasyon (örneğin, PowerShell) sahip. Çalışan olduğu gibi bırakın.

2. Yeni bir lisans grubu oluşturma (veya var olan hangi toouse gruplar karar) ve gerekli tüm kullanıcıların üye olarak ekleneceği emin olun.

3. Gerekli hello lisansları toothose grupları atama; Amacınız tooreflect hello olmalıdır aynı durumu lisans, var olan Otomasyon (örneğin, PowerShell) toothose kullanıcılar da uyguluyor.

4. Lisansları uygulanan tooall kullanıcılar bu gruplara verildiğinden emin olun. Bu, her grup hello işleme durumunu denetleyerek ve denetim günlüklerini denetleyerek yapılabilir.

  - Nokta onay bireysel kullanıcılar kendi lisans ayrıntıları bakarak yapabilirsiniz. Bunlar sahip Merhaba, aynı "doğrudan" atanan lisansları ve "devralınan" gruplarından görürsünüz.

  - Bir PowerShell Betiği çok çalıştırabilirsiniz[lisansları toousers nasıl atandığını doğrulayın](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Merhaba aynı Ürün lisans toohello kullanıcı hem doğrudan hem de bir grubu üzerinden atandığında, yalnızca bir lisans hello kullanıcı tarafından kullanılır. Bu nedenle hiçbir ek lisanslar gerekli tooperform geçiş ' dir.

5. Hiçbir lisans anlaşmalarını hata durumuna kullanıcılar için her grubu denetleyerek başarısız olduğunu doğrulayın. Daha fazla bilgi için bkz: [belirleme ve bir grubu için lisans sorunlarını çözmek](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Merhaba özgün doğrudan atamalarını kaldırmayı düşünün; toodo isteyebilirsiniz "Dalgalar", toomonitor içinde kademeli olarak, hello sonucu bir kullanıcı alt kümesini üzerinde ilk.

  Kullanıcıların özgün doğrudan atamalarını hello bırakabilir, ancak hello kullanıcılar hala korur, lisanslı gruplarına ayrıldığında büyük olasılıkla hello özgün lisans istediğiniz istediğiniz.

## <a name="an-example"></a>Bir örnek

1.000 kullanıcının bulunduğu bir kuruluşta sahibiz. Tüm kullanıcılar, Enterprise Mobility + güvenlik (EMS) lisansı gerektirir. 200 kullanıcılar hello Finans departmanı ve Office 365 Kurumsal E3 lisanslar gerektirir. Ekleme ve lisans dönün ve Git gibi kullanıcılardan kaldırma şirket içinde çalışan bir PowerShell komut dosyası sunuyoruz. Lisanslar otomatik olarak Azure AD tarafından yönetilen şekilde grup tabanlı lisanslama ile tooreplace hello betik istiyoruz.

İşte hangi hello geçiş işlemi görünüm ister:

1. Azure portal Ata hello EMS lisansı toohello hello kullanarak **tüm kullanıcılar** Azure AD grubu. Merhaba E3 lisans toohello Ata **Finans departmanı** tüm gerekli hello kullanıcıları içeren grup.

2. Her grup için tüm kullanıcılar için lisans atama tamamlandığını onaylayın. Her grup için select gidin toohello dikey **lisansları**ve hello hello üstündeki hello işleme durumunu denetleyin **lisansları** dikey.

  - Aramak için "en son lisans değişiklikleri uygulanan tooall kullanıcılar silinmiş" tooconfirm işleme tamamlandı.

  - Üstteki kendisi için lisansları olmayan başarıyla atanmış olan kullanıcılar hakkında bir bildirim arayın. Bazı kullanıcılar için lisans dışında karşılaştınız mı? Bazı kullanıcılar, çakışan lisans grubu lisansları Devralmayı Engelle SKU'ları var mı?

3. Nokta hello doğrudan ve uygulanan Grup lisansları sahip oldukları bazı kullanıcılar tooverify denetleyin. Bir kullanıcı seçin dikey penceresine gidin toohello **lisansları**ve lisansları hello durumunu inceleyin.

  - Bu beklenen hello kullanıcı durumu geçiş işlemi sırasında oluşur:

      ![Beklenen kullanıcı durumu](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Bu, hem doğrudan hem de devralınan lisansları hello kullanıcının sahip doğrular. Biz, bkz: her ikisi de **EMS** ve **E3** atanır.

  - Her etkin hello Hizmetleri Lisans tooshow ayrıntılarını seçin. Merhaba doğrudan ve Grup lisansları etkinleştir hello kullanıcı için aynı hizmet planları tam olarak Merhaba, bu kullanılan toocheck olabilir.

      ![hizmet planları denetleyin](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Hem doğrudan hem de Grup lisansları eşdeğer olduğunu doğruladıktan sonra kullanıcıları doğrudan lisanslarını kaldırma başlatabilirsiniz. Merhaba Portalı'nda bireysel kullanıcılar için kaldırarak bunu test etmek ve ardından toplu olarak kaldırılan Otomasyon betikleri toohave çalıştırın. Aynı kullanıcı hello doğrudan lisansların hello portalı üzerinden kaldırıldı hello bir örneği burada verilmiştir. Merhaba lisans durumu değişmeden kalır, ancak biz artık doğrudan atamaları görmek dikkat edin.

  ![doğrudan lisansları kaldırıldı](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Sonraki adımlar

toolearn grupları aracılığıyla lisans yönetimi için diğer senaryolar hakkında daha fazla okuma

* [Azure Active Directory'de lisansları tooa grup atama](active-directory-licensing-group-assignment-azure-portal.md)
* [Grup tabanlı Azure Active Directory lisanslaması nedir?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory'deki bir gruba lisans sorunlarını tanımlama ve](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory grup tabanlı ilave senaryolar lisanslama](active-directory-licensing-group-advanced.md)
