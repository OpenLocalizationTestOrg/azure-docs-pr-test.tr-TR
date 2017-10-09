
Merhaba NC ve NV boyutları olarak da bilinen GPU etkin örnekleridir. NVIDIA GPU kartlarına sahip bu özel amaçlı sanal makineler, farklı senaryolar ve kullanım amaçları için iyileştirilmiştir. Merhaba NV boyutları en iyi duruma getirilmiş ve uzak görselleştirme, akış, oyun, kodlama ve OpenGL ve DirectX gibi çerçeveler kullanılarak VDI senaryoları için tasarlanmıştır. Merhaba NC boyutları daha yoğun ve ağ yoğunluklu uygulamalar ve CUDA ve OpenCL tabanlı uygulamalar ve benzetimleri gibi algoritmaları için iyileştirilir. 


Merhaba NV örnekleri NVIDIA Tesla M60 GPU kartı tarafından açık ve Masaüstü için NVIDIA kılavuz uygulamalar ve sanal masaüstlerini müşteriler mümkün toovisualize nerede kendi veri veya benzetimleri hızlandırılmış. Kullanıcılar kendi grafik yoğun iş akışlarında hello NV örnekleri tooget üstün grafik yeteneği mümkün toovisualize olması ve ayrıca kodlama ve işleme gibi tek duyarlıklı iş yükleri çalıştırın. Merhaba Tesla M60 4096 CUDA çekirdek 1080 p H.264 too36 akışları ile bir çift GPU tasarımı sunar. 

Merhaba NC örnekleri NVIDIA Tesla K80 kartı tarafından güç sağlar. Kullanıcılar artık enerji keşif uygulamaları, kaza simülasyonları, ışın izlemeli işleme, derin öğrenme ve çok daha fazlası için CUDA yardımıyla verileri çok daha hızlı işleyebilir. Merhaba Tesla K80 çift GPU tasarım too8.93 Teraflops tek duyarlıklı performansını ayarlama too2.91 çift duyarlıklı Teraflops kurup 4992 CUDA çekirdeğiyle sunar.

## <a name="nv-instances"></a>NV Örnekleri

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | GPU | En fazla veri diski |
| --- | --- | --- | --- | --- | --- |
| Standard_NV6 |6 |56 |380 | 1 | 8 |
| Standard_NV12 |12 |112 |680 | 2 | 16 |
| Standard_NV24 |24 |224 |1440 | 4 | 32 |

1 GPU = M60 kartın yarısı.

## <a name="nc-instances"></a>NC Örnekleri

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | GPU | En fazla veri diski |
| --- | --- | --- | --- | --- | --- |
| Standard_NC6 |6 |56 | 380 | 1 | 8 |
| Standard_NC12 |12 |112 | 680 | 2 | 16 |
| Standard_NC24 |24 |224 | 1440 | 4 | 32 |
| Standard_NC24r* |24 |224 | 1440 | 4 | 32 |

1 GPU = K80 kartın yarısı.

*RDMA özellikli


