---
title: "Azure Active Directory B2C: Bölge kullanılabilirliği & veri residency | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C kiracılar türleri hakkında"
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
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="6ecac-103">Azure Active Directory B2C: Bölge kullanılabilirliği & veri residency</span><span class="sxs-lookup"><span data-stu-id="6ecac-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="6ecac-104">Bölge kullanılabilirliği ve veri residency Azure geri kalanından farklı Azure AD B2C'ye uygulamak iki çok farklı kavram olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ecac-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="6ecac-105">Bu makalede, bu iki kavram arasındaki farkları açıklamaktadır ve nasıl Azure Azure AD B2C ile uygulandıkları karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="6ecac-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="6ecac-106">Özet</span><span class="sxs-lookup"><span data-stu-id="6ecac-106">Summary</span></span>
<span data-ttu-id="6ecac-107">Azure AD B2C olan **genel olarak kullanılabilir dünya çapında** için seçeneğiyle **Amerika Birleşik Devletleri ya da Avrupa veri residency**.</span><span class="sxs-lookup"><span data-stu-id="6ecac-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="6ecac-108">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="6ecac-108">Concepts</span></span>
* <span data-ttu-id="6ecac-109">**Bölge kullanılabilirliği** hizmet kullanılabilir olduğu için başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="6ecac-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="6ecac-110">**Veri residency** kullanıcı verilerinin depolandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="6ecac-111">Bölge kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="6ecac-111">Region availability</span></span>
<span data-ttu-id="6ecac-112">Azure AD B2C, dünya çapında Azure genel bulut kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="6ecac-113">Bu kullanılabilirlik veri residency ile eşleştiği en diğer Azure Hizmetleri izleyin modelden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="6ecac-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="6ecac-114">Her iki Azure'nın bu örneklerde görebilirsiniz [tarafından ürünleri kullanılabilir bölge](https://azure.microsoft.com/regions/services/) sayfa ve [Active Directory B2C fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="6ecac-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="6ecac-115">Veri yerleşikliği</span><span class="sxs-lookup"><span data-stu-id="6ecac-115">Data residency</span></span>
<span data-ttu-id="6ecac-116">Azure AD B2C, Amerika Birleşik Devletleri veya Avrupa kullanıcı verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="6ecac-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="6ecac-117">Veri residency hangi ülke/bölge seçili göre belirlenir zaman [Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6ecac-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="6ecac-119">Amerika Birleşik Devletleri aşağıdaki ülkelerde/bölgelerde için veri bulunur:</span><span class="sxs-lookup"><span data-stu-id="6ecac-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="6ecac-120">Amerika Birleşik Devletleri, Kanada, Kosta Rika, Dominik Cumhuriyeti, El Salvador, Guatemala, Meksika, Panama, Porto Riko ve Trinidad ve Tobago</span><span class="sxs-lookup"><span data-stu-id="6ecac-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="6ecac-121">Veri Avrupa'da aşağıdaki ülkelerde/bölgelerde bulunur:</span><span class="sxs-lookup"><span data-stu-id="6ecac-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="6ecac-122">Cezayir, Avusturya, Azerbaycan, Bahreyn, Beyaz Rusya, Belçika, Bulgaristan, Hırvatistan, Kıbrıs, Çek Cumhuriyeti, Danimarka, Mısır, Estonya, Finlandiya, Fransa, Almanya, Yunanistan, Macaristan, İzlanda, İrlanda, İsrail, İtalya, Ürdün, Kazakistan, Kenya, Kuveyt, Lativa, Lübnan, Liechtenstein, Lituania, Lüksemburg, Makedonya (EYC), Malta, Karadağ, Fas, Hollanda, Nijerya, Norveç, Umman, Pakistan, Polonya, Portekiz, Katar, Romanya, Rusya, Suudi Arabistan, Sırbistan, Slovakya, Slovenya, Güney Afrika, İspanya, İsveç, İsviçre, Tunus, Türkiye, Ukrayna, Birleşik Arap Emirlikleri ve İngiltere.</span><span class="sxs-lookup"><span data-stu-id="6ecac-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="6ecac-123">Kalan ülkelerde/bölgelerde listeye eklenen sürecinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="6ecac-124">Şimdilik, Azure AD B2C ülkelerde/bölgelerde yukarıdaki birini seçerek kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ecac-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="6ecac-125">Afganistan, Arjantin, Avustralya, Brezilya, Şili, Kolombiya, Ekvator, Hong Kong ÖİB, Hindistan, Endonezya, Irak, Japonya, Kore, Malezya, Yeni Zelanda, Paraguay, Peru, Filipin, Singapur, Sri Lanka, Tayvan, Tayland, Uruguay ve Venezuela.</span><span class="sxs-lookup"><span data-stu-id="6ecac-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="6ecac-126">Önizleme Kiracı</span><span class="sxs-lookup"><span data-stu-id="6ecac-126">Preview tenant</span></span>
<span data-ttu-id="6ecac-127">Azure AD B2C'ın Önizleme dönemi boyunca B2C Kiracı oluşturduysanız olasıdır, **Kiracı türü** diyor **Önizleme Kiracı**.</span><span class="sxs-lookup"><span data-stu-id="6ecac-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="6ecac-128">Bu durumda, yalnızca geliştirme ve test amaçlıdır ve üretim uygulamaları için değil, Kiracı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ecac-129">Üretim ölçeği B2C Kiracı Önizleme B2C Kiracı hiçbir geçiş yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="6ecac-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="6ecac-130">Önizleme B2C Kiracı sildiğinizde ve bir üretim ölçeği B2C Kiracı aynı etki alanı adı ile yeniden oluşturmanız bilinen vardır Not verir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="6ecac-131">Farklı bir etki alanı adı ile bir üretim ölçeği B2C Kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ecac-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Önizleme Kiracı ekran görüntüsü](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
