---
title: "Azure Active Directory B2C: Bölge kullanılabilirliği & veri residency | Microsoft Docs"
description: "Azure Active Directory B2C kiracılar hello türleri üzerinde bir konu"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: Bölge kullanılabilirliği & veri residency
Bölge kullanılabilirliği ve veri residency tooAzure AD B2C'hello Azure kalanından farklı uygulamak iki çok farklı kavram olmasıdır. Bu makalede bu iki kavramları arasında hello farkları açıklamaktadır ve bunların Azure AD B2C karşı tooAzure nasıl uygulayacağınıza karşılaştırın.

## <a name="summary"></a>Özet
Azure AD B2C olan **genel olarak kullanılabilir dünya çapında** hello seçeneğine sahip **Amerika Birleşik Devletleri ya da Avrupa veri residency**.

## <a name="concepts"></a>Kavramlar
* **Bölge kullanılabilirliği** toowhere başvuran bir hizmeti kullanılabilir durumda.
* **Veri residency** toowhere kullanıcı verilerin depolandığı anlamına gelir.

## <a name="region-availability"></a>Bölge kullanılabilirliği
Azure AD B2C'hello Azure genel bulut tüm dünyada kullanılabilir. 

Bu kullanılabilirlik veri residency ile eşleştiği en diğer Azure Hizmetleri izleyin hello modelden farklıdır. Her iki Azure'nın bu örneklerde görebilirsiniz [tarafından ürünleri kullanılabilir bölge](https://azure.microsoft.com/regions/services/) sayfası ve hello [Active Directory B2C fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Veri yerleşikliği
Azure AD B2C, Amerika Birleşik Devletleri veya Avrupa kullanıcı verilerini depolar.

Veri residency hangi ülke/bölge seçili göre belirlenir zaman [Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).

![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Merhaba Amerika Birleşik Devletleri ülkelerde/bölgelerde aşağıdaki hello için veri bulunur:

> Amerika Birleşik Devletleri, Kanada, Kosta Rika, Dominik Cumhuriyeti, El Salvador, Guatemala, Meksika, Panama, Porto Riko ve Trinidad ve Tobago

Veri Avrupa'da ülkelerde/bölgelerde aşağıdaki Merhaba bulunur:

> Cezayir, Avusturya, Azerbaycan, Bahreyn, Beyaz Rusya, Belçika, Bulgaristan, Hırvatistan, Kıbrıs, Çek Cumhuriyeti, Danimarka, Mısır, Estonya, Finlandiya, Fransa, Almanya, Yunanistan, Macaristan, İzlanda, İrlanda, İsrail, İtalya, Ürdün, Kazakistan, Kenya, Kuveyt, Lativa, Lübnan, Liechtenstein, Lituania, Lüksemburg, Makedonya (EYC), Malta, Karadağ, Fas, Hollanda, Nijerya, Norveç, Umman, Pakistan, Polonya, Portekiz, Katar, Romanya, Rusya, Suudi Arabistan, Sırbistan, Slovakya, Slovenya, Güney Afrika, İspanya, İsveç, İsviçre, Tunus, Türkiye, Ukrayna, Birleşik Arap Emirlikleri ve İngiltere.

Merhaba kalan ülkelerde/bölgelerde toohello listesi eklenmekte olan hello devam etmektedir.  Şimdilik, Azure AD B2C hello ülkelerinde yukarıdaki birini seçerek kullanmaya devam edebilirsiniz.

> Afganistan, Arjantin, Avustralya, Brezilya, Şili, Kolombiya, Ekvator, Hong Kong ÖİB, Hindistan, Endonezya, Irak, Japonya, Kore, Malezya, Yeni Zelanda, Paraguay, Peru, Filipin, Singapur, Sri Lanka, Tayvan, Tayland, Uruguay ve Venezuela.

## <a name="preview-tenant"></a>Önizleme Kiracı
Azure AD B2C'ın Önizleme dönemi boyunca B2C Kiracı oluşturduysanız olasıdır, **Kiracı türü** diyor **Önizleme Kiracı**. Merhaba Durum buysa, yalnızca geliştirme ve test amaçlıdır ve üretim uygulamaları için değil, Kiracı kullanmanız gerekir.

> [!IMPORTANT]
> B2C Kiracı tooa üretim ölçeği B2C Kiracı Önizleme hiçbir geçiş yolundan yoktur. Önizleme B2C Kiracı sildiğinizde bilinen sorunlar unutmayın ve üretim ölçeği B2C Kiracı ile yeniden oluşturmanız aynı etki alanı adı hello. Bir üretim ölçeği B2C Kiracı farklı etki alanı adı ile toocreate var.


![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
