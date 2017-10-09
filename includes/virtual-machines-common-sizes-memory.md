
* M-serisi Hello hello yüksek vCPU sayısı (yukarı too128 Vcpu'lar) ve (yukarı too2.0 Tıb) en büyük bellek hello bulutta herhangi bir VM'nin sunar.  Son derece büyük veritabanları veya yüksek vCPU sayısı ve büyük miktarlarda belleğin yararlı olacağı diğer uygulamalar için idealdir.

* Dv2-Serisi D-serisi, G-serisi ve hello DS/GS ortaklarınıza daha hızlı Vcpu, daha iyi geçici depolama performansı, talep veya daha yüksek bellek taleplerini sahip uygulamalar için idealdir.  Bu seçenekler birçok kurumsal sınıf uygulama için güçlü bir bileşim sunar.

* D-serisi VM'ler, daha yüksek işlem gücü ve geçici disk performans talep tasarlanmış toorun uygulamalarıdır. D Serisi VM'ler daha hızlı işlemcilere, daha yüksek bellek-vCPU oranına ve geçici depolama için katı hal sürücüsüne (SSD) sahiptir. Merhaba duyuru hello Azure blogu hakkında ayrıntılar için bkz [yeni D-serisi sanal makine boyutlarını](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Dv2 serisi, takip toohello özgün D-serisi, daha güçlü bir CPU özellikleri. Merhaba Dv2 serisi CPU yaklaşık %35 hello daha hızlı D-serisi CPU'dur. En son nesil hello üzerinde temel aldığı 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) işlemci ve hello Intel Turbo artırma teknolojisi 2.0 GHz too3.1 gidebilirsiniz. Merhaba Dv2 serisi sahip D-serisi hello gibi aynı bellek ve disk yapılandırmalarını hello.


## <a name="esv3-series"></a>ESv3 serisi

ACU: 160-190

ESv3-serisi örnekleri üzerinde hello dayalı 2.3 GHz Intel XEON® E5-2673 v4 (Broadwell) işlemci ve Intel Turbo artırma teknolojisi 2.0 ile 3.5 GHz elde etmek ve premium depolama kullanın. Ev3 serisi örnekleri, yoğun bellek kullanımlı kurumsal uygulamalar için idealdir.


| Boyut             | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4,000 / 32 (50)                                                       | 3200/48                                | 2/orta                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8,000 / 64 (100)                                                      | 6400/96                                | 2/orta                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16,000 / 128 (200)                                                    | 12.800/192                              | 4/yüksek                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32,000 / 256 (400)                                                    | 25.600/384                              | 8/yüksek                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64,000 / 512 (800)                                                    | 51.200/768                              | 8/aşırı yüksek                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128,000/1024 (1600)                                                   | 80,000 / 1200                             | 8/aşırı yüksek                             |



## <a name="ev3-series"></a>Ev3 serisi

ACU: 160-190 

Ev3-serisi örnekleri üzerinde hello dayalı 2.3 GHz Intel XEON® E5-2673 v4 (Broadwell) işlemci ve Intel Turbo artırma teknolojisi 2.0 ile 3.5 GHz elde edebilirsiniz. Ev3 serisi örnekleri, yoğun bellek kullanımlı kurumsal uygulamalar için idealdir.

Veri disk depolaması, sanal makinelerden ayrı olarak faturalandırılır. toouse premium depolama diskleri hello ESv3 boyutları kullanın. Merhaba fiyatlandırma ve faturalama metre ESv3 boyutları için olan hello Ev3-serisi ile aynı. 


| Boyut            | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum geçici depolama aktarım hızı: IOPS / Okuma MB/sn / Yazma MB/sn | Maksimum NIC/Ağ bant genişliği |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2/orta                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2/orta                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4/yüksek                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8/yüksek                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8/aşırı yüksek           |
| Standard_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8/aşırı yüksek           |


## <a name="m-series"></a>M serisi*

ACU: 160-180

| Boyut            | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2048           | 32             | 80,000 / 800 (6348)       | 40.000/1000                            | 8 / 16000          |
| Standard_M128s** | 128  | 2048        | 4096           | 64             | 160,000 / 1,600 (12,696) | 80.000/2000                            | 8 / 25000          |



* M serisi sanal makineler Intel® Hyper-Threading Teknolojisine sahiptir.

**64’ten fazla sanal işlemci şu desteklenen konuk işletim sistemlerinden birini gerektirir: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 SP2 ve Red Hat Enterprise Linux veya LIS 4.2.1 ile CentOS 7.3 

<br>

## <a name="gs-series"></a>GS Serisi*

ACU: 180 - 240

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10.000/100 (264) |5000/125 |2 / 2000 |
| Standard_GS2 |4 |56 |112 |8 |20.000/200 (528) |10.000/250 |2 / 4000 |
| Standard_GS3 |8 |112 |224 |16 |40.000/400 (1056) |20.000/500 |4 / 8000 |
| Standard_GS4 |16 |224 |448 |32 |80.000/800 (2112) |40.000/1000 |8 / 6000 - 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160.000/1600 (4224) |80.000/2000 |8 / 20000 |

* hello en fazla disk verimliliği (IOPS veya MB/sn) GS serisi VM ile olası hello sayıyla sınırlı olabilir, boyutu ve hello şeritleme disklerin bağlı. Ayrıntılar için bkz. [Premium Depolama: Azure sanal makine iş yükleri için yüksek performanslı depolama](../articles/storage/common/storage-premium-storage.md). 

** Yalıtılmış toohardware ayrılmış tooa tek müşteri örneğidir.


<br>

## <a name="g-series"></a>G Serisi

ACU: 180 - 240

| Boyut         | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum geçici depolama aktarım hızı: IOPS / Okuma MB/sn / Yazma MB/sn | Maksimum veri diski/aktarım hızı: IOPS | Maks NIC / Beklenen ağ performansı (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000/93/46                                           | 4/4x500                       | 2 / 2000                     |
| Standard_G2  | 4         | 56          | 768            | 12000/187/93                                         | 8/8x500                       | 2 / 4000                     |
| Standard_G3  | 8         | 112         | 1536          | 24000/375/187                                        | 16/16x500                     | 4 / 8000                |
| Standard_G4  | 16        | 224         | 3072          | 48000/750/375                                        | 32/32x500                     | 8 / 6000 - 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6144          | 96000/1500/750                                       | 64/64x500                     | 8 / 20000           |

* Yalıtılmış toohardware ayrılmış tooa tek müşteri örneğidir.
<br>


## <a name="dsv2-series"></a>DSv2 Serisi*

ACU: 210 - 250

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8000/64 (72) |6400/96 |2 / 1500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16.000/128 (144) |12.800/192 |4 / 3000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32.000/256 (288) |25.600/384 |8 / 6000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64.000/512 (576) |51.200/768 |8 / 6000 - 12000 &#8224; |
| Standard_DS15_v2** |20 |140 |280 |40 |80.000/640 (720) |64.000/960 |8 / 20000***

* hello en fazla disk verimliliği (IOPS veya MB/sn) DSv2 serisi VM ile olası hello sayıyla sınırlı olabilir, boyutu ve hello şeritleme disklerin bağlı.  Ayrıntılar için bkz. [Premium Depolama: Azure sanal makine iş yükleri için yüksek performanslı depolama](../articles/storage/common/storage-premium-storage.md).

** Örnek; Bu, sanal makine yalnızca VM bizim Intel Haswell düğümde hello yalıtılmış bir düğümdür.

***25.000 Mbps, Hızlandırılmış Ağ Bağlantısı.

<br>

## <a name="dv2-series"></a>Dv2 Serisi

ACU: 210 - 250

| Boyut              | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum geçici depolama aktarım hızı: IOPS / Okuma MB/sn / Yazma MB/sn | Maksimum veri diski/aktarım hızı: IOPS | Maks NIC / Beklenen ağ performansı (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000/93/46                                           | 4/4x500                         | 2 / 1500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12000/187/93                                         | 8/8x500                         | 4 / 3000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24000/375/187                                        | 16/16x500                       | 8 / 6000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48000/750/375                                        | 32/32x500                       | 8 / 6000 - 12000 &#8224;          |
| Standard_D15_v2* | 20        | 140         | 1000          | 60000/937/468                                        | 40/40x500                       | 8 / 20000** |

* Örnek; Bu, sanal makine yalnızca VM bizim Intel Haswell düğümde hello yalıtılmış bir düğümdür.

**25.000 Mbps, Hızlandırılmış Ağ Bağlantısı.

<br>

## <a name="ds-series"></a>DS Serisi*

ACU: 160

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8000/64 (72) |6400/64 |2 / 1000 |
| Standard_DS12 |4 |28 |56 |8 |16.000/128 (144) |12.800/128 |4 / 2000 |
| Standard_DS13 |8 |56 |112 |16 |32.000/256 (288) |25.600/256 |8 / 4000 |
| Standard_DS14 |16 |112 |224 |32 |64.000/512 (576) |51.200/512 |8 / 6000 - 8000 &#8224; |

* hello en fazla disk verimliliği (IOPS veya MB/sn) DS serisi VM ile olası hello sayıyla sınırlı olabilir, boyutu ve hello şeritleme disklerin bağlı.  Ayrıntılar için bkz. [Premium Depolama: Azure sanal makine iş yükleri için yüksek performanslı depolama](../articles/storage/common/storage-premium-storage.md).


## <a name="d-series"></a>D Serisi

ACU: 160

| Boyut         | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum geçici depolama aktarım hızı: IOPS / Okuma MB/sn / Yazma MB/sn | Maksimum veri diski/aktarım hızı: IOPS | Maks NIC / Beklenen ağ performansı (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11 | 2         | 14          | 100            | 6000/93/46                                           | 4/4x500                         | 2 / 1000                     |
| Standard_D12 | 4         | 28          | 200            | 12000/187/93                                         | 8/8x500                         | 4 / 2000                     |
| Standard_D13 | 8         | 56          | 400            | 24000/375/187                                        | 16/16x500                       | 8 / 4000                     |
| Standard_D14 | 16        | 112         | 800            | 48000/750/375                                        | 32/32x500                       | 8 / 6000 - 8000 &#8224;                |

<br>

