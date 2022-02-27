---
layout: post
title: "synchronized方法、wait/notify与监视器"
date: 2012-05-29 20:05:01
category: "program"
tags: [java,同步]
---
名词解释：wait等待某个条件发生，而改变这个条件超出了当前方法的控制能力，常由另一个任务来改变。而notify和notifyAll则表示感兴趣的事件发生了，于是唤醒wait之后动作执行。<!-- more -->  
1.synchronized方法调用synchronized方法(同一锁时)，由外向内获取锁，由内向外释放锁。即在synchronized块类调用新的synchronized方法时，新的synchronized方法直接获取锁。  
2.同步代码中执行obj.wait()之后其它线程可获得监视器对象，否则另一个同步代码块就不能执行notify()或notifyAll()方法了。  
3.示例：  

```
public class Test {
 /**
  * notify通知wait唤醒
  * @param args
  */
 public static void main(String[] args) {
  final Object sync = new Object();
  new Thread(){
   public void run() {
	 synchronized (sync) { //同步块
	  try {
	   sync.wait(5*1000); //处于等待,5s
	   System.out.println("wait over...");
	  } catch (Exception e) {
	   System.out.println("err...");
	  }
	 }
   }
  }.start();

  try {
   Thread.sleep(4*1000); //通知等待提前1s唤醒
   synchronized (sync) { //同步块
	sync.notify(); 
	System.out.println("notify...");
   }
  } catch (InterruptedException e) {
   e.printStackTrace();
  }
 }
}
```
