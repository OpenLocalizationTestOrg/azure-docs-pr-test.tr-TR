---
title: "Azure AD Connect: Bir Active Directory Federasyon Hizmetleri (AD FS) grubu güncelleştirme hello SSL sertifikası | Microsoft Docs"
description: "Bu belge ayrıntıları hello adımları tooupdate hello SSL sertifikasını Azure AD Connect kullanarak AD FS grubunda."
services: active-directory
keywords: "Azure ad connect, adfs ssl güncelleştirme, adfs sertifika güncelleştirme, değişiklik adfs sertifika, yeni adfs sertifika, adfs sertifika ssl sertifikası, güncelleştirme ssl sertifikası adfs, adfs ssl sertifikası, adfs, ssl, sertifika, adfs hizmet iletişimi sertifikasına, güncelleştirme Federasyon yapılandırma, güncelleştirme adfs Federasyon yapılandırma, aad bağlanma"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Bir Active Directory Federasyon Hizmetleri (AD FS) grubu için Hello SSL sertifikasını güncelleştir

## <a name="overview"></a>Genel Bakış
Bu makalede, Azure AD Connect tooupdate hello SSL sertifikası bir Active Directory Federasyon Hizmetleri (AD FS) grubu için nasıl kullanabileceğiniz açıklanır. AD FS oturum açma hello kullanıcı yöntemi seçili olmasa bile, başlangıç AD FS grubu için hello Azure AD Connect aracı tooeasily güncelleştirme hello SSL sertifikası kullanabilirsiniz.

Tüm Federasyon ve üç basit adımda Web uygulaması Ara sunucusu (WAP) sunucuları arasında hello AD FS grubu için SSL sertifikası güncelleştirme hello tüm işlem gerçekleştirebilirsiniz:

![Üç adımı](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>Daha fazla AD FS tarafından kullanılan sertifikalar hakkında toolearn bkz [AD FS tarafından kullanılan sertifikaları anlama](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Ön koşullar

* **AD FS grubu**: AD FS grubunuzu tabanlı Windows Server 2012 R2 veya sonrası olduğundan emin olun.
* **Azure AD Connect**: Bu hello emin olun, Azure AD Connect sürümüdür 1.1.443.0 veya sonraki bir sürümü. Merhaba görev kullanacağınız **güncelleştirme AD FS SSL sertifikası**.

![Güncelleştirme SSL görevi](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>1. adım: AD FS grubu bilgileri sağlayın

Azure AD Connect hello AD FS grubunu tooobtain bilgilerini tarafından otomatik olarak çalışır:
1. AD FS (Windows Server 2016 veya sonraki) Hello grubu bilgileri sorgulama.
2. Azure AD Connect ile yerel olarak depolanan önceki çalıştığında, başvuru hello bilgileri.

Merhaba ekleyerek veya kaldırarak hello sunucuları tooreflect hello geçerli yapılandırmasını hello AD FS grubunu görüntülenen sunucularının listesini değiştirebilirsiniz. Merhaba sunucu bilgilerini sağlanan hemen Azure AD Connect hello bağlantısı ve geçerli SSL sertifikası durumunu görüntüler.

![AD FS sunucu bilgisi](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Merhaba listesi artık hello AD FS grubunun parçası olan bir sunucu içeriyorsa, tıklatın **kaldırmak** , AD FS grubunuzdaki sunucuların hello listeden toodelete hello sunucusu.

![Çevrimdışı sunucu listesinde](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Merhaba listesinden bir sunucu kaldırma sunucuların bir AD FS için Azure AD Connect grupta yerel bir işlemdir ve bilgi hello Azure AD Connect yerel olarak tutar AD FS grubu için güncelleştirmeleri hello. Azure AD Connect, AD FS tooreflect hello değişiklik hello yapılandırmayı değiştirmeniz değil.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>2. adım: yeni bir SSL sertifikası sağlayın

AD FS grubu sunucuları hakkında bilgi hello onaylanıp sonra Azure AD Connect hello yeni SSL sertifikası için sorar. Bir parola korumalı PFX sertifika toocontinue hello yükleme sağlar.

![SSL sertifikası](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Merhaba sertifika verdikten sonra Azure AD Connect Önkoşullar bir dizi aracılığıyla gider. Sertifika hello hello sertifika tooensure hello AD FS grubu için doğru olduğundan emin olun:

-   Merhaba hello sertifikanın konu adı/alternatif konu adı, aynı hello Federasyon Hizmeti adı Merhaba, veya joker sertifikadır olur.
-   Merhaba sertifika 30 günden fazla bir süre için geçerlidir.
-   Merhaba sertifika güven zinciri geçerli değil.
-   Merhaba, parola korumalı sertifikasıdır.

## <a name="step-3-select-servers-for-hello-update"></a>3. adım: hello güncelleştirme sunucuları seçin

Merhaba sonraki adımda, güncelleştirilmiş toohave hello SSL sertifikasına sahip olmanız hello sunucuları seçin. Çevrimdışı sunucuları hello güncelleştirmesi seçilemez.

![Sunucuları tooupdate seçin](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Merhaba yapılandırmayı tamamladıktan sonra Azure AD Connect hello güncelleştirme hello durumunu gösterir ve bir seçenek tooverify hello AD FS oturum açma sağlayan hello iletisi görüntüler.

![Yapılandırma tamamlandı](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>SSS

* **Ne hello sertifikasının konu adını hello hello yeni AD FS SSL sertifikası için olması gerekiyor mu?**

    Azure AD Connect hello sertifikanın konu adı/alternatif konu adı hello hello Federasyon Hizmeti adı içerip içermediğini denetler. Örneğin, Federasyon Hizmeti adınız fs.contoso.com ise fs.contoso.com hello konu adı/alternatif konu adı olmalıdır.  Joker karakterli sertifikalar da kabul edilir.

* **Neden kimlik bilgilerini hello WAP sunucusu sayfasında yeniden soruluyor?**

    TooAD FS sunucularına bağlanmak için sağladığınız hello kimlik bilgilerini de hello ayrıcalık toomanage hello WAP sunucuları yoksa, Azure AD Connect hello WAP sunucularında yönetici ayrıcalıklarına sahip kimlik bilgilerini ister.

* **Merhaba sunucu çevrimdışı olarak gösterilir. Ne yapmalıyım?**

    Merhaba sunucu çevrimdışıysa azure AD Connect hiçbir işlem gerçekleştirilemiyor. Merhaba sunucusu hello AD FS grubunu parçası ise, hello bağlantı toohello sunucu denetleyin. Merhaba sorunun giderilmiş sonra hello Yenile simgesine tooupdate hello durum hello Sihirbazı'nda tuşuna basın. Merhaba bölümü sunucusuysa Merhaba grubu daha önce ancak şimdi artık var, tıklatın **kaldırmak** toodelete, Azure AD Connect sunucuları hello listesinden korur. Azure AD Connect hello listesinden kaldırmayı hello sunucu hello AD FS yapılandırmasını kendisini değiştirmez. AD FS Windows Server 2016 veya sonraki sürümlerde, hello sunucu kalır hello yapılandırma ayarlarında kullanıyorsanız ve gösterilecek yeniden hello sonraki kez hello görev çalıştırılır.

* **Merhaba yeni SSL sertifikası ile bir alt grup Sunucularım kümesini güncelleştirebilir miyim?**

    Evet. Merhaba görev her zaman çalıştırabilirsiniz **SSL sertifikasını Güncelleştir** yeniden sunucuları kalan tooupdate hello. Merhaba üzerinde **Select sunucuları için SSL sertifika güncelleştirme** sayfasında, üzerinde hello sunucularının listesini sıralayabilirsiniz **SSL sona erme tarihi** henüz güncelleştirilmemiş tooeasily erişim hello sunucuları.

* **Merhaba Server'da çalıştırmak hello önceki kaldırıldı, ancak bunu hala çevrimdışı ve listelenen olarak hello AD FS sunucuları sayfasında gösteriliyor. Neden kaldırdım bile sonra hello çevrimdışı sunucu hala var mı?**

    Azure AD Connect hello listesinden kaldırmayı hello sunucu hello AD FS yapılandırmasını kaldırmaz. Azure AD Connect hello grubu hakkındaki tüm bilgileri için AD FS (Windows Server 2016 veya daha yüksek) başvuruyor. Merhaba sunucu hello AD FS yapılandırmasını hala varsa, geri hello listesinde listelenir.  

## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD Connect ve federasyon](active-directory-aadconnectfed-whatis.md)
- [Active Directory Federasyon Hizmetleri Yönetimi ve Azure AD Connect ile özelleştirme](active-directory-aadconnect-federation-management.md)
