---
title: "aaaEnterprise durum gezici genel bakış | Microsoft Docs"
description: "Windows cihazlarda Kurumsal durumda Dolaşım ayarları hakkında bilgi sağlar. Kurumsal durumda dolaşım, kullanıcılar Windows cihazlarını arasında birleştirilmiş bir deneyim sağlar ve yeni bir cihaz yapılandırmak için gereken hello süreyi azaltır."
services: active-directory
keywords: "windows bulut Kurumsal durumda dolaşım, Kurumsal eşitleme nedir"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Kurumsal Durumda Dolaşıma genel bakış
Windows 10 ile [Azure Active Directory (Azure AD)](active-directory-whatis.md) kullanıcılar kazanç hello özelliği toosecurely eşitleme kullanıcı ayarlarını ve uygulama ayarlarını veri toohello bulut. Kurumsal durumda dolaşım, kullanıcılar Windows cihazlarını arasında birleştirilmiş bir deneyim sağlar ve yeni bir cihaz yapılandırmak için gereken hello süreyi azaltır. Kurumsal durumda Dolaşım çalışır benzer toohello standart [tüketici ayarları eşitleme](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) , ilk kez sunulmuştur Windows 8'de. Ayrıca, Kurumsal durumda Dolaşım sunar:

* **Ayrımı Kurumsal ve tüketici veri** – kuruluşlar kendi veri denetiminde, ve şirket verilerinin tüketici bulut hesabında ya da bir kurumsal bulut hesabı tüketici verilerde hiçbir karıştırma.
* **Gelişmiş Güvenlik** – verileri, Azure Rights Management (Azure RMS) kullanarak hello kullanıcının Windows 10 cihaz ayrılmadan önce otomatik olarak şifrelenir ve veri REST hello bulutta şifrelenmiş kalır. Tüm içerik REST hello ad alanları, ayarları ve Windows uygulama adlarını gibi dışında hello bulutta şifrelenmiş kalır.  
* **Daha iyi yönetim ve izleme** – sağlar denetim ve görünürlük kimin ayarları kuruluşunuzdaki ve hangi cihazların Merhaba Azure AD portalı tümleştirme yoluyla eşitlenir üzerinden. 

Kurumsal durumda Dolaşım birden çok Azure bölgelerde kullanılabilir. Merhaba üzerinde kullanılabilir bölgelerin güncelleştirilmiş hello listesini bulabilirsiniz [bölgelere göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) sayfasında Azure Active Directory altında.

| Makale | Açıklama |
| --- | --- |
| [Azure Active Directory'de gezici Kurumsal durumu etkinleştir](active-directory-windows-enterprise-state-roaming-enable.md) |Kurumsal durumda Dolaşım Premium Azure Active Directory (Azure AD) abonelik kullanılabilir tooany kuruluşla olur. Konusunda daha fazla ayrıntı için tooget bir Azure AD abonelik bkz hello [Azure AD ürün](https://azure.microsoft.com/services/active-directory) sayfası. |
| [Ayarlar ve veri dolaşımı SSS](active-directory-windows-enterprise-state-roaming-faqs.md) |Bu konuda, BT yöneticileri, ayarları ve uygulama veri eşitleme hakkında olabilir bazı sorular yanıtlanmaktadır. |
| [Grup İlkesi ve ayarları eşitleme için MDM ayarları](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 Grup İlkesi ve mobil cihaz Yönetimi (MDM) ilkesi ayarları toolimit ayarları eşitleme sağlar. |
| [Windows 10 Dolaşım ayarları başvurusu](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |Merhaba, çıkan ve/veya Yedeklenen Windows 10'da tüm hello ayarlarının tam listesi verilmiştir. |
| [Sorun giderme](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |Bu konu, sorun giderme için bazı temel adımların geçer ve bilinen sorunların bir listesini içerir. |

