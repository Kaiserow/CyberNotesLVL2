# Transport Layer

Application layerda çalışan çeşitli uygulamalar, source ve destination hostlar arasında iletilmesi gereken çeşitli veriler üretirler. Farklı hostlarda çalışan uygulamalar arasında mantıksal (logical) iletişimi sağlamak transport layer'ın görevidir. Transport layer bu iletişimi sağlarken, iki host arasında geçici bir session kurma ve uygulamalar için reliable bir iletişim sağlama prensiplerine uyarak iletişim sağlaması gerekebilir.

Transport layer, ağlarda çalışan cihazların üstündeki farklı uygulamardan, verileri çeşitli ağdalardaki ve çeşitli cihazlardaki ilgili uygulamalara taşır. Yani aslında bir nevi Network Layer ile Application Layer arasında köprü görevi görür.

Transport layer'ın hedef host türü, verilerin taşınması gereken media türü, verilerin izlediği yol, bir bağlantıdaki tıkanıklık (congestion) veya ağın boyutu hakkında bilgisi yoktur. 

Transport Layer iki tip protokolü içerir; Transmission Control Protocol (TCP) ve User Datagram Protocol (UDP)

## Transport Layer Responsibilities

### Tracking Individual Conversations

Transport Layerda, bir kaynak uygulama ile bir hedef uygulama arasında akan her veri kümesi bir "conversation" olarak bilinir ve ayrı ayrı izlenir. Bu birden fazla conversationu sürdürmek ve izlemek taşıma katmanının sorumluluğundadır. Bir cihaz aynı anda birden fazla uygulamayla iletişim kuruyor olabilir. Bu noktada transport layerın bu özelliği devreye girer.

### Segmenting Data and Reassembling Segments

Çoğu ağda tek bir pakete dahil edilebilecek veri miktarı sınırlıdır. Bu nedenle, veriler yönetilebilir parçalara bölünmelidir.

Uygulama verilerini uygun büyüklükteki bloklara bölmek transport layerın sorumluluğundadır. Kullanılan transport layer protokolüne bağlı olarak transport layer blokları segment (TCP) veya datagram (UDP) olarak adlandırılır. Veriler parçalara bölünerek daha yönetilebilir ve taşınabilir olur.
