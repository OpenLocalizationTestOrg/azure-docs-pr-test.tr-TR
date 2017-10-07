---
title: "aaaAzure Media Services çıkış meta veri şema | Microsoft Docs"
description: "Merhaba konu Azure Media Services çıkış meta veri şema genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a>Meta verileri çıktı
## <a name="overview"></a>Genel Bakış
Kodlama işinin bir giriş varlık (veya varlıklar) ile ilişkili istediğiniz tooperform kodlama bazı görevler. Örneğin, bir MP4 dosyası tooH.264 MP4 bit hızı Uyarlamalı kodlamak ayarlar; küçük resim oluşturma; yer paylaşımları oluşturun. Bir görev tamamlandığında, çıkış varlık oluşturulur.  Merhaba çıkış varlık içeriyor video, ses, küçük resimleri, vb. hello çıkış varlığına hello çıkış varlık hakkındaki meta verileri dosyasıyla de içerir. Merhaba hello meta veri XML dosyası adına sahip biçimini izleyen hello: &lt;source_file_name&gt;_manifest.xml (örneğin, BigBuckBunny_manifest.xml).  

Tooexamine hello meta veri dosyası istiyorsanız, oluşturabileceğiniz bir **SAS** Bulucu ve indirme hello dosya tooyour yerel bilgisayar.  

Bu konuda hangi hello çıktı metada ele alınmıştır, hello öğeleri ve hello XML Şeması türleri (&lt;source_file_name&gt;_manifest.xml) dayanır. Merhaba giriş varlık hakkında meta veriler içeren hello dosyası hakkında daha fazla bilgi için bkz: [giriş meta verileri](media-services-input-metadata-schema.md).  

> [!NOTE]
> Merhaba tam şeması kod ve bu konuda hello sonunda XML örneği bulabilirsiniz.  
>
>

## <a name="AssetFiles "></a>AssetFiles kök öğesi
Merhaba kodlama işinin AssetFile girişlerinde koleksiyonu.  

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **AssetFile**<br/><br/> minOccurs = "0" maxOccurs = "1" |Bir [AssetFile öğesi](media-services-output-metadata-schema.md) parçası olan hello AssetFiles koleksiyonu. |

## <a name="AssetFile "></a>AssetFile öğesi
Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Öznitelikler
| Ad | Tür | Açıklama |
| --- | --- | --- |
| **Ad**<br/><br/> Gerekli |**xs: String** |Merhaba medya varlık dosya adı. |
| **Boyut**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:Long** |Merhaba varlık dosyasının bayt cinsinden boyutu. |
| **Süre**<br/><br/> Gerekli |**xs: Duration** |İçerik play geri süresi. |

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **Kaynakları** |İşlenmiş giriş/kaynak medya dosyaları koleksiyonu içinde bu AssetFile tooproduce sipariş. Daha fazla bilgi için bkz: [Source öğesi](media-services-output-metadata-schema.md). |
| **VideoTracks**<br/><br/> minOccurs = "0" maxOccurs = "1" |Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla video parçaları içerebilir. Bu hello bu video parçaları koleksiyonudur. Daha fazla bilgi için bkz: [VideoTracks öğesi](media-services-output-metadata-schema.md). |
| **AudioTracks**<br/><br/> minOccurs = "0" maxOccurs = "1" |Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla ses izleri içerebilir. Bu hello bu ses izleri koleksiyonudur. Daha fazla bilgi için bkz: [AudioTracks öğesi](media-services-output-metadata-schema.md). |

## <a name="Sources "></a>Sources öğesi
İşlenmiş giriş/kaynak medya dosyaları koleksiyonu içinde bu AssetFile tooproduce sipariş.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **Kaynak**<br/><br/> minOccurs "1" maxOccurs = "unbounded" = |Bu varlık oluşturulurken kullanılan bir giriş/kaynak dosyası. Daha fazla bilgi için bkz: [Source öğesi](media-services-output-metadata-schema.md). |

## <a name="Source "></a>Source öğesi
Bu varlık oluşturulurken kullanılan bir giriş/kaynak dosyası.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Öznitelikler
| Ad | Tür | Açıklama |
| --- | --- | --- |
| **Ad**<br/><br/> Gerekli |**xs: String** |Giriş kaynağının dosya adı. |

## <a name="VideoTracks "></a>VideoTracks öğesi
Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla video parçaları içerebilir. Bu hello bu video parçaları koleksiyonudur.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **VideoTrack**<br/><br/> minOccurs "1" maxOccurs = "unbounded" = |Belirli bir video hello üst AssetFile izler. Daha fazla bilgi için bkz: [VideoTrack öğesi](media-services-output-metadata-schema.md#VideoTrack). |

## <a name="VideoTrack"></a>VideoTrack öğesi
Belirli bir video hello üst AssetFile izler.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Öznitelikler
| Ad | Tür | Açıklama |
| --- | --- | --- |
| **Kimliği**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Bu video izlemeyi sıfır tabanlı dizini. **Not:** bu mutlaka hello olarak kullanılan bir MP4 dosyasına TrackID değil. |
| **FourCC**<br/><br/> Gerekli |**xs: String** |Görüntü codec FourCC kodu. |
| **Profili** |**xs: String** |H264 profili (yalnızca geçerli tooH264 codec). |
| **Düzeyi** |**xs: String** |H264 düzeyi (yalnızca geçerli tooH264 codec). |
| **Genişlik**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Kodlanmış video genişliğini piksel cinsinden. |
| **Yükseklik**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Piksel cinsinden görüntü yüksekliği kodlanmış. |
| **DisplayAspectRatioNumerator**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:double** |Video görüntü en boy oranını pay. |
| **DisplayAspectRatioDenominator**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:double** |Video görüntü en boy oranını payda. |
| **Kare hızı**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:decimal** |Video kare hızı .3f biçiminde ölçülür. |
| **TargetFramerate**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:decimal** |Hedef video kare hızı .3f biçiminde hazır. |
| **Bit hızı**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Ortalama video bit hızı hello AssetFile gelen hesaplanan olarak kilobit / saniye. Yalnızca hello başlangıç akışı yükü sayar ve hello paketleme yükünü içermez. |
| **TargetBitrate**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Bu video izlemek için ortalama bit hızı kilobit hello kodlama hazır aracılığıyla istendiği gibi hedefleyin. |
| **MaxGOPBitrate**<br/><br/> minInclusive = "0" |**xs:int** |Max GOP ortalama bit hızı kilobit bu video izlemek için. |

## <a name="AudioTracks "></a>AudioTracks öğesi
Her fiziksel AssetFile içinde uygun bir kapsayıcı biçimi, araya eklemeli sıfır veya daha fazla ses izleri içerebilir. Bu hello bu ses izleri koleksiyonudur.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **AudioTrack**<br/><br/> minOccurs "1" maxOccurs = "unbounded" = |Belirli bir ses hello üst AssetFile izler. Daha fazla bilgi için bkz: [AudioTrack öğesi](media-services-output-metadata-schema.md). |

## <a name="AudioTrack "></a>AudioTrack öğesi
Belirli bir ses hello üst AssetFile izler.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Öznitelikler
| Ad | Tür | Açıklama |
| --- | --- | --- |
| **Kimliği**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Bu ses parça sıfır tabanlı dizini. **Not:** bu mutlaka hello olarak kullanılan bir MP4 dosyasına TrackID değil. |
| **Codec** |**xs: String** |Ses izleme codec dizesi. |
| **EncoderVersion** |**xs: String** |EAC3 için gereken isteğe bağlı Kodlayıcı sürüm dizesi. |
| **Kanalları**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Ses kanal sayısı. |
| **SamplingRate**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Saniye başına örnekleri veya Hz ses örnekleme hızı. |
| **Bit hızı**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Merhaba AssetFile gelen hesaplanan olarak saniyedeki ortalama ses bit hızı. Yalnızca hello başlangıç akışı yükü sayar ve hello paketleme yükünü içermez. |
| **BitsPerSample**<br/><br/> minInclusive = "0"<br/><br/> Gerekli |**xs:int** |Merhaba wFormatTag biçimi için örnek başına bit yazın. |

### <a name="child-elements"></a>Alt öğeler
| Ad | Açıklama |
| --- | --- |
| **LoudnessMeteringResultParameters**<br/><br/> minOccurs = "0" maxOccurs = "1" |Sonuç parametreleri ölçüm ses yüksekliği. Daha fazla bilgi için bkz: [LoudnessMeteringResultParameters öğesi](media-services-output-metadata-schema.md). |

## <a name="LoudnessMeteringResultParameters "></a>LoudnessMeteringResultParameters öğesi
Sonuç parametreleri ölçüm ses yüksekliği.  

Bir XML örneğinde bulabilirsiniz [XML örneği](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Öznitelikler
| Ad | Tür | Açıklama |
| --- | --- | --- |
| **DPLMVersionInformation** |**xs: String** |**Dolby** Geliştirme Seti sürüm ölçümü profesyonel ses yüksekliği. |
| **DialogNormalization**<br/><br/> minInclusive "-31" maxInclusive = = "-1"<br/><br/> Gerekli |**xs:int** |LoudnessMetering ayarlandığında gerekli DPLM oluşturulan DialogNormalization |
| **IntegratedLoudness**<br/><br/> minInclusive "-70" maxInclusive = = "10"<br/><br/> Gerekli |**xs:float** |Tümleşik ses yüksekliği |
| **IntegratedLoudnessUnit**<br/><br/> Gerekli |**xs: String** |Tümleşik ses yüksekliği birimi. |
| **IntegratedLoudnessGatingMethod**<br/><br/> Gerekli |**xs: String** |Tanımlayıcı geçişi |
| **IntegratedLoudnessSpeechPercentage**<br/><br/> minInclusive "0" maxInclusive = = "100" |**xs:float** |Yüzde olarak hello programı üzerinden konuşma içeriği. |
| **SamplePeak**<br/><br/> Gerekli |**xs:float** |Yoğun mutlak örnek değeri, sıfırlama veya son başlatıldığından beri kanal başına kaldırılır.  DBFS birimleridir. |
| **SamplePeakUnit**<br/><br/> Sabit "dBFS" =<br/><br/> Gerekli |**xs:anySimpleType** |Örnek en yüksek birim. |
| **TruePeak**<br/><br/> Gerekli |**xs:float** |Kanal başına en fazla true en yüksek değer, göredir ITU-R BS.1770-2, sıfırlama veya son başlatıldığından beri temizlendi. DBTP birimleridir. |
| **TruePeakUnit**<br/><br/> Sabit "dBTP" =<br/><br/> Gerekli |**xs:anySimpleType** |TRUE en yüksek birim. |

## <a name="schema-code"></a>Şema kodu
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Width" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video width in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Height" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video height in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Framerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="MaxGOPBitrate">  
                              <xs:annotation>  
                                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Channels" use="required">  
                              <xs:annotation>  
                                <xs:documentation>number of audio channels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="SamplingRate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <a name="xml"></a>XML örneği
 Merhaba, hello çıkış meta veri dosyası örneği verilmiştir.  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
