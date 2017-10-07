---
title: "Azure Active Directory etki alanı Hizmetleri: Sorun giderme kılavuzu | Microsoft Docs"
description: "Azure AD etki alanı Hizmetleri için sorun giderme kılavuzu"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Azure AD etki alanı Hizmetleri - sorun giderme kılavuzu
Bu makale, ayarlama veya Azure Active Directory (AD) etki alanı Hizmetleri yönetme karşılaşabileceğiniz sorunları için sorun giderme ipuçları sağlar.

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Azure AD dizininiz için Azure AD Etki Alanı Hizmetleri'ni etkinleştirilemiyor
Hataları sorun giderme tooenable dizininiz için Azure AD Etki Alanı Hizmetleri'ni deneyin ve alır veya başarısız olduğunda bu bölümde yardımcı geri too'Disabled yükseğe '.

Sorun giderme karşılaştığınız toohello hata iletisi karşılık gelen adımları hello seçin.

| **Hata iletisi** | **Çözümleme** |
| --- |:--- |
| *Merhaba adı contoso100.com Bu ağda zaten kullanılıyor. Kullanımda olmayan bir ad belirtin.* |[Merhaba sanal ağındaki etki alanı adı çakışması](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba hizmeti, 'Azure AD etki alanı Hizmetleri Sync' adlı yeterli izinlere toohello uygulaması yok. 'Azure AD etki alanı Hizmetleri Sync' olarak adlandırılan hello uygulamayı silin ve ardından tooenable etki alanı Hizmetleri, Azure AD kiracınızın deneyin.* |[Etki Alanı Hizmetleri toohello Azure AD etki alanı Hizmetleri eşitleme uygulama yeterli izinlere sahip değil](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba etki alanı Hizmetleri, Azure AD kiracınızın uygulama değil sahip hello izinleri tooenable etki alanı Hizmetleri gereklidir. Merhaba uygulama tanımlayıcısı d87dcbc6-a371-462e-88e3-28ad15ec4e64 Hello uygulamayla silip tooenable Azure AD kiracınız için etki alanı Hizmetleri'ni deneyin.* |[Merhaba etki alanı Hizmetleri uygulaması kiracınızda düzgün yapılandırılmamış](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba Microsoft Azure AD uygulaması, Azure AD kiracınızda devre dışı bırakılır. Merhaba uygulama tanımlayıcısı 00000002-0000-0000-c000-000000000000 Hello uygulamayla etkinleştirin ve tooenable Azure AD kiracınız için etki alanı Hizmetleri'ni deneyin.* |[Merhaba Microsoft Graph uygulaması, Azure AD kiracınızda devre dışı bırakıldı](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Etki alanı adı çakışması
**Hata iletisi:**

*Merhaba adı contoso100.com Bu ağda zaten kullanılıyor. Kullanımda olmayan bir ad belirtin.*

**Düzeltme:**

Merhaba ile mevcut bir etki alanına sahip değil sağlamak aynı etki alanı adı bu sanal ağ üzerinde kullanılabilir. Örneğin, "contoso.com" zaten mevcut hello seçilen sanal ağ üzerinde adlı bir etki alanına sahip olduğunuzu varsayar. Daha sonra tooenable hello içeren bir Azure AD etki alanı Hizmetleri yönetilen etki alanı deneyin aynı etki alanı adını (diğer bir deyişle, "contoso.com") bu sanal ağ üzerinde. Tooenable Azure AD etki alanı Hizmetleri çalışırken bir hatayla karşılaşırsınız.

Bu sanal ağ üzerinde hello etki alanı adı için tooname çakışmaları nedeniyle bu başarısız olur. Bu durumda, Azure AD etki alanı Hizmetleri yönetilen etki alanını farklı bir ad tooset kullanmanız gerekir. Alternatif olarak, hello varolan etki alanının sağlanmasını ve tooenable Azure AD etki alanı Hizmetleri devam edin.

### <a name="inadequate-permissions"></a>Yetersiz izinler
**Hata iletisi:**

*Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba hizmeti, 'Azure AD etki alanı Hizmetleri Sync' adlı yeterli izinlere toohello uygulaması yok. 'Azure AD etki alanı Hizmetleri Sync' olarak adlandırılan hello uygulamayı silin ve ardından tooenable etki alanı Hizmetleri, Azure AD kiracınızın deneyin.*

**Düzeltme:**

Azure AD dizininizi 'Azure AD etki alanı Hizmetleri Sync' hello ada sahip bir uygulama ise toosee kontrol edin. Bu uygulama zaten varsa, onu silin ve Azure AD etki alanı hizmetlerini yeniden etkinleştirin.

Gerçekleştirmek hello adımları toocheck hello varlığı hello uygulama ve toodelete için aşağıdaki, hello uygulama zaten varsa:

1. Toohello gidin **Klasik Azure portalı** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Select hello **Active Directory** hello sol bölmedeki düğüm.
3. Select hello Azure AD kiracısını (dizin) tooenable istediğiniz Azure AD etki alanı Hizmetleri.
4. Toohello gidin **uygulamaları** sekmesi.
5. Select hello **Şirketimin sahip olduğu uygulamalar** hello açılır seçeneği.
6. Adlı bir uygulama için denetleme **Azure AD etki alanı Hizmetleri eşitleme**. Merhaba uygulaması varsa, toodelete devam onu.
7. Merhaba uygulaması sildikten sonra tooenable Azure AD Etki Alanı Hizmetleri'nde bir kez daha deneyin.

### <a name="invalid-configuration"></a>Geçersiz yapılandırma
**Hata iletisi:**

*Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba etki alanı Hizmetleri, Azure AD kiracınızın uygulama değil sahip hello izinleri tooenable etki alanı Hizmetleri gereklidir. Merhaba uygulama tanımlayıcısı d87dcbc6-a371-462e-88e3-28ad15ec4e64 Hello uygulamayla silip tooenable Azure AD kiracınız için etki alanı Hizmetleri'ni deneyin.*

**Düzeltme:**

Azure AD dizininizi (ile bir d87dcbc6-a371-462e-88e3-28ad15ec4e64 uygulama tanıtıcısı) ' AzureActiveDirectoryDomainControllerServices' hello adda bir uygulamanız varsa toosee denetleyin. Bu uygulama zaten varsa ve ardından yeniden etkinleştirin Azure AD etki alanı Hizmetleri toodelete gerekir.

PowerShell komut dosyası toofind Merhaba uygulaması aşağıdaki hello kullanın ve silin.

> [!NOTE]
> Bu komut dosyası kullanan **Azure AD PowerShell sürüm 2** cmdlet'leri. Tüm kullanılabilir cmdlet'leri ve toodownload hello modülü tam listesi için hello okuma [Azuread'i PowerShell başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph devre dışı
**Hata iletisi:**

Etki Alanı Hizmetleri bu Azure AD kiracısında etkin değil. Merhaba Microsoft Azure AD uygulaması, Azure AD kiracınızda devre dışı bırakılır. Merhaba uygulama tanımlayıcısı 00000002-0000-0000-c000-000000000000 Hello uygulamayla etkinleştirin ve tooenable Azure AD kiracınız için etki alanı Hizmetleri'ni deneyin.

**Düzeltme:**

Bir uygulama 00000002-0000-0000-c000-000000000000 hello tanımlayıcıyla devre dışı bıraktıysanız toosee denetleyin. Bu uygulama Merhaba Microsoft Azure AD uygulaması ve grafik API'sine erişim tooyour Azure AD Kiracı sağlar. Azure AD etki alanı Hizmetleri, Azure AD Kiracı tooyour yönetilen bu uygulama etkin toobe toosynchronize gereken etki alanı.

tooresolve bu hata, bu uygulamayı etkinleştir ve Azure AD kiracınız için tooenable etki alanı Hizmetleri'ni deneyin.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Toohello Azure AD etki alanı Hizmetleri yönetilen etki alanı içinde oluşturulamıyor toosign kullanıcılardır
Bir veya daha fazla kullanıcı Azure AD kiracınızda yeni oluşturulan toohello yönetilen etki alanında oluşturulamıyor toosign varsa, aşağıdaki sorun giderme adımları hello gerçekleştirin:

* **UPN biçimini kullanarak oturum açın:** hello UPN biçimini kullanarak toosign deneyin (örneğin, 'joeuser@contoso.com') yerine hello SAMAccountName biçimi ('CONTOSO\joeuser'). Merhaba SAMAccountName, UPN önek aşırı uzun veya olan hello aynı hello yönetilen etki alanındaki başka bir kullanıcı olarak kullanıcılar için otomatik olarak oluşturulabilir. Merhaba UPN biçimini toobe Azure AD kiracısı içinde benzersiz garanti edilmez.

> [!NOTE]
> Merhaba UPN biçiminde toosign toohello Azure AD etki alanı Hizmetleri yönetilen etki alanında kullanmanızı öneririz.
>
>

* Sahip olduğundan emin olun [parola eşitleme etkin](active-directory-ds-getting-started-password-sync.md) hello Başlarken Kılavuzu'nda gösterilen hello adımları uygun olarak.
* **Dış hesaplar:** hello etkilenen kullanıcı hesabı hello Azure AD Kiracı dış hesap olmadığından emin olun. Dış hesaplar örnekleri arasında Microsoft hesapları (örneğin, 'joe@live.com') veya bir dış kullanıcı hesapları Azure AD dizini. Bu tür kullanıcı hesapları için kimlik bilgileri Azure AD etki alanı Hizmetleri yok olduğundan, bu kullanıcılar toohello yönetilen etki alanında oturum açamazsınız.
* **Eşitlenen hesaplar:** hello etkilenen kullanıcı hesapları şirket içi dizininden eşitlenirse doğrulayın:

  * Dağıtılan veya toohello güncelleştirilmiş [en son sürümü Azure AD Connect, önerilen](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Azure AD Connect çok yapılandırdığınız[tam eşitleme gerçekleştirmek](active-directory-ds-getting-started-password-sync.md).
  * Dizininizi Hello boyutuna bağlı olarak, bu kullanıcı hesapları için uzun sürebilir ve karmaları toobe Azure AD Etki Alanı Hizmetleri'nde kullanılabilir kimlik bilgisi. Yetecek kadar uzun süre (Merhaba boyutu dizininizin - tooa günde birkaç saat veya iki büyük dizinler için) bağlı olarak kimlik doğrulaması yeniden denemeden önce bekleyin emin olun.
  * Önceki adımları hello doğruladıktan sonra Hello sorun devam ederse, Microsoft Azure AD eşitleme hizmeti hello yeniden başlatmayı deneyin. Eşitleme makinenizden bir komut istemi başlatın ve aşağıdaki komutları hello yürütün:

    1. net stop 'Microsoft Azure AD eşitleme'
    2. net start 'Microsoft Azure AD eşitleme'
* **Yalnızca bulut hesapları**: hello etkilenen kullanıcı hesabının bir yalnızca bulut kullanıcı hesabı, Azure AD etki alanı Hizmetleri etkin sonra hello kullanıcı parolalarını değişmiş emin olun. Bu adım hello kimlik bilgisi karmaları oluşturulan Azure AD etki alanı Hizmetleri toobe için gerekli neden olur.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Kullanıcı Azure AD kiracınıza kaldırıldı, yönetilen etki alanınızdan kaldırılmaz
Azure AD kullanıcı nesnelerinin yanlışlıkla silinmesine karşı sizi korur. Bir kullanıcı hesabı Azure AD kiracınıza sildiğinizde, hello karşılık gelen kullanıcı taşınan toohello geri dönüşüm kutusu nesnesidir. Bu silme işlemini eşitlenmiş tooyour yönetilen etki alanında olduğunda, kullanıcı hesabı toobe devre dışı olarak işaretlenmiş karşılık gelen hello neden olur. Bu özellik, kurtarabilir veya hello kullanıcı hesabı daha sonra geri yardımcı olur.

kullanıcı hesabı hello kalırken, yönetilen etki alanınızdaki durumu devre dışı Merhaba, bir kullanıcı hesabıyla yeniden oluşturmak olsa bile Azure AD dizininizi aynı UPN hello. Yönetilen etki alanınızdan tooremove hello kullanıcı hesabı, gereksinim duyduğunuz tooforce Azure AD kiracınıza silin.

tooremove hello kullanıcı hesabından tam olarak yönetilen etki alanınızı hello kullanıcı kalıcı olarak Azure AD kiracınıza silin. Merhaba ile Merhaba Kaldır MsolUser PowerShell cmdlet'ini kullanın '-RemoveFromRecycleBin' seçeneği, bu konuda açıklandığı gibi [MSDN makalesine](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Bizimle İletişim Kurun
Çok Hello Azure Active Directory etki alanı Hizmetleri ürün ekibine başvurun[paylaşmak geri bildirim veya destek](active-directory-ds-contact-us.md).
