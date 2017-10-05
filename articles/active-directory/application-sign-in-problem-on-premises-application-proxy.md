---
title: "Azure AD uygulama proxy'si kullanarak bir şirket içi uygulama oturum açma sorunları | Microsoft Docs"
description: "Azure AD uygulama proxy'si kullanarak Azure AD ile tümleşik bir şirket içi uygulamasında oturum kaldıramadığınızda karşılaştığı yaygın sorunları giderme"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 5687f789355cc9769d26b53e98486bb213c66419
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-on-premises-application-using-the-azure-ad-application-proxy"></a><span data-ttu-id="b1619-103">Azure AD uygulama proxy'si kullanarak bir şirket içi uygulama oturum açma sorunları</span><span class="sxs-lookup"><span data-stu-id="b1619-103">Problems signing in to an on-premises application using the Azure AD application proxy</span></span>

<span data-ttu-id="b1619-104">Bir şirket içi uygulamanızı imzalama sorun yaşıyorsanız, sorunu çözmek için aşağıdaki adımları izleyerek deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1619-104">If you are having problems signing in an on-premises application, you can try following the steps below to resolving your problem.</span></span>

## <a name="i-can-load-my-application-but-something-on-the-page-looks-broken"></a><span data-ttu-id="b1619-105">Uygulamam yük yükleyebilirsiniz, ancak sayfasında bir şey bozuk görünüyor</span><span class="sxs-lookup"><span data-stu-id="b1619-105">I can load my application, but something on the page looks broken</span></span>

<span data-ttu-id="b1619-106">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-106">The following documents can help you to resolve some of the most common issues in this category.</span></span>

  * [<span data-ttu-id="b1619-107">Uygulamama ulaşabiliyorum ama uygulama sayfası doğru görüntülenmiyor</span><span class="sxs-lookup"><span data-stu-id="b1619-107">I can get to my application, but the application page isn't displaying correctly</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-appearance-broken-problem/)
  * [<span data-ttu-id="b1619-108">Uygulamama ulaşabiliyorum ama uygulamanın yüklenmesi fazla uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="b1619-108">I can get to my application, but the application takes too long to load</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-load-speed-problem/)
  * [<span data-ttu-id="b1619-109">Uygulamama ulaşabiliyorum ama uygulama sayfasındaki bağlantılar çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="b1619-109">I can get to my application, but the links on the application page do not work</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-links-broken-problem/)

## <a name="im-having-a-connectivity-problem-my-application"></a><span data-ttu-id="b1619-110">Uygulamam bağlantı sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-110">I'm having a connectivity problem my application</span></span>
  <span data-ttu-id="b1619-111">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-111">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="b1619-112">Uygulamam için hangi bağlantı noktalarını açacağımı bilmiyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-112">I don't know what ports to open for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-ports-how-to/)
  * [<span data-ttu-id="b1619-113">Uygulamam için bağlayıcı grubunda çalışan bağlayıcı olmadığından sorunla karşılaştım</span><span class="sxs-lookup"><span data-stu-id="b1619-113">I encountered a problem because there was no working connector in a connector group for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-no-working-connector/)

## <a name="im-having-a-problem-configuring-the-azure-ad-application-proxy-in-the-admin-portal"></a><span data-ttu-id="b1619-114">Yönetim Portalı'nda Azure AD uygulama proxy'si yapılandırma bir sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-114">I'm having a problem configuring the Azure AD Application Proxy in the admin portal</span></span>
  <span data-ttu-id="b1619-115">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-115">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="b1619-116">Uygulama Proxy’si uygulamasını yapılandırırken zorluk sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-116">I am having difficulty configuring an application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-how-to/)
  * [<span data-ttu-id="b1619-117">Uygulama Proxy’si uygulamamda çoklu oturum açmayı yapılandırmayı bilmiyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-117">I don't know how to configure single sign-on to my application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-sso-how-to/)
  * [<span data-ttu-id="b1619-118">Yönetim portalında uygulamamı oluştururken bir sorunla karşılaştım</span><span class="sxs-lookup"><span data-stu-id="b1619-118">I encountered a problem when creating my application in admin portal</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-problem/)

## <a name="im-having-a-problem-setting-up-back-end-authentication-to-my-application"></a><span data-ttu-id="b1619-119">Uygulamam için arka uç kimlik doğrulaması kurmada sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-119">I'm having a problem setting up back-end authentication to my application</span></span>
  <span data-ttu-id="b1619-120">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-120">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="b1619-121">Kerberos Sınırlı Temsilini yapılandırmayı bilmiyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-121">I don't know how to configure Kerberos Constrained Delegation</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-kerberos-constrained-delegation-how-to/)
  * [<span data-ttu-id="b1619-122">Uygulamamı PingAccess’le nasıl yapılandıracağımı bilmiyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-122">I don't know how to configure my application with PingAccess</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-ping-access-how-to/)

## <a name="im-having-a-problem-when-signing-in-to-my-application"></a><span data-ttu-id="b1619-123">Uygulamam için oturum açarken sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-123">I'm having a problem when signing in to my application</span></span>
  <span data-ttu-id="b1619-124">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-124">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="b1619-125">"Bu Şirket Uygulamasına Erişilemiyor" hatası alıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-125">I get a "Can't Access this Corporate Application" error</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-sign-in-bad-gateway-timeout-error/)

## <a name="im-having-a-problem-with-the-application-proxy-agent-connector"></a><span data-ttu-id="b1619-126">Uygulama Proxy Aracısı Bağlayıcısı ile ilgili bir sorun yaşıyorum</span><span class="sxs-lookup"><span data-stu-id="b1619-126">I'm having a problem with the Application Proxy Agent Connector</span></span>
  <span data-ttu-id="b1619-127">Aşağıdaki belgeler, bu kategoriye giren yaygın sorunların çoğunu çözmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1619-127">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="b1619-128">Uygulama Proxy’si Aracı Bağlayıcısı’nı yüklerken sorun yaşıyorum.</span><span class="sxs-lookup"><span data-stu-id="b1619-128">I am having issues installing the Application Proxy Agent Connector </span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connector-installation-problem/)

## <a name="next-steps"></a><span data-ttu-id="b1619-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1619-129">Next steps</span></span>
[<span data-ttu-id="b1619-130">Şirket içi uygulamalara güvenli uzaktan erişim sağlama</span><span class="sxs-lookup"><span data-stu-id="b1619-130">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
