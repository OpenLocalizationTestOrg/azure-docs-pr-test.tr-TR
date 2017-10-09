---
title: "Azure MFA için aaaAccess ve kullanım raporları | Microsoft Docs"
description: "Bu, nasıl toouse hello Azure çok faktörlü kimlik doğrulama özelliği - raporları açıklar."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="56285-103">Azure multi-Factor Authentication raporlarında</span><span class="sxs-lookup"><span data-stu-id="56285-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="56285-104">Azure çok faktörlü kimlik doğrulaması ve kuruluşunuz tarafından kullanılan çeşitli raporlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="56285-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="56285-105">Bu raporlar hello multi-Factor Authentication Yönetim Portalı erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="56285-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="56285-106">Merhaba, hello kullanılabilir raporlar listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="56285-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="56285-107">Rapor</span><span class="sxs-lookup"><span data-stu-id="56285-107">Report</span></span> | <span data-ttu-id="56285-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56285-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="56285-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="56285-109">Usage</span></span> |<span data-ttu-id="56285-110">Merhaba kullanım raporları bilgileri görüntüler genel kullanımı, kullanıcı özeti ve kullanıcı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="56285-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="56285-111">Sunucu durumu</span><span class="sxs-lookup"><span data-stu-id="56285-111">Server Status</span></span> |<span data-ttu-id="56285-112">Bu rapor, çok faktörlü kimlik doğrulama için hesabınızla ilişkili sunucularını hello durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="56285-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="56285-113">Engellenmiş kullanıcı geçmişi</span><span class="sxs-lookup"><span data-stu-id="56285-113">Blocked User History</span></span> |<span data-ttu-id="56285-114">Bu raporlar istekleri tooblock hello geçmişini göster kullanıcı veya engelini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="56285-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="56285-115">Atlanmış kullanıcı geçmişi</span><span class="sxs-lookup"><span data-stu-id="56285-115">Bypassed User History</span></span> |<span data-ttu-id="56285-116">Bir kullanıcının telefon numarası için çok faktörlü kimlik doğrulama isteklerini toobypass Hello geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="56285-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="56285-117">Sahtekarlık Uyarısı</span><span class="sxs-lookup"><span data-stu-id="56285-117">Fraud Alert</span></span> |<span data-ttu-id="56285-118">Belirttiğiniz hello tarih aralığı içinde gönderilen sahtekarlık uyarısı geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="56285-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="56285-119">Sıraya alınmış</span><span class="sxs-lookup"><span data-stu-id="56285-119">Queued</span></span> |<span data-ttu-id="56285-120">Sıraya alınan işleme ve durumlarını listeler raporları.</span><span class="sxs-lookup"><span data-stu-id="56285-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="56285-121">Merhaba rapor tamamlandığında, bir bağlantı toodownload veya Görünüm hello rapor sağlanır.</span><span class="sxs-lookup"><span data-stu-id="56285-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="56285-122">Raporları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="56285-122">View reports</span></span>
1. <span data-ttu-id="56285-123">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="56285-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="56285-124">Merhaba sol tarafta, Active Directory'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="56285-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="56285-125">Kimlik doğrulama sağlayıcıları kullanmadığınıza bağlı olarak bu iki seçenekten birini izleyin:</span><span class="sxs-lookup"><span data-stu-id="56285-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="56285-126">**Seçenek 1**: Merhaba çok faktörlü kimlik doğrulama sağlayıcıları sekmesini tıklatın. MFA sağlayıcınızı seçin ve hello tıklatın **Yönet** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="56285-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="56285-127">**Seçenek 2**: dizin ve Git toohello seçin **yapılandırma** sekmesi. Merhaba çok faktörlü kimlik doğrulaması bölümü altında seçin **hizmet ayarlarını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="56285-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="56285-128">Merhaba MFA Hizmeti Ayarları sayfası Hello altındaki hello Git toohello portal bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="56285-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="56285-129">Hello Azure multi-Factor Authentication Yönetim Portalı'da, hello hello istediğiniz rapor türünü seçin **bir raporu görüntülemek** sol gezinti hello bölümünde.</span><span class="sxs-lookup"><span data-stu-id="56285-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="56285-130"><center>![Bulut](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="56285-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="56285-131">**Ek Kaynaklar**</span><span class="sxs-lookup"><span data-stu-id="56285-131">**Additional Resources**</span></span>

* [<span data-ttu-id="56285-132">Kullanıcılar için</span><span class="sxs-lookup"><span data-stu-id="56285-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="56285-133">MSDN'deki Azure çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="56285-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
