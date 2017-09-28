---
title: "Sipi test dosyası | Microsoft Docs"
description: "Test dosyası ReadyForTest bağımlılıkları denetle"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="d4744-103">Sipi test dosyası</span><span class="sxs-lookup"><span data-stu-id="d4744-103">Sipi test file</span></span>

<span data-ttu-id="d4744-104">Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d4744-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="d4744-105">İşiniz bittiğinde, uygulamanız Azure B2C Kiracısında kullanım için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d4744-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4744-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4744-106">Prerequisites</span></span>

<span data-ttu-id="d4744-107">Tüketicinin kaydolmasını ve oturum açmasını kabul eden bir uygulama oluşturmak için öncelikle uygulamayı Azure Active Directory B2C kiracısına kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4744-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d4744-108">[Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md) makalesinde ana hatlarıyla belirtilen adımları izleyerek kendi kiracınızı edinin.</span><span class="sxs-lookup"><span data-stu-id="d4744-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="d4744-109">Azure portalında Azure AD B2C dikey penceresinden oluşturulan uygulamaların aynı konumdan yönetilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4744-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="d4744-110">B2C uygulamalarını PowerShell veya başka bir portal kullanarak düzenlerseniz bu uygulamalar desteklenmez duruma gelir ve Azure AD B2C ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="d4744-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="d4744-111">[Hatalı uygulamalar](#faulted-apps) bölümünden ayrıntılara bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4744-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="d4744-112">B2C ayarlarına gidin</span><span class="sxs-lookup"><span data-stu-id="d4744-112">Navigate to B2C settings</span></span>

<span data-ttu-id="d4744-113">[Azure portalında](https://portal.azure.com/) B2C kiracısının Genel Yöneticisi olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d4744-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="d4744-114">Sonraki adımları kaydettirmekte olduğunuz uygulama türüne göre seçin:</span><span class="sxs-lookup"><span data-stu-id="d4744-114">Choose next steps based on the application type you are registering:</span></span>
