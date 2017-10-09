<!-- F-series, Fs-series* -->

F-serisi hello üzerinde temel 2.4 GHz Intel Xeon® E5-2673 v3 saat hızları hello Intel Turbo artırma teknolojisi 2.0 ile 3.1 GHz daha yüksek elde edebilirsiniz (Haswell) işlemci. Bu olduğu hello aynı Dv2-VMs dizi hello olarak CPU performans.  Daha düşük bir saat başına listesi fiyattan hello F-serisi hello en iyi fiyat-performans hello Azure Portföy vCPU başına hello Azure işlem birimi (ACU) dayalı olarak değerdir. 

F Serisi VM'ler, daha hızlı CPU'ya ihtiyaç duyan ancak çok fazla belleğe veya vCPU başına geçici depolamaya ihtiyaç duymayan iş yükleri için harika bir seçenektir.  Analiz, oyun sunucuları, web sunucuları ve toplu işleme gibi iş yükleri hello F-serisi hello değerinden yararlı olacaktır.

Merhaba Fs-serisi hello F-serisi, toplama tooPremium depolama birimindeki tüm hello avantajları sağlar.

## <a name="fs-series"></a>Fs Serisi*

ACU: 210 - 250

| Boyut | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum veri diskleri | Maksimum önbelleğe alınmış ve geçici depolama aktarım hızı: IOPS-MB/sn (önbellek boyutu GiB biriminde) | Maksimum önbelleğe alınmamış disk aktarım hızı: IOPS-MB/sn | Maks NIC / Beklenen ağ performansı (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4000/32 (12) |3200/48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8000/64 (24) |6400/96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16.000/128 (48) |12.800/192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32.000/256 (96) |25.600/384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64.000/512 (192) |51.200/768 |8 / 6000-12000 &#8224; |

MB/sn = 10^6 bayt/saniye ve GiB = 1024^3 bayt.

* hello en fazla disk verimliliği (IOPS veya MB/sn) Fs serisiyle VM olası hello sayıyla sınırlı olabilir, boyutu ve hello şeritleme disklerin bağlı.  Ayrıntılar için bkz. [Premium Depolama: Azure sanal makine iş yükleri için yüksek performanslı depolama](../articles/storage/common/storage-premium-storage.md).


<br>

## <a name="f-series"></a>F Serisi

ACU: 210 - 250

| Boyut         | Sanal işlemci | Bellek: GiB | Geçici depolama (SSD) GiB | Maksimum geçici depolama aktarım hızı: IOPS / Okuma MB/sn / Yazma MB/sn | Maksimum veri diski/aktarım hızı: IOPS | Maks NIC / Beklenen ağ performansı (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000/46/23                                           | 2/2x500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000/93/46                                           | 4/4x500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12000/187/93                                         | 8/8x500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24000/375/187                                        | 16/16x500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48000/750/375                                        | 32/32x500                       | 8 / 6000 - 12000 &#8224;           |


<br>


