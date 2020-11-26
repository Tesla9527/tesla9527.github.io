---
layout:     post
title:      "创建ISO8583文件"
subtitle:   ""
date:       2019-09-25
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - ISO8583
---

最近在信用卡账务的测试中，需要造ISO8583的请求文件，一番Google和尝试后搞定。

代码如下：

```java
import com.solab.iso8583.MessageFactory;
import com.solab.iso8583.IsoMessage;
import com.solab.iso8583.IsoType;
import com.solab.iso8583.parse.ConfigParser;
import com.solab.iso8583.impl.SimpleTraceGenerator;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class CreateMessage {
    public static void main(String[] args) throws IOException{
        // Check http://j8583.sourceforge.net/javadoc/index.html
        MessageFactory<IsoMessage> mf = new MessageFactory<>();
       /*
        try {
            String path = "config.xml";
            ConfigParser.configureFromUrl(mf, new File(path).toURI().toURL());
        } catch (IOException e) {
            e.printStackTrace();
        }*/

        mf.setForceSecondaryBitmap(true);
        mf.setUseBinaryBitmap(true);
      //mf.setAssignDate(true); // This sets field 7 automatically
      //mf.setTraceNumberGenerator(new SimpleTraceGenerator((int) (System.currentTimeMillis() % 100000)));

        IsoMessage m = mf.newMessage(0x1644); // You must use 0x200, 0x400, etc.
        //m.setBinary(true);
        m.setForceSecondaryBitmap(true);
        m.setValue(24, "697", IsoType.NUMERIC, 3); // Function Code
        m.setValue(48, "010502522219090300000004073011010122001P", IsoType.LLLVAR, 6); // Additional Data
        m.setValue(71, "00000001", IsoType.ALPHA, 8); // Message Number
        FileOutputStream fout = new FileOutputStream("Header.txt", true);
        m.write(fout,0);
        //fout.write('\n');
        System.out.println(m.debugString());
    }
}
```