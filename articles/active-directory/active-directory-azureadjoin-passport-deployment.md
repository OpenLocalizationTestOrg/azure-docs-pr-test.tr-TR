---
title: "aaaEnable Microsoft iş için Windows Hello kuruluşunuzdaki | Microsoft Docs"
description: "Dağıtım yönergeleri tooenable Microsoft Passport, kuruluşunuzda."
services: active-directory
documentationcenter: 
keywords: "Microsoft Passport, Microsoft Windows Hello iş dağıtım için yapılandırma"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Microsoft iş için Windows Hello kuruluşunuzda etkinleştir
Sonra [Windows 10 etki alanına katılmış cihazları Azure Active Directory ile bağlanma](active-directory-azureadjoin-devices-group-policy.md), kuruluşunuzda iş için Microsoft Windows Hello tooenable aşağıdaki hello:

1. System Center Configuration Manager dağıtma  
2. İlke ayarlarını yapılandırın
3. Merhaba sertifika profili yapılandırma  

## <a name="deploy-system-center-configuration-manager"></a>System Center Configuration Manager dağıtma
Windows Hello üzerinde iş tuşları temel alarak toodeploy kullanıcı sertifikaları hello aşağıdaki gerekir:

* **System Center Configuration Manager geçerli dalının** -tooinstall sürümü 1606 veya üzeri gerekiyor. Daha fazla bilgi için bkz: Merhaba [System Center Configuration Manager belgeleri](https://technet.microsoft.com/library/mt346023.aspx) ve [System Center Configuration Manager ekip blogu](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Ortak anahtar altyapısı (PKI)** -tooenable Microsoft Windows Hello kullanıcı sertifikaları kullanarak işletmeler için bir PKI yerinde olmalıdır. Bir yoksa veya toouse istemiyorsanız, kullanıcı sertifikaları için Windows Server yüklü 10551 (veya daha iyi) yapı 2016 sahip yeni bir etki alanı denetleyicisi dağıtabilirsiniz. Çok olarak Hello adımları[varolan bir etki alanında etki alanı Denetleyicisi'nin çoğaltmasını yükleme](https://technet.microsoft.com/library/jj574134.aspx) veya çok[yeni bir ortam oluşturuyorsanız yeni bir Active Directory ormanı yüklemek](https://technet.microsoft.com/library/jj574166). (Merhaba ISO'ları indirmek için kullanılabilir [Signiant medya Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>İlke ayarlarını yapılandırın
Microsoft Windows Hello tooconfigure hello iş ilke ayarları için iki seçeneğiniz vardır:

* Active Directory'de Grup İlkesi 
* Merhaba System Center Configuration Manager 

Grup İlkesi kullanarak Active Directory'de yöntemi tooconfigure Microsoft Windows Hello iş ilke ayarları için önerilen hello ' dir. 

Ayrıca toodeploy sertifikaları kullandığınızda, System Center Configuration Manager kullanarak hello tercih edilen yöntemdir. Bu senaryo:

* Merhaba yeni dağıtım senaryoları ile uyumluluk sağlar
* Merhaba istemci tarafında Windows 10 sürüm 1607 ya da daha iyi gerektirir.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Microsoft iş için Windows Hello Active Directory'de Grup İlkesi aracılığıyla yapılandırın
**Adımları**:

1. Sunucu Yöneticisi'ni açın ve çok gidin**Araçları** > **Grup İlkesi Yönetimi**.
2. Grup İlkesi Yönetimi'nden tooenable Azure AD katılım istediğiniz toohello etki alanı karşılık gelen toohello etki alanı düğümüne gidin.
3. Sağ **Grup İlkesi nesneleri**seçip **yeni**. Grup İlkesi nesnesi, örneğin, etkinleştirmek için Windows Hello iş adlandırın. **Tamam** düğmesine tıklayın.
4. Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.
5. Çok gidin**Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows Bileşenleri** > **iş için Windows Hello**.
6. Sağ **etkinleştirmek için Windows Hello iş**ve ardından **Düzenle**.
7. Select hello **etkin** seçenek düğmesine ve ardından **Uygula**. **Tamam** düğmesine tıklayın.
8. Şimdi hello Grup İlkesi nesnesi tooa konumu tercih ettiğiniz bağlayabilirsiniz. tooenable tüm hello etki alanına katılmış Windows 10 cihazları, kuruluşunuzda bağlantı hello Grup İlkesi toohello etki alanı için bu ilke. Örneğin:
   * Windows 10 etki alanına katılmış bilgisayarları nerede bulunacağı Active Directory'de belirli kuruluş birimi (OU)
   * Azure AD ile kayıtlı otomatik olarak Windows 10 etki alanına katılmış bilgisayarları içeren belirli bir güvenlik grubu

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>System Center Configuration Manager kullanarak iş için Windows Hello yapılandırın
**Adımları**:

1. Açık hello **System Center Configuration Manager**ve ardından çok gidin**varlıklar ve uyumluluk > uyumluluk ayarları > Şirket kaynağına erişim > İş profilleri için Windows Hello**.
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Merhaba üstte Hello araç çubuğunda **iş profili için Windows Hello oluşturma**.
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. Merhaba üzerinde **genel** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. Merhaba, **adı** metin kutusuna, bu gibi bir durumda profil için bir ad yazın **WHfB Profilim**.
   
    b. **İleri**’ye tıklayın.
4. Merhaba üzerinde **desteklenen platformlar** iletişim, bu Windows Hello iş profili ile hazırlanacak ve ardından select hello platformları **sonraki**.
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. Merhaba üzerinde **ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Olarak **yapılandırmak için Windows Hello iş**seçin **etkin**.
   
    b. Olarak **bir Güvenilir Platform Modülü (TPM) kullanmak**seçin **gerekli**. 
   
    c. Olarak **kimlik doğrulama yöntemini**seçin **sertifika tabanlı**.
   
    d. **İleri**’ye tıklayın.
6. Merhaba üzerinde **Özet** iletişim kutusunda, tıklatın **sonraki**.
7. Merhaba üzerinde **tamamlama** iletişim kutusunda, tıklatın **Kapat**.
8. Merhaba üstte Hello araç çubuğunda **dağıtma**.
   
    ![İş için Windows Hello yapılandırın](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Merhaba sertifika profili yapılandırma
Şirket içi kimlik doğrulaması için sertifika tabanlı kimlik doğrulaması kullanıyorsanız, tooconfigure gerekir ve bir sertifika profili dağıtın. Bu görev bir NDES sunucusu ve hello System Center Configuration Manager sertifika kayıt noktası site rolü tooset gerektirir. Daha fazla ayrıntı için bkz: Merhaba [Configuration Manager'da sertifika profilleri için Önkoşullar](https://technet.microsoft.com/library/dn261205.aspx).

1. Açık hello **System Center Configuration Manager**ve ardından çok gidin**varlıklar ve uyumluluk > uyumluluk ayarları > Şirket kaynağına erişim > sertifika profilleri**.
2. Akıllı kart oturum açma genişletilmiş anahtar kullanımı (EKU) sahip bir şablon seçin.

Merhaba üzerinde **SCEP kaydı** sayfa toochoose ihtiyacınız hello sertifika profili, **yükle yoksa başarısız iş için tooPassport** hello olarak **anahtar depolama sağlayıcısı**.

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

