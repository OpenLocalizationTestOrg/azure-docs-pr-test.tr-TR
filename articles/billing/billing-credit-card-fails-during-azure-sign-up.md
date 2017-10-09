---
title: "aaaCredit kartı Azure işaretini yukarı | Microsoft Docs"
description: "Azure için toosign çalıştığınızda kredi veya ATM kartı reddedildi olduğunda tooresolve nasıl yayınlar öğrenin."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
keywords: "Kredi Kartı Reddedildi, ATM kartı reddedildi, kredi kartı reddedildi, kredi kartı getirmiyor"
ms.assetid: 407ef3db-2a64-4a04-a08f-7d1d1c4860c7
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: a246f443638b10693b1a3d3335cc56ed24dddb5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="your-debit-card-or-credit-card-is-declined-at-azure-sign-up"></a><span data-ttu-id="cc13c-104">Azure kaydolma ATM kartı veya kredi kartı reddedildi</span><span class="sxs-lookup"><span data-stu-id="cc13c-104">Your debit card or credit card is declined at Azure sign-up</span></span>
<span data-ttu-id="cc13c-105">ATM kartı veya kredi kartı reddedildi veya Azure'a kaydolduğunuzda kabul edilmedi, sorunları aşağıdaki hello birini karşı karşıya:</span><span class="sxs-lookup"><span data-stu-id="cc13c-105">If your debit card or credit card is declined or not accepted when you sign up for Azure, you might be facing one of hello following issues:</span></span>

* <span data-ttu-id="cc13c-106">**Merhaba kredi kartı veya ATM kartı sağlayıcısı ülkeniz için kabul edilmedi.**</span><span class="sxs-lookup"><span data-stu-id="cc13c-106">**hello credit card or debit card provider is not accepted for your country.**</span></span> <span data-ttu-id="cc13c-107">Bir kart seçtiğinizde, yalnızca seçtiğiniz hello ülkede geçerli hello seçenekleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc13c-107">When you choose a card, you only see hello options that are valid in hello country that you select.</span></span> <span data-ttu-id="cc13c-108">Banka veya kartı veren tooconfirm başvurun kredi kartınızdan uluslararası işlemleri için etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="cc13c-108">Contact your bank or card issuer tooconfirm that your credit card is enabled for international transactions.</span></span> <span data-ttu-id="cc13c-109">Bkz: desteklenen ülke ve para [Azure satın alma ile ilgili SSS](https://azure.microsoft.com/pricing/faq/).</span><span class="sxs-lookup"><span data-stu-id="cc13c-109">See supported countries and currencies in [Azure Purchase FAQ](https://azure.microsoft.com/pricing/faq/).</span></span>
* <span data-ttu-id="cc13c-110">**Kredi veya ATM kartı bilgilerinizi yanlış veya eksik.**</span><span class="sxs-lookup"><span data-stu-id="cc13c-110">**Your credit or debit card information is inaccurate or incomplete.**</span></span> <span data-ttu-id="cc13c-111">Merhaba ad, adres ve kart doğrulama kodu girdiğiniz ne hello kart üzerinde basılıdır tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="cc13c-111">hello name, address, and CVV code you enter must match exactly what’s printed on hello card.</span></span>
* <span data-ttu-id="cc13c-112">**Bir sanal veya ön ödemeli kart kullanıyorsunuz.**</span><span class="sxs-lookup"><span data-stu-id="cc13c-112">**You're using a virtual or prepaid card.**</span></span> <span data-ttu-id="cc13c-113">Sanal veya ön ödemeli kredi veya ATM kartı Azure abonelikleri için ödeme olarak kabul değil.</span><span class="sxs-lookup"><span data-stu-id="cc13c-113">Virtual or prepaid credit or debit cards aren't accepted as payment for Azure subscriptions.</span></span>
* <span data-ttu-id="cc13c-114">**Merhaba etkin olmayan veya engellenen karttır.**</span><span class="sxs-lookup"><span data-stu-id="cc13c-114">**hello card is inactive or blocked.**</span></span> <span data-ttu-id="cc13c-115">Banka tooensure başvurun kartınız etkindir.</span><span class="sxs-lookup"><span data-stu-id="cc13c-115">Contact your bank tooensure your card is active.</span></span>
* <span data-ttu-id="cc13c-116">**Diğer kaydolma sorunları yaşıyor olabilir** nasıl çok denetleyin[Azure kaydolma sorunlarını giderme](billing-troubleshoot-azure-sign-up-issues.md).</span><span class="sxs-lookup"><span data-stu-id="cc13c-116">**You may be experiencing other sign-up issues** Check out how too[troubleshoot Azure sign-up](billing-troubleshoot-azure-sign-up-issues.md).</span></span>

<span data-ttu-id="cc13c-117">Ödeme bilgilerinizi güncelleştirdikten sonra tekrar oturum deneyin.</span><span class="sxs-lookup"><span data-stu-id="cc13c-117">After you update your payment information, try signing up again.</span></span>

## <a name="representing-a-business-that-doesnt-want-toopay-by-card-set-up-invoicing"></a><span data-ttu-id="cc13c-118">Toopay kartı tarafından istememektedir bir iş temsil eden?</span><span class="sxs-lookup"><span data-stu-id="cc13c-118">Representing a business that doesn't want toopay by card?</span></span> <span data-ttu-id="cc13c-119">Faturalama yukarı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cc13c-119">Set up invoicing</span></span>
<span data-ttu-id="cc13c-120">Bir iş temsil ediyorsa, fatura ödeme yöntemleriyle denetimleri, ertesi gün denetimleri veya Banka havaleleri gibi Azure aboneliğiniz için ödeme.</span><span class="sxs-lookup"><span data-stu-id="cc13c-120">If you represent a business, you can pay for your Azure subscription with invoice payment methods like checks, overnight checks, or wire transfers.</span></span> <span data-ttu-id="cc13c-121">Fatura ile toopay ayarladıktan sonra tooanother ödeme seçeneği değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc13c-121">You can’t change tooanother payment option after you’re set up toopay by invoice.</span></span> <span data-ttu-id="cc13c-122">Fatura tarafından toopay bkz [Azure faturalama - nasıl tooinvoice](https://azure.microsoft.com/pricing/invoicing/).</span><span class="sxs-lookup"><span data-stu-id="cc13c-122">toopay by invoice, see [Azure Billing - How tooinvoice](https://azure.microsoft.com/pricing/invoicing/).</span></span>

## <a name="update-your-credit-card-or-debit-card-information"></a><span data-ttu-id="cc13c-123">Kredi kartı veya ATM kartı bilgilerinizi güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="cc13c-123">Update your credit card or debit card information</span></span>
<span data-ttu-id="cc13c-124">Oturumu sonra [Ödeme bilgilerinizi yönetmek](billing-how-to-change-credit-card.md) toochange veya bir kart kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cc13c-124">After you sign up, [manage your payment information](billing-how-to-change-credit-card.md) toochange or remove a card.</span></span>

## <a name="need-more-help-contact-support"></a><span data-ttu-id="cc13c-125">Daha fazla yardım gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="cc13c-125">Need more help?</span></span> <span data-ttu-id="cc13c-126">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="cc13c-126">Contact support.</span></span>
<span data-ttu-id="cc13c-127">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="cc13c-127">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
