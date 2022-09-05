# Facade Pattern
### Facade는 건물의 앞쪽정면이라는 뜻
### 여러개의 객체와 실제 사용하는 서브객체의 사이에 복잡한 의존관계가 있을때, facade라는 객체를 두고, 여기서 제공하는 interface만을 활용하여
### 기능을 사용하는 방식이다. facade는 자신이 가지고 있는 각 클래스의 기능을 명확히 알아야 한다

# Facade Pattern 실습

### 1. Ftp클래스 생성
```java
package com.company.design.facade;

public class Ftp {

    private String host;
    private int port;
    private String path;

    public Ftp(String host, int port,String path) {
        this.host = host;
        this.port = port;
        this.path = path;
    }

    public void connect() {
        System.out.println("FTP Host : "+host+" Port : " + port + "로 연결합니다");

    }

    public void moveDirectory() {
        System.out.println("FTP path : " +path+"로 이동합니다");

    }

    public void disConnect(){
        System.out.println("FTP 연결을 종료합니다");

    }




}
```

### 2. Reader클래스 생성
```java
package com.company.design.facade;

public class Reader {
    private String fileName;

    public Reader(String fileName) {
        this.fileName = fileName;
    }

    public void fileConnect() {
        String msg = String.format("Reader %s로 연결 합니다",fileName);
        System.out.println(msg);

    }
    public void fileRead(){
        String msg = String.format("Reader %s의 내용을 읽어 옵니다",fileName);
        System.out.println(msg);

    }

    public void fileDisconnect() {
        String msg = String.format("Reader %s로 연결종료합니다",fileName);
        System.out.println(msg);

    }
}
```
### 3.Writer클래스 생성
```java
package com.company.design.facade;

public class Writer {
    private String fileName;

    public Writer(String fileName){
        this.fileName = fileName;
    }

    public void write() {
        String msg = String.format("Writer %s로 파일쓰기를 합니다",fileName);
        System.out.println(msg);


    }

    public void fileConnect() {
        String msg = String.format("Writer %s로 연결 합니다",fileName);
        System.out.println(msg);

    }
    public void fileDisconnect() {
        String msg = String.format("Writer %s로 종료 합니다",fileName);
        System.out.println(msg);


    }
}
```

### 4. main클래스 초기 -> facade 객체를 통해서 이용할수 있게 만들거다
```java
package com.company.design;

import com.company.design.facade.Ftp;
import com.company.design.facade.Reader;
import com.company.design.facade.Writer;
import com.company.design.observer.Button;
import com.company.design.observer.IButtonListener;

public class Main {
    public static void main(String[] args) {
        Ftp ftpClient = new Ftp("www.foo.co.kr",22,"/home/etc");
        ftpClient.connect();
        ftpClient.moveDirectory();

        Writer writer = new Writer("text.tmp");
        writer.fileConnect();
        writer.write();


        Reader reader = new Reader("text.tmp");
        reader.fileConnect();
        reader.fileRead();

        reader.fileDisconnect();
        writer.fileDisconnect();
        ftpClient.disConnect();






    }

}
```

### 5. SftpClient클래스생성
```java
package com.company.design.facade;

public class SftpClient {
    private Ftp ftp;
    private Reader reader;
    private Writer writer;

    public SftpClient(Ftp ftp, Reader reader, Writer writer) {
        this.ftp = ftp;
        this.reader = reader;
        this.writer = writer;
    }
    //오버로딩
    public SftpClient(String host, int port, String path, String fileName) {
        this.ftp = new Ftp(host, port, path);
        this.reader = new Reader(fileName);
        this.writer = new Writer(fileName);
    }
    public void connect() {
        ftp.connect();
        ftp.moveDirectory();
        writer.fileConnect();
        reader.fileConnect();
    }

    public void disConnect() {
        writer.fileDisconnect();
        reader.fileDisconnect();
        ftp.disConnect();
    }

    public void read() {
        reader.fileRead();
    }

    public void write() {
        writer.write();
    }



}
```

### 6. main클래스 변경
```java
package com.company.design;

import com.company.design.facade.Ftp;
import com.company.design.facade.Reader;
import com.company.design.facade.SftpClient;
import com.company.design.facade.Writer;
import com.company.design.observer.Button;
import com.company.design.observer.IButtonListener;

public class Main {
    public static void main(String[] args) {
//        Ftp ftpClient = new Ftp("www.foo.co.kr",22,"/home/etc");
//        ftpClient.connect();
//        ftpClient.moveDirectory();
//
//        Writer writer = new Writer("text.tmp");
//        writer.fileConnect();
//        writer.write();
//
//
//        Reader reader = new Reader("text.tmp");
//        reader.fileConnect();
//        reader.fileRead();
//
//        reader.fileDisconnect();
//        writer.fileDisconnect();
//        ftpClient.disConnect();

        //facade패턴 적용
        SftpClient sftpClient =new SftpClient("www.foo.co.kr",22,"/home/etc","text.tmp");
        sftpClient.connect();
        sftpClient.write();
        sftpClient.read();
        sftpClient.disConnect();






    }

}
```
# 결론
### 여러가지 객체의 의존성들을 안쪽으로 숨겨주는 패턴 -> facade패턴


