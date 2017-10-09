---
title: "Azure Active Directory etki alanı Hizmetleri: Azure Active Directory Uygulama Ara sunucusu dağıtma | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanları üzerinde Azure AD uygulama proxy'si kullanın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD uygulama proxy'si bir Azure AD etki alanı Hizmetleri yönetilen etki alanında dağıtma
Azure Active Directory (AD) uygulama proxy'si hello erişilen şirket içi uygulamalar toobe yayımlayarak uzaktan çalışanlar destek yardımcı olan Internet. Azure AD etki alanı Hizmetleri ile şirket içi tooAzure altyapı Hizmetleri çalışan şimdi yükseltme-ve-shift eski uygulamalar olabilir. Ardından hello Azure AD uygulama proxy'si, kuruluşunuzdaki tooprovide güvenli uzaktan erişim toousers kullanarak bu uygulamaları yayımlayabilirsiniz.

Yeni toohello Azure AD uygulama proxy'si değilseniz, bu özellik hakkında daha fazla bilgi ile Merhaba aşağıdaki makaleye bakın: [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. Bir **Azure AD Basic veya Premium lisansı** olan gerekli toouse hello Azure AD uygulama proxy'si.
4. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Görev 1 - etkinleştir Azure AD uygulama proxy'si Azure AD dizininiz için
Aşağıdaki adımları tooenable hello Azure AD dizininiz için Azure AD uygulama proxy'si hello gerçekleştirin.

1. Merhaba içinde bir yönetici olarak oturum açın [Azure portal](http://portal.azure.com).

2. Tıklatın **Azure Active Directory** toobring hello directory genel bakış ayarlama. Tıklatın **kurumsal uygulamalar**.

    ![Azure AD dizini seçin](./media/app-proxy/app-proxy-enable-start.png)
3. Tıklatın **uygulama proxy'si**. Bir Azure AD temel veya Azure AD Premium aboneliğiniz yoksa, bir seçenek tooenable bir deneme bakın. İki durumlu **uygulama ara sunucusunu etkinleştirme?** çok**etkinleştirmek** tıklatıp **kaydetmek**.

    ![Uygulama Ara sunucusunu etkinleştirme](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload bağlayıcı Merhaba, hello tıklatın **bağlayıcı** düğmesi.

    ![Bağlayıcıyı indir](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Hello indirme sayfasında hello lisans koşullarını ve Gizlilik Sözleşmesi kabul ve hello **karşıdan** düğmesi.

    ![Yükleme Onayla](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Görev 2 - sağlama etki alanına katılmış Windows sunucuları toodeploy hello Azure AD uygulama ara sunucusu Bağlayıcısı
Windows Server sanal hello Azure AD uygulama ara sunucusu Bağlayıcısı yükleme makinelerin etki alanına katılmış gerekir. Yayımlanmakta hello uygulamalara bağlı olarak birden çok sunucu hello bağlayıcı yüklendiği tooprovision seçebilirsiniz. Yardımcı daha ağır kimlik doğrulama yükü işlemek ve bu dağıtım seçeneğini daha yüksek kullanılabilirlik sağlar.

Merhaba bağlayıcı sunucuları sağlamak hello aynı sanal ağ (veya bağlı ve eşlenen bir sanal ağ), etkinleştirdiğiniz içinde Azure AD etki alanı Hizmetleri yönetilen etki alanı. Benzer şekilde, hello uygulama proxy'si yayımlama hello uygulamaları barındıran hello hello üzerinde yüklü toobe sunucunuz aynı Azure sanal ağı.

tooprovision bağlayıcı sunucuları başlıklı hello makalesinde ana hatlarıyla hello görevleri izleyin [Windows sanal makine tooa yönetilen etki alanına Katıl](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Görev 3 - yükleme ve kaydetme hello Azure AD uygulama ara sunucusu Bağlayıcısı
Daha önce Windows Server sanal makine sağlanan ve toohello yönetilen etki alanına katıldı. Bu görevde, bu sanal makineye hello Azure AD uygulama ara sunucusu Bağlayıcısı yükler.

1. Merhaba connector yükleme paketini toohello VM hello Azure AD Web uygulaması Ara sunucusu Bağlayıcısı yüklemeniz kopyalayın.

2. Çalıştırma **AADApplicationProxyConnectorInstaller.exe** hello sanal makine üzerinde. Merhaba yazılım lisans koşullarını kabul edin.

    ![Yükleme için koşulları kabul edin](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Yükleme sırasında istendiğinde tooregister hello Bağlayıcısı hello Azure AD dizininizin uygulama proxy'si ile demektir.
    * Sağlayın, **Azure AD genel yönetici kimlik bilgileri**. Genel yönetici kiracınız, Microsoft Azure kimlik bilgilerinizden farklı olabilir.
    * Hello Yöneticisi kullanılan hesap tooregister hello bağlayıcı toohello ait olmalıdır hello uygulaması Ara sunucusu hizmetini etkinleştirdiğiniz aynı dizin. Hello Yöneticisi hello Kiracı etki alanı contoso.com ise, örneğin, olmalıdır admin@contoso.com veya diğer geçerli diğer o etki alanı üzerinde.
    * IE Artırılmış güvenlik yapılandırması için hello sunucusu Merhaba bağlayıcısını yüklediğiniz açıksa, hello kayıt ekranı engellenebilir. tooallow erişimi, hello hata iletisindeki hello yönergeleri izleyin. Internet Explorer Artırılmış Güvenlik seçeneğinin devre dışı olduğundan emin olun.
    * Bağlayıcı kaydı başarısız olursa bkz. [Uygulama Proxy’si Sorunlarını Giderme](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Yüklü bağlayıcı](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello bağlayıcı çalışma hello Azure AD uygulama ara sunucusu Bağlayıcısı sorun gidericisini düzgün çalışır. Başarılı bir rapor sonra çalışan hello sorun gidericisini görmeniz gerekir.

    ![Sorun gidericisini başarılı](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Azure AD dizininizi'hello uygulama proxy sayfasında listelenen yeni yüklenmiş hello bağlayıcı görmeniz gerekir.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Birden çok sunucuya tooinstall bağlayıcılar hello Azure AD uygulama proxy'si yayımlanan uygulamalar kimlik doğrulaması için yüksek kullanılabilirlik tooguarantee seçebilirsiniz. Merhaba tooinstall hello Bağlayıcısı diğer sunucuları birleştirilmiş tooyour yönetilen etki alanı, yukarıda listelenen aynı adımları gerçekleştirin.
>
>

## <a name="next-steps"></a>Sonraki Adımlar
Azure AD uygulama proxy'si hello ayarlayın ve Azure AD etki alanı Hizmetleri yönetilen etki alanınız ile tümleşik.

* **Uygulamaları tooAzure sanal makinelerinizi geçirmek:** uygulamalarınızı şirket içi sunucuları tooAzure sanal makineleri birleştirilmiş tooyour yönetilen etki alanından yükseltme ve üst karakter olabilir. Bunun yapılması, sunucuları şirket içi çalışan hello altyapı maliyetinden kurtulun yardımcı olur.

* **Azure AD uygulama proxy'si ile uygulama yayımlama:** , Azure hello Azure AD uygulama proxy'si kullanarak sanal makineleri üzerinde çalışan uygulamaları yayımlama. Daha fazla bilgi için bkz: [Azure AD uygulama proxy'si ile uygulama yayımlama](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Dağıtım Not - Azure AD uygulama proxy'si kullanarak yayımlama IWA (tümleşik Windows kimlik doğrulaması) uygulamaları
Tooimpersonate kullanıcılar, uygulama Proxy bağlayıcıları izin vererek tümleşik Windows kimlik doğrulaması (IWA) kullanarak oturum açma tek tooyour uygulamaları etkinleştirmek ve gönderip şirket adına belirteçleri. Merhaba bağlayıcı toogrant hello gerekli izinleri tooaccess kaynakları için hello yönetilen etki alanı kerberos Kısıtlı temsilci (KCD) yapılandırın. Merhaba kaynak tabanlı KCD mekanizması yönetilen etki alanlarında daha yüksek güvenlik için kullanın.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Kaynak tabanlı kerberos Kısıtlı temsilci hello Azure AD uygulama ara sunucusu Bağlayıcısı için etkinleştirme
Kullanıcıların kimliğine bürünebileceği şekilde hello Azure uygulama ara sunucusu Bağlayıcısı kerberos Kısıtlı temsilci (KCD), hello yönetilen etki alanında yapılandırılması gerekir. Bir Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanında, etki alanı yönetici ayrıcalıklarına sahip değil. Bu nedenle, **geleneksel hesap düzeyinde KCD, yönetilen bir etki alanında yapılandırılamaz**.

Bu konuda açıklandığı gibi kaynak tabanlı KCD kullanın [makale](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Toobe üyesi ihtiyacınız hello 'AAD DC yöneticileri' grubunun tooadminister hello yönetilen AD PowerShell cmdlet'lerini kullanarak etki alanı.
>
>

Merhaba Get-ADComputer PowerShell cmdlet tooretrieve hello ayarları hangi hello Azure AD uygulama ara sunucusu bağlayıcısının yüklendiği hello bilgisayar için kullanın.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Bundan sonra kaynak tabanlı KCD yukarı hello Set-ADComputer cmdlet'i tooset hello kaynak sunucusu için kullanın.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Yönetilen etki alanınızda birden çok uygulama proxy'si bağlayıcı dağıttıysanız, tooconfigure gereken kaynak tabanlı KCD her tür bağlayıcı örneği.


## <a name="related-content"></a>İlgili İçerik
* [Azure AD etki alanı Hizmetleri - başlangıç kılavuzu](active-directory-ds-getting-started.md)
* [Yönetilen bir etki alanında Kerberos Kısıtlanmış temsilci seçimini yapılandırın](active-directory-ds-enable-kcd.md)
* [Kerberos kısıtlanmış Temsile genel bakış](https://technet.microsoft.com/library/jj553400.aspx)
