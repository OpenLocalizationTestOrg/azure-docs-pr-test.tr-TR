---
title: "Uzantılar uygulama - Azure AD B2C | Microsoft Docs"
description: "B2c uzantıları uygulama geri yükleme"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: 17500b572a0e92c1c233c6967840a5b6d96e21cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="b3cf6-103">Azure AD B2C: Uzantıları uygulaması</span><span class="sxs-lookup"><span data-stu-id="b3cf6-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="b3cf6-104">Azure AD B2C dizini oluşturulduğunda, bir uygulama olarak adlandırılan `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` yeni dizini içinde otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span></span> <span data-ttu-id="b3cf6-105">Bu uygulamayı denir **b2c uzantıları uygulaması**, görünür olan *uygulama kayıtlar*.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="b3cf6-106">Azure AD B2C hizmeti tarafından kullanıcılar ve özel öznitelikler hakkında bilgi depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span></span> <span data-ttu-id="b3cf6-107">Uygulama silinirse, Azure AD B2C düzgün çalışmaz ve üretim ortamınıza etkilenecek.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3cf6-108">Kiracı hemen silinecek planlama sürece b2c uzantıları uygulama silmeyin.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span></span> <span data-ttu-id="b3cf6-109">Uygulama 30 günden fazla bir süre için silinen kalırsa, kullanıcı bilgilerini kalıcı olarak kaybolur.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-the-extensions-app-is-present"></a><span data-ttu-id="b3cf6-110">Uzantılar uygulama mevcut olduğunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="b3cf6-110">Verifying that the extensions app is present</span></span>

<span data-ttu-id="b3cf6-111">B2c uzantıları uygulama mevcut olduğunu doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="b3cf6-111">To verify that the b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="b3cf6-112">Azure AD B2C kiracınızın içinde tıklayın **daha fazla hizmet** sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-112">Inside your Azure AD B2C tenant, click on **More services** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="b3cf6-113">Aramak ve açmak **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="b3cf6-114">İle başlayan uygulama Ara **b2c uzantıları uygulaması**</span><span class="sxs-lookup"><span data-stu-id="b3cf6-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-the-extensions-app"></a><span data-ttu-id="b3cf6-115">Uzantılar uygulama Kurtar</span><span class="sxs-lookup"><span data-stu-id="b3cf6-115">Recover the extensions app</span></span>

<span data-ttu-id="b3cf6-116">B2c uzantıları uygulama yanlışlıkla sildiyseniz, kurtarma için 30 gün sahip.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span></span> <span data-ttu-id="b3cf6-117">Grafik API'sini kullanarak uygulamayı geri yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b3cf6-117">You can restore the app using the Graph API:</span></span>

1. <span data-ttu-id="b3cf6-118">Gözat [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="b3cf6-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="b3cf6-119">Siteye silinen uygulama için geri yüklemek istediğiniz Azure AD B2C dizini için genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span></span>
1. <span data-ttu-id="b3cf6-120">Bir HTTP GET URL karşı sorun `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api-version ile 1.6 =.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-120">Issue an HTTP GET against the URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="b3cf6-121">Değiştirdiğinizden emin olun `{tenantName}` Kiracı adınız ile.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-121">Make sure to replace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="b3cf6-122">Bu işlem tüm son 30 gün içinde silinmiş uygulamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-122">This operation will list all of the applications that have been deleted within the past 30 days.</span></span>
1. <span data-ttu-id="b3cf6-123">'B2c uzantısı uygulama' ve kopyalama ile adı başladığı listesinde uygulamayı bulmak, `objectid` özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="b3cf6-124">Bir HTTP POST URL karşı sorun `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="b3cf6-125">Değiştir `{OBJECTID}` URL ile kısmı `objectid` önceki adımdan.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span></span> 

<span data-ttu-id="b3cf6-126">Şimdi yapabilir olmalıdır [geri yüklenen uygulama görmek](#verifying-that-the-extensions-app-is-present) Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b3cf6-127">Son 30 gün içinde sildiyseniz uygulamanın yalnızca geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-127">An application can only be restored if it has been deleted within the last 30 days.</span></span> <span data-ttu-id="b3cf6-128">30 günden fazla olması durumunda, verileri kalıcı olarak kaybolur.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="b3cf6-129">Daha fazla yardım için destek bileti dosya.</span><span class="sxs-lookup"><span data-stu-id="b3cf6-129">For more assistance, file a support ticket.</span></span>