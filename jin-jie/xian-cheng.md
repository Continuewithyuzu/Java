---
description: >-
  参考
  https://www.cnblogs.com/XiaoLin-Java/p/14735926.html#:~:text=%E6%B2%A1%E6%9C%89%E9%82%A3%E4%B9%88%E5%BC%BA%E5%A4%A7%E3%80%82-,2.2%E3%80%81%E5%AE%9E%E7%8E%B0%20Runnable%20%E6%8E%A5%E5%8F%A3,%E7%94%A
---

# 线程

## 在 Java 中实现线程的方式有 2 种，一种是继承 Thread，一种是实现 Runnable 接口。

​ 如果一个进程没有任何线程，我们成为单线程应用程序；如果一个进程有多个线程存在，我们成为多线程应用程序。进程执行时一定会有一个主线程(main 线程)存在，主线程有能力创建其他线程。多个线程抢占 CPU，导致程序的运行轨迹不确定。多线程的运行结果也不确定。

### 2.1、继承Thread类 <a href="#id-21-ji-cheng-thread-lei" id="id-21-ji-cheng-thread-lei"></a>

​ 线程开启我们需要用到了`java.lang.Thread`类，API中该类中定义了有关线程的一些方法，具体如下：

> 构造方法

* `public Thread()`:分配一个新的线程对象。
* `public Thread(String name)`:分配一个指定名字的新的线程对象。
* `public Thread(Runnable target)`:分配一个带有指定目标新的线程对象。
* `public Thread(Runnable target,String name)`:分配一个带有指定目标新的线程对象并指定名字。

> 常用方法

* `public String getName()`:获取当前线程名称。
* `public void start()`:导致此线程开始执行; Java虚拟机调用此线程的run方法。
* `public void run()`:此线程要执行的任务在此处定义代码。
* `public static void sleep(long millis)`:使当前正在执行的线程以指定的毫秒数暂停（暂时停止执行）。
* `public static Thread currentThread()`:返回对当前正在执行的线程对象的引用。

​ 继承 Thread 实现多线程，**必须重写 run 方法**，**启动的时候调用的也是调用线程对象的start()方法来启动该线程**，_如果直接调用run()方法的话，相当于普通类的执行，此时相当于只有主线程在执行。_

看一个代码：

```java
public class myLearningThread {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start();

        for (int i=1;i<501;i++){
            System.out.println("MainThread"+i);
        }
    }

    public static class MyThread extends Thread{
        @Override
        public void run() {
            for (int i =1;i<501;i++){
                System.out.println("A Thread"+i);
            }
        }
    }
}
```

输出结果：

```
D:\Java_developtool\JDK17\bin\java.exe "-javaagent:D:\软件\IntelliJ IDEA 2023.3.1\lib\idea_rt.jar=39710:D:\软件\IntelliJ IDEA 2023.3.1\bin" -Dfile.encoding=UTF-8 -classpath D:\Java_code\Class\out\production\Class myLearningThread
MainThread1
MainThread2
MainThread3
MainThread4
MainThread5
MainThread6
MainThread7
MainThread8
MainThread9
MainThread10
MainThread11
MainThread12
MainThread13
MainThread14
MainThread15
MainThread16
MainThread17
MainThread18
MainThread19
MainThread20
MainThread21
MainThread22
MainThread23
MainThread24
MainThread25
MainThread26
MainThread27
MainThread28
MainThread29
MainThread30
MainThread31
MainThread32
A Thread1
A Thread2
MainThread33
MainThread34
A Thread3
MainThread35
MainThread36
A Thread4
A Thread5
MainThread37
MainThread38
A Thread6
MainThread39
A Thread7
A Thread8
A Thread9
A Thread10
A Thread11
A Thread12
MainThread40
A Thread13
A Thread14
A Thread15
MainThread41
MainThread42
MainThread43
MainThread44
MainThread45
MainThread46
MainThread47
MainThread48
MainThread49
A Thread16
A Thread17
A Thread18
A Thread19
A Thread20
A Thread21
A Thread22
A Thread23
A Thread24
A Thread25
A Thread26
A Thread27
A Thread28
MainThread50
A Thread29
A Thread30
A Thread31
A Thread32
A Thread33
A Thread34
A Thread35
A Thread36
A Thread37
A Thread38
A Thread39
A Thread40
A Thread41
A Thread42
A Thread43
A Thread44
A Thread45
A Thread46
A Thread47
MainThread51
MainThread52
MainThread53
MainThread54
MainThread55
MainThread56
MainThread57
MainThread58
MainThread59
MainThread60
MainThread61
MainThread62
MainThread63
MainThread64
MainThread65
MainThread66
MainThread67
MainThread68
MainThread69
MainThread70
MainThread71
MainThread72
MainThread73
MainThread74
MainThread75
MainThread76
MainThread77
MainThread78
MainThread79
MainThread80
MainThread81
MainThread82
MainThread83
MainThread84
MainThread85
MainThread86
MainThread87
MainThread88
MainThread89
MainThread90
MainThread91
A Thread48
MainThread92
A Thread49
A Thread50
A Thread51
A Thread52
A Thread53
A Thread54
A Thread55
A Thread56
A Thread57
A Thread58
A Thread59
A Thread60
A Thread61
A Thread62
A Thread63
A Thread64
A Thread65
A Thread66
A Thread67
A Thread68
MainThread93
MainThread94
MainThread95
A Thread69
A Thread70
MainThread96
A Thread71
MainThread97
MainThread98
MainThread99
MainThread100
MainThread101
MainThread102
MainThread103
MainThread104
MainThread105
MainThread106
MainThread107
MainThread108
MainThread109
MainThread110
MainThread111
MainThread112
MainThread113
MainThread114
MainThread115
MainThread116
MainThread117
MainThread118
MainThread119
MainThread120
MainThread121
MainThread122
MainThread123
MainThread124
MainThread125
MainThread126
MainThread127
MainThread128
MainThread129
MainThread130
MainThread131
MainThread132
MainThread133
MainThread134
MainThread135
MainThread136
MainThread137
MainThread138
MainThread139
MainThread140
MainThread141
MainThread142
MainThread143
MainThread144
MainThread145
MainThread146
MainThread147
MainThread148
MainThread149
MainThread150
MainThread151
MainThread152
MainThread153
MainThread154
MainThread155
MainThread156
MainThread157
MainThread158
MainThread159
MainThread160
MainThread161
MainThread162
MainThread163
MainThread164
MainThread165
MainThread166
MainThread167
MainThread168
MainThread169
A Thread72
A Thread73
A Thread74
A Thread75
A Thread76
A Thread77
A Thread78
A Thread79
A Thread80
A Thread81
A Thread82
A Thread83
A Thread84
A Thread85
A Thread86
A Thread87
A Thread88
A Thread89
A Thread90
A Thread91
A Thread92
A Thread93
A Thread94
A Thread95
A Thread96
A Thread97
A Thread98
A Thread99
A Thread100
A Thread101
A Thread102
A Thread103
A Thread104
A Thread105
A Thread106
A Thread107
A Thread108
A Thread109
A Thread110
A Thread111
A Thread112
A Thread113
A Thread114
A Thread115
A Thread116
A Thread117
A Thread118
A Thread119
A Thread120
A Thread121
A Thread122
A Thread123
A Thread124
A Thread125
A Thread126
A Thread127
A Thread128
A Thread129
A Thread130
A Thread131
A Thread132
A Thread133
A Thread134
A Thread135
A Thread136
A Thread137
A Thread138
A Thread139
MainThread170
A Thread140
A Thread141
A Thread142
A Thread143
A Thread144
A Thread145
A Thread146
MainThread171
A Thread147
MainThread172
MainThread173
MainThread174
MainThread175
MainThread176
MainThread177
MainThread178
MainThread179
MainThread180
MainThread181
MainThread182
MainThread183
MainThread184
MainThread185
MainThread186
MainThread187
MainThread188
MainThread189
MainThread190
MainThread191
MainThread192
MainThread193
MainThread194
MainThread195
MainThread196
MainThread197
MainThread198
MainThread199
MainThread200
MainThread201
MainThread202
MainThread203
MainThread204
MainThread205
MainThread206
MainThread207
MainThread208
MainThread209
MainThread210
MainThread211
MainThread212
MainThread213
MainThread214
MainThread215
MainThread216
MainThread217
MainThread218
MainThread219
MainThread220
MainThread221
MainThread222
MainThread223
MainThread224
MainThread225
MainThread226
MainThread227
MainThread228
MainThread229
MainThread230
MainThread231
MainThread232
MainThread233
MainThread234
MainThread235
MainThread236
MainThread237
MainThread238
MainThread239
MainThread240
MainThread241
MainThread242
MainThread243
MainThread244
A Thread148
A Thread149
A Thread150
A Thread151
A Thread152
A Thread153
A Thread154
A Thread155
A Thread156
A Thread157
A Thread158
A Thread159
A Thread160
A Thread161
A Thread162
A Thread163
A Thread164
A Thread165
A Thread166
A Thread167
A Thread168
A Thread169
A Thread170
A Thread171
A Thread172
A Thread173
A Thread174
A Thread175
A Thread176
A Thread177
A Thread178
A Thread179
A Thread180
A Thread181
A Thread182
A Thread183
A Thread184
A Thread185
A Thread186
A Thread187
A Thread188
A Thread189
A Thread190
A Thread191
A Thread192
A Thread193
A Thread194
A Thread195
A Thread196
A Thread197
A Thread198
A Thread199
A Thread200
A Thread201
A Thread202
A Thread203
A Thread204
A Thread205
A Thread206
A Thread207
A Thread208
A Thread209
A Thread210
A Thread211
A Thread212
A Thread213
A Thread214
A Thread215
A Thread216
A Thread217
A Thread218
A Thread219
A Thread220
A Thread221
A Thread222
A Thread223
A Thread224
A Thread225
A Thread226
A Thread227
A Thread228
A Thread229
A Thread230
A Thread231
A Thread232
A Thread233
A Thread234
A Thread235
A Thread236
A Thread237
A Thread238
A Thread239
A Thread240
A Thread241
A Thread242
A Thread243
A Thread244
A Thread245
A Thread246
A Thread247
A Thread248
A Thread249
A Thread250
A Thread251
A Thread252
A Thread253
A Thread254
A Thread255
A Thread256
A Thread257
A Thread258
A Thread259
A Thread260
A Thread261
A Thread262
A Thread263
A Thread264
A Thread265
A Thread266
A Thread267
A Thread268
A Thread269
MainThread245
MainThread246
MainThread247
MainThread248
MainThread249
MainThread250
MainThread251
MainThread252
MainThread253
MainThread254
MainThread255
A Thread270
A Thread271
A Thread272
A Thread273
A Thread274
A Thread275
A Thread276
A Thread277
A Thread278
A Thread279
MainThread256
MainThread257
MainThread258
MainThread259
MainThread260
MainThread261
MainThread262
MainThread263
MainThread264
MainThread265
A Thread280
A Thread281
A Thread282
A Thread283
A Thread284
A Thread285
A Thread286
A Thread287
A Thread288
A Thread289
A Thread290
A Thread291
A Thread292
A Thread293
A Thread294
A Thread295
A Thread296
A Thread297
A Thread298
A Thread299
A Thread300
A Thread301
A Thread302
A Thread303
A Thread304
A Thread305
A Thread306
A Thread307
A Thread308
A Thread309
A Thread310
A Thread311
A Thread312
A Thread313
A Thread314
A Thread315
A Thread316
A Thread317
A Thread318
A Thread319
A Thread320
A Thread321
A Thread322
A Thread323
A Thread324
A Thread325
A Thread326
A Thread327
A Thread328
A Thread329
A Thread330
A Thread331
A Thread332
A Thread333
A Thread334
A Thread335
A Thread336
A Thread337
A Thread338
A Thread339
A Thread340
A Thread341
A Thread342
A Thread343
A Thread344
A Thread345
A Thread346
A Thread347
A Thread348
A Thread349
A Thread350
A Thread351
A Thread352
A Thread353
A Thread354
A Thread355
A Thread356
A Thread357
A Thread358
A Thread359
A Thread360
A Thread361
A Thread362
A Thread363
A Thread364
A Thread365
A Thread366
A Thread367
A Thread368
A Thread369
A Thread370
A Thread371
A Thread372
A Thread373
A Thread374
A Thread375
A Thread376
A Thread377
A Thread378
A Thread379
A Thread380
A Thread381
A Thread382
A Thread383
A Thread384
A Thread385
A Thread386
A Thread387
A Thread388
A Thread389
A Thread390
A Thread391
A Thread392
A Thread393
A Thread394
A Thread395
A Thread396
A Thread397
A Thread398
A Thread399
A Thread400
A Thread401
A Thread402
A Thread403
A Thread404
A Thread405
A Thread406
A Thread407
A Thread408
A Thread409
A Thread410
A Thread411
A Thread412
A Thread413
A Thread414
A Thread415
A Thread416
A Thread417
A Thread418
A Thread419
A Thread420
A Thread421
A Thread422
A Thread423
A Thread424
A Thread425
A Thread426
A Thread427
A Thread428
A Thread429
A Thread430
A Thread431
A Thread432
A Thread433
A Thread434
A Thread435
A Thread436
A Thread437
A Thread438
A Thread439
A Thread440
A Thread441
A Thread442
A Thread443
A Thread444
A Thread445
A Thread446
A Thread447
A Thread448
A Thread449
A Thread450
A Thread451
A Thread452
A Thread453
A Thread454
A Thread455
A Thread456
A Thread457
A Thread458
A Thread459
A Thread460
A Thread461
A Thread462
A Thread463
A Thread464
A Thread465
A Thread466
A Thread467
A Thread468
A Thread469
A Thread470
A Thread471
A Thread472
A Thread473
A Thread474
A Thread475
A Thread476
A Thread477
A Thread478
A Thread479
A Thread480
A Thread481
A Thread482
A Thread483
A Thread484
A Thread485
A Thread486
A Thread487
A Thread488
A Thread489
A Thread490
A Thread491
A Thread492
A Thread493
A Thread494
A Thread495
A Thread496
A Thread497
A Thread498
A Thread499
A Thread500
MainThread266
MainThread267
MainThread268
MainThread269
MainThread270
MainThread271
MainThread272
MainThread273
MainThread274
MainThread275
MainThread276
MainThread277
MainThread278
MainThread279
MainThread280
MainThread281
MainThread282
MainThread283
MainThread284
MainThread285
MainThread286
MainThread287
MainThread288
MainThread289
MainThread290
MainThread291
MainThread292
MainThread293
MainThread294
MainThread295
MainThread296
MainThread297
MainThread298
MainThread299
MainThread300
MainThread301
MainThread302
MainThread303
MainThread304
MainThread305
MainThread306
MainThread307
MainThread308
MainThread309
MainThread310
MainThread311
MainThread312
MainThread313
MainThread314
MainThread315
MainThread316
MainThread317
MainThread318
MainThread319
MainThread320
MainThread321
MainThread322
MainThread323
MainThread324
MainThread325
MainThread326
MainThread327
MainThread328
MainThread329
MainThread330
MainThread331
MainThread332
MainThread333
MainThread334
MainThread335
MainThread336
MainThread337
MainThread338
MainThread339
MainThread340
MainThread341
MainThread342
MainThread343
MainThread344
MainThread345
MainThread346
MainThread347
MainThread348
MainThread349
MainThread350
MainThread351
MainThread352
MainThread353
MainThread354
MainThread355
MainThread356
MainThread357
MainThread358
MainThread359
MainThread360
MainThread361
MainThread362
MainThread363
MainThread364
MainThread365
MainThread366
MainThread367
MainThread368
MainThread369
MainThread370
MainThread371
MainThread372
MainThread373
MainThread374
MainThread375
MainThread376
MainThread377
MainThread378
MainThread379
MainThread380
MainThread381
MainThread382
MainThread383
MainThread384
MainThread385
MainThread386
MainThread387
MainThread388
MainThread389
MainThread390
MainThread391
MainThread392
MainThread393
MainThread394
MainThread395
MainThread396
MainThread397
MainThread398
MainThread399
MainThread400
MainThread401
MainThread402
MainThread403
MainThread404
MainThread405
MainThread406
MainThread407
MainThread408
MainThread409
MainThread410
MainThread411
MainThread412
MainThread413
MainThread414
MainThread415
MainThread416
MainThread417
MainThread418
MainThread419
MainThread420
MainThread421
MainThread422
MainThread423
MainThread424
MainThread425
MainThread426
MainThread427
MainThread428
MainThread429
MainThread430
MainThread431
MainThread432
MainThread433
MainThread434
MainThread435
MainThread436
MainThread437
MainThread438
MainThread439
MainThread440
MainThread441
MainThread442
MainThread443
MainThread444
MainThread445
MainThread446
MainThread447
MainThread448
MainThread449
MainThread450
MainThread451
MainThread452
MainThread453
MainThread454
MainThread455
MainThread456
MainThread457
MainThread458
MainThread459
MainThread460
MainThread461
MainThread462
MainThread463
MainThread464
MainThread465
MainThread466
MainThread467
MainThread468
MainThread469
MainThread470
MainThread471
MainThread472
MainThread473
MainThread474
MainThread475
MainThread476
MainThread477
MainThread478
MainThread479
MainThread480
MainThread481
MainThread482
MainThread483
MainThread484
MainThread485
MainThread486
MainThread487
MainThread488
MainThread489
MainThread490
MainThread491
MainThread492
MainThread493
MainThread494
MainThread495
MainThread496
MainThread497
MainThread498
MainThread499
MainThread500

进程已结束，退出代码为 0
```

​ 从结果我们可以看出，每一次抢占CPU资源的线程是不同的，多个线程轮流使用 CPU，谁先抢占到谁使用 CPU 并执行线程。所以执行结果不确定。

#### 2.1.1、继承Thread类的优点 <a href="#id-211-ji-cheng-thread-lei-de-you-dian" id="id-211-ji-cheng-thread-lei-de-you-dian"></a>

​ 编码简单

#### 2.1.2、继承Thread类的缺点 <a href="#id-212-ji-cheng-thread-lei-de-que-dian" id="id-212-ji-cheng-thread-lei-de-que-dian"></a>

​ 线程类已经继承了Thread类了就无法再继承其他类了，功能不能通过其他类继承拓展，功能没有那么强大。

***

### 2.2、实现 Runnable 接口 <a href="#id-22-shi-xian-runnable-jie-kou" id="id-22-shi-xian-runnable-jie-kou"></a>

​ 采用`java.lang.Runnable`也是非常常见的一种，我们只需要重写run方法即可。

​ 步骤如下：

1. 定义Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。
2. 创建Runnable实现类的实例，并以此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。
3. 调用线程对象的start()方法来启动线程
