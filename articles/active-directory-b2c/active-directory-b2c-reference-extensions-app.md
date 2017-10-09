---
title: "Uzantılar uygulama - Azure AD B2C | Microsoft Docs"
description: "Merhaba b2c uzantıları uygulama geri yükleme"
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
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="d5378-103">Azure AD B2C: Uzantıları uygulaması</span><span class="sxs-lookup"><span data-stu-id="d5378-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="d5378-104">Azure AD B2C dizini oluşturulduğunda, bir uygulama olarak adlandırılan `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` hello yeni dizini içinde otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d5378-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="d5378-105">Bu uygulama, başvurulan tooas hello **b2c uzantıları uygulaması**, görünür olan *uygulama kayıtlar*.</span><span class="sxs-lookup"><span data-stu-id="d5378-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="d5378-106">Hello Azure AD B2C hizmet toostore bilgileri kullanıcılar ve özel öznitelikler hakkında tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5378-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="d5378-107">Merhaba uygulama silinirse, Azure AD B2C düzgün çalışmaz ve üretim ortamınıza etkilenecek.</span><span class="sxs-lookup"><span data-stu-id="d5378-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5378-108">Kiracı tooimmediately delete planlama sürece hello b2c uzantıları uygulama silmeyin.</span><span class="sxs-lookup"><span data-stu-id="d5378-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="d5378-109">Merhaba uygulama 30 günden fazla bir süre için silinen kalırsa, kullanıcı bilgilerini kalıcı olarak kaybolur.</span><span class="sxs-lookup"><span data-stu-id="d5378-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="d5378-110">Bu hello uzantıları uygulama varsa doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="d5378-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="d5378-111">b2c uzantıları uygulaması hello tooverify bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d5378-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="d5378-112">Azure AD B2C kiracınızın içinde tıklayın **daha fazla hizmet** hello sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="d5378-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="d5378-113">Aramak ve açmak **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="d5378-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="d5378-114">İle başlayan uygulama Ara **b2c uzantıları uygulaması**</span><span class="sxs-lookup"><span data-stu-id="d5378-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="d5378-115">Merhaba uzantıları uygulama Kurtar</span><span class="sxs-lookup"><span data-stu-id="d5378-115">Recover hello extensions app</span></span>

<span data-ttu-id="d5378-116">Merhaba b2c uzantıları uygulama yanlışlıkla sildiyseniz, 30 gün toorecover sahip.</span><span class="sxs-lookup"><span data-stu-id="d5378-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="d5378-117">Merhaba uygulamasına hello grafik API'sini kullanarak geri yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5378-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="d5378-118">Çok Gözat[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="d5378-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="d5378-119">Toohello sitede toorestore silinmiş hello uygulama için istediğiniz hello Azure AD B2C dizini için genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d5378-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="d5378-120">Bir HTTP GET hello URL karşı sorun `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api-version ile 1.6 =.</span><span class="sxs-lookup"><span data-stu-id="d5378-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="d5378-121">Emin tooreplace olun `{tenantName}` Kiracı adınız ile.</span><span class="sxs-lookup"><span data-stu-id="d5378-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="d5378-122">Bu işlem tüm son 30 gün içinde hello silinmiş hello uygulamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="d5378-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="d5378-123">'B2c uzantısı uygulama' ve kopyalama ile Merhaba adı başladığı hello listesinde Hello uygulamayı bulmak, `objectid` özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="d5378-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="d5378-124">Bir HTTP POST hello URL karşı sorun `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="d5378-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="d5378-125">Hello yerine `{OBJECTID}` hello URL'sinin hello ile `objectid` hello önceki adımdaki.</span><span class="sxs-lookup"><span data-stu-id="d5378-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="d5378-126">Artık çok gerekir[geri hello uygulama görmek](#verifying-that-the-extensions-app-is-present) hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="d5378-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d5378-127">Son 30 gün içinde hello silindiyse, uygulamanın yalnızca geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d5378-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="d5378-128">30 günden fazla olması durumunda, verileri kalıcı olarak kaybolur.</span><span class="sxs-lookup"><span data-stu-id="d5378-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="d5378-129">Daha fazla yardım için destek bileti dosya.</span><span class="sxs-lookup"><span data-stu-id="d5378-129">For more assistance, file a support ticket.</span></span>
