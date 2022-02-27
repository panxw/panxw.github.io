---
layout: post
title: "消除Animation残余线条"
date: 2013-02-26 20:05:01
category: "android"
tags: [Animation,TranslateAnimation]
---
消除Animation残余线条办法：  
#### 1,继承TranslateAnimation或RotateAnimation，在applyTransformation中刷新动画parentView的界面。如：
```
private final class MyTranslateAnimation extends TranslateAnimation {
		private View backgroundView;

		public MyTranslateAnimation(View backgroundView, int fromXType, float fromXValue, int toXType, float toXValue,
				int fromYType, float fromYValue, int toYType, float toYValue) {
			super(fromXType, fromXValue, toXType, toXValue, fromYType, fromYValue, toYType, toYValue);
			this.backgroundView = backgroundView;
		}

		@Override
		protected void applyTransformation(float interpolatedTime, Transformation t) {
			super.applyTransformation(interpolatedTime, t);
			backgroundView.postInvalidate();
		}
}
```

#### 2,调用：
```
TranslateAnimation cardAnimation = new MyTranslateAnimation(backgroundView, Animation.RELATIVE_TO_PARENT, 0.01f,
				Animation.RELATIVE_TO_PARENT, 0.35f, Animation.RELATIVE_TO_PARENT, 0.1f, Animation.RELATIVE_TO_PARENT,
				0.1f);
cardAnimation.setDuration(2000);
cardAnimation.setRepeatCount(Animation.INFINITE);
cardAnimation.setRepeatMode(Animation.REVERSE);
imageView.setAnimation(cardAnimation);
```
