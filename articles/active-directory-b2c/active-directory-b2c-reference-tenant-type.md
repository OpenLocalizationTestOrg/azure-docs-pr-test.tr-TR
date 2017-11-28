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
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="894f0-103">Azure Active Directory B2C: Bölge kullanılabilirliği & veri residency</span><span class="sxs-lookup"><span data-stu-id="894f0-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="894f0-104">Bölge kullanılabilirliği ve veri residency tooAzure AD B2C'hello Azure kalanından farklı uygulamak iki çok farklı kavram olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="894f0-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="894f0-105">Bu makalede bu iki kavramları arasında hello farkları açıklamaktadır ve bunların Azure AD B2C karşı tooAzure nasıl uygulayacağınıza karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="894f0-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="894f0-106">Özet</span><span class="sxs-lookup"><span data-stu-id="894f0-106">Summary</span></span>
<span data-ttu-id="894f0-107">Azure AD B2C olan **genel olarak kullanılabilir dünya çapında** hello seçeneğine sahip **Amerika Birleşik Devletleri ya da Avrupa veri residency**.</span><span class="sxs-lookup"><span data-stu-id="894f0-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="894f0-108">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="894f0-108">Concepts</span></span>
* <span data-ttu-id="894f0-109">**Bölge kullanılabilirliği** toowhere başvuran bir hizmeti kullanılabilir durumda.</span><span class="sxs-lookup"><span data-stu-id="894f0-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="894f0-110">**Veri residency** toowhere kullanıcı verilerin depolandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="894f0-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="894f0-111">Bölge kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="894f0-111">Region availability</span></span>
<span data-ttu-id="894f0-112">Azure AD B2C'hello Azure genel bulut tüm dünyada kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="894f0-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="894f0-113">Bu kullanılabilirlik veri residency ile eşleştiği en diğer Azure Hizmetleri izleyin hello modelden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="894f0-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="894f0-114">Her iki Azure'nın bu örneklerde görebilirsiniz [tarafından ürünleri kullanılabilir bölge](https://azure.microsoft.com/regions/services/) sayfası ve hello [Active Directory B2C fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="894f0-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="894f0-115">Veri yerleşikliği</span><span class="sxs-lookup"><span data-stu-id="894f0-115">Data residency</span></span>
<span data-ttu-id="894f0-116">Azure AD B2C, Amerika Birleşik Devletleri veya Avrupa kullanıcı verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="894f0-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="894f0-117">Veri residency hangi ülke/bölge seçili göre belirlenir zaman [Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="894f0-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="894f0-119">Merhaba Amerika Birleşik Devletleri ülkelerde/bölgelerde aşağıdaki hello için veri bulunur:</span><span class="sxs-lookup"><span data-stu-id="894f0-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="894f0-120">Amerika Birleşik Devletleri, Kanada, Kosta Rika, Dominik Cumhuriyeti, El Salvador, Guatemala, Meksika, Panama, Porto Riko ve Trinidad ve Tobago</span><span class="sxs-lookup"><span data-stu-id="894f0-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="894f0-121">Veri Avrupa'da ülkelerde/bölgelerde aşağıdaki Merhaba bulunur:</span><span class="sxs-lookup"><span data-stu-id="894f0-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="894f0-122">Cezayir, Avusturya, Azerbaycan, Bahreyn, Beyaz Rusya, Belçika, Bulgaristan, Hırvatistan, Kıbrıs, Çek Cumhuriyeti, Danimarka, Mısır, Estonya, Finlandiya, Fransa, Almanya, Yunanistan, Macaristan, İzlanda, İrlanda, İsrail, İtalya, Ürdün, Kazakistan, Kenya, Kuveyt, Lativa, Lübnan, Liechtenstein, Lituania, Lüksemburg, Makedonya (EYC), Malta, Karadağ, Fas, Hollanda, Nijerya, Norveç, Umman, Pakistan, Polonya, Portekiz, Katar, Romanya, Rusya, Suudi Arabistan, Sırbistan, Slovakya, Slovenya, Güney Afrika, İspanya, İsveç, İsviçre, Tunus, Türkiye, Ukrayna, Birleşik Arap Emirlikleri ve İngiltere.</span><span class="sxs-lookup"><span data-stu-id="894f0-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="894f0-123">Merhaba kalan ülkelerde/bölgelerde toohello listesi eklenmekte olan hello devam etmektedir.</span><span class="sxs-lookup"><span data-stu-id="894f0-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="894f0-124">Şimdilik, Azure AD B2C hello ülkelerinde yukarıdaki birini seçerek kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="894f0-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="894f0-125">Afganistan, Arjantin, Avustralya, Brezilya, Şili, Kolombiya, Ekvator, Hong Kong ÖİB, Hindistan, Endonezya, Irak, Japonya, Kore, Malezya, Yeni Zelanda, Paraguay, Peru, Filipin, Singapur, Sri Lanka, Tayvan, Tayland, Uruguay ve Venezuela.</span><span class="sxs-lookup"><span data-stu-id="894f0-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="894f0-126">Önizleme Kiracı</span><span class="sxs-lookup"><span data-stu-id="894f0-126">Preview tenant</span></span>
<span data-ttu-id="894f0-127">Azure AD B2C'ın Önizleme dönemi boyunca B2C Kiracı oluşturduysanız olasıdır, **Kiracı türü** diyor **Önizleme Kiracı**.</span><span class="sxs-lookup"><span data-stu-id="894f0-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="894f0-128">Merhaba Durum buysa, yalnızca geliştirme ve test amaçlıdır ve üretim uygulamaları için değil, Kiracı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="894f0-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="894f0-129">B2C Kiracı tooa üretim ölçeği B2C Kiracı Önizleme hiçbir geçiş yolundan yoktur.</span><span class="sxs-lookup"><span data-stu-id="894f0-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="894f0-130">Önizleme B2C Kiracı sildiğinizde bilinen sorunlar unutmayın ve üretim ölçeği B2C Kiracı ile yeniden oluşturmanız aynı etki alanı adı hello.</span><span class="sxs-lookup"><span data-stu-id="894f0-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="894f0-131">Bir üretim ölçeği B2C Kiracı farklı etki alanı adı ile toocreate var.</span><span class="sxs-lookup"><span data-stu-id="894f0-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
