---
title: "Azure kaydolma sorunlarını giderme | Microsoft Docs"
description: "Bazı ortak Azure oturum giderme açıklar yukarı sorunları."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 647509ea36e487aca5db661adb3268e845988f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Azure için kaydolma sorunlarını giderme
Azure için kaydolamazsınız, ortak sorunları gidermek için bu makaledeki ipuçları kullanın. Kredi kartınız sırasında ile ilgili bir sorun varsa, kaydolma, bkz: [Azure kaydolma ATM kartı veya kredi kartı reddedildi](billing-credit-card-fails-during-azure-sign-up.md). Bir Azure hesabı varsa, ancak oturum açamıyorum yoksa bkz [Azure Aboneliğim yönetmek oturum açamıyorum](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>İlerleme çubuğu "Kartı tarafından kimlik doğrulaması" bölümünde askıda kalır

Kart tarafından kimlik doğrulamayı tamamlamak için üçüncü taraf tanımlama bilgileri için tarayıcınızın izin verilmelidir.

![Kayıt sırasında asılı kartı bölüme göre kimlik doğrulama ekran görüntüsü](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Tarayıcınızın tanımlama bilgisi ayarları güncelleştirmek için aşağıdaki adımları kullanın.

1. Chrome kullanıyorsanız, Git **ayarları** > **Göster Gelişmiş ayarları** > **gizlilik** > **içeriği ayarları**. İşaretini **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri**.
2. Edge kullanıyorsanız, Git **ayarları** > **görünüm Gelişmiş ayarları** > **tanımlama bilgilerini**. Seçin **tanımlama bilgilerini engelleme**.
3. Azure kaydolma sayfayı yenileyin ve sorunun giderilmiş olup olmadığını denetleyin.
4. Yenileme sorunu çözmek alamadık, çıkın ve tarayıcınızı yeniden başlatın ardından yeniden deneyin.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Kredi kartı form fatura adresimi desteklemiyor
Fatura adresini seçtiğiniz ülkede olması gereken **ilgili** bölümü. Doğru ülke seçtiğinizden emin olun.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Hiçbir metin iletileri veya kaydolma Hesap doğrulama sırasında çağrıları
Genellikle çok daha hızlı olsa da, teslim edilecek doğrulama kodu dört dakika kadar sürebilir. Doğrulama için girdiğiniz telefon numarası, hesap için kişi bir sayı olarak saklanmaz.

Bazı ipuçları şunlardır:
* Bir VoIP telefon numarası için telefon doğrulama işlemi kullanılamaz.
* Telefon numarasını kontrol edin, açılır menüde seçilen ülke kodu gibi girin.
* Telefonunuza kısa mesaj (SMS) almazsa deneyin **beni** seçeneği.
* Telefonunuz çağrıları veya SMS iletileri dayalı ABD numarasından alabileceğinizden emin olun.

SMS mesajı ya da telefon araması aldığınızda, metin kutusuna aldığınız kodu girin.

## <a name="credit-card-declined-or-not-accepted"></a>Kredi kartı reddedildi veya kabul edilmedi
Sanal veya ön ödemeli kredi veya ATM kartı Azure abonelikleri için ödeme olarak kabul değil. Başka ne kartınız reddetti neden olabilir görmek için bkz: [Azure kaydolma ATM kartı veya kredi kartı reddedildi](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"Ücretsiz deneme sürümü kullanılabilir değil"
Bir Azure aboneliği geçmişte kullandınız mı? Azure kullanım koşulları sözleşmesini Azure için yeni olan bir kullanıcı için ücretsiz deneme etkinleştirme sınırlar. Başka türde bir Azure aboneliğiniz varsa, ücretsiz deneme etkinleştirilemiyor. Olmayı göz önünde bulundurun bir [Kullandıkça Öde aboneliğine](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Ücretsiz deneme hesabımdaki ı bir ücret gördüğünüz
Küçük bir görebilirsiniz doğrulama 3 ile 5 gün içinde kaldırıldı, oturumu sonra kredi kartı hesabınızdaki basılı tutun. Maliyetleri yönetme hakkında kaygılı varsa, daha fazla bilgi edinin [beklenmeyen maliyetleri önleme](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>MSDN, BizSpark, BizSparkPlus veya MPN gibi Azure avantajı planı etkinleştirilemiyor
Doğru oturum açma kimlik bilgilerini kullandığınızdan emin olun. Daha sonra uygun olduğunuzdan emin olmak için avantajı programı denetleyin. 

* MSDN
  * Uygunluk durumunuzu doğrulayın, [MSDN hesap sayfası](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Durumunuzu doğrulayamıyorsanız başvurun [MSDN Abonelikleri müşteri hizmetleri merkezleri](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Oturum [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) ve BizSpark ve BizSpark artı için uygunluk durumunuzu doğrulayın.
  * Durumunuzu doğrulayamıyorsanız yapabilecekleriniz [BizSpark forumlarına Yardım](http://aka.ms/bzforums).
* MPN
  * Oturum [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) ve uygunluk durumunuzu doğrulayın. Uygun varsa [bulut platformu yetkinlikleri](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), ek faydalar uygun olabilir.
  * Durumunuzu doğrulayamıyorsanız başvurun [MPN Destek](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Yeni açık olarak Azure Abonelik etkinleştirilemiyor
Açık olarak Azure bir aboneliği oluşturmak için geçerli bir çevrimiçi hizmet etkinleştirme (OSA) anahtarı için ilişkili en az bir açık olarak Azure belirtecine sahip olmalıdır. Kişi Microsoft Partners birini OSA anahtar yoksa, listelenen [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.
