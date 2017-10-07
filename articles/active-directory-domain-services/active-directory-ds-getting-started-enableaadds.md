---
title: "Azure Active Directory Domain Services: Azure Active Directory Domain Services’ı etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Görev 3: Azure Active Directory Domain Services'i etkinleştirme
Bu görevde, aşağıdaki adımları hello yaparak dizininiz için Azure Active Directory etki alanı Hizmetleri (Azure AD DS) etkinleştirin:

1. Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba Hello sol bölmesinde seçin **Active Directory** düğmesi.
3. Azure AD DS tooenable istediğiniz hello Azure Active Directory (Azure AD) kiracısını (dizin) seçin.

    ![Azure AD Dizini Seçme](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Merhaba üzerinde **Önizleme dizin** hello sayfasında, **yapılandırma** sekmesi.

    ![Dizinin yapılandır sekmesi](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Altında **etki alanı Hizmetleri**, hello değiştirme **bu dizin için etki alanı Hizmetleri'ni etkinleştirme** çok seçenek**Evet**.  
    Ek Azure Active Directory etki alanı Hizmetleri yapılandırma seçenekleri hello sayfasında görüntülenir.

    ![Etki Alanı Hizmetlerini Etkinleştirme](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Azure Active Directory etki alanı Hizmetleri kiracınız için etkinleştirdiğinizde, Azure AD oluşturur ve kullanıcıların kimliğini doğrulamak için gerekli olan hello Kerberos ve NTLM kimlik bilgisi karmalarını depolar.
   >
   >
6. Merhaba belirtin **DNS etki alanı adı, etki alanı Hizmetleri'nin**.

   * Merhaba dizinin Hello varsayılan etki alanı adı (ile bir **. onmicrosoft.com** soneki) varsayılan olarak seçilidir.

   * Merhaba liste Azure AD dizininiz için yapılandırılan tüm etki alanlarını içerir, her ikisi de dahil olmak üzere doğrulandı ve doğrulanmamış hello üzerinde yapılandırdığınız etki alanları **etki alanları** sekmesi.

   * Özel bir etki alanı adı da girebilirsiniz. Bu örnekte, hello özel etki alanı adıdır *contoso100.com*.

     > [!WARNING]
     > Belirtilen etki alanı adınızı Hello önek (örneğin, *contoso100* hello içinde *contoso100.com* etki alanı adı) 15 veya daha az karakter içermelidir. 15 karakterden uzun bir ön ek ile Azure Active Directory Domain Services etki alanı oluşturamazsınız.
     >
     >
7. Etki alanı zaten hello sanal ağında yok, yönetilen hello için seçtiğiniz bu hello DNS etki alanı adını sağlayın. Özellikle, toosee olup olmadığını kontrol edin:

   * Merhaba sahip bir etki alanı zaten hello sanal ağda aynı DNS etki alanı adı.

   * Merhaba seçtiğiniz sanal ağ varsa ile şirket içi ağınıza bir VPN bağlantısı ve bir etki alanı hello ile şirket içi ağınızda aynı DNS etki alanı adı.

   * Bu ada sahip olan bir bulut hizmetini hello sanal ağda bulunan.
8. Azure Active Directory etki alanı Hizmetleri toobe kullanılabilir istediğiniz bir sanal ağı seçin. Merhaba sanal ağ ve hello oluşturduğunuz ayrılmış bir alt ağ seçin **Bağlan etki alanı Hizmetleri toothis sanal ağ** aşağı açılan liste. Ayrıca hello aşağıdakileri dikkate alın:

   * Belirttiğiniz hello sanal ağının tooan Azure Active Directory etki alanı Hizmetleri tarafından desteklenen Azure bölgesine ait emin olun. tooascertain Azure Active Directory etki alanı Hizmetleri kullanılabilir olduğu Azure bölgelerini Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).

   * Burada Azure Active Directory etki alanı Hizmetleri desteklenmiyor tooa bölgeye ait sanal ağlar hello aşağı açılan listesinde görünmüyor.

   * Ayrılmış bir alt ağ hello sanal ağ içinde Azure Active Directory etki alanı Hizmetleri için kullanın. Yapmak *değil* hello ağ geçidi alt ağı seçin. Bkz. [ağ ile ilgili dikkat edilmesi gerekenler](active-directory-ds-networking.md).

   * Benzer şekilde, Azure Resource Manager kullanılarak oluşturulan sanal ağlar hello aşağı açılan listede görünmez. Resource Manager tabanlı sanal ağlar şu anda Azure Active Directory Domain Services'de desteklenmemektedir.
9. tooenable Azure Active Directory etki alanı Hizmetleri, hello sayfanın hello sonundaki hello görev bölmesinde tıklatın **kaydetmek**.
    * Azure Active Directory etki alanı Hizmetleri dizininiz için etkin durumdayken, hello sayfası durumunu görüntüler *bekleyen*.

        ![Domain Services Etkinleştirme penceresi](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services, yönetilen etki alanınız için yüksek kullanılabilirlik sağlar. Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdikten sonra etki alanı Hizmetleri hello sanal ağda kullanılabilir hello IP görüntülenen birer birer adresleridir. Yakında hello hizmet etki alanınız için yüksek kullanılabilirlik sağlar gibi hello ikinci IP adresi kısa bir süre sonra hello ilk olarak görüntülenir. Ne zaman yüksek kullanılabilirlik yapılandırılmış ve etki alanınız için etkin, hello iki IP adresi görmeniz gerekir **etki alanı Hizmetleri** hello bölümünü **yapılandırma** sekmesi.
        >
        >
    * Etki alanı Hizmetleri'nin kullanılabilir sanal ağınızdaki hello hello ilk IP adresi yaklaşık 20 too30 dakika sonra **IP adresi** hello alanını **yapılandırma** sayfası.

        ![Sağlanan ilk IP’yi gösteren Domain Services penceresi](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Yüksek kullanılabilirlik etki alanınız için işletimsel olduğunda, iki IP adresi hello sayfasında görüntülenir. Yönetilen etki alanınız, bu iki IP adresindeki seçilen sanal ağlarınız üzerinde kullanılabilir.

10. Sanal ağınız için hello DNS ayarlarını güncelleştirebilmeniz için hello iki IP adresi unutmayın. Bunun yapılması, sanal makinelerin hello sanal ağ tooconnect toohello etki alanındaki etki alanına katılım gibi işlemler sağlar.

    ![Sağlanan her iki IP’yi gösteren Domain Services penceresi](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Azure AD kiracınız (örneğin, kullanıcıların veya grupların hello numarası) Hello boyutuna bağlı olarak, eşitleme tooyour yönetilen etki alanı biraz uzun sürebilir. Bu eşitleme işlemi hello arka planda gerçekleşir. On binlerce nesne içeren büyük kiracılar için veya tüm kullanıcılar, grup üyelikleri ve kimlik bilgilerini toobe eşitlenen için iki gün sürebilir.
>
>

## <a name="next-step"></a>Sonraki adım
[Görev 4: hello hello Azure sanal ağı için DNS ayarlarını güncelleştirme](active-directory-ds-getting-started-update-dns.md)
