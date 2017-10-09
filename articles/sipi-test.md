---
title: "Sipi test dosyası | Microsoft Docs"
description: "Dosya toocheck ReadyForTest bağımlılıkları test"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="7f6da-103">Sipi test dosyası</span><span class="sxs-lookup"><span data-stu-id="7f6da-103">Sipi test file</span></span>

<span data-ttu-id="7f6da-104">Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7f6da-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="7f6da-105">İşiniz bittiğinde, uygulamanızı hello Azure B2C Kiracı kullanmak için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="7f6da-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f6da-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f6da-106">Prerequisites</span></span>

<span data-ttu-id="7f6da-107">toobuild tüketicinin kaydolmasını ve oturum açma kabul eden bir uygulama, ilk Azure Active Directory B2C kiracısı ile tooregister Merhaba uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f6da-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="7f6da-108">Kendi Kiracı özetlenen hello adımları kullanarak alma [bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7f6da-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="7f6da-109">Hello hello Azure AD B2C dikey penceresinde hello Azure portalında oluşturulan uygulamaları yönetilen aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="7f6da-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="7f6da-110">PowerShell veya başka bir portal kullanarak hello B2C uygulamaları düzenlerseniz, desteklenmeyen haline gelir ve Azure AD B2C ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="7f6da-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="7f6da-111">Merhaba ayrıntıları görmek [hatalı uygulamaları](#faulted-apps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="7f6da-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="7f6da-112">TooB2C ayarları gidin</span><span class="sxs-lookup"><span data-stu-id="7f6da-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="7f6da-113">İçinde toohello oturum [Azure portal](https://portal.azure.com/) hello B2C kiracısının genel Yöneticisi hello gibi.</span><span class="sxs-lookup"><span data-stu-id="7f6da-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="7f6da-114">Sonraki adımlar kaydettirmekte olduğunuz hello uygulama türüne göre seçin:</span><span class="sxs-lookup"><span data-stu-id="7f6da-114">Choose next steps based on hello application type you are registering:</span></span>
