---
title: 'Azure Active Directory Connect: SSS - | Microsoft Docs'
description: "Bu sayfa, Azure AD Connect hakkında sık bir sorulan sorular."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Azure Active Directory Connect için sık sorulan sorular

## <a name="general-installation"></a>Genel yükleme
**S: Hello Azure AD genel yönetici etkin 2FA varsa yükleme çalışacak mı?**  
Şubat 2016 ile yapılar Merhaba, bu desteklenir.

**S: bir şekilde tooinstall Azure AD Connect katılımsız var mı?**  
Yalnızca desteklenen tooinstall Azure AD Connect olduğu hello Yükleme Sihirbazı'nı kullanarak. Katılımsız ve sessiz bir yükleme desteklenmez.

**S: olduğu bir etki alanına erişilemiyor bir ormana sahibim. Azure AD Connect yükleme nasıl yaparım?**  
Şubat 2016 ile yapılar Merhaba, bu desteklenir.

**S: Sunucu Çekirdeği üzerinde AD DS'yi sistem durumu aracısı çalışmanın hello mu?**  
Evet. Merhaba aracıyı yükledikten sonra hello aşağıdaki PowerShell cmdlet'ini kullanarak hello kayıt işlemini tamamlamak: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Ağ
**S: sahip bir güvenlik duvarı, ağ aygıtı veya başka bir şey hello en uzun süre bağlantıları sınırlayan Ağımdaki açık kalabilir. Ne kadar süreyle my istemci tarafı zaman aşımı eşiği Azure AD Connect kullanırken olmalıdır?**  
Tüm ağ yazılımı, fiziksel aygıtların ya da başka bir şey, hello Azure AD Connect istemcisinin yüklü olduğu sunucu bağlantıları açık kalabileceği en uzun süre hello arasında bağlantı için en az 5 dakika (300 saniye) eşiğinin kullanması gereken sınırları hello ve Azure Active Directory. Bu, daha önce yayımlanmış tooall Microsoft Identity eşitleme araçları da geçerlidir.

**S: desteklenen SLD'ler (tek etiketli etki alanları) misiniz?**  
Hayır, Azure AD Connect, şirket içi ormanlar/SLD'ler kullanarak etki alanları desteklemez.

**S: "noktalı" adlı NetBIOS desteklenir?**  
Hayır, Azure AD Connect, şirket içi ormanlar/etki, hello NetBIOS adı içerdiği bir süre desteklemiyor "." Merhaba adı.

## <a name="federation"></a>Federasyon
**S: t, bana toorenew isteyen bir e-posta almaya devam ederseniz ne yapmalıyım my Office 365 sertifika**  
Hello özetlenen hello yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md) nasıl toorenew hello sertifika üzerindeki konu.

**S: "Otomatik olarak bağlı olan taraf O365 bağlı olan taraf için ayarlanmış güncelleştir" sahibim. My belirteç imzalama sertifikası otomatik olarak geldiğinde ı tootake herhangi bir işlem var mı?**  
Merhaba makalesinde ana hatlarıyla hello yönergeleri kullanmanız [sertifikaları Yenile](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Ortam
**S: Azure AD Connect yüklendikten sonra desteklenen BT toorename hello sunucusu mi?**  
Hayır. Merhaba sunucu adını değiştirme neden hello eşitleme altyapısı toonot mümkün tooconnect toohello SQL veritabanı olacaktır ve hello hizmet mümkün toostart olmaz.

## <a name="identity-data"></a>Kimlik verileri
**S: hello UPN (userPrincipalName) özniteliği Azure AD'de eşleşmiyor: şirket içi UPN - neden hello?**  
Bu makalelere bakın:

* [İçinde Office 365, Azure veya Intune eşleşmiyor kullanıcı adları şirket içi UPN veya alternatif oturum açma kimliği hello](https://support.microsoft.com/en-us/kb/2523192)
* [Bir kullanıcı hesabı toouse farklı bir Federasyon etki alanına UPN hello değiştirdikten sonra değişiklikleri hello Azure Active Directory eşitleme aracı tarafından eşitlenen değil](https://support.microsoft.com/en-us/kb/2669550)

Azure AD tooallow hello eşitleme altyapısı tooupdate hello userPrincipalName açıklandığı gibi yapılandırabilirsiniz [Azure AD Connect eşitleme hizmeti özelliklerini](active-directory-aadconnectsyncservice-features.md).

**S: desteklenen BT toosoft eşleşme şirket içi AD grup/kişisi nesneleri mevcut Azure AD grup/kişisi nesnelerle mi?**  
Hayır, bu şu anda desteklenmiyor.

**S: olan desteklenen BT toomanually ayarlamak İmmutableıd özniteliği var olan Azure AD Grup/başvurun nesneleri toohard eşleşen onu tooon içi AD Grup/kişi nesneleri?**  
Hayır, bu şu anda desteklenmiyor.



## <a name="custom-configuration"></a>Özel yapılandırma
**S: hello PowerShell cmdlet'leri için Azure AD Connect belgelenen nerede?**  
Bu sitede belgelenen hello cmdlet'leri Hello özel durum ile Azure AD Connect içinde bulunan diğer PowerShell cmdlet'leri müşteri kullanım için desteklenmez.

**S: "sunucu dışa aktarma/sunucu alma bulundu" kullanabilirim *Eşitleme Hizmeti Yöneticisi'ni* toomove yapılandırma sunucusu arasında?**  
Hayır. Bu seçenek, tüm yapılandırma ayarlarını almaz ve kullanılmamalıdır. Bunun yerine hello ikinci sunucusunda hello toocreate hello temel Yapılandırma Sihirbazı'nı kullanın ve hello eşitleme kuralı Düzenleyicisi toogenerate PowerShell komut dosyaları toomove sunucular arasında herhangi bir özel kural kullanmanız gerekir. Bkz: [çarpma geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**S: parolalar için hello Azure oturum açma sayfası önbelleğe alınabilir ve bir parola input öğesi hello otomatik tamamlama ile içerdiğinden bu engellenebilir = "false" özniteliği?**</br>
Şu anda hello otomatik tamamlama etiketi de dahil olmak üzere hello parola giriş alanı değiştirme hello HTML özniteliklerini desteklemiyoruz. Şu anda tooadd olanak tanıyan özel Javascript için izin veren bir özellik üzerinde herhangi bir öznitelik toohello parola alan çalışıyoruz. Bu 2017 kullanılabilir sonraki parçası olmalıdır.

**S: Azure oturum açma sayfası Hello üzerinde önceden başarıyla oturum açtıktan kullanıcılar için kullanıcı adları gösterilir.  Bu davranış kapalı?**</br>
Şu anda hello oturum açma sayfası değiştirme hello HTML özniteliklerini desteklemiyoruz. Şu anda tooadd olanak tanıyan özel Javascript için izin veren bir özellik üzerinde herhangi bir öznitelik toohello parola alan çalışıyoruz. Bu 2017 kullanılabilir sonraki parçası olmalıdır.

**S: bir şekilde tooprevent eşzamanlı oturum var mı?**</br>
Hayır.



## <a name="troubleshooting"></a>Sorun giderme
**S: Azure AD Connect ile ilgili Yardım nasıl alabilirim?**

[Arama hello Microsoft Bilgi Bankası (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Azure AD Connect desteği hakkında teknik çözümler toocommon onarım sorunlar için Microsoft Bilgi Bankası (KB) Hello arayın.

[Microsoft Azure Active Directory forumları](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Arama ve teknik sorular ve yanıtlar hello Topluluğu'ndan veya kendi tıklayarak soru sorun göz atmak [burada](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Azure AD Connect müşteri desteği](https://manage.windowsazure.com/?getsupport=true)

* Bu bağlantıyı tooget destek hello Azure portal aracılığıyla kullanın.

