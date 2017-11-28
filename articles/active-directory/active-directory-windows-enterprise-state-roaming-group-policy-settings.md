---
title: "aaaGroup ilke ve MDM ayarlarını | Microsoft Docs"
description: "Şirkete ait cihazlarda kullanılmalıdır Yönetimi (MDM) ayarları Grup İlkesi ve mobil cihaz hakkında bilgi sağlar. Bu ilkeler, uygulanan toohello kullanıcının tüm aygıt olan."
services: active-directory
keywords: "Grup İlkesi ve kurumsal durumda dolaşım, Kurumsal durumda dolaşım, windows bulut için MDM ayarları nelerdir"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="14430-105">Grup İlkesi ve MDM ayarları</span><span class="sxs-lookup"><span data-stu-id="14430-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="14430-106">Bu ilkeler uygulanan toohello kullanıcının tüm aygıt olduğundan bu Grup İlkesi ve mobil cihaz Yönetimi (MDM) ayarları yalnızca şirkete ait cihazlarda kullanır.</span><span class="sxs-lookup"><span data-stu-id="14430-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied toohello user’s entire device.</span></span> <span data-ttu-id="14430-107">Kişisel bir MDM İlkesi toodisable ayarları eşitleme uygulama, kullanıcının sahip olduğu cihaz bu aygıtın hello kullanımını olumsuz etkiler.</span><span class="sxs-lookup"><span data-stu-id="14430-107">Applying an MDM policy toodisable settings sync for a personal, user-owned device will negatively impact hello use of that device.</span></span> <span data-ttu-id="14430-108">Ayrıca, diğer kullanıcı hesapları hello aygıtta hello İlkesi tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="14430-108">Additionally, other user accounts on hello device will also be affected by hello policy.</span></span>

<span data-ttu-id="14430-109">Kişisel (yönetilmeyen) cihazlar için gezici toomanage kullanmak istediğiniz kuruluşların Azure portal tooenable hello veya Grup İlkesi veya MDM kullanmak yerine gezici devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="14430-109">Enterprises that want toomanage roaming for personal (unmanaged) devices can use hello Azure portal tooenable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="14430-110">tabloları aşağıdaki hello hello İlkesi ayarları açıklanır.</span><span class="sxs-lookup"><span data-stu-id="14430-110">hello following tables describe hello policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="14430-111">MDM ayarları</span><span class="sxs-lookup"><span data-stu-id="14430-111">MDM settings</span></span>
<span data-ttu-id="14430-112">tooboth Windows 10 ve Windows 10 Mobile Hello MDM ilke ayarlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="14430-112">hello MDM policy settings apply tooboth Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="14430-113">Windows 10 Mobile destek kullanıcının OneDrive hesabına gezici dayalı yalnızca Microsoft hesabı yok.</span><span class="sxs-lookup"><span data-stu-id="14430-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="14430-114">Lütfen Azure AD için hangi cihazlar desteklenir ile ilgili ayrıntılar için "Aygıtları ve uç noktaları" bölümü çok temel eşitleniyor.</span><span class="sxs-lookup"><span data-stu-id="14430-114">Please refer too“Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="14430-115">Ad</span><span class="sxs-lookup"><span data-stu-id="14430-115">Name</span></span> | <span data-ttu-id="14430-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14430-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14430-117">Microsoft hesabı bağlantıya izin ver</span><span class="sxs-lookup"><span data-stu-id="14430-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="14430-118">Merhaba cihazda bir Microsoft hesabı kullanarak kullanıcıların tooauthenticate sağlar</span><span class="sxs-lookup"><span data-stu-id="14430-118">Allows users tooauthenticate using a Microsoft account on hello device</span></span> |
| <span data-ttu-id="14430-119">Ayarlarımı eşitlemesine izin ver</span><span class="sxs-lookup"><span data-stu-id="14430-119">Allow Sync My Settings</span></span> |<span data-ttu-id="14430-120">Kullanıcı tooroam Windows ayarları ve uygulama verilerini sağlar; Bu ilkeyi devre dışı bırakma eşitleme yanı sıra, mobil cihazlarda yedeklemelerinin devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="14430-120">Allows users tooroam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="14430-121">Grup İlkesi ayarları</span><span class="sxs-lookup"><span data-stu-id="14430-121">Group Policy settings</span></span>
<span data-ttu-id="14430-122">Active Directory etki alanına katılmış tooan tooWindows 10 aygıtları Hello Grup İlkesi ayarlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="14430-122">hello Group Policy settings apply tooWindows 10 devices that are joined tooan Active Directory domain.</span></span> <span data-ttu-id="14430-123">Merhaba Tablo ayrıca 'hello açıklamasında kullanmayın ile' belirtilmiştir toomanage eşitleme ayarları görünür, ancak kuruluş durumu Dolaşım için Windows 10 için çalışmaz eski ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="14430-123">hello table also includes legacy settings that would appear toomanage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in hello description.</span></span>

| <span data-ttu-id="14430-124">Ad</span><span class="sxs-lookup"><span data-stu-id="14430-124">Name</span></span> | <span data-ttu-id="14430-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="14430-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14430-126">Hesaplar: Blok Microsoft hesapları</span><span class="sxs-lookup"><span data-stu-id="14430-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="14430-127">Bu ilke ayarı, kullanıcıların bu bilgisayarda yeni Microsoft hesapları eklemesini engeller</span><span class="sxs-lookup"><span data-stu-id="14430-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="14430-128">Eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-128">Do not sync</span></span> |<span data-ttu-id="14430-129">Kullanıcı tooroam Windows ayarları ve uygulama verilerini engeller</span><span class="sxs-lookup"><span data-stu-id="14430-129">Prevents users tooroam Windows settings and app data</span></span> |
| <span data-ttu-id="14430-130">Eşitleme kişiselleştirme</span><span class="sxs-lookup"><span data-stu-id="14430-130">Do not sync personalize</span></span> |<span data-ttu-id="14430-131">Devre dışı bırakır hello Temalar grubunun eşitleniyor</span><span class="sxs-lookup"><span data-stu-id="14430-131">Disables syncing of hello Themes group</span></span> |
| <span data-ttu-id="14430-132">Tarayıcı ayarlarını eşitlemesini değil</span><span class="sxs-lookup"><span data-stu-id="14430-132">Do not sync browser settings</span></span> |<span data-ttu-id="14430-133">Devre dışı bırakır hello Internet Explorer grubunun eşitleniyor</span><span class="sxs-lookup"><span data-stu-id="14430-133">Disables syncing of hello Internet Explorer group</span></span> |
| <span data-ttu-id="14430-134">Parola Eşitleme yok</span><span class="sxs-lookup"><span data-stu-id="14430-134">Do not sync passwords</span></span> |<span data-ttu-id="14430-135">Parolaları grubu devre dışı bırakır eşitleniyor</span><span class="sxs-lookup"><span data-stu-id="14430-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="14430-136">Diğer Windows ayarları eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="14430-137">Diğer Windows Ayarları grubu devre dışı bırakır eşitleniyor</span><span class="sxs-lookup"><span data-stu-id="14430-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="14430-138">Masaüstü kişiselleştirme eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="14430-139">Kullanmayın; hiçbir etkisi yoktur</span><span class="sxs-lookup"><span data-stu-id="14430-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="14430-140">Ölçülen bağlantılarında eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-140">Do not sync on metered connections</span></span> |<span data-ttu-id="14430-141">Dolaşım devre dışı bırakır tarifeli cep telefonu 3 G gibi bağlantısı</span><span class="sxs-lookup"><span data-stu-id="14430-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="14430-142">Uygulamaları eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-142">Do not sync apps</span></span> |<span data-ttu-id="14430-143">Kullanmayın; hiçbir etkisi yoktur</span><span class="sxs-lookup"><span data-stu-id="14430-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="14430-144">Uygulama ayarları eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-144">Do not sync app settings</span></span> |<span data-ttu-id="14430-145">Devre dışı bırakır uygulama verileri dolaşımı</span><span class="sxs-lookup"><span data-stu-id="14430-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="14430-146">Başlangıç ayarları eşitleme değil</span><span class="sxs-lookup"><span data-stu-id="14430-146">Do not sync start settings</span></span> |<span data-ttu-id="14430-147">Kullanmayın; hiçbir etkisi yoktur</span><span class="sxs-lookup"><span data-stu-id="14430-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="14430-148">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="14430-148">Related topics</span></span>
* [<span data-ttu-id="14430-149">Kurumsal durumda Dolaşım genel bakış</span><span class="sxs-lookup"><span data-stu-id="14430-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="14430-150">Azure Active Directory'de gezici Kurumsal durumunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="14430-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="14430-151">Ayarlar ve veri dolaşımı SSS</span><span class="sxs-lookup"><span data-stu-id="14430-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="14430-152">Windows 10 Dolaşım ayarları başvurusu</span><span class="sxs-lookup"><span data-stu-id="14430-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="14430-153">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="14430-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

