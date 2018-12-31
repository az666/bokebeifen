---
title: 利用机智云APP学习JAVA安卓
tags: android
date: 2018-7-12 11:09:00
---
## 学习android ##

> 昨天遇到了一个很好的视频教程，今天果断把电脑拿回来，在宿舍开始我的android学习之路，学东西不系统，坚持不了只能一点一点摸索，今天进展非常顺利，爽的很，今天成功按照教程将机智云官方SDk添加到androidstudio中。
> 一、成功完成了SDK的初始化
> 二、完成了启动图的添加
> 三、完成了bug的修复，一步一步心惊肉跳，紧张无比。。。
> 四、完成了android 6.0以后的权限动态验证。
> 教程链接--发烧友学院--哎呀，太好了这个网站，很丰富的教程。
> [嵌入式开发安卓篇](http://t.elecfans.com/3160.html)


----------
![视频教程](https://i.loli.net/2018/07/12/5b476ecd6b3cd.png)

----------
![编程界面](https://i.loli.net/2018/07/12/5b476e6219918.png)

----------
<!--more-->

```
package com.example.administrator.jizhiyun;

import android.content.Context;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import com.gizwits.gizwifisdk.api.GizWifiDevice;
import com.gizwits.gizwifisdk.api.GizWifiSDK;
import com.gizwits.gizwifisdk.enumration.GizEventType;
import com.gizwits.gizwifisdk.enumration.GizWifiErrorCode;
import com.gizwits.gizwifisdk.listener.GizWifiDeviceListener;
import com.gizwits.gizwifisdk.listener.GizWifiSDKListener;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ConcurrentHashMap;
import static android.os.Build.VERSION.SDK;
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initSDK();
    }
    protected  void initSDK(){
// 设置 SDK 监听
        GizWifiSDK.sharedInstance().setListener(mListener);
// 设置 AppInfo
        ConcurrentHashMap<String,String > appInfo= new ConcurrentHashMap<>();
        appInfo.put("appId", "45689bece90b485db90470b97f320d26");
        appInfo.put("appSecret", "d08095085c314eee87cb078bcd160035");
// 设置要过滤的设备 productKey 列表。不过滤则直接传 null
        List<ConcurrentHashMap<String,String>> productInfo = new ArrayList<>();
        ConcurrentHashMap<String,String> product = new ConcurrentHashMap<>();
        product.put("productKey", "30c07f8fac834377aa096067fab24220");
        product.put("productSecret", "3548e22cd9124fcba728d3db9b767090");
        productInfo.add(product);
// 指定要切换的域名信息。使用机智云生产环境则传 null
        ConcurrentHashMap<String, Object> cloudServiceInfo = new ConcurrentHashMap<>();
        cloudServiceInfo.put("openAPIInfo", "your_api_domain");
// 调用 SDK 的启动接口
       // GizWifiSDK.sharedInstance().startWithAppInfo(context:this, appInfo, productInfo, null, false);
        GizWifiSDK.sharedInstance().startWithAppInfo(this, appInfo, productInfo, null, false);
    }
    // 实现系统事件通知回调
      private   GizWifiSDKListener mListener = new GizWifiSDKListener() {
        @Override
        public void didNotifyEvent(GizEventType eventType, Object eventSource, GizWifiErrorCode eventID, String eventMessage) {
            super.didNotifyEvent(eventType, eventSource, eventID, eventMessage);
            Log.e( "wenzheng", "didNotifyEvent" + eventType.toString());
            //初始化成功
        }
    };
}

```


----------

```
package com.example.administrator.jizhiyun.ui;

import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.os.PersistableBundle;
import android.support.annotation.NonNull;
import android.support.annotation.Nullable;
import android.support.v4.app.ActivityCompat;
import android.support.v4.content.ContextCompat;
import android.support.v7.app.AppCompatActivity;
import android.widget.Switch;
import android.widget.Toast;

import com.example.administrator.jizhiyun.MainActivity;
import com.example.administrator.jizhiyun.R;

import java.util.ArrayList;
import java.util.List;

public class SplashActivity extends AppCompatActivity{
    private Handler mHander = new Handler(){
        @Override
        public void handleMessage(Message msg) {
            super.handleMessage(msg);
            if (msg.what==107){
                startActivity(new Intent(SplashActivity.this, MainActivity.class));
                finish();//摧毁当前页面

            }
        }
    };
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);
        checkAndroidPrimisson();
    }
    private  void checkAndroidPrimisson(){
        //安卓6.0以上要动态授权
        if (Build.VERSION.SDK_INT >= 23) {
            requestRunPerMisson(new String[]{
                    Manifest.permission.READ_EXTERNAL_STORAGE ,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE,
                    Manifest.permission.ACCESS_FINE_LOCATION,
                    Manifest.permission.ACCESS_WIFI_STATE,
                    Manifest.permission.READ_PHONE_STATE
            });
        }else {
            mHander.sendEmptyMessageDelayed(107,2500);

        }
    }
   private void requestRunPerMisson(String[] strings){
        int status = 0;
        for (String permisson : strings){
            //判断是否已经授权
            if (ContextCompat.checkSelfPermission(this,permisson) != PackageManager.PERMISSION_GRANTED){
                ActivityCompat.requestPermissions(this,strings,108);
            }else {
                status++;

            }
            if (status==5){
                mHander.sendEmptyMessageDelayed(107,2500);
            }
        }
   }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        switch(requestCode){
            case 108:
                if (grantResults.length >0){
                    List<String> denioedPermisson = new ArrayList<>();
                    for (int i=0; i< grantResults.length;i++){
                        int grantPermisson = grantResults[i];
                        String permisson = permissions[i];
                        if (grantPermisson != PackageManager.PERMISSION_GRANTED){
                            denioedPermisson.add(permisson);
                        }
                    }
                    if (denioedPermisson.isEmpty()){
                        //权限全部通过
                        mHander.sendEmptyMessage(107);
                    }
                    else{
                        Toast.makeText(this,"您拒绝了部分权限",Toast.LENGTH_SHORT).show();
                        mHander.sendEmptyMessageDelayed(107,2500);
                    }
                }

        }
    }
}
```
![](https://i.loli.net/2018/07/12/5b476e9275091.png)


----------

> 今天学的很舒服，很开心。喜欢这种流畅的感觉，最讨厌编程的时候发生各种问题了，但是有问题能完美解决，是最舒服的。