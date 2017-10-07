---
title: "Azure Active Directory katılım aracılığıyla aaaExtending bulut özellikleri tooWindows 10 cihazları | Microsoft Docs"
description: "Azure AD katılım tooget Azure Active Directory'de kayıtlı Windows 10 cihazlarına nasıl kullanabilir ayrıntılı genel bakış sağlar."
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
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme
## <a name="what-is-azure-active-directory-join"></a>Azure Active Directory Join nedir?
Azure Active Directory katılım (Azure AD katılımı) Azure Active Directory tooenable Merkezi Yönetimi'nde hello aygıtın şirkete ait bir cihazı kaydeder hello işlevdir. Bu, çalışanlar ve öğrenciler tooconnect toohello Kurumsal bulut Azure Active Directory üzerinden gibi kullanıcılar için mümkün kılar. Bu, Basitleştirilmiş Windows dağıtımları ve erişim tooorganizational uygulamaları ve herhangi bir Windows aygıtı kaynaklardan sağlar, hem şirkete ait hem de (KCG) kişisel.

Azure AD birleştirme ilk/bulut-yalnızca bulut--olan kuruluşlar için genellikle bir şirket içi Windows Server Active Directory altyapısına sahip olmayan küçük ve orta ölçekli işletmeler yöneliktir. Konusu, Azure AD birleştirme kullanabilirsiniz ve ayrıca olur, geleneksel etki alanına katılma (örneğin mobil aygıtlar) yapmanın ya da tooaccess Office 365 veya Azure AD ile tümleşik diğer SaaS uygulamaları öncelikle isteyen kullanıcılar için kuramadığı cihazlarda büyük kuruluşlar tarafından kullanılması.

Merhaba geleneksel etki alanına katılma hala hello sunmasına karşın etki alanına katılma özellikli cihazlarda içi en iyi deneyimi, Azure AD birleştirme etki alanına katılma olamaz cihazlar için uygundur. Azure AD birleştirme hello bulut kullanıcıları yönetme için uygundur. Bunu Grup İlkesi ve System Center Configuration Manager (SCCM) gibi geleneksel etki alanı yönetim araçlarını kullanarak mobil cihaz yönetimi özellikleri yerine kullanarak yapar.

![Kurumsal ve kişisel aygıtlar şirket içi Active Directory ve Azure AD ile genel bakış](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Kuruluşların Azure AD katılım neden benimsemeyi?
* **Büyük ölçüde da işletmeler hello bulut**: taşınmış veya olan, şirket içi kullanım alanını azaltmaya ve daha fazla hello bulutta toooperate istediğiniz tooa modeli taşıyorsanız, Azure AD katılımı, faydalanabilir. Belki de el ile veya şirket içi Active Directory eşitleme aracılığıyla Azure AD hesapları oluşturdunuz. Her iki durumda da, Azure AD'de bir hesabınız varsa ve tooWindows 10 toosign kullanabilirsiniz. Kullanıcılarınızın kendi bilgisayarları tooAzure AD ya da hello out-of-box deneyimi (OOBE) veya hello ayarları menüsü üzerinden birleştirebilirsiniz. Katıldıktan sonra kullanıcılar tek oturum açma (SSO) erişimi toocloud kaynakları, Office 365 gibi tarayıcılarını veya Office uygulamaları keyfini çıkarın.
* **Eğitim kurumları**: yeterli yanıt hakkında sık hello senaryoları biri eğitim kurumları iki kullanıcı türlerine sahip: Fakülte ve öğrenciler. Bunun nedenle bunlar için şirket içi hesapları oluşturma arzu Fakülte üyeleri hello kuruluşunuzun daha uzun vadeli üyeleri olarak kabul edilir. Ancak Öğrenciler hello kuruluş shorter-term üyesi olan ve bu nedenle Azure AD'de yönetilebilir. Bu dizin ölçek toohello bulut şirket içi depolanan yerine gönderilemez anlamına gelir. Ayrıca Öğrenciler tooWindows kendi Azure AD hesaplarıyla oturum ve tooOffice 365 kaynakları tarayıcılarını veya Office uygulamaları erişmek anlamına gelir.
* **Perakende işletmeler**: biz heard hakkında müşterilerden başka bir kendi desire toomanage Mevsimlik çalışanları daha kolay bir senaryodur.  Yeniden hesapları daha uzun vadeli, tam zamanlı çalışanlar için genellikle şirket içi etki alanına katılmış makinede hesapları olarak oluşturulur. Ancak Mevsimlik çalışanlardır arzu toomanage olacak şekilde hello org shorter-term üyeleri bunları burada kullanıcı lisansları daha kolay taşınabilir geçici. Office 365 lisansına sahip hello bulutta bu kullanıcı hesapları oluşturma tooWindows ve bir Azure AD hesabının Office uygulamalarıyla imzalama hello kullanıcılar tooget hello avantajlarını sağlar. Bu sırada, bunlar çıktıktan sonra daha fazla esneklik, lisansları ile koruyun.
* **Diğer işletmelerin**: şirket içi Active Directory Kullanıcıları korumayı olsa bile, yine Azure AD alanına katılmış olması kullanıcılar kalmaktan faydalanabilir. Azure AD için Azure AD Basitleştirilmiş katılma deneyimi, verimli aygıt yönetimi, otomatik mobil cihaz Yönetimi kayıt ve çoklu oturum açma özelliği sunar ve şirket içi kaynakları olmasıdır.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Azure AD katılım hangi yetenekleri sunar?
Azure AD katılımı ile Merhaba aşağıdaki alın:

* **Şirkete ait cihazlar kendi kendine sağlama**: Windows 10, BT katılımı olmadan hello out-of-box deneyiminde, yepyeni, naylon aygıt kullanıcıları yapılandırabilirsiniz.
* **Modern form faktörleri desteği**: Azure AD birleştirme özellikleri hello geleneksel etki alanına Katıl sahip olmayan cihazlarda çalışır.  
* **Mevcut Kurumsal hesaplar için destek**: kullanıcılar artık toocreate gerekir ve bakımını bir Windows 8 ile yaptığınız gibi kişisel bir Microsoft hesabı tooget hello şirket tarafından verilen aygıtlarda en iyi deneyimi. Bunlar, mevcut iş hesaplarını Azure AD'de de yerine kullanabilirsiniz. Çoğu kuruluş için temel olarak kullanıcıları ayarlama ve tooWindows hello ile aynı oturum açma yani tooaccess Office 365 kullandıkları kimlik bilgileri.
* **Otomatik mobil cihaz Yönetimi kayıt**: cihazlar bağlıyken mobil cihaz Yönetimi'nde otomatik olarak da kaydedilebilir tooAzure AD. Bu işlem Microsoft Intune ve iş ortağı mobil cihaz yönetimi çözümleri ile çalışır. Aygıt Yönetimi Intune ile işiniz bittiğinde, BT yöneticilerinin İzleyici/hello SCCM yönetim konsolunda etki alanına katılmış cihazları yanı sıra Azure AD alanına katılmış cihazları yönetebilirsiniz.
* **Çoklu oturum açma toocompany kaynakları**: kullanıcıların keyfini çoklu oturum açma hello Windows Masaüstü tooapps ve Office 365 ve aracılığıylakimlikdoğrulamasıiçinAzureADbağlıişuygulamalarıbinlercegibihellobulutkaynaklarında[Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Birleştirilmiş tooAzure AD şirkete ait cihazları da keyfini çıkarın SSO tooon içi kaynaklar hello aygıt bir şirket ağındaki ve her yerden olduğunda bu kaynakları hello kullanıma sunulan zaman [Azure AD uygulama proxy'si](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **İşletim sistemi durumda Dolaşım**: erişilebilirlik ayarlarını, Web siteleri, Wi-Fi parolalar ve diğer ayarları eşitlenir şirkete ait aygıtlarda kişisel bir Microsoft hesabı gerek kalmadan.
* **Kurumsal kullanıma hazır Windows mağazası**: hello Windows mağazası uygulama edinme ve Azure AD hesapları ile lisans destekler. Kuruluşların yapabildikleri toplu lisans uygulamaları ve bunları kullanılabilir toohello kullanıcıların kuruluşlarında.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Farklı cihazları Azure AD'ye katılımı ile nasıl çalışır?
| Kurumsal cihaz (birleştirilmiş tooon içi etki alanı) | Kurumsal cihaz (birleştirilmiş toohello bulut) | Kişisel cihaz |
| --- | --- | --- |
| (Bugün yaptıkları gibi) Kullanıcılar Windows'a iş kimlik bilgileriyle oturum açabilir. |Kullanıcılar tooWindows Azure AD'de yönetilen iş kimlik bilgileriyle oturum açabilir. Bu, üç durumda Kurumsal cihazlar için geçerlidir: <ol><li>Merhaba kuruluşunuzun Active Directory şirket içinde (örneğin, küçük bir işletme) sahip değil.</li><li>Merhaba kuruluş Active Directory'de tüm kullanıcı hesapları oluşturma değil (örneğin, hesapları Öğrenciler, danışmanlar ya da Mevsimlik çalışanları için Active Directory'de oluşturulan değil).</li><li>Merhaba kuruluş telefonları veya mobil SKU (örneğin, geçen ikincil cihaz tooa Fabrika/perakende kat) çalıştıran tabletler gibi birleştirilmiş tooan (şirket içi) etki alanı olamaz şirket cihazları var.</li></ol> Hem yönetilen hem de Federasyon kuruluşlar için Kurumsal aygıtların birleştirme Azure AD katılımı destekler. |Kullanıcıların oturum açma tooWindows kişisel Microsoft hesabı kimlik bilgilerini (değişiklik) ile. |
| Kullanıcıların erişim tooroaming ayarlarını ve hello enterprise Windows mağazası sahip. Bu hizmetler, iş hesaplarıyla çalışır ve kişisel bir Microsoft hesabı gerektirmez. Bu, kendi şirket içi Active Directory tooAzure AD kuruluşlar tooconnect gerektirir. |Kullanıcılar, Self Servis Kurulum yapabilirsiniz. Her iki yöntem desteklenir, ancak bunlar hello ilk çalıştırma deneyimi (FRX) kendi iş hesabını alternatif toohaving BT hello cihazları sağlamak, gidebilirsiniz. |Active Directory veya Azure AD kullanıcıların yönetilen bir iş hesabı kolayca ekleyebilirsiniz. |
| Kullanıcılar, hello Masaüstü toowork uygulamaları, Web siteleri ve şirket içi kaynakları ve Azure AD kimlik doğrulaması için kullanmak bulut uygulamaları dahil olmak üzere kaynaklar--SSO sahipsiniz. |Cihazları otomatik olarak hello Kurumsal directory (Azure AD) kayıtlı ve mobil cihaz Yönetimi'nde otomatik olarak kaydedilir. (Azure AD Premium özelliği). |Kullanıcıların uygulamalara ve bu iş hesabıyla toowebsites/kaynaklarına arasında SSO özelliği vardır. |
| Kullanıcılar kendi kişisel Microsoft hesapları tooaccess kendi kişisel resimleri ve dosyaları Kurumsal verileri etkilemeden ekleyebilirsiniz. (Dolaşım ayarları, kullanıcılar iş hesaplarını toowork devam edin.) Merhaba Microsoft hesabı artık hello Dolaşım ayarları sürücüleri ve SSO sağlar. |Kullanıcılar, winlogon üzerinde Self Servis parola sıfırlama (SSPR) Unutulan parolayı sıfırlayabilirsiniz anlamı yapabilirsiniz. (Azure AD Premium özelliği). |Kullanıcıların erişim toohello enterprise Windows mağazası olması, böylece edinmeli ve kişisel cihazlarını satır iş kolu uygulamaları kullanın. |

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

