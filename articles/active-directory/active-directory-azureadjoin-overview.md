---
title: "Bulut özelliklerini Azure Active Directory katılım aracılığıyla Windows 10 cihazlarına genişletme | Microsoft Docs"
description: "Windows 10 cihazlarının Azure Active Directory'de kayıtlı için Azure AD katılımını nasıl kullanabilir ayrıntılı genel bakış sağlar."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d3a3d3efe1c43caff3b8d2956c14e8c90d05d22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="extending-cloud-capabilities-to-windows-10-devices-through-azure-active-directory-join"></a>Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme
## <a name="what-is-azure-active-directory-join"></a>Azure Active Directory Join nedir?
Azure Active Directory katılım (Azure AD katılımı) Azure cihaz merkezi yönetimini etkinleştirmek için Active Directory'de şirkete ait bir cihazı kaydeden bir işlevdir. Bu, kullanıcıların Kurumsal bulut Azure Active Directory üzerinden bağlanmak için çalışanlar ve öğrenciler gibi mümkün kılar. Bu Basitleştirilmiş Windows dağıtımları ve kurumsal uygulamalara ve kaynaklara erişim herhangi bir Windows CİHAZDAN sağlar, hem şirkete ait hem de (KCG) kişisel.

Azure AD birleştirme ilk/bulut-yalnızca bulut--olan kuruluşlar için genellikle bir şirket içi Windows Server Active Directory altyapısına sahip olmayan küçük ve orta ölçekli işletmeler yöneliktir. Bu, Azure AD birleştirme ve ayrıca geleneksel etki alanına katılma (örneğin mobil aygıtlar) yapma yeteneğine sahip cihazlarda büyük kuruluşlar tarafından kullanılan, veya kaldırılacak öncelikle erişim Office 365 veya diğer SaaS uygulamaları gereken kullanıcılar için Azure AD ile tümleşik da belirtti.

En iyi şirket içi etki alanına katılma özellikli cihazlarda deneyimi geleneksel etki alanına katılmayı hala sunmasına karşın, Azure AD birleştirme etki alanına katılma olamaz cihazlar için uygundur. Azure AD birleştirme, kullanıcıların bulutta yönetmek için uygundur. Bunu Grup İlkesi ve System Center Configuration Manager (SCCM) gibi geleneksel etki alanı yönetim araçlarını kullanarak mobil cihaz yönetimi özellikleri yerine kullanarak yapar.

![Kurumsal ve kişisel aygıtlar şirket içi Active Directory ve Azure AD ile genel bakış](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Kuruluşların Azure AD katılım neden benimsemeyi?
* **Bulutu büyük ölçüde işletmeler**: taşınmış veya olan, şirket içi kullanım alanını azaltmaya ve daha fazla bulut çalışmak istediğiniz bir modele taşıma, Azure AD katılımı, faydalanabilir. Belki de el ile veya şirket içi Active Directory eşitleme aracılığıyla Azure AD hesapları oluşturdunuz. Her iki durumda da, Azure AD'de bir hesabınız varsa ve Windows 10'a oturum açmak için kullanabilirsiniz. Kullanıcılarınızın Azure ad out-of-box deneyimi (OOBE) ya da ayarlar menüsünü bilgisayarlarını birleştirebilirsiniz. Katıldıktan sonra kullanıcılar tek oturum açma (SSO) erişimi tarayıcılarını veya Office uygulamaları, Office 365 gibi bulut kaynaklarına keyfini çıkarın.
* **Eğitim kurumları**: yeterli yanıt hakkında sık senaryoları biri eğitim kurumları iki kullanıcı tür vardır: Fakülte ve öğrenciler. Bunun nedenle bunlar için şirket içi hesapları oluşturma arzu Fakülte üyeleri kuruluşun daha uzun vadeli üyeleri olarak kabul edilir. Ancak Öğrenciler kuruluş shorter-term üyesi olan ve bu nedenle Azure AD'de yönetilebilir. Bu dizin ölçek şirket içi depolanan yerine buluta gönderilemez anlamına gelir. Ayrıca Öğrenciler için Windows Azure AD hesaplarına ile oturum açın ve Office 365 kaynaklarına erişimi tarayıcılarını veya Office uygulamaları alma anlamına gelir.
* **Perakende işletmeler**: biz heard hakkında müşterilerden başka bir Mevsimlik çalışanları daha kolay yönetmek için kendi desire senaryodur.  Yeniden hesapları daha uzun vadeli, tam zamanlı çalışanlar için genellikle şirket içi etki alanına katılmış makinede hesapları olarak oluşturulur. Ancak bunları burada kullanıcı lisansları daha kolay taşınabildiğinden yönetmek için tercih edilir şekilde Mevsimlik çalışanları shorter-term org üyeleridir. Office 365 lisansına sahip bulutta bu kullanıcı hesapları oluşturma Windows ve Office uygulamaları Azure AD hesabı ile oturum açma avantajları elde etmelerine olanak sağlar. Bu sırada, bunlar çıktıktan sonra daha fazla esneklik, lisansları ile koruyun.
* **Diğer işletmelerin**: şirket içi Active Directory Kullanıcıları korumayı olsa bile, yine Azure AD alanına katılmış olması kullanıcılar kalmaktan faydalanabilir. Azure AD için Azure AD Basitleştirilmiş katılma deneyimi, verimli aygıt yönetimi, otomatik mobil cihaz Yönetimi kayıt ve çoklu oturum açma özelliği sunar ve şirket içi kaynakları olmasıdır.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Azure AD katılım hangi yetenekleri sunar?
Azure AD katılımı ile aşağıdaki alın:

* **Şirkete ait cihazlar kendi kendine sağlama**: Windows 10, BT katılımı olmadan out-of-box deneyiminde, yepyeni, naylon aygıt kullanıcıları yapılandırabilirsiniz.
* **Modern form faktörleri desteği**: Azure AD birleştirme yetenekleri katılma geleneksel etki alanı olmayan cihazlarda çalışır.  
* **Mevcut Kurumsal hesaplar için destek**: kullanıcılar artık ihtiyaç duymadığınız oluşturmak ve korumak bir Windows 8 ile yaptığınız gibi şirket tarafından verilen aygıtlarda en iyi deneyimi almak için kişisel bir Microsoft hesabı. Bunlar, mevcut iş hesaplarını Azure AD'de de yerine kullanabilirsiniz. Çoğu kuruluş için bu temel olarak kullanıcıların ayarlayabilir ve Office 365 erişimi için kullandıkları aynı kimlik bilgileriyle oturum anlamına gelir.
* **Otomatik mobil cihaz Yönetimi kayıt**: cihazları otomatik olarak kaydedilebilir Azure AD'ye bağlıyken mobil cihaz yönetimi. Bu işlem Microsoft Intune ve iş ortağı mobil cihaz yönetimi çözümleri ile çalışır. Aygıt Yönetimi Intune ile işiniz bittiğinde, BT yöneticilerinin İzleyici/SCCM yönetim konsolunda etki alanına katılmış cihazları yanı sıra Azure AD alanına katılmış cihazları yönetebilirsiniz.
* **Çoklu oturum açma şirket kaynaklarına**: kullanıcıların keyfini çoklu oturum açma Windows masaüstünden uygulamaları ve Office 365 ve Azure AD üzerinden kimlik doğrulaması için kullanan iş uygulamalar binlerce gibi bulut kaynaklarına [Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Azure AD'ye katılan şirkete ait cihazlar da keyfini çıkarın SSO şirket içi kaynaklara aygıt bir şirket ağındaki ve her yerden olduğunda bu kaynakları aracılığıyla sunulur zaman [Azure AD uygulama proxy'si](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **İşletim sistemi durumda Dolaşım**: erişilebilirlik ayarlarını, Web siteleri, Wi-Fi parolalar ve diğer ayarları eşitlenir şirkete ait aygıtlarda kişisel bir Microsoft hesabı gerek kalmadan.
* **Kurumsal kullanıma hazır Windows mağazası**: Windows mağazası uygulama alma ve Azure AD hesapları ile lisans destekler. Kuruluşların yapabildikleri toplu lisans uygulamaları ve bunları kullanıcılara kuruluşlarındaki sunma.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Farklı cihazları Azure AD'ye katılımı ile nasıl çalışır?
| Kurumsal cihaz (şirket içi etki alanına katılmış) | Kurumsal cihaz (buluta birleştirilmiş) | Kişisel cihaz |
| --- | --- | --- |
| (Bugün yaptıkları gibi) Kullanıcılar Windows'a iş kimlik bilgileriyle oturum açabilir. |Kullanıcılar için Windows Azure AD'de yönetilen iş kimlik bilgileriyle oturum açabilirsiniz. Bu, üç durumda Kurumsal cihazlar için geçerlidir: <ol><li>Kuruluşunuzun Active Directory şirket içinde (örneğin, küçük bir işletme) sahip değil.</li><li>Kuruluş tüm kullanıcı hesaplarını Active Directory'de oluşturmaz (örneğin, hesapları Öğrenciler, danışmanlar ya da Mevsimlik çalışanları için Active Directory'de oluşturulan değil).</li><li>Kuruluş telefonları veya mobil SKU (bir Fabrika/perakende kat gerçekleştirilecek Örneğin, ikincil bir aygıt) çalıştıran tabletler gibi bir (şirket içi) etki alanına katılamaz şirket cihazları var.</li></ol> Hem yönetilen hem de Federasyon kuruluşlar için Kurumsal aygıtların birleştirme Azure AD katılımı destekler. |Kullanıcılar Windows için kendi kişisel Microsoft hesabı kimlik bilgilerinizle (değişiklik yok) oturum açın. |
| Kullanıcıların Dolaşım ayarlarına erişim ve Windows mağazası Kurumsal sahip. Bu hizmetler, iş hesaplarıyla çalışır ve kişisel bir Microsoft hesabı gerektirmez. Bu, kuruluşların kendi şirket içi Active Directory için Azure AD connect gerektirir. |Kullanıcılar, Self Servis Kurulum yapabilirsiniz. Bunlar ilk çalıştırma deneyimi (FRX) kendi iş hesabını BT sağlama sahip alternatif olarak aygıtları gidebilirsiniz yöntemlerin her ikisi de desteklenir. |Active Directory veya Azure AD kullanıcıların yönetilen bir iş hesabı kolayca ekleyebilirsiniz. |
| Kullanıcılar iş uygulamaları, Web siteleri ve şirket içi kaynakları ve Azure AD kimlik doğrulaması için kullanmak bulut uygulamaları dahil olmak üzere kaynaklar--SSO masaüstünden sahipsiniz. |Cihazları otomatik olarak Kurumsal directory (Azure AD) içinde kayıtlı ve mobil cihaz Yönetimi'nde otomatik olarak kaydedilir. (Azure AD Premium özelliği). |Kullanıcılar, uygulamalarında ve bu iş hesabı ile Web siteleri/kaynaklarına SSO yeteneğine sahiptir. |
| Kullanıcılar kendi kişisel resimleri ve dosyaları Kurumsal verileri etkilemeden erişmek için kendi kişisel Microsoft hesapları ekleyebilirsiniz. (Dolaşım ayarları kendi iş hesaplarıyla çalışmaya devam.) Microsoft hesabı artık Dolaşım ayarları sürücüleri ve SSO sağlar. |Kullanıcılar, winlogon üzerinde Self Servis parola sıfırlama (SSPR) Unutulan parolayı sıfırlayabilirsiniz anlamı yapabilirsiniz. (Azure AD Premium özelliği). |Kullanıcıların Kurumsal Windows mağazası erişimi olması, böylece edinmeli ve kişisel cihazlarını satır iş kolu uygulamaları kullanın. |

## <a name="additional-information"></a>Ek bilgiler
* [Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

