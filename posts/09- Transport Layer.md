# Transport Layer

Application layerda çalışan çeşitli uygulamalar, source ve destination hostlar arasında iletilmesi gereken çeşitli veriler üretirler. Farklı hostlarda çalışan uygulamalar arasında mantıksal (logical) iletişimi sağlamak transport layer'ın görevidir. Transport layer bu iletişimi sağlarken, iki host arasında geçici bir session kurma ve uygulamalar için reliable bir iletişim sağlama prensiplerine uyarak iletişim sağlaması gerekebilir.

Transport layer, ağlarda çalışan cihazların üstündeki farklı uygulamardan, verileri çeşitli ağdalardaki ve çeşitli cihazlardaki ilgili uygulamalara taşır. Yani aslında bir nevi Network Layer ile Application Layer arasında köprü görevi görür.

Transport layer'ın hedef host türü, verilerin taşınması gereken media türü, verilerin izlediği yol, bir bağlantıdaki tıkanıklık (congestion) veya ağın boyutu hakkında bilgisi yoktur. 

Transport Layer iki tip protokolü içerir; Transmission Control Protocol (TCP) ve User Datagram Protocol (UDP)

## Transport Layer Responsibilities

### Tracking Individual Conversations

Transport Layerda, bir kaynak uygulama ile bir hedef uygulama arasında akan her veri kümesi bir "conversation" olarak bilinir ve ayrı ayrı izlenir. Bu birden fazla conversationu sürdürmek ve izlemek taşıma katmanının sorumluluğundadır. Bir cihaz aynı anda birden fazla uygulamayla iletişim kuruyor olabilir. Bu noktada transport layerın bu özelliği devreye girer. Transport layer protokolleri, ilgili uygulamaya ilgili veriyi iletebilmek için portları kullanır. Her uygulamaya özel bir port atanarak, ilgili uygulamanın ilgili veriyi alması sağlanır.

### Segmenting Data and Reassembling Segments

Çoğu ağda tek bir pakete dahil edilebilecek veri miktarı sınırlıdır. Bu nedenle, veriler yönetilebilir parçalara bölünmelidir.

Uygulama verilerini uygun büyüklükteki bloklara bölmek transport layerın sorumluluğundadır. Kullanılan transport layer protokolüne bağlı olarak transport layer blokları segment (TCP) veya datagram (UDP) olarak adlandırılır. Veriler parçalara bölünerek daha yönetilebilir ve taşınabilir olur.

#### NOT: Datagramlar, UDP tarafından bölünmez. UDP ne bölünme işlemlerinden ne de birleştirme işlemlerinden sorumludur. UDP'nin yapmadığını bu vesileyle IP yapar (MTU'ya göre). Bunun yanında segmentleri bölen protokol TCP protokolüdür. Ayrıca hedef noktada, böldüğü segmentleri sırayla birleştirmekle de sorumludur.

Hem TCP hem de UDP verilerin üstüne header ekler. Bu headerlar, veri iletişiminin fonksiyonlarını belirleyen alanları içerir. Örneğin TCP hedef hostta segmentleri birleştirmek için headerındaki alanları kullanır.

Bazen video streaming gibi yüksek bant genişliği tüketen uygulamalar, ağdaki diğer servislerin performansını olumsuz etkileyebilir. Bu durumu daha yönetilebilir hale getirmek için, transport layer’da çalışan TCP protokolü segmentation ve multiplexing kullanır.

Segmentation, büyük verilerin küçük parçalara (segment) bölünerek daha kolay taşınmasını sağlar.
Multiplexing ise, aynı cihaz üzerindeki birden fazla uygulamanın farklı port numaraları üzerinden, aynı anda veri gönderebilmesini mümkün kılar.

Örneğin, aynı anda YouTube’dan video izlerken WhatsApp’tan mesajlaştığınızı düşünün. Her ikisi de farklı uygulamalar olmasına rağmen, aynı anda çalışabiliyor — işte bu, multiplexing sayesinde mümkündür.

# Transmission Control Protocol (TCP)

TCP protokolü, UDP ve network layerda görev alan IP protokolünün aksine "reliable" bir protokoldür. TCP, verilerin hedefe ulaşıp ulaşmadığını garanti eder, eğer ulaşmadıysa da bir daha gönderir.

TCP aşağıdaki yöntemleri kullanarak, "reliability" ve "flow control" sağlar;

• Segmentler, belirli bir hosttan belirli bir uygulamaya giderken numaralandırılır ve iletim sırasında takip edilir.

• Her bir segmentin karşıya ulaşıp ulaşmadığından emin olmak için onay "acknowledgement" alır.

• Onay alınmayan (unacknowledged) segmentleri belirli bir süre sonra tekrar gönderir.

• Hedefine yanlış sırada ulaşan segmentleri doğru sıraya dizer.

• Verilerin, karşı tarafın kabul edebileceği oranda gönderilmesini sağlar. 

TCP, verileri izlemek ve conversation'un durumunu yönetebilmek için ilk olarak bir bağlantı kurması gerekir (establish connection). TCP'nin bu özelliği ona aynı zamanda connection-oriented (bağlantı odaklı) protokol denmesinin nedenidir.

# User Datagram Protocol (UDP)

UDP, TCP'ye göre çok daha basit bir protokoldür, çünkü reliability veya flow control sağlamak gibi bir derdi yoktur. Bu nedenle de header fieldları çok daha azdır. Fakat UDP datagramları, bu özelliği sayesinde TCP segmentlerinden çok daha hızlı bir şekilde işlenebilir.

TCP'nin segmentlere uygulamış olduğu segmentation işleminin aksine, UDP protokolünün datagramları bölmek gibi bir görevi yoktur. Eğer bir datagram çok büyükse ve bölünmesi gerekiyorsa (MTU'dan fazlaysa), bu işlemi IP, fragmentation yaparak bölecektir.

UDP, güvenilirlik (reliability) veya akış kontrolü (flow control) sağlamadığından, önceden kurulmuş bir bağlantıya ihtiyaç duymaz. Bu nedenle de UDP, bağlantısız (connectionless) bir protokoldür.
Ayrıca UDP, istemci ve sunucu arasında gönderilen veya alınan verileri takip etmediği için, durumsuz (stateless) bir protokol olarak da bilinir. Bu kavramların karışmaması için kısa tanımlar vermek gerekirse;

![image](images/conceptsexplanations.png)

State'ten kasıt da, bağlantının hangi aşamada olduğunu bilmesidir. Örneğin en basit anlamda TCP protokolü, SYN ile bağlantı kurulduğunu, FIN ile de bağlantının kapandığını bilir. Böylece durum takibi yapmış olur. (SYN ile FIN'in ne olduğu sonra anlatılacaktır.) UDP bunların hiçbirini önemsemediğinden "stateless" bir protokoldür.

Ayrıca UDP, best-effort'u benimseyen bir protokoldür. Yani bir nevi, elinden gelenin en iyisini yapar ama verinin karşı tarafa ulaşıp ulaşmadığını garanti etmez. UDP kısaca;

🔸 Stateless               → Önceki gönderimlere dair bilgi tutulmaz

🔸 Connectionless          → Bağlantı kurulmaz (no handshake)

🔸 No Reliability          → Paket garantisi yok (no delivery guarantee)

🔸 No Acknowledgment (ACK) → Alındı bilgisi istenmez

🔸 No Retransmission       → Paket kaybolursa tekrar gönderilmez

🔸 No Flow Control         → Gönderici hızı alıcıya göre ayarlanmaz

🔸 No Congestion Control   → Ağ tıkanıklığına karşı önlem almaz

                                ↓

     ✅ **Best-Effort Delivery Model**
     
     → Paketler "elimden gelenin en iyisi" prensibiyle gönderilir,
     
     → Ulaşır mı? Sıralı mı? Tam mı? → Umursanmaz

                  
                  
  şeklinde anlatılabilir.

## The Right Transport Layer Protocol for the Right Application
  
Bazı uygulamalar bir takım verilerin kaybolmasını tolere edebilir ama oluşabilecek herhangi bir gecikmeyi (delay) kabul edemezler. Bu gibi durumlarda UDP iyi bir tercih olabilir. UDP tercihe edilebilecek uygulamalara bir örnek olarak, VoIP verilebilir. Acknowledgment, yani bir verinin ulaştığının onaylanmasını beklemek ve ulaşmadıysa da tekrar yollamak gibi işlemler gecikmeye sebep olabilir. Bu yüzden de VoIP gibi gerçek zamanlı iletişim içeren uygulamalarda bu kabul edilemez bir problemdir. 

UDP ayrıca, verinin az olduğu ve retransmission işleminin hızlı bir şekilde yapılabildiği request-reply uygulamalarında da kullanılır. Fakat bu noktada, retransmission işleminin UDP tarafından gerçekleşmediğini, onun yerine uygulama tarafından tekrar gönderim sağlandığının altını çizmekte fayda var. 2 konu önce gördüğümüz DNS sorguları bu tarzda bir iletişimdir ve burada UDP kullanılır. Örneğin istemci, bilinen bir domain name için bir DNS sunucusundan IPv4 ve IPv6 adresleri ister. İstemci önceden belirlenmiş bir süre içinde bir yanıt almazsa, isteği tekrar gönderir.

Bunun yanında TCP ise, verilerin tamamının ulaşması gerektiğini garanti eden uygulamalar için kullanılır. Örneğin, bir bankanın web sayfasındayken bilgilerinize erişim sağladığınız esnada herhangi bir veri kaybı istenmeyen bir durumdur ve bu yüzden de TCP kullanılmalıdır.

Gerçek zamanlı iletişimler, (Skype, Zoom gibi VoIP kullanan uygulamalar) çeşitli oyunlar, DNS, DHCP ve NTP protokolleri dışında ağlarda çoğunlukla -çoğu canlı yayın ve video akışın da bile- TCP kullanılır. Bunun nedenlerinden bazıları TCP'nin, buffering, bandwidth probing, congestion control gibi kullanıcı deneyimine yönelik işlevler içermesidir.

Mesela, önceden kaydedilmiş ses ve video içeriğini yayınlayan (stream eden) uygulamalar genellikle TCP kullanır.

Örneğin, bir film platformunda isteğe bağlı (on-demand) bir video izlerken ağınız aniden gerekli bant genişliğini sağlayamazsa, uygulama oynatmayı duraklatabilir.
Bu esnada ekranda "buffering..." (önbelleğe alınıyor) gibi bir mesaj görebilirsiniz.
Bu, TCP'nin veriyi mümkün olan hızla iletmeye devam ettiği sırada, uygulamanın videoyu oynatabilmesi için yeterli miktarda veriyi yeniden önbelleğe almayı beklediği anlamına gelir.
Yeterli veri yüklendiğinde ve ağ hızı belli bir seviyeye ulaştığında, video oynatıcı kaldığı yerden devam eder.

# TCP Header

TCP, yukarıda bahsettiğimiz özellikleri sağlamak için aynı diğer protokoller gibi çeşitli özelliklerini faaliyete geçirebilmesini sağlayan bir header'a ihtiyaç duyar.

![image](images/tcpheader.png)

## TCP Header Fields

#### Source Port -> Kaynak uygulamanın port numarasıyla ilişkilendirilmiştir.

#### Destination Port -> Hedef uygulamanın port numarasıyla ilişkilendirilmiştir.

#### Sequence Number -> Verinin tekrar birleştirilmesi için (reassembly) kullanılan kısımdır. Bu,  TCP'nin reliable, ordered delivery ve reassembly özelliklerini taşımasına olanak tanıyan alanlardan biridir.

#### Acknowledgement Number -> Bu alan, verinin alıcı tarafından alındığını ve sıradaki verinin beklendiğini belirtir. Böylece, TCP'nin reliable bir protokol olmasını sağlar.

#### Header Length -> "Data Offset" olarak da adlandırılabilir. TCP segment header'ının uzunluğunu belirtir.

#### Reserved -> Şu an aktif olarak kullanılmaz ama protokol geliştiricileri için gelecekte TCP’ye yeni bayraklar veya özellikler eklenmesi gerektiğinde kullanılmak üzere ayrılmıştır.

#### Control Bits -> TCP segmentinin amacını ve fonksiyonunu belirlemeye yarayan alandır. Bu alan bit kodlarını ya da diğer bir ismiyle flagları içerir. Daha önceden de bahsettiğimiz, SYN/ACK gibi gösterimler flag olarak adlandırılır ve TCP'nin "Stateful" olmasıyla doğrudan ilişkilidir.

#### Window Size -> Tek bir seferde alıcı tarafından kabul edilebilecek byte sayısını belirtir. Bu da doğrudan TCP'nin "Flow Control" özelliği ile ilgilidir. (İleride daha ayrıntılı bahsedilecek)

#### Checksum -> Segment headerında ya da verinin kendisinde bir hata olup olmadığının kontrolü için kullanılır.

#### Urgent -> Adın da anlaşılacağı üzere, verinin acil işlenmesi gereken kısmını tanımlar.

HTTP, FTP, SMTP, SSH gibi protokoller TCP kullanır. TCP kullanmayan uygulamaların, TCP'nin sunduğu özellikleri kendileri sağlamaları gerekebilir.

# UDP Header

![image](images/udpheader.png)

Görüldüğü üzere TCP header'ından çok daha basit bir yapısı vardır. Bu da kolay işlenebilmesini sağlar.

## UDP Header Fields

#### Source Port -> Kaynak uygulamayı tanımlayan porttur.

#### Destination Port -> Hedef uygulamayı tanımlayan porttur.

#### Length -> UDP Datagram Header uzunluğudur.

#### Checksum -> Hem header hem de veri üzerinde hata kontrolü yapar.

UDP; DNS, DHCP, SNMP, VoIP gibi uygulamalarda ve flow control, error detection, acknowledgement ile error recovery gerektirmeyen ya da bunları uygulamanın kendisi bir şekilde karşılayan, uygulamalarda kullanılır.

DNS ve SNMP varsayılan olarak UDP kullansa da, her ikisi de TCP kullanabilir. DNS requesti veya DNS replyı 512 bayttan fazlaysa, örneğin bir DNS yanıtı birçok domain name resolution içeriyorsa, DNS TCP kullanır. Benzer şekilde, bazı durumlarda ağ yöneticisi SNMP'yi TCP kullanacak şekilde yapılandırmak isteyebilir.










