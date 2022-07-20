---
layout: post
title: "CSharp Learn Tests"
date: 2022-07-16 20:05:01
category: "program"
tags: [CSharp]
---
```
using System; //all required
using System.Threading;//Threading
namespace RectangleApplication  //name space
{
	class Rectangle
	{
		// member variables 
		double length;
		double width;
		string name;

		//set virtual as could be overrided
		public virtual void Acceptdetails()
		{
			length = 4.5;    
			width = 3.5;
			name = "rectangle";
		}

		public double GetArea()
		{
			return length * width;
		}

		public string GetName(){
			return name;	
		}

		//set virtual as could be overrided
		public virtual void Display()
		{
			Console.WriteLine("Length: {0}", length);
			Console.WriteLine("Width: {0}", width);
			Console.WriteLine("Area: {0}", GetArea());
			Console.WriteLine("Name is{0}",GetName());
		}

	}

	//child class derived from Rectangle
	class MyRectangle:Rectangle{
		string version;

		//overide base 
		public override  void Acceptdetails(){
			base.Acceptdetails();
			version = "1.0 version";
		}

		//override base
		public override  void Display(){
			base.Display();
			Console.WriteLine("version: {0}",version);
		}
	}

	//it's a interface
	interface Observer{
		void onResult();	
	}

	//interface user
	class EventManager{
	Observer observer;

		public EventManager(Observer o){
			observer = o;	
		}

		private void CallToChildThread(){
			Console.WriteLine("execute in child thread");	
			Thread.Sleep(500);
			observer.onResult();
			Console.WriteLine("done");
		}

		public void Start(){
			ThreadStart childref = new ThreadStart(CallToChildThread);
			Thread childThread = new Thread(childref);
			childThread.Start();
		}
	}

	//interface implement class
	class MyObserver:Observer{
		public void onResult(){
			Console.WriteLine("onResult returned");	
		}
	}

  //test
	class TestClient
	{
		static void Main(string[] args)
		{
			Thread th = Thread.CurrentThread;
			th.Name = "MainThread";
			Console.WriteLine("threadName:{0}",th.Name);	

			//class
			Rectangle r = new Rectangle();
			r.Acceptdetails();
			r.Display();

			//class extneds and overide
			Rectangle mr = new MyRectangle();
			mr.Acceptdetails();
			mr.Display();

			//tests
			TestIfStatement();
			TestWhileStatement();
			TestForStatement();

			//EventManager and interface
			EventManager em = new EventManager(new MyObserver());
			em.Start();
			
			Console.ReadLine();
		}

		static void TestForStatement(){
			int i=0;
			int j=0;
			for(;i<10;i++){
				j=0;
				for(;j<2;j++){
					if(i*j%2==0){
						Console.WriteLine("{0} * {1} is odd",i,j);	
					}else{
						continue;	
					}
				}
			}
		}

		static void TestWhileStatement(){
			int a=1;
			int sum=0;
			while(a<100){
				sum+=a;	
				a++;
			}
			Console.WriteLine("sum={0}",sum);	
		}

		static void TestIfStatement(){
			bool flag = true;
			if(flag){
				Console.WriteLine("true");
			}else{
				Console.WriteLine("false");
			}
		}
	}
}

```
