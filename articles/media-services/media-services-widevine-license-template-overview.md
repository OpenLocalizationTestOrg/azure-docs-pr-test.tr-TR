---
title: "aaaWidevine lisans şablonu genel bakış | Microsoft Docs"
description: "Bu konuda tooconfigure Widevine lisansları kullanılan Widevine lisans şablonu genel bir bakış sağlar."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="c233c-103">Widevine lisans şablonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="c233c-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="c233c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c233c-104">Overview</span></span>
<span data-ttu-id="c233c-105">Azure Media Services şimdi tooconfigure ve istek Widevine lisansları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c233c-105">Azure Media Services now enables you tooconfigure and request Widevine licenses.</span></span> <span data-ttu-id="c233c-106">Merhaba son kullanıcı player tooplay çalıştığında, korumalı Widevine, bir istek gönderilen toohello lisans teslimat hizmeti tooobtain lisans içeriktir.</span><span class="sxs-lookup"><span data-stu-id="c233c-106">When hello end user player tries tooplay your Widevine protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="c233c-107">Merhaba lisans hizmeti hello isteği onaylarsa, gönderilen toohello istemcisi olan hello lisans verir ve olması kullanılan toodecrypt ve play hello belirtilen içerik.</span><span class="sxs-lookup"><span data-stu-id="c233c-107">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="c233c-108">Widevine lisans isteği bir JSON iletisi olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c233c-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="c233c-109">Hiçbir değer yalnızca "{}" boş bir iletiyle toocreate seçebilirsiniz ve bir lisans şablonu ile tüm varsayılanları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c233c-109">You can choose toocreate an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="c233c-110">Çoğu durumda Hello varsayılan çalışır.</span><span class="sxs-lookup"><span data-stu-id="c233c-110">hello default works for most cases.</span></span> <span data-ttu-id="c233c-111">Örneğin, temel MS lisans teslimat senaryoları için her zaman varsayılan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c233c-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="c233c-112">Tooset hello "Sağlayıcı" ve "content_id" değerlerini gerekiyorsa bir sağlayıcı Google Widevine kimlik bilgileriyle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="c233c-112">If you do need tooset hello "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="c233c-113">JSON iletisi</span><span class="sxs-lookup"><span data-stu-id="c233c-113">JSON message</span></span>
| <span data-ttu-id="c233c-114">Ad</span><span class="sxs-lookup"><span data-stu-id="c233c-114">Name</span></span> | <span data-ttu-id="c233c-115">Değer</span><span class="sxs-lookup"><span data-stu-id="c233c-115">Value</span></span> | <span data-ttu-id="c233c-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c233c-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c233c-117">Yükü</span><span class="sxs-lookup"><span data-stu-id="c233c-117">payload</span></span> |<span data-ttu-id="c233c-118">Base64 kodlu dize</span><span class="sxs-lookup"><span data-stu-id="c233c-118">Base64 encoded string</span></span> |<span data-ttu-id="c233c-119">bir istemci tarafından gönderilen hello lisans isteği.</span><span class="sxs-lookup"><span data-stu-id="c233c-119">hello license request sent by a client.</span></span> |
| <span data-ttu-id="c233c-120">content_id</span><span class="sxs-lookup"><span data-stu-id="c233c-120">content_id</span></span> |<span data-ttu-id="c233c-121">Base64 kodlu dize</span><span class="sxs-lookup"><span data-stu-id="c233c-121">Base64 encoded string</span></span> |<span data-ttu-id="c233c-122">Tanımlayıcı için her content_key_specs.track_type tooderive KeyId(s) ve içerik anahtarlar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-122">Identifier used tooderive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="c233c-123">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="c233c-123">provider</span></span> |<span data-ttu-id="c233c-124">Dize</span><span class="sxs-lookup"><span data-stu-id="c233c-124">string</span></span> |<span data-ttu-id="c233c-125">Kullanılan toolook içerik anahtarları ve ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="c233c-125">Used toolook up content keys and policies.</span></span> <span data-ttu-id="c233c-126">MS anahtar teslim Widevine lisans teslim için kullanılırsa, bu parametre yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="c233c-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="c233c-127">policy_name</span></span> |<span data-ttu-id="c233c-128">Dize</span><span class="sxs-lookup"><span data-stu-id="c233c-128">string</span></span> |<span data-ttu-id="c233c-129">Daha önce kaydedilmiş bir ilke adı.</span><span class="sxs-lookup"><span data-stu-id="c233c-129">Name of a previously registered policy.</span></span> <span data-ttu-id="c233c-130">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c233c-130">Optional</span></span> |
| <span data-ttu-id="c233c-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="c233c-131">allowed_track_types</span></span> |<span data-ttu-id="c233c-132">Enum</span><span class="sxs-lookup"><span data-stu-id="c233c-132">enum</span></span> |<span data-ttu-id="c233c-133">SD_ONLY veya SD_HD.</span><span class="sxs-lookup"><span data-stu-id="c233c-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="c233c-134">Bir lisans anahtarları içerik denetimleri eklenmelidir</span><span class="sxs-lookup"><span data-stu-id="c233c-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="c233c-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="c233c-135">content_key_specs</span></span> |<span data-ttu-id="c233c-136">dizi JSON yapısını bkz **içerik anahtarı belirtimlerin** aşağıda</span><span class="sxs-lookup"><span data-stu-id="c233c-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="c233c-137">Hangi içerik tooreturn anahtarları hakkında daha ayrıntılı denetim.</span><span class="sxs-lookup"><span data-stu-id="c233c-137">A finer grained control on what content keys tooreturn.</span></span> <span data-ttu-id="c233c-138">İçerik anahtarı Spec aşağıda ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="c233c-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="c233c-139">Allowed_track_types ve content_key_specs yalnızca biri belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="c233c-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="c233c-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="c233c-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="c233c-141">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="c233c-141">boolean.</span></span> <span data-ttu-id="c233c-142">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-142">true or false</span></span> |<span data-ttu-id="c233c-143">Policy_overrides tarafından belirtilen ilke öznitelikler kullanın ve tüm daha önce depolanan ilke atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c233c-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="c233c-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="c233c-144">policy_overrides</span></span> |<span data-ttu-id="c233c-145">JSON yapısındaki bkz **ilkesini geçersiz kılar** aşağıda</span><span class="sxs-lookup"><span data-stu-id="c233c-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="c233c-146">Bu lisans için ilke ayarları.</span><span class="sxs-lookup"><span data-stu-id="c233c-146">Policy settings for this license.</span></span>  <span data-ttu-id="c233c-147">Hello olayda bu varlık önceden tanımlanmış bir ilke sahip, bu belirtilen değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-147">In hello event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="c233c-148">session_init</span><span class="sxs-lookup"><span data-stu-id="c233c-148">session_init</span></span> |<span data-ttu-id="c233c-149">JSON yapısındaki bkz **oturum başlatma** aşağıda</span><span class="sxs-lookup"><span data-stu-id="c233c-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="c233c-150">İsteğe bağlı verileri toolicense geçirildi.</span><span class="sxs-lookup"><span data-stu-id="c233c-150">Optional data passed toolicense.</span></span> |
| <span data-ttu-id="c233c-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="c233c-151">parse_only</span></span> |<span data-ttu-id="c233c-152">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="c233c-152">boolean.</span></span> <span data-ttu-id="c233c-153">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-153">true or false</span></span> |<span data-ttu-id="c233c-154">Merhaba lisans isteği ayrıştırılır, ancak hiçbir lisans verilir.</span><span class="sxs-lookup"><span data-stu-id="c233c-154">hello license request is parsed but no license is issued.</span></span> <span data-ttu-id="c233c-155">Ancak, değerleri form hello lisans isteği hello yanıt olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c233c-155">However, values form hello license request are returned in hello response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="c233c-156">İçerik anahtarı özellikleri</span><span class="sxs-lookup"><span data-stu-id="c233c-156">Content Key Specs</span></span>
<span data-ttu-id="c233c-157">Önceden var olan bir ilke yoksa, hello hiçbirini değerleri hello içerik anahtarı Spec hiçbir gerek toospecify yoktur.  Bu içerikle ilişkili hello önceden varolan ilke kullanılan toodetermine hello çıkış koruma HDCP ve CGMS gibi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c233c-157">If a pre-existing policy exist, there is no need toospecify any of hello values in hello Content Key Spec.  hello pre-existing policy associated with this content will be used toodetermine hello output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="c233c-158">Önceden var olan bir ilke hello Widevine lisans sunucusu ile kayıtlı değilse, hello içerik sağlayıcı hello lisans isteği hello değerleri ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c233c-158">If a pre-existing policy is not registered with hello Widevine License Server, hello content provider can inject hello values into hello license request.</span></span>   

<span data-ttu-id="c233c-159">Her content_key_specs hello seçeneği use_policy_overrides_exclusively bağımsız olarak tüm parçaları için belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c233c-159">Each content_key_specs must be specified for all tracks, regardless of hello option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="c233c-160">Ad</span><span class="sxs-lookup"><span data-stu-id="c233c-160">Name</span></span> | <span data-ttu-id="c233c-161">Değer</span><span class="sxs-lookup"><span data-stu-id="c233c-161">Value</span></span> | <span data-ttu-id="c233c-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c233c-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c233c-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="c233c-163">content_key_specs.</span></span> <span data-ttu-id="c233c-164">track_type</span><span class="sxs-lookup"><span data-stu-id="c233c-164">track_type</span></span> |<span data-ttu-id="c233c-165">Dize</span><span class="sxs-lookup"><span data-stu-id="c233c-165">string</span></span> |<span data-ttu-id="c233c-166">Bir izleme türü adı.</span><span class="sxs-lookup"><span data-stu-id="c233c-166">A track type name.</span></span> <span data-ttu-id="c233c-167">Content_key_specs hello lisans istekte belirtilmişse, tüm izleyen emin toospecify türleri açıkça olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c233c-167">If content_key_specs is specified in hello license request, make sure toospecify all track types explicitly.</span></span> <span data-ttu-id="c233c-168">Hata toodo hatası tooplayback son 10 saniye kadar neden olur.</span><span class="sxs-lookup"><span data-stu-id="c233c-168">Failure toodo so will result in failure tooplayback past 10 seconds.</span></span> |
| <span data-ttu-id="c233c-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="c233c-169">content_key_specs</span></span>  <br/> <span data-ttu-id="c233c-170">security_level</span><span class="sxs-lookup"><span data-stu-id="c233c-170">security_level</span></span> |<span data-ttu-id="c233c-171">uint32</span><span class="sxs-lookup"><span data-stu-id="c233c-171">uint32</span></span> |<span data-ttu-id="c233c-172">Kayıttan yürütme için istemci sağlamlık gereksinimlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c233c-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="c233c-173">1 - yazılım tabanlı whitebox crypto gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c233c-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="c233c-174">2 - yazılım şifreleme ve karıştırılmış bir kod çözücü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c233c-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="c233c-175">3 - bir donanım yedeklenmiş güvenilir yürütme ortamında hello anahtar malzeme ve şifreleme işlemlerinin gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c233c-175">3 - hello key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="c233c-176">4 - hello şifreleme ve kod çözme içeriğinin bir donanım yedeklenmiş güvenilir yürütme ortamında gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c233c-176">4 - hello crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="c233c-177">5 - hello şifre, kod çözme ve tüm işleme (sıkıştırılmış ve sıkıştırılmamış) hello ortamının bir donanım yedeklenmiş güvenilir yürütme ortamında ele alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c233c-177">5 - hello crypto, decoding and all handling of hello media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="c233c-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="c233c-178">content_key_specs</span></span> <br/> <span data-ttu-id="c233c-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="c233c-179">required_output_protection.hdc</span></span> |<span data-ttu-id="c233c-180">dize - şunlardan biri: HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="c233c-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="c233c-181">HDCP gerekip gerekmediğini belirtir</span><span class="sxs-lookup"><span data-stu-id="c233c-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="c233c-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="c233c-182">content_key_specs</span></span> <br/><span data-ttu-id="c233c-183">anahtar</span><span class="sxs-lookup"><span data-stu-id="c233c-183">key</span></span> |<span data-ttu-id="c233c-184">Base64</span><span class="sxs-lookup"><span data-stu-id="c233c-184">Base64</span></span> <br/><span data-ttu-id="c233c-185">kodlu bir dize</span><span class="sxs-lookup"><span data-stu-id="c233c-185">encoded string</span></span> |<span data-ttu-id="c233c-186">Bu izleme için içerik anahtar toouse. Belirtilmişse, track_type hello veya key_id gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c233c-186">Content key toouse for this track. If specified, hello track_type or key_id is required.</span></span>  <span data-ttu-id="c233c-187">Bu seçenek tooinject hello içerik anahtarı oluşturun veya bir anahtarı aramak Widevine lisans sunucusu izin vererek yerine bu izleme için hello içerik sağlayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c233c-187">This option allows hello content provider tooinject hello content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="c233c-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="c233c-188">content_key_specs.key_id</span></span> |<span data-ttu-id="c233c-189">Base64 ile kodlanmış ikili, dizesi 16 bayt</span><span class="sxs-lookup"><span data-stu-id="c233c-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="c233c-190">Merhaba anahtar için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="c233c-190">Unique identifier for hello key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="c233c-191">İlkeyi geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="c233c-191">Policy Overrides</span></span>
| <span data-ttu-id="c233c-192">Ad</span><span class="sxs-lookup"><span data-stu-id="c233c-192">Name</span></span> | <span data-ttu-id="c233c-193">Değer</span><span class="sxs-lookup"><span data-stu-id="c233c-193">Value</span></span> | <span data-ttu-id="c233c-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c233c-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c233c-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-195">policy_overrides.</span></span> <span data-ttu-id="c233c-196">can_play</span><span class="sxs-lookup"><span data-stu-id="c233c-196">can_play</span></span> |<span data-ttu-id="c233c-197">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="c233c-197">boolean.</span></span> <span data-ttu-id="c233c-198">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-198">true or false</span></span> |<span data-ttu-id="c233c-199">Bu kayıttan yürütme gösterir Merhaba içerik izin verilir.</span><span class="sxs-lookup"><span data-stu-id="c233c-199">Indicates that playback of hello content is allowed.</span></span> <span data-ttu-id="c233c-200">Varsayılan false olur.</span><span class="sxs-lookup"><span data-stu-id="c233c-200">Default is false.</span></span> |
| <span data-ttu-id="c233c-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-201">policy_overrides.</span></span> <span data-ttu-id="c233c-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="c233c-202">can_persist</span></span> |<span data-ttu-id="c233c-203">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="c233c-203">boolean.</span></span> <span data-ttu-id="c233c-204">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-204">true or false</span></span> |<span data-ttu-id="c233c-205">Çevrimdışı kullanım için kalıcı toonon geçici depolama hello lisans olabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-205">Indicates that hello license may be persisted toonon-volatile storage for offline use.</span></span> <span data-ttu-id="c233c-206">Varsayılan false olur.</span><span class="sxs-lookup"><span data-stu-id="c233c-206">Default is false.</span></span> |
| <span data-ttu-id="c233c-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-207">policy_overrides.</span></span> <span data-ttu-id="c233c-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="c233c-208">can_renew</span></span> |<span data-ttu-id="c233c-209">Boolean true veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-209">boolean true or false</span></span> |<span data-ttu-id="c233c-210">Bu lisans yenilenmesini izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="c233c-211">TRUE ise, hello lisans hello süresi sinyal tarafından genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="c233c-211">If true, hello duration of hello license can be extended by heartbeat.</span></span> <span data-ttu-id="c233c-212">Varsayılan false olur.</span><span class="sxs-lookup"><span data-stu-id="c233c-212">Default is false.</span></span> |
| <span data-ttu-id="c233c-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-213">policy_overrides.</span></span> <span data-ttu-id="c233c-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-214">license_duration_seconds</span></span> |<span data-ttu-id="c233c-215">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-215">int64</span></span> |<span data-ttu-id="c233c-216">Bu özel lisans için Hello zaman penceresi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-216">Indicates hello time window for this specific license.</span></span> <span data-ttu-id="c233c-217">0 değeri hiçbir sınırı toohello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-217">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="c233c-218">Varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="c233c-218">Default is 0.</span></span> |
| <span data-ttu-id="c233c-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-219">policy_overrides.</span></span> <span data-ttu-id="c233c-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-220">rental_duration_seconds</span></span> |<span data-ttu-id="c233c-221">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-221">int64</span></span> |<span data-ttu-id="c233c-222">Kayıttan yürütme izin sırada hello zaman penceresi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-222">Indicates hello time window while playback is permitted.</span></span> <span data-ttu-id="c233c-223">0 değeri hiçbir sınırı toohello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-223">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="c233c-224">Varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="c233c-224">Default is 0.</span></span> |
| <span data-ttu-id="c233c-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-225">policy_overrides.</span></span> <span data-ttu-id="c233c-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-226">playback_duration_seconds</span></span> |<span data-ttu-id="c233c-227">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-227">int64</span></span> |<span data-ttu-id="c233c-228">Merhaba hello lisans süre içinde kayıttan yürütme başladıktan sonra zaman penceresini görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="c233c-228">hello viewing window of time once playback starts within hello license duration.</span></span> <span data-ttu-id="c233c-229">0 değeri hiçbir sınırı toohello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-229">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="c233c-230">Varsayılan 0'dır.</span><span class="sxs-lookup"><span data-stu-id="c233c-230">Default is 0.</span></span> |
| <span data-ttu-id="c233c-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-231">policy_overrides.</span></span> <span data-ttu-id="c233c-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="c233c-232">renewal_server_url</span></span> |<span data-ttu-id="c233c-233">Dize</span><span class="sxs-lookup"><span data-stu-id="c233c-233">string</span></span> |<span data-ttu-id="c233c-234">Bu lisans tüm sinyal (yenileme) istekleri toohello URL belirtilen yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="c233c-234">All heartbeat (renewal) requests for this license shall be directed toohello specified URL.</span></span> <span data-ttu-id="c233c-235">Bu alan yalnızca can_renew doğru olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="c233c-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-236">policy_overrides.</span></span> <span data-ttu-id="c233c-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-237">renewal_delay_seconds</span></span> |<span data-ttu-id="c233c-238">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-238">int64</span></span> |<span data-ttu-id="c233c-239">Kaç saniye yenileme ilk denenmeden önce license_start_time sonra.</span><span class="sxs-lookup"><span data-stu-id="c233c-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="c233c-240">Bu alan yalnızca can_renew doğru olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="c233c-241">Varsayılan 0'dır</span><span class="sxs-lookup"><span data-stu-id="c233c-241">Default is 0</span></span> |
| <span data-ttu-id="c233c-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-242">policy_overrides.</span></span> <span data-ttu-id="c233c-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="c233c-244">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-244">int64</span></span> |<span data-ttu-id="c233c-245">Merhaba gecikme hatası durumunda sonraki Lisans yenileme istekleri arasındaki saniye cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="c233c-245">Specifies hello delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="c233c-246">Bu alan yalnızca can_renew doğru olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="c233c-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-247">policy_overrides.</span></span> <span data-ttu-id="c233c-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="c233c-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="c233c-249">Int64</span><span class="sxs-lookup"><span data-stu-id="c233c-249">int64</span></span> |<span data-ttu-id="c233c-250">kayıttan yürütme yenileme sırasında toocontinue izin süreyi Hello pencere girişimi, henüz hello lisans sunucusu toobackend sorunları nedeniyle başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c233c-250">hello window of time, in which playback is allowed toocontinue while renewal is attempted, yet unsuccessful due toobackend problems with hello license server.</span></span> <span data-ttu-id="c233c-251">0 değeri hiçbir sınırı toohello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-251">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="c233c-252">Bu alan yalnızca can_renew doğru olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="c233c-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="c233c-253">policy_overrides.</span></span> <span data-ttu-id="c233c-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="c233c-254">renew_with_usage</span></span> |<span data-ttu-id="c233c-255">Boolean true veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-255">boolean true or false</span></span> |<span data-ttu-id="c233c-256">Kullanım başlatıldığında hello Lisans yenileme için gönderilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="c233c-256">Indicates that hello license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="c233c-257">Bu alan yalnızca can_renew doğru olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="c233c-258">Oturum başlatma</span><span class="sxs-lookup"><span data-stu-id="c233c-258">Session Initialization</span></span>
| <span data-ttu-id="c233c-259">Ad</span><span class="sxs-lookup"><span data-stu-id="c233c-259">Name</span></span> | <span data-ttu-id="c233c-260">Değer</span><span class="sxs-lookup"><span data-stu-id="c233c-260">Value</span></span> | <span data-ttu-id="c233c-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c233c-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c233c-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="c233c-262">provider_session_token</span></span> |<span data-ttu-id="c233c-263">Base64 kodlu dize</span><span class="sxs-lookup"><span data-stu-id="c233c-263">Base64 encoded string</span></span> |<span data-ttu-id="c233c-264">Bu oturum belirteci geri hello lisans geçirilir ve sonraki yenileme içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="c233c-264">This session token is passed back in hello license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="c233c-265">Merhaba Oturum belirteci oturumları kalıcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="c233c-265">hello session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="c233c-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="c233c-266">provider_client_token</span></span> |<span data-ttu-id="c233c-267">Base64 kodlu dize</span><span class="sxs-lookup"><span data-stu-id="c233c-267">Base64 encoded string</span></span> |<span data-ttu-id="c233c-268">İstemci belirteci toosend hello lisans yanıt olarak yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="c233c-268">Client token toosend back in hello license response.</span></span>  <span data-ttu-id="c233c-269">Merhaba lisans isteği istemci belirteci içeriyorsa, bu değer yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="c233c-269">If hello license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="c233c-270">Merhaba istemci belirteci lisans oturumları korunur.</span><span class="sxs-lookup"><span data-stu-id="c233c-270">hello client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="c233c-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="c233c-271">override_provider_client_token</span></span> |<span data-ttu-id="c233c-272">Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="c233c-272">boolean.</span></span> <span data-ttu-id="c233c-273">TRUE veya false</span><span class="sxs-lookup"><span data-stu-id="c233c-273">true or false</span></span> |<span data-ttu-id="c233c-274">Bir istemci belirteci false ve hello lisans isteği içeriyorsa, istemci belirteci bu yapısında belirtilmiş olsa bile hello istek hello belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="c233c-274">If false and hello license request contains a client token, use hello token from hello request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="c233c-275">TRUE ise, her zaman bu yapısı içinde belirtilen hello belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="c233c-275">If true, always use hello token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="c233c-276">.NET türlerini kullanarak, Widevine lisansları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c233c-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="c233c-277">Media Services .NET Widevine lisansları yapılandırmanıza olanak tanıyan API'ları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c233c-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a><span data-ttu-id="c233c-278">Merhaba Media Services .NET SDK'sı tanımlanan sınıflar</span><span class="sxs-lookup"><span data-stu-id="c233c-278">Classes as defined in hello Media Services .NET SDK</span></span>
<span data-ttu-id="c233c-279">Merhaba, bu tür hello tanımları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c233c-279">hello following are hello definitions of these types.</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="c233c-280">Örnek</span><span class="sxs-lookup"><span data-stu-id="c233c-280">Example</span></span>
<span data-ttu-id="c233c-281">örnekte gösterildiği nasıl aşağıdaki hello toouse .NET API'lerini tooconfigure basit Widevine lisansı.</span><span class="sxs-lookup"><span data-stu-id="c233c-281">hello following example shows how toouse .NET APIs tooconfigure  a simple Widevine license.</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="c233c-282">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c233c-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c233c-283">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c233c-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c233c-284">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c233c-284">See also</span></span>
[<span data-ttu-id="c233c-285">PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma</span><span class="sxs-lookup"><span data-stu-id="c233c-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

