---
title: "Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme | Microsoft Docs"
description: "Azure AD Connect eşitleme nasıl çalışır ve nasıl açıklanmaktadır toocustomize."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme
Hello Azure Active Directory Connect Eşitleme Hizmetleri (Azure AD Connect eşitleme) Azure AD Connect ana bileşenidir. Bu ilgili toosynchronize kimlik verilerini şirket içi ortamınız ile Azure AD arasındaki tüm hello işlemlerini ilgilenir. Azure AD Connect eşitleme Azure Active Directory Bağlayıcısı yapılandırılmış hello ile DirSync, Azure AD eşitleme ve Forefront Identity Manager hello ardıl ' dir.

Bu konuda hello olduğu için giriş **Azure AD Connect eşitleme** (olarak da bilinir **eşitleme altyapısı**) ve listeleri diğer konular ilgili tooit tooall bağlar. Bağlantılar tooAzure AD Connect, bkz: [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

Merhaba eşitleme hizmeti hello şirket içi iki bileşenden oluşur **Azure AD Connect eşitleme** bileşeni ve hello Hizmet tarafı Azure AD'de adlı **Azure AD Connect eşitleme hizmeti**. Merhaba DirSync, Azure AD eşitleme ve Azure AD Connect için ortak bir hizmettir.

## <a name="azure-ad-connect-sync-topics"></a>Azure AD Connect eşitleme konuları
| Konu | Ne kapsar ve ne zaman tooread |
| --- | --- |
| **Azure AD Connect eşitleme temelleri** | |
| [Merhaba mimarisini anlama](active-directory-aadconnectsync-understanding-architecture.md) |Bu, kimin yeni toohello eşitleme altyapısı bulunur ve hello mimarisi ve kullanılan hello terimler hakkında toolearn istiyor. |
| [Teknik kavramlar](active-directory-aadconnectsync-technical-concepts.md) |Merhaba hello mimarisi konu ve kısaca kısa bir sürümünü açıklar kullanılan terimler. |
| [Azure AD Connect için topolojiler](active-directory-aadconnect-topologies.md) |Merhaba farklı topolojileri ve senaryoları hello eşitleme altyapısı destekler açıklar. |
| **Özel yapılandırma** | |
| [Çalışan hello Yükleme Sihirbazı'nı yeniden](active-directory-aadconnectsync-installation-wizard.md) |Ne seçeneklerini açıklar sahip hello Azure AD Connect Yükleme Sihirbazı'nı yeniden çalıştırdığınızda kullanılabilir. |
| [Bildirim temelli hazırlama anlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Bildirim temelli hazırlama adlı hello yapılandırma modeli açıklar. |
| [Bildirim temelli hazırlama ifadelerini anlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Bildirim temelli hazırlama kullanılan hello ifade dili Hello sözdizimi anlatılmaktadır. |
| [Merhaba varsayılan yapılandırmayı anlama](active-directory-aadconnectsync-understanding-default-configuration.md) |Merhaba out-of-box kuralları ve hello varsayılan yapılandırmayı açıklar. Ayrıca hello kuralları hello out-of-box senaryoları toowork için birlikte nasıl çalıştığını açıklar. |
| [Kullanıcıları ve kişileri anlama](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Merhaba önceki konuda devam eder ve kullanıcıları ve kişileri hello yapılandırmasını birlikte, özellikle bir Çoklu orman ortamında nasıl çalıştığını açıklar. |
| [Nasıl toomake değişiklik toohello varsayılan yapılandırması](active-directory-aadconnectsync-change-the-configuration.md) |Toomake ortak bir yapılandırma değişikliği tooattribute nasıl akacağını aracılığıyla anlatılmaktadır. |
| [Merhaba varsayılan yapılandırmasını değiştirmek için en iyi uygulamalar](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Destek sınırlamaları ve değişiklikleri toohello out-of-box yapılandırma sağlama. |
| [Filtrelemeyi Yapılandırma](active-directory-aadconnectsync-configure-filtering.md) |Merhaba nasıl nesneleri yükleniyor toolimit tooAzure AD ve adım adım nasıl eşitlenmiş için farklı seçenekleri açıklar tooconfigure Bu seçenekler. |
| **Özellikler ve senaryolar** | |
| [Yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Merhaba açıklar *yanlışlıkla silmeleri engelleme* özelliği ve nasıl tooconfigure onu. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |İçeri aktarma, eşitleme ve verileri dışarı aktarma hello yerleşik Zamanlayıcı, açıklar. |
| [Parola Eşitleme uygulama](active-directory-aadconnectsync-implement-password-synchronization.md) |Parola Eşitleme nasıl çalışır, açıklar nasıl tooimplement ve nasıl toooperate ve sorun giderme. |
| [Cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md) |Cihaz geri yazma Azure AD Connect nasıl çalıştığı açıklanmaktadır. |
| [Dizin genişletmeleri](active-directory-aadconnectsync-feature-directory-extensions.md) |Nasıl tooextend hello Azure AD şema kendi özel özniteliklere sahip açıklar. |
| **Eşitleme hizmeti** | |
| [Azure AD Connect eşitleme hizmeti özellikleri](active-directory-aadconnectsyncservice-features.md) |Merhaba eşitleme hizmeti yan ve nasıl toochange eşitleme ayarlarını Azure AD'de açıklar. |
| [Yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Açıklar nasıl tooenable ve **userPrincipalName** ve **proxyAddresses** yinelenen öznitelik değerleri dayanıklılık. |
| **İşlemler ve kullanıcı Arabirimi** | |
| [Eşitleme Hizmeti Yöneticisi](active-directory-aadconnectsync-service-manager-ui.md) |Merhaba Eşitleme Hizmeti Yöneticisi'ni de dahil olmak üzere kullanıcı Arabirimi, açıklar [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md), [Bağlayıcılar](active-directory-aadconnectsync-service-manager-ui-connectors.md), [meta veri deposu Tasarımcısı](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), ve [meta veri deposu arama](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) sekmeleri. |
| [İşletimsel görevleri ve ilgili önemli noktalar](active-directory-aadconnectsync-operations.md) |Olağanüstü durum kurtarma gibi işletimsel sorunlar açıklanmaktadır. |
| **Nasıl Yapılır...** | |
| [Hello Azure AD hesabı Sıfırla](active-directory-aadconnectsync-howto-azureadaccount.md) |Nasıl tooreset hello hizmetin kimlik bilgilerini hello Azure AD Connect eşitleme tooAzure AD alanından tooconnect kullanılır. |
| **Daha fazla bilgi ve başvurular** | |
| [Bağlantı Noktaları](active-directory-aadconnect-ports.md) |Bağlantı noktalarını listeler hello eşitleme altyapısı ve şirket içi dizinlere ve Azure AD arasında tooopen gerekir. |
| [TooAzure Active Directory öznitelikleri eşitlenir](active-directory-aadconnectsync-attributes-synchronized.md) |AD ve Azure AD şirket içi arasında eşitlenen tüm öznitelikleri listeler. |
| [İşlevler Başvurusu](active-directory-aadconnectsync-functions-reference.md) |Bildirim temelli hazırlama kullanılabilen tüm işlevleri listeler. |

## <a name="additional-resources"></a>Ek Kaynaklar
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

