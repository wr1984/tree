### 跑马灯效果中动画问题的处理




### Tree Grow

### GreenSock

- 静态方法

```
TweenLite.to( target:Object, duration:Number, vars:Object):TweenLite

功能：用来创建动画

参数：target:要创建动画的影片剪辑

        duration:动画持续的时间，以秒为单位（如果整个动画模式是基于帧的话则以帧为单位）

        vars：要参与动画的属性，以对象形式来写，比如{x:100,y:100,…},这些属性是动画完成的目标

例：TweenLite.to(mc, 1, {x:100});

   var myTween:TweenLite = new TweenLite(mc, 1, {x:100});  //以第一个代码效果相同

   var myTween:TweenLite = TweenLite.to(mc, 1, {x:100});   //以第一个代码效果相同


TweenLite.from( target:Object, duration:Number, vars:Object):TweenLite

功能：用来创建动画,与TweenLite.to不同的是，这个函数动画的属性目标是影片剪辑的现有属性，初始属性是vars设定的属性

参数：target:要创建动画的影片剪辑

        duration:动画持续的时间，以秒为单位（如果整个动画模式是基于帧的话则以帧为单位）

        vars：要参与动画的属性，以对象形式来写，比如{x:100,y:100,…},这些属性是动画的初始属性

例：TweenLite.from(mc, 1, {x:100});

 

TweenLite.delayedCall( delay:Number,onComplete:Function,onCompleteParams:Array = null, useFrames:Boolean = false):TweenLite

功能：用于在一定时间或一定帧数后自动执行一个函数，相当于一个延迟器吧

参数：delay:要延迟执行函数的时间（或是帧数）

        onComplete:要延迟执行的函数

        onCompleteParams：要延迟执行的函数的参数，以数组形式传入

        useFrames:指明是用时间还是帧数来记时

例：TweenLite.delayedCall(1, myFunction, ["param1", 2]);


TweenLite.killTweensOf( target:Object, complete:Boolean = false, vars:Object = null):void

功能：用来消除动画

参数：target:要消除动画的影片剪辑

        complete:如果为真则会在消除动画的同时把动画属性设为完成时的值，如果为假则不会

        vars：要消除动画的属性，以对象形式来写，比如{x:true,y:true,…},这些属性将不再参与动画

例：TweenLite.killTweensOf(mc, false, {alpha:true, x:true});

```

- 动画属性对象vars：

	
	delay:Number   在开始动画前要等待的时间,单位为秒（或帧数） 
	
	useFrames:Boolean   如果设为true则动画模式是基于帧的，否则是基于时间的（指的是动画函数中要指定时间的地方）
	
	ease:Function  缓动函数，默认为Quad.easeOut
	
	easeParams:Array 缓动函数的参数，以数组形式传入，注意只是有些缓动函数才需要需要参数的
	
	immediateRender:Boolean 当值为false时，
	
	overwrite:int  用来控制同一个对象上有多个动画时的覆盖之类的情况,tweenlite只有1和2这两种情况可选,具体请见OverwriteManager
	
	onInit:Function 当动画开始渲染（或是说开始运行时）前要执行的函数
	
	onInitParams:Array onInit函数的参数，以数组形式传入
	
	onStart:Function 当动画开始渲染时要执行的函数，有可能会被执行多次，因为动画时可以重复开始的
	
	onStartParams:Array onStart函数的参数，以数组形式传入
	
	onUpdate:Function 当每一次动画属性值发生变化时调用的函数
	
	onUpdateParams:Array  onUpdate函数的参数，以数组形式传入
	
	onComplete:Function 当动画执行完毕后要调用的函数
	
	onCompleteParams:Array  onComplete函数的参数，以数组形式传入
	
	onReverseComplete:Function  当一个动画被反转后又回到了原点时调用的函数
	
	onReverseComplete:Array  onReverseComplete函数的参数，以数组形式传入
	



- OverwriteManager

	NONE(0)  同一个物体上的动画之间不会被覆盖
	
	ALL_IMMEDIATE(1) 会立即覆盖之前的所有动画（包括运行的和没运行的），也是也tweenlite的默认模式，被覆盖的动画会保持覆盖那一刻的现状
	
	AUTO(2) 当动画开始运行时（即不包括延迟或暂停之类的）覆盖，且只会覆盖同一物体上的正在运行的动画中的有重叠的动画属性。是TweenMax、TimelineLite、TimelineMax的默认覆盖模式
	
	CONCURRENT(3) 当动画开始运行时覆盖，会覆盖同一物体上正在运行的所有动画
	
	ALL_ONSTART(4)  当动画开始运行时覆盖，会覆盖同一物体上的所有动画（包括运行的和没运行的）
	
	PREEXISTING(5)  当动画开始运行时覆盖，会覆盖同一物体上在本动画之前创建的所有动画（包括运行的和没运行的）
	
	可以使用OverwriteManager.init(OverwriteManager.AUTO);来给所有动画定义覆盖方式，如果想给不同动画定义不同覆盖方式，则在具体的vars对象中定义
	
	2、3、4、5类型都需要导入OverwriteManager类
	
### STweenMax的vars对象支持的属性

		delay:Number   在开始动画前要等待的时间,单位为秒（或帧数） 
		
		useFrames:Boolean   如果设为true则动画模式是基于帧的，否则是基于时间的（指的是动画函数中要指定时间的地方）
		
		ease:Function  缓动函数，默认为Quad.easeOut
		
		easeParams:Array 缓动函数的参数，以数组形式传入，注意只是有些缓动函数才需要需要参数的
		
		immediateRender:Boolean 当值为false时，
		
		overwrite:int  用来控制同一个对象上有多个动画时的覆盖之类的情况,tweenlite只有1和2这两种情况可选,具体请见OverwriteManager
		
		onInit:Function 当动画开始渲染（或是说开始运行时）前要执行的函数
		
		onInitParams:Array onInit函数的参数，以数组形式传入
		
		onStart:Function 当动画开始渲染时要执行的函数，有可能会被执行多次，因为动画时可以重复开始的
		
		onStartParams:Array onStart函数的参数，以数组形式传入
		
		onUpdate:Function 当每一次动画属性值发生变化时调用的函数
		
		onUpdateParams:Array  onUpdate函数的参数，以数组形式传入
		
		onComplete:Function 当动画执行完毕后要调用的函数
		
		onCompleteParams:Array  onComplete函数的参数，以数组形式传入
		
		onReverseComplete:Function  当一个动画被反转后又回到了原点时调用的函数
		
		onReverseComplete:Array  onReverseComplete函数的参数，以数组形式传入
		
		onRepeat:Function  当每次动画重新执行时要调用的函数
		
		onRepeatParams:Array   onRepeat函数的参数，以数组形式传入
		
		paused:Boolean   当值为真时，动画将会暂停播放
		
		reversed:Boolean  当值为真时，动画将会倒退播放，注意必须设置currentProgress为1或currentTime为动画持续时间，倒退播放才起作用
		
		repeat:int  设定动画的循环播放次数，要想无限循环请使用-1。循环的次数不包括动画的第一次播放
		
		repeatDelay：Number  设定动画每一次循环之间的间隔时间（或是帧），单位为妙
		
		yoyo:Boolean   当值为真时，动画循环的方式为： 向前播放-向后播放-向前播放，而如果yoyo为假的时候，循环的方式为:向前播放-回到原点向前播放。向后播放也会被算作一次循环。
		
		startAt:Object   设定动画的各种初始属性，以对象方式来写  


 

## TweenMax实例属性

		currentProgress:Number[读写]    用来读取或设置动画的当前进程，0表示开始，0.5表示一半，1表示结束，
		
		totalProgress:Number[读写]     用来读取或设置动画的当前进程，0表示开始，0.5表示一半，1表示结束，可读可写，与currentProgress不同的是，该属性是相对于动画整体而言的，即动画如果设置了循环，那循环的部分也会算在内
		
		currentTime:Number[写]   用来设置动画的当前时间，以秒（或帧）为单位，只可写。
		
		totalTime:Number [写]  用来设置动画的当前时间，以秒（或帧）为单位，只可写。该属性会把循环也算在内
		
		repeat:int[写] 用来设置动画重复（或者说循环）次数，当设为-1时为无限循环
		
		repeatDelay:Number[读写]  动画每次循环间隔的秒数（或帧数）
		
		yoyo:Boolean  与循环配合使用，当值为真时，循环模式为来回，即1-2-3,3-2-1,1-2-3,  当值为假时，循环模式为单向循环，即1-2-3,1-2-3,1-2-3
		
		timeScale:Number[读写]   用来读取或设置该实例动画的回放速率，例如1为正常速度，0.5为一半速度，2为2倍速度
		
		totalDuration:Number[读写]  用来设置或读取动画的持续秒数（或帧数），包括了所有循环、循环间隔所用的时间。
		
		duration:Number[读写]    用来设置或读取动画执行一次的持续秒数（或帧数），即不包括循环、循环间隔的时间。

 

### TweenMax实例方法

		complete( skipRender:Boolean = false, suppressEvents:Boolean = false ):void
		
		      说明：用来立刻完成动画
		
		      参数：skipRender：设为true的时候动画属性会停留在目前状态，为false时会设为最终状态
		
		              suppressEvents:当为true时，onComplete, onUpdate, onReverseComplete等事件不会触发
		
		killProperties( names:Array ):void
		
		      说明：用来删除某个动画中的动画属性,并且被删除的动画属性不会被设为最终状态
		
		      参数：names:要删除的动画属性，以数组形式传入，如["x","y"] 
		
		updateTo( vars:Object, resetDuration:Boolean = false ):void
		
		      说明：用来在动画创建后(或正在运行中)改变它的vars对象,如果使用了该方法，那么当 resetDuration为真且动画没在运行当中的时候会重新启动动画
		
		      参数：vars：要改变的属性
		
		              resetDuration：为真且动画没在运行的时候会重启动画，如果为假则不会重启动画

 

### TweenMax静态属性/方法

		globalTimeScale:Number[读写]   用来读取或设置所有动画的回放速率，例如1为正常速度，0.5为一半速度，2为2倍速度，能取的最小值为0.0001 
		
		killTweensOf()   //移除所有动画，并会把各种动画属性都设置到最终状态,无参数
		
		to( target:Object, duration:Number, vars:Object ):TweenMax
		
		         说明：与TweenLite.to()用法相同，不过功能有所增加，体现在vars的属性上
		
		from( target:Object, duration:Number, vars:Object ):TweenMax
		
		         说明：与TweenLite.from()用法相同，不过功能有所增加，体现在vars的属性上
		
		fromTo( target:Object, duration:Number, fromVars:Object, toVars:Object ):TweenMax
		
		        说明：与to()、from()用法差不多，只不过是从指定动画属性到指定动画属性，fromVars对象里只写初始化的要进行动画的属性，，其他的诸如delay、onUpdate等属性只能写在toVars对象里。
		
		allTo( targets:Array, duration:Number, vars:Object, stagger:Number = 0, onCompleteAll:Function = null, onCompleteAllParams:Array = null ):Array
		
		       说明：与to()用法差不多。不过这个函数能驱动多个显示对象。
		
		       参数：targets:要进行动画的显示对象，可以有多个，以数组形式传入
		
		               duration:动画持续的秒数（或帧数）
		
		               vars：设置动画的一些属性及其他参数
		
		               stagger:每个显示对象间的动画开始间隔秒数
		
		              onCompleteAll:当所有显示对象都完成动画后要调用的函数
		
		              onCompleteAllParams： onCompleteAll函数的参数，以数组形式传入
		
		allFrom( targets:Array, duration:Number, vars:Object, stagger:Number = 0, onCompleteAll:Function = null, onCompleteAllParams:Array = null ):Array
		
		     说明：与allTo()用法相同
		
		allFromTo( targets:Array, duration:Number, fromVars:Object, toVars:Object, stagger:Number = 0, onCompleteAll:Function = null, onCompleteAllParams:Array = null ):Array
		
		     说明:与fromTo()功能相同，只不过能驱动多个显示对象做动画，用法与allTo()、allFrom()相同
		
		delayedCall( delay:Number, onComplete:Function, onCompleteParams:Array = null, useFrames:Boolean = false ):TweenMax
		
		     说明：用于在一定时间（或帧数）后调用一个函数
		
		     参数：delay:要延迟的秒数（或帧数）
		
		             onComplete:要延迟执行的函数
		
		             onCompleteParams: onComplete的参数，以数组形式传入
		
		             useFrame:设定延迟的时间模式是基于秒数还是帧数
		
		getAllTweens()
		
		     说明：获取所有还没完成的动画实例，已经完成了的动画不会获取到。当autoRemoveChildren属性设为真的时候，已经完成的动画就不会再存在于时间轴上了
		
		getTweensOf( target:Object ):Array
		
		     说明：用来获取某个物体上的所有TweenLiteTweenMax对象
		
		     参数：target:目标物体    
		
		isTweening( target:object ):Boolean
		
		     说明：用来侦测某个物体是否在进行动画
		
		     参数：target:要侦测的物体
		
		killAll( complete:Boolean = false, tweens:Boolean = true, delayedCalls:Boolean = true ):void
		
		     说明：用来消除所有的动画和/或延迟函数
		
		     参数：complete:当为真时在动画或延迟函数消除前会完成执行
		
		             tweens:当为真时，会保留动画
		
		             delayedCalls：当为真时会保留延迟函数
		
		killChildTweensOf( parent:DisplayObjectContainer, complete:Boolean = false ):void
		
		     说明:用来消除一个显示对象容器内的所有子对象的动画
		
		     参数：parent:目标显示对象容器
		
		             complete:在动画消除前是否强制动画执行完
		
		pauseAll( tweens:Boolean = true, delayedCalls:Boolean = true ):void
		
		    说明：用来暂停所有动画或延迟函数
		
		    参数：tweens:如果为真则所有动画都会暂停
		
		            delayedCalls:如果为真则所有延迟函数都会暂停
		
		resumeAll( tweens:Boolean = true, delayedCalls:Boolean = true ):void
		
		     说明:用来继续所有暂停了的动画和延迟函数
		
		     参数：tweens:如果为真，所有暂停的动画都会继续
		
		             delayedCalls：如果为真，所有暂停的延迟函数都会继续
		             

### TimelineLite实例属性

currentProgress:Number[读写]  用来设置或读取动画的进程度.例如0表示开始，0.5表示一半，1表示完成。totalProgress在TimelineLite中与currentProgress含义相同，但在TimelineMax中，totalProgress会把循环以及循环间隔包括在内。

duration:Number[读写]   用来设置或读取Timeline持续的秒数（或帧数）

timeScale:Number[读写]  用来设置或读取时间轴的回放速率,比如0.5为一半速率，1为正常速度，2为2倍速度

totalDuration:Number[读写]  用来设置或读取总的持续时间（或帧数），包括循环和循环间隔的时间

useFrame:Boolean[读]  是否启用帧模式

 

### TimelineLite实例方法

TimelineLite( vars:Object = null )

TimelineLite类的构造函数。传入一个vars对象作为参数

 

append( tween:TweenCore, offset:Number = 0 ):TweenCore

       说明：在时间轴的末端添加一个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例

       参数：tween:要添加的TweenLite、TweenMax、TimelineLite、TimelineMax动画实例

               offset:相对于时间轴末端要偏移的秒数（或帧数），例如如果你想要添加的本段动画跟原本时间轴上的最后一段动画有3秒的间距，那你可以把这个参数设为3，又例如你想要添加的本段动画跟原本时间轴上的最后一段动画有2秒的重叠，那你可以把这个参数设为-2.

      该方法返回的是添加进去的动画实例

insert( tween:TweenCore, timeOrLabel:* = 0 ):TweenCore

      说明：在指定的时间、帧或标签中插入一个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例

      参数：tween: 要插入的TweenLite、TweenMax、TimelineLite、TimelineMax动画实例

              timeOrLabel：指定插入动画的时间点，可以是秒数（或帧数），和标签（以字符串表示）

      该方法返回的是插入进去的动画实例

appendMultiple( tweens:Array, offset:Number = 0, align:String = "normal", stagger:Number = 0 ):Array

      说明：可以一次添加多个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例到时间轴的末端。

      参数：tweens:一个包括了要添加的动画实例的数组

              offset:相对于时间轴末端要偏移的秒数（或帧数）

              align:添加的动画的排列模式，因为添加进去的有多个动画，所以要决定它们是如何排列的，有三中模式可选：TweenAlign.SEQUENCE:添加的动画会根据先后顺序一个接一个的依次排列；TweenAlign.START：把添加的所有动画重叠在一起，并且会忽略它们的delay；TweenAlign.NORMAL：把所有添加的动画重叠在一起，并且不会忽略它们的delay。

             stagger:添加进去的每个动画之间运行的时间间距，单位为秒

      该方法返回的是添加进去的动画实例数组

insertMultiple( tweens:Array, timeOrLabel:String = "0", align:Number = normal, stagger:* = 0 ):Array

      说明：一次性向指定的时间、帧数或标签插入多个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例，用法与appendMultiple相同，就不再累述

prepend( tween:TweenCore, adjustLabels:Boolean = false ):TweenCore

      说明：在时间轴的开始处插入一个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例，它会把后面的动画向后挤走

      参数：tween:要插入的动画实例

              adjustLabels：如果为true,那么时间轴上标签也会跟着被挤走的动画往后挪

      该方法返回插入的动画实例

prependMultiple( tweens:Array, align:String = "normal", stagger:Number = 0, adjustLabels:Boolean = false ):Array

      说明：一次性的在时间轴的开始处插入多个TweenLite、TweenMax、TimelineLite、TimelineMax动画实例，它会把后面的动画向后挤走。用法与appenfMultiple等相同

addLable( label:String, time:Number ):void

      说明：在时间轴上添加一个帧标签，以后gotoAndStop() gotoAndPlay()就可使直接使用这个标签作为参数了

      参数：label:标签名称

              time：指明要在哪个时间点（或帧数）上增加标签，单位为秒

removeLable( label:String ):Number

    说明：从时间轴上移除一个标签，并返回这个标签的时间点

    参数：lable:要移除的标签名称

goto( timeOrLabel:*, suppressEvents:Boolean = true ):void

     说明：相当于把播放头跳转到特定的时间点（或帧数）或标签，而且不会改变时间轴的暂停状态

     参数 ：timeOrLable:要跳转到的秒数（或帧数）或标签

              suppressEvents：如果为true,则播放头到达任何位置都不引起onComplete、onUpdate等事件的触发

gotoAndPlay( timeOrLabel:*, suppressEvents:Boolean = true ):void

     说明：把播放头跳转到指定的地方并从那里播放

     参数：timeOrLable:要跳转到的秒数（或帧数）或标签

             suppressEvents：如果为true,则播放头到达任何位置都不引起onComplete、onUpdate等事件的触发

gotoAndStop( timeOrLabel:*, suppressEvents:Boolean = true ):void

     说明：把播放头跳转到指定的地方并暂停时间轴

     参数：timeOrLable:要跳转到的秒数（或帧数）或标签

             suppressEvents：如果为true,则播放头到达任何位置都不引起onComplete、onUpdate等事件的触发

stop():void

     说明：暂停动画，应该不是停止

getChildren( nested:Boolean = true, tweens:Boolean = true, timelines:Boolean = true, ignoreBeforeTime:Number = -9999999999 ):Array

     说明：可以获取时间轴内的所有动画和时间轴实例，包括嵌套的

     参数：nested:如果为true，则嵌套的动画实例或时间轴实例也会包括在内，否则只会包括最顶层的

             tweens:如果为true,则会包括动画实例

             timelines:如果为true，则会包括时间轴实例

             ignoreBeforeTime: 开始时间少于这个数的动画或时间轴是例会被忽略

getLableTime( label:String ):Number

     说明：返回标签的时间点，如果标签不存在则返回-1

     参数：lable:目标标签名称

getTweensOf( target:Object, nested:Boolean = true ):Array

     说明： 返回特定物体上的动画实例

     参数：target:目标物体

             nested:如果为true，则动画中嵌套的时间轴实例也会返回

killTweensOf( target:Object, nested:Boolean = true, vars:Object = null ):Boolean

    说明：删除某个物体上的一个或多个动画

    参数：target:目标物体

            nested:是否影响到嵌套的动画

            vars:指明要删除的动画属性，如{alpha:true,x:true},如果省略该参数，则所有动画属性都会删除

remove( tween:TweenCore, skipDisable:Boolean = false ):void

    说明：从时间轴上移除一个TweenLite, TweenMax, TimelineLite, or TimelineMax实例

    参数：tween:要移除的TweenLite, TweenMax, TimelineLite, or TimelineMax实例

            skipDisable:一般不要去改变，保留它的默认值即可，是什么意义我也看不明白

clear( tweens:Array = null ):void

    说明：用来清空时间轴上的所有动画和时间轴实例，如果传入一个数组参数，则可以删除特定的动画

    参数：tweens:要删除的动画组成的数组

shiftChildren( amount:Number, adjustLabels:Boolean = false, ignoreBeforeTime:Number = 0 ):void

    说明：把时间轴中的所有动画的开始时间向后推一定的时间，以留出一定的空间

    参数：amount:要延长的秒数（或帧数）

            adjustLabels：如果true则时间轴上的lable也会相应调整

            ignoreBeforeTime：所有在这个在这个时间或这个时间之后开始的动画的开始时间都会向后推

invalidate()


