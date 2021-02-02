## JAVA  中的流
    
### 什么是流

流代表任何有能力产出数据的数据源对象或者是有能力接受数据的接收端对象，流主要用于传输数据    
    
### Java的流类型

java 中的4个基本的抽象流类型，所有的流都继承自这四个类型
   
|     |输入流      |输出流       |
| ---- | ---------- | -------  |
|字节流|InputStream|outputStream|
|字符流|Reader     |Writer      | 
### InputStream
输入流用于读取文件内容,这个类是按照字节读取文件,所以当面对中文时不能保证绝对正确

**FileInputStream**
```
  String filePath="C:\\123.txt";
        try {
            FileInputStream filein=new FileInputStream(filePath);
            byte[] buf = new byte[1024];
            filein.read(buf);
            String fileContent=new String(buf, "UTF-8");
            System.out.println(fileContent);
            filein.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
```
###Reader
Reader 为字符型的流，每次读取一个字符所以不会造成中文的乱码 

**FileReader**   
```java
String filePath="C:\\123.txt";
        try {
            FileReader fileReader=new FileReader(filePath);
            int ch=  fileReader.read();
            fileReader.close();
            System.out.println((char)ch);
        } catch (Exception e) {
            e.printStackTrace();
        }
```
###OutputStream
用于写入文件以字节方式

**FileOutputStream**
```java
  String Outpath="c:\\456.txt";
        try {

            FileOutputStream fileOutputStream=new FileOutputStream(Outpath,true);
            String filecontent="正在进行文件写入测试\r\n";
            fileOutputStream.write(filecontent.getBytes());
            fileOutputStream.close();

        }catch (Exception e){
            e.printStackTrace();
        }
```
**FileWriter**
```java
 String Outpath="c:\\456.txt";
        try
        {
          FileWriter fileWriter= new FileWriter(Outpath,true);
          fileWriter.append("测试写入");
          fileWriter.write("write");
          fileWriter.close();
        }catch (Exception e){
            e.printStackTrace();
        }
```

      
   