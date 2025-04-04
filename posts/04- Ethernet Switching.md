# Ethernet 

Networking'in ilk yıllarında her üretici kendi interconnecting network cihazlarını ve networking protokollerini kullanıyordu. Bu yüzden, farklı üreticilerden ekipman alındığında, onların birlikte çalışabileceği garanti edilemiyordu. Networkler yaygınlaşmaya başladığında, farklı üreticileri aynı noktada birleştirmeye yarayan çeşitli kurallar tanımlanarak standartlar oluşturuldu.

Uzun bir süre boyuncu resmi bir şekilde kullanılan local area networking protokol standartı yoktu. Ancak zamanla ethernet diğerlerinden çok daha popüler hale geldi. Ethernet protokolleri, verinin nasıl biçimlendirileceğini ve wired network üzerinden nasıl iletileceğini tanımlar. Ayrıca ethernet standartları, OSI modelinin 1. ve 2. katmanlarını yönetir. Ethernet teknolojisi daha popüler hale gelmesiyle beraber artık bir standart haline gelmişti ve neredeyse tüm wired local area networklerinde ethernet kullanılıyordu.

The Institute of Electrical and Electronics Engineers, ya da IEEE, ethernet ve wireless standartlarının da dahil olduğu networking standartlarını yönetir. IEEE komiteleri, bağlantılar için standartları, medya gerekliliklerini ve iletişim protokollerini yönetmek ve onaylamakla yükümlüdür. Her standarta, hangi komitenin o standartı onaylayıp yönettiğini belli edecek şekilde bir sayı atanmıştır. Ethernet standartlarından sorumlu olan komite, 802.3'tür. 

Ethernetin 1973'te ortaya çıkmasından bu yana, zamanla bu teknolojiyi geliştirmek için çeşitli standartlar öne sürüldü. Ethernetin bu zamanla gelişebilme özelliği onu popüler yapan ana nedenlerden bir tanesidir. Ethernet'in her sürümünün kendine özgü bir standardı vardır. Örneğin 802.3 100BASE-T, twisted-pair kablo standartlarını kullanan 100 Megabit ethernet'i temsil eder. Buradaki "100 Mbps" ifadesi hızını, "BASE" ifadesi baseband iletimi kullanıldığını ve "T" ifadesi ise kablonun türünü yani buradaki ifadeye göre de twisted-pair olduğunu temsil eder.

Ethernetin ilk versiyonları maksimum 10 Mbps'a kadar desteklerken, günümüzde ise ethernetin saniyede 1.6TbE (Terabit Ethernet) desteklemesi için kullanılacak standartın da geliştirme aşamasında olduğunu söyleyelim. Bunun haricinde, günlük kullanımda 1GbE ve 10GbE yaygın olsa da, veri merkezleri ve büyük ağ altyapılarında 100GbE ve üzeri hızlar kullanılıyor.

# Ethernet Frames

Ethernet, wireless (WLAN) ile beraber günümüzde kullanılan 2 farklı LAN teknolojisinden biridir. Ethernet teknolojisi, twisted-pair, coaxial kablo ve fiber optik gibi kabloları kullanarak kablolu iletişime olanak tanır. Ethernet, data link layerda ve physical layerda çalışır. IEEE 802.2 ve 802.3 standartlarında tanımlanan bir ağ teknolojileri ailesidir.

## Data Link Sublayers

Ethernetin de dahil olduğu IEEE 802 LAN/MAN protokollerinin çalışabilmesi için yani data link layer'ın yönetilebilmesi için bu katman, "Logical Link Control (LLC)" ve "Media Access Control (MAC)" adı verilen iki farklı sublayer'e bölünmüştür.

### LLC Sublayer

IEEE 802.2 sublayer'ı, üst katmanlardaki ağ yazılımları ile alt katmanlardaki cihaz donanımları arasında iletişim kurar. Frame'in içine, hangi network layer protokolünün kullanıldığının bilgisini ekler. Bu bilgi, birden fazla Layer 3 protokolünün (IPv4 ve IPv6 gibi) aynı network interface ve media üzerinde çalışmasını sağlar.

### MAC Sublayer

Bu sublayer (örneğin IEEE 802.3, 802.11 veya 802.15) donanıma entegre edilmiştir ve veri encapsulation'ını ile media access control'ünü sağlar. Data link layer adreslemesini sağlar ve çeşitli physical layer teknolojileriyle (yani twisted-pairlar, fiber optik kablolar veya kablosuz iletim sağlayan bluetooth ve RFID, NFC gibi teknolojiler) entegre olarak çalışır.

#### Data Encapsulation

MAC Sublayer'ının data encapsulation ve medyaya erişim sağlamakla sorumlu olduğunu söylemiştik. Data encapsulationa şunlar dahil olabilir;

##### Ethernet Frame -> Ethernet frame'inin iç yapısını oluşturur.

##### Ethernet Addressing -> Frame'in içine source MAC adresi ve destination MAC adresi koyarak verinin NIC'ten NIC'e iletilmesine olanak tanır.

##### Ethernet Error detection -> Ethernet frame'i, frame check sequence (FCS) adı verilen bir hata kontrol trailer'ine sahiptir.

#### Accessing the Media

IEEE 802.3 MAC sublayerı, bakır ve fiber gibi çeşitli medya türleri üzerinden farklı Ethernet iletişim standartlarına ilişkin özellikleri içerir. Örneğin, IEEE 802.3z standartı, fiber üstünde gigabit ethernet destekler.

# Ethernet Frame Fields

Minimum ethernet frame'inin boyutu 64 byte ve beklenen maksimum boyutu ise 1518 byte'tır. Bu, destination MAC adresi alanından frame check sequence (FCS) alanına kadar olan tüm baytları içerir. Frame boyutu tanımlanırken "Preamble" alanı dahil edilmez. 64 bayttan küçük olan herhangi bir frame "collision fragment" ya da "runt frame" olarak adlandırılır ve alıcı istasyonlar tarafından otomatik olarak atılır. 1500 bayttan fazla veri içeren frame'ler ise "jumbo" ya da "baby giant frame" olarak adlandırılır. Alıcı cihazlar nasıl 64 bayttan az olduğunda frame'i dropluyorsa, 1500 bayttan fazla olduğunda da frame'i droplarlar. Bu tür droplanan frame'lere collisionslar (çarpışmalar) veya istenmeyen sinyaller sebep olabilir. Bununla beraber jumbo frame'lerin çoğu Gigabit Ethernet ve Fast Ethernet destekleyen switchler ile NIC'ler tarafından kabul edilir.

![image](images/ethernetframefields.png)

## Preamble and Start Delimiter Fields

7 byte olan Preamble ve 1 byte olan Start Frame Delimiter (SFD) ya da diğer adıyla Start of Frame, gönderici ve alıcı cihaz arasındaki senkronizasyon için kullanılır. Bu ilk 8 byte, alıcı node'ları uyarmak için kullanılır. Aslında ilk birkaç byte, alıcılara yeni bir frame almaları için hazır olmaları gerektiğini söyler.

## Destination MAC Address Field

Bu 6 byte'lık alan alıcıyı tanımlar. Ayrıca unicast, multicast veya broadcast adresi olabileceğini unutmayalım.

## Source MAC Address Field

Bu 6 byte'lık alan da kaynağı tanımlar. Yani aslında kaynak NIC adresidir.

## Type/Length

Bu 2 byte'lık alan ise, ethernet frame'inin içine encapsulate edilen bir üst katman protokolünü ifade eder. Bir üst katman protokolleri IPv4 (hexadecimal gösterim olarak -> 0x800), IPv6 (0x86DD) veya ARP (0x806) gibi protokoller olabilir. Ayrıca bu alanın, EtherType olarak da adlandırıldığını görebilirsiniz.

## Data Field

Bu alan 46 - 1500 byte arasında, üst katman tarafından encapsulate edilmiş, genellikle layer 3 PDU veya daha genel kullanım olarak IPv4 paketlerini içerir. Tüm frame'ler en az 64 byte uzunluğunda olmalıdır demiştik. Eğer küçük bir paket encapsulate edilirse, frame'in boyutunu arttırmak için "pad" adı verilen ek bitler eklenir.

#### NOT: Layer 3 PDU (Protocol Data Unit), çeşitli Layer 3 protokollerinin paketlerini genel olarak temsil etmek için kullanılır. Yani layer 3 pdu diyince buna, IPv4, IPv6, ARP, ICMP gibi protokol paketleri de dahildir.

## Frame Check Sequence Field

4 byte'tan oluşan bu alan, framedeki hataları tespit etmek için kullanılır. Bunu yapmak için, "Cyclic Redundancy Check (CRC)" kullanır. Gönderici cihaz CRC sonuçlarını, FCS alanına dahil eder. Alıcı cihaz frame'i aldığında hatalara bakmak için CRC oluşturur. Eğer iki cihazın da oluşturduğu CRC'ler eşleşirse, hata meydana gelmemiş demektir. Fakat eşleşmemesi durumunda verinin değişime uğradığı söylenebilir ve bu yüzden de frame droplanır. Bu değişim, bitleri temsil eden elektrik sinyallerindeki bir bozukluğa işaret edebilir.



