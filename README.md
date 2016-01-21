# Java 網路資料爬蟲包
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.abola/crawler/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.abola/crawler)

本套件為網路上常見的資料協定、格式，提供了簡易且方便(easy-to-use)的操作接口。套件主要以Jsoup為核心擴展，整合Apache Commons-VFS後，提供更多種協定的操作，也可支援壓縮格式處理。

Requires JDK 1.6 or higher

To add a dependency on CrawlerPack using Maven, use the following:

    <dependency>
        <groupId>com.github.abola</groupId>
        <artifactId>crawler</artifactId>
        <version>0.9.2</version>
    </dependency>

To add a dependency using Gradle:

    dependencies {
        compile 'com.github.abola:crawler:0.9.2'
    }


And easy-to-use example

    // URI format source
    String uri = "https://raw.githubusercontent.com/abola/CrawlerPack/master/test.json";
    
    CrawlerPack
        .getFromJson(uri)
        .select("results name").text() ;

## 爬蟲包特色
### 支援常見網路協定
使用 Apache Commons-VFS 所支援所有協定，常見網路協定如http/https,samba(cifs),ftp,sftp等…詳細列表請參考 https://commons.apache.org/proper/commons-vfs/filesystems.html

### 支援常見資料格式
* JSON
* XML
* HTML 

### 支援 中文XML標籤 / 中文JSON欄位
爬蟲包套件可正常的處理使用中文命名的XML或JSON

 XML

    <集合>
      <元素>元素名稱1</元素>
      <元素>元素名稱2</元素>
    </集合>


 JSON

    {"集合":[
        {"元素":"元素名稱1"}
        , {"元素":"元素名稱2"}
    ]}


## 使用範例

#### JSON format example

    // 即時PM2.5資料
    String url = "http://opendata2.epa.gov.tw/AQX.json";

    CrawlerPack
        .getFromJson(url)
        .getElementsByTag("pm2.5").text();

#### XML format example
    
    // 10萬月薪以上的工作資料
    String url = "http://www.104.com.tw/i/apis/jobsearch.cfm?order=2&fmt=4&cols=JOB,NAME&slmin=100000&sltp=S&pgsz=20";
    
    CrawlerPack
        .getFromXml(url)
        .select("item").get(0).attr("job") ;

#### Html format example

    // ptt 笨版最新文章列表
    String url = "https://www.ptt.cc/bbs/StupidClown/index.html";

    CrawlerPack
        .getFromHtml(url)
        .select("div.title > a").text();
        
#### Compressed data example

    // 北市Youbike資訊
    String url = "gz:https://tcgbusfs.blob.core.windows.net/blobyoubike/YouBikeTP.gz";
    
    // 目前編號0004站借用資訊
    CrawlerPack
        .getFromJson(url)
        .select("0004")
        .select("sarea, ar, tot, sbi").text();
        
        
## 發展中項目 
* 在 http/https 中支援 cookie 


## Change log
#### 0.9.2
* 修正解析註解以及 js 中特殊符號的錯誤
* 修正動態網頁資料被cache的問題

#### 0.9.1
* 增加授權，使用Apache 2.0 公開授權
* 專案已上傳至公開的 Maven Repository 現在可以直接透過pom.xml使用爬蟲包
* 修正 https PKIX 驗證無法通過的問題

## Reference
* JCConf 2015 TW 高效率資料爬蟲組合包 投影片 http://www.slideshare.net/ssuser438746/jcconf-2015-tw
