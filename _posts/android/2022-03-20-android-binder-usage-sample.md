---
layout: post
title: "Android无处不在的Binder身影。"
date: 2022-03-20 20:05:01
category: android
tags: [Android, Binder, Proxy, Stub]
---


#### 1.Android Framwrok使用Binder的例子

ActivityThread，内部类ApplicationThread继承了ApplicationThreadNative，用于接收AMS的消息回调。而ApplicationThreadNative实则是继承了Binder类，重写了asInterface，onTransact等方法：

```
/** {@hide} */
public abstract class ApplicationThreadNative extends Binder
        implements IApplicationThread {
    /**
     * Cast a Binder object into an application thread interface, generating
     * a proxy if needed.
     */
    static public IApplicationThread asInterface(IBinder obj) {
        if (obj == null) {
            return null;
        }
        IApplicationThread in =
            (IApplicationThread)obj.queryLocalInterface(descriptor);
        if (in != null) {
            return in;
        }
        
        return new ApplicationThreadProxy(obj);
    }
    
    public ApplicationThreadNative() {
        attachInterface(this, descriptor);
    }
    
    @Override
    public boolean onTransact(int code, Parcel data, Parcel reply, int flags){
		//处理各种AMS的回调
	
	}
}
```

ContentProvider也是类似实现。内部Transport类继承自ContentProviderNative，ContentProviderNative也是一个继承自Binder的类。不止于此，其它还有很多类似的例子。


#### 2.应用开发者通过aidl使用Binder的例子

当我们通过aidl定义远程调用接口后，aidl.exe工具会帮助我们生成Binder调用模板代码，继承Stub类实现接口方法，可以用在服务端，在Service的onBinder方法返回Stub子类实现的对象。模板代码也用于客户端，主要使用asInterface，将远程调用Binder传入Proxy类，生成远程Binder的调用代理 。

aidl的方式，大大方便和简化了应用开发者使用Binder的难度。只需要按aidl的语法定义接口，就能自动生成规范的服务端与客户端进行Binder调用的代码。

aidl文件
```
interface IMultiCPCallback {
    String getUUID();
}
```

Service中bindService的时候，获取远程Binder调用代理。asInterface会将传入service(也就是远程Binder对象）到Proxy类中，Proxy类实现了CPCallback，用户通过mCPCallback调用的操作，都传递给了Proxy，Proxy持有远程调用Binder对象，Proxy通过调用远程调用Binder的对象，就可完成远程Binder调用。
```
    private CPCallback mCPCallback;
	
    private ServiceConnection connection = new ServiceConnection() {

        @Override
        public void onServiceDisconnected(ComponentName name) {
            mCPCallback=null;
        }

        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            mCPCallback = CPCallback.Stub.asInterface(service);
        }
    };

```


生成的Binder调用代码。
```

/*
 * This file is auto-generated.  DO NOT MODIFY.
 * Original file: D:\\MulticpSdk\\multicplibrary\\src\\main\\aidl\\com\\panxw\\aidl\\CPInterface.aidl
 */
package com.panxw.aidl;

public interface CPInterface extends android.os.IInterface {
    /**
     * Local-side IPC implementation stub class.（Client，也就是本地Binder实现类）
     */
    public static abstract class Stub extends android.os.Binder implements com.panxw.aidl.CPInterface {
        private static final java.lang.String DESCRIPTOR = "com.panxw.aidl.CPInterface";

        /**
         * Construct the stub at attach it to the interface.
         */
        public Stub() {
            this.attachInterface(this, DESCRIPTOR);
        }

        /**
         * Cast an IBinder object into an com.panxw.aidl.CPInterface interface,
         * generating a proxy if needed.
         */
        public static com.panxw.aidl.CPInterface asInterface(android.os.IBinder obj) {//服务连接后，获取远程Binder的调用代理。
            if ((obj == null)) {
                return null;
            }
            android.os.IInterface iin = obj.queryLocalInterface(DESCRIPTOR);
            if (((iin != null) && (iin instanceof com.panxw.aidl.CPInterface))) {
                return ((com.panxw.aidl.CPInterface) iin);
            }
            return new com.panxw.aidl.CPInterface.Stub.Proxy(obj);  //通过远程Binder对象obj生成远程调用代理类。
        }

        @Override
        public android.os.IBinder asBinder() {
            return this;
        }

        @Override
        public boolean onTransact(int code, android.os.Parcel data, android.os.Parcel reply, int flags) throws android.os.RemoteException {
            java.lang.String descriptor = DESCRIPTOR;
            switch (code) {
                case INTERFACE_TRANSACTION: {
                    reply.writeString(descriptor);
                    return true;
                }
                case TRANSACTION_getUUID: {
                    data.enforceInterface(descriptor);
                    java.lang.String _result = this.getUUID();//服务端Service继承Stub，实现定义服务接口，生成Binder对象，返回给onBinder
                    reply.writeNoException();
                    reply.writeString(_result);
                    return true;
                }
                default: {
                    return super.onTransact(code, data, reply, flags);
                }
            }
        }

        private static class Proxy implements com.panxw.aidl.CPInterface {
            private android.os.IBinder mRemote;

            Proxy(android.os.IBinder remote) {//参数就是远程Binder对象引用
                mRemote = remote;
            }

            @Override
            public android.os.IBinder asBinder() {
                return mRemote;
            }

            public java.lang.String getInterfaceDescriptor() {
                return DESCRIPTOR;
            }

            @Override
            public java.lang.String getUUID() throws android.os.RemoteException {
                android.os.Parcel _data = android.os.Parcel.obtain();
                android.os.Parcel _reply = android.os.Parcel.obtain();
                java.lang.String _result;
                try {
                    _data.writeInterfaceToken(DESCRIPTOR);
                    mRemote.transact(Stub.TRANSACTION_getUUID, _data, _reply, 0);//调用getUUID，能过远程Binder调用对象引用，向远程服务发起调用请求。
                    _reply.readException();
                    _result = _reply.readString();
                } finally {
                    _reply.recycle();
                    _data.recycle();
                }
                return _result;
            }
        }

        static final int TRANSACTION_getUUID = (android.os.IBinder.FIRST_CALL_TRANSACTION + 0);
    }

    public java.lang.String getUUID() throws android.os.RemoteException;
}
```