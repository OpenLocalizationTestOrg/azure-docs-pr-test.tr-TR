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
# <a name="widevine-license-template-overview"></a>Widevine lisans şablonu genel bakış
## <a name="overview"></a>Genel Bakış
Azure Media Services şimdi tooconfigure ve istek Widevine lisansları sağlar. Merhaba son kullanıcı player tooplay çalıştığında, korumalı Widevine, bir istek gönderilen toohello lisans teslimat hizmeti tooobtain lisans içeriktir. Merhaba lisans hizmeti hello isteği onaylarsa, gönderilen toohello istemcisi olan hello lisans verir ve olması kullanılan toodecrypt ve play hello belirtilen içerik.

Widevine lisans isteği bir JSON iletisi olarak biçimlendirilir.  

>[!NOTE]
> Hiçbir değer yalnızca "{}" boş bir iletiyle toocreate seçebilirsiniz ve bir lisans şablonu ile tüm varsayılanları oluşturulur. Çoğu durumda Hello varsayılan çalışır. Örneğin, temel MS lisans teslimat senaryoları için her zaman varsayılan olmalıdır. Tooset hello "Sağlayıcı" ve "content_id" değerlerini gerekiyorsa bir sağlayıcı Google Widevine kimlik bilgileriyle eşleşmelidir.

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

## <a name="json-message"></a>JSON iletisi
| Ad | Değer | Açıklama |
| --- | --- | --- |
| Yükü |Base64 kodlu dize |bir istemci tarafından gönderilen hello lisans isteği. |
| content_id |Base64 kodlu dize |Tanımlayıcı için her content_key_specs.track_type tooderive KeyId(s) ve içerik anahtarlar kullanılır. |
| Sağlayıcı |Dize |Kullanılan toolook içerik anahtarları ve ilkeleri. MS anahtar teslim Widevine lisans teslim için kullanılırsa, bu parametre yoksayılır. |
| policy_name |Dize |Daha önce kaydedilmiş bir ilke adı. İsteğe bağlı |
| allowed_track_types |Enum |SD_ONLY veya SD_HD. Bir lisans anahtarları içerik denetimleri eklenmelidir |
| content_key_specs |dizi JSON yapısını bkz **içerik anahtarı belirtimlerin** aşağıda |Hangi içerik tooreturn anahtarları hakkında daha ayrıntılı denetim. İçerik anahtarı Spec aşağıda ayrıntılı bilgi için bkz.  Allowed_track_types ve content_key_specs yalnızca biri belirtilebilir. |
| use_policy_overrides_exclusively |Boole değeri. TRUE veya false |Policy_overrides tarafından belirtilen ilke öznitelikler kullanın ve tüm daha önce depolanan ilke atlayabilirsiniz. |
| policy_overrides |JSON yapısındaki bkz **ilkesini geçersiz kılar** aşağıda |Bu lisans için ilke ayarları.  Hello olayda bu varlık önceden tanımlanmış bir ilke sahip, bu belirtilen değerler kullanılır. |
| session_init |JSON yapısındaki bkz **oturum başlatma** aşağıda |İsteğe bağlı verileri toolicense geçirildi. |
| parse_only |Boole değeri. TRUE veya false |Merhaba lisans isteği ayrıştırılır, ancak hiçbir lisans verilir. Ancak, değerleri form hello lisans isteği hello yanıt olarak döndürülür. |

## <a name="content-key-specs"></a>İçerik anahtarı özellikleri
Önceden var olan bir ilke yoksa, hello hiçbirini değerleri hello içerik anahtarı Spec hiçbir gerek toospecify yoktur.  Bu içerikle ilişkili hello önceden varolan ilke kullanılan toodetermine hello çıkış koruma HDCP ve CGMS gibi olacaktır.  Önceden var olan bir ilke hello Widevine lisans sunucusu ile kayıtlı değilse, hello içerik sağlayıcı hello lisans isteği hello değerleri ekleyemezsiniz.   

Her content_key_specs hello seçeneği use_policy_overrides_exclusively bağımsız olarak tüm parçaları için belirtilmelidir. 

| Ad | Değer | Açıklama |
| --- | --- | --- |
| content_key_specs. track_type |Dize |Bir izleme türü adı. Content_key_specs hello lisans istekte belirtilmişse, tüm izleyen emin toospecify türleri açıkça olmasını sağlayın. Hata toodo hatası tooplayback son 10 saniye kadar neden olur. |
| content_key_specs  <br/> security_level |uint32 |Kayıttan yürütme için istemci sağlamlık gereksinimlerini tanımlar. <br/> 1 - yazılım tabanlı whitebox crypto gereklidir. <br/> 2 - yazılım şifreleme ve karıştırılmış bir kod çözücü gereklidir. <br/> 3 - bir donanım yedeklenmiş güvenilir yürütme ortamında hello anahtar malzeme ve şifreleme işlemlerinin gerçekleştirilmesi gerekir. <br/> 4 - hello şifreleme ve kod çözme içeriğinin bir donanım yedeklenmiş güvenilir yürütme ortamında gerçekleştirilmesi gerekir.  <br/> 5 - hello şifre, kod çözme ve tüm işleme (sıkıştırılmış ve sıkıştırılmamış) hello ortamının bir donanım yedeklenmiş güvenilir yürütme ortamında ele alınması gerekir. |
| content_key_specs <br/> required_output_protection.hdc |dize - şunlardan biri: HDCP_NONE, HDCP_V1, HDCP_V2 |HDCP gerekip gerekmediğini belirtir |
| content_key_specs <br/>anahtar |Base64 <br/>kodlu bir dize |Bu izleme için içerik anahtar toouse. Belirtilmişse, track_type hello veya key_id gereklidir.  Bu seçenek tooinject hello içerik anahtarı oluşturun veya bir anahtarı aramak Widevine lisans sunucusu izin vererek yerine bu izleme için hello içerik sağlayıcı sağlar. |
| content_key_specs.key_id |Base64 ile kodlanmış ikili, dizesi 16 bayt |Merhaba anahtar için benzersiz tanımlayıcı. |

## <a name="policy-overrides"></a>İlkeyi geçersiz kılar
| Ad | Değer | Açıklama |
| --- | --- | --- |
| policy_overrides. can_play |Boole değeri. TRUE veya false |Bu kayıttan yürütme gösterir Merhaba içerik izin verilir. Varsayılan false olur. |
| policy_overrides. can_persist |Boole değeri. TRUE veya false |Çevrimdışı kullanım için kalıcı toonon geçici depolama hello lisans olabilir gösterir. Varsayılan false olur. |
| policy_overrides. can_renew |Boolean true veya false |Bu lisans yenilenmesini izin verildiğini gösterir. TRUE ise, hello lisans hello süresi sinyal tarafından genişletilebilir. Varsayılan false olur. |
| policy_overrides. license_duration_seconds |Int64 |Bu özel lisans için Hello zaman penceresi gösterir. 0 değeri hiçbir sınırı toohello süresini gösterir. Varsayılan 0'dır. |
| policy_overrides. rental_duration_seconds |Int64 |Kayıttan yürütme izin sırada hello zaman penceresi gösterir. 0 değeri hiçbir sınırı toohello süresini gösterir. Varsayılan 0'dır. |
| policy_overrides. playback_duration_seconds |Int64 |Merhaba hello lisans süre içinde kayıttan yürütme başladıktan sonra zaman penceresini görüntüleme. 0 değeri hiçbir sınırı toohello süresini gösterir. Varsayılan 0'dır. |
| policy_overrides. renewal_server_url |Dize |Bu lisans tüm sinyal (yenileme) istekleri toohello URL belirtilen yönlendirilmiş. Bu alan yalnızca can_renew doğru olduğunda kullanılır. |
| policy_overrides. renewal_delay_seconds |Int64 |Kaç saniye yenileme ilk denenmeden önce license_start_time sonra. Bu alan yalnızca can_renew doğru olduğunda kullanılır. Varsayılan 0'dır |
| policy_overrides. renewal_retry_interval_seconds |Int64 |Merhaba gecikme hatası durumunda sonraki Lisans yenileme istekleri arasındaki saniye cinsinden belirtir. Bu alan yalnızca can_renew doğru olduğunda kullanılır. |
| policy_overrides. renewal_recovery_duration_seconds |Int64 |kayıttan yürütme yenileme sırasında toocontinue izin süreyi Hello pencere girişimi, henüz hello lisans sunucusu toobackend sorunları nedeniyle başarısız olur. 0 değeri hiçbir sınırı toohello süresini gösterir. Bu alan yalnızca can_renew doğru olduğunda kullanılır. |
| policy_overrides. renew_with_usage |Boolean true veya false |Kullanım başlatıldığında hello Lisans yenileme için gönderilen gösterir. Bu alan yalnızca can_renew doğru olduğunda kullanılır. |

## <a name="session-initialization"></a>Oturum başlatma
| Ad | Değer | Açıklama |
| --- | --- | --- |
| provider_session_token |Base64 kodlu dize |Bu oturum belirteci geri hello lisans geçirilir ve sonraki yenileme içinde yer alır.  Merhaba Oturum belirteci oturumları kalıcı olmaz. |
| provider_client_token |Base64 kodlu dize |İstemci belirteci toosend hello lisans yanıt olarak yedekleyin.  Merhaba lisans isteği istemci belirteci içeriyorsa, bu değer yoksayılır. Merhaba istemci belirteci lisans oturumları korunur. |
| override_provider_client_token |Boole değeri. TRUE veya false |Bir istemci belirteci false ve hello lisans isteği içeriyorsa, istemci belirteci bu yapısında belirtilmiş olsa bile hello istek hello belirteci kullanın.  TRUE ise, her zaman bu yapısı içinde belirtilen hello belirteci kullanın. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>.NET türlerini kullanarak, Widevine lisansları yapılandırma
Media Services .NET Widevine lisansları yapılandırmanıza olanak tanıyan API'ları sağlar. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Merhaba Media Services .NET SDK'sı tanımlanan sınıflar
Merhaba, bu tür hello tanımları verilmiştir.

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

### <a name="example"></a>Örnek
örnekte gösterildiği nasıl aşağıdaki hello toouse .NET API'lerini tooconfigure basit Widevine lisansı.

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


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca bkz.
[PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma](media-services-protect-with-drm.md)

