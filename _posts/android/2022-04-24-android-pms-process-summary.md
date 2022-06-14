---
layout: post
title: "Android PMS调用过程及关键代码"
date: 2022-04-24 00:00:00
category: "android"
tags: [Android, pms, process, summary]
---
#### 1.调用过程。
App层使用pms服务流程，先通过context的getPackageManager取得PackageManger对象后，再调用PackageManger相关操作方法完成相应处理。

而这个context实质是ContextImpl，在ActivityThread中创建应用时生成的。这个类提供了getPackageManager()，内部通过ActivityThread.getPackageManager()获得IPackageManager对象，再生成ApplicationPackageManager对象，返回给APP层。

PackageManger类是一个抽象类，ApplicationPackageManager继承自PackageManger，使用PMS服务对象进行封装，进而间接操作PMS服务，完成相应操作。

ActivityThread.getPackageManger()，是通过ServiceManager.getService()获取了PMS服务对象，再生成PMS服务代理对象，最后返回给ContextImpl。

#### 2.关键代码
PackageManagerService.java//实现PMS服务端接口，对客户端提供各种操作。
```
public class PackageManagerService extends IPackageManager.Stub { 

    @Override
    public boolean onTransact(int code, Parcel data, Parcel reply, int flags)
            throws RemoteException {
        try {
            return super.onTransact(code, data, reply, flags);
        } catch (RuntimeException e) {
            if (!(e instanceof SecurityException) && !(e instanceof IllegalArgumentException)) {
                Slog.wtf(TAG, "Package Manager Crash", e);
            }
            throw e;
        }
    }
	
	//main方法由SystemServer调用。
    public static final IPackageManager main(Context context, Installer installer,
            boolean factoryTest, boolean onlyCore) {
        PackageManagerService m = new PackageManagerService(context, installer,
                factoryTest, onlyCore);
        ServiceManager.addService("package", m); //注册服务
        return m;
    }
}
```

PackageManager.java //抽象类，作为Context的getPackageManager返回类型。
```
public abstract class PackageManager {


}
```

ApplicationPackageManager.java//继承自PackageManager，使用PMS对象封装各类操作。
```
final class ApplicationPackageManager extends PackageManager {
	private IPackageManager mPM; //PMS服务对象 
	
    ApplicationPackageManager(ContextImpl context,
                              IPackageManager pm) {
        mContext = context;
        mPM = pm;
    }

}
```

ContextImpl.java//ActivityThread中创建该对象，并通过getPackageManager返回ApplicationPackageManager对象给应用层。
```
class ContextImpl extends Context {

    @Override
    public PackageManager getPackageManager() {
        if (mPackageManager != null) {
            return mPackageManager;
        }

        IPackageManager pm = ActivityThread.getPackageManager(); //获取PMS服务
        if (pm != null) {
            // Doesn't matter if we make more than one instance.
            return (mPackageManager = new ApplicationPackageManager(this, pm));//使用PMS服务对像初始化ApplicationPackageManager
        }

        return null;
    }
	
}
```

ActivityThread.java //生成ContextImpl对象，及通过ServiceManager获取PMS服务对象。
```
public final class ActivityThread {

    public static IPackageManager getPackageManager() {
        if (sPackageManager != null) {
            //Slog.v("PackageManager", "returning cur default = " + sPackageManager);
            return sPackageManager;
        }
        IBinder b = ServiceManager.getService("package");//通过ServiceManager获取PMS服务对象。
        //Slog.v("PackageManager", "default service binder = " + b);
        sPackageManager = IPackageManager.Stub.asInterface(b); //返回服务调用代理 
        //Slog.v("PackageManager", "default service = " + sPackageManager);
        return sPackageManager;
    }


   private Context createBaseContextForActivity(ActivityClientRecord r,
            final Activity activity) {
        ContextImpl appContext = new ContextImpl(); //创建appContext， 生成ContextImpl对象。
        appContext.init(r.packageInfo, r.token, this);
        appContext.setOuterContext(activity);
		
	}
	
}
```



