```
ROEMS = []
for model in model_list:
    for ft_pair in foldlist:
        # Fits model to fold within training data
        fitted_model = model.fit(ft_pair[0])
        # Generates predictions using fitted_model on respective CV test data
        predictions = fitted_model.transform(ft_pair[1])
        # Generates and prints a ROEM metric CV test data
        r = roem(spark, predictions, 'userId', 'viewed')
        print ("ROEM: ", r)

    # Fits model to all of training data and generates preds for test data
    v_fitted_model = model.fit(training)
    v_predictions = v_fitted_model.transform(test)
    v_ROEM = roem(spark, v_predictions, 'userId', 'viewed')

    # Adds validation ROEM to ROEM list
    ROEMS.append(v_ROEM)
    print ("Validation ROEM: ", v_ROEM)
```

<pre>[11279.031s][warning][gc,alloc] Executor task launch worker for task 5.0 in stage 306542.0 (TID 1267484): Retried waiting for GCLocker too often allocating 524290 words
23/05/08 20:40:47 ERROR Executor: Exception in task 5.0 in stage 306542.0 (TID 1267484)
java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)
23/05/08 20:40:47 ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker for task 5.0 in stage 306542.0 (TID 1267484),5,main]
java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)
23/05/08 20:40:47 WARN TaskSetManager: Lost task 5.0 in stage 306542.0 (TID 1267484) (192.168.0.102 executor driver): java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)

23/05/08 20:40:47 ERROR TaskSetManager: Task 5 in stage 306542.0 failed 1 times; aborting job
23/05/08 20:40:47 ERROR Instrumentation: org.apache.spark.SparkException: Job aborted due to stage failure: Task 5 in stage 306542.0 failed 1 times, most recent failure: Lost task 5.0 in stage 306542.0 (TID 1267484) (192.168.0.102 executor driver): java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)

Driver stacktrace:
	at org.apache.spark.scheduler.DAGScheduler.failJobAndIndependentStages(DAGScheduler.scala:2785)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2(DAGScheduler.scala:2721)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2$adapted(DAGScheduler.scala:2720)
	at scala.collection.mutable.ResizableArray.foreach(ResizableArray.scala:62)
	at scala.collection.mutable.ResizableArray.foreach$(ResizableArray.scala:55)
	at scala.collection.mutable.ArrayBuffer.foreach(ArrayBuffer.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.abortStage(DAGScheduler.scala:2720)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1$adapted(DAGScheduler.scala:1206)
	at scala.Option.foreach(Option.scala:407)
	at org.apache.spark.scheduler.DAGScheduler.handleTaskSetFailed(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.doOnReceive(DAGScheduler.scala:2984)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2923)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2912)
	at org.apache.spark.util.EventLoop$$anon$1.run(EventLoop.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.runJob(DAGScheduler.scala:971)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2263)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2284)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2303)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2328)
	at org.apache.spark.rdd.RDD.count(RDD.scala:1266)
	at org.apache.spark.ml.recommendation.ALS$.train(ALS.scala:995)
	at org.apache.spark.ml.recommendation.ALS.$anonfun$fit$1(ALS.scala:737)
	at org.apache.spark.ml.util.Instrumentation$.$anonfun$instrumented$1(Instrumentation.scala:191)
	at scala.util.Try$.apply(Try.scala:213)
	at org.apache.spark.ml.util.Instrumentation$.instrumented(Instrumentation.scala:191)
	at org.apache.spark.ml.recommendation.ALS.fit(ALS.scala:714)
	at jdk.internal.reflect.GeneratedMethodAccessor281.invoke(Unknown Source)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at py4j.reflection.MethodInvoker.invoke(MethodInvoker.java:244)
	at py4j.reflection.ReflectionEngine.invoke(ReflectionEngine.java:374)
	at py4j.Gateway.invoke(Gateway.java:282)
	at py4j.commands.AbstractCommand.invokeMethod(AbstractCommand.java:132)
	at py4j.commands.CallCommand.execute(CallCommand.java:79)
	at py4j.ClientServerConnection.waitForCommands(ClientServerConnection.java:182)
	at py4j.ClientServerConnection.run(ClientServerConnection.java:106)
	at java.base/java.lang.Thread.run(Thread.java:829)
Caused by: java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.&lt;init&gt;(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	... 1 more
</pre>

<pre>
Last executed at 2023-05-08 20:40:48 in 1h 3m 5s

                                                                                

ROEM:  0.14075444631558656

                                                                                

ROEM:  0.1366260682401408

                                                                                

ROEM:  0.13587507904701498

                                                                                

ROEM:  0.13803017572633478

                                                                                

ROEM:  0.13727506550611898
Validation ROEM:  0.1356706037872063

                                                                                

ROEM:  0.14474120764282794

                                                                                

ROEM:  0.14136984923590126

                                                                                

ROEM:  0.14153907725813322

                                                                                

ROEM:  0.1425040414393903

                                                                                

ROEM:  0.14213708187268603
Validation ROEM:  0.14117375967652315

                                                                                

ROEM:  0.14787772094503449

                                                                                

ROEM:  0.14582085321894883

                                                                                

ROEM:  0.14546634585062665

                                                                                

ROEM:  0.14547138894507203

                                                                                

ROEM:  0.14576846084327386
Validation ROEM:  0.14448727511458756

                                                                                

ROEM:  0.15010971998534908

                                                                                

ROEM:  0.14879013993007492

                                                                                

ROEM:  0.14849746986113657

                                                                                

ROEM:  0.14861044049793995

                                                                                

ROEM:  0.14908673632892938
Validation ROEM:  0.14678156134309708

                                                                                

ROEM:  0.14019821815420547

                                                                                

ROEM:  0.1362020837389854

                                                                                

ROEM:  0.13529030682079363

                                                                                

ROEM:  0.13749499807654314

                                                                                

ROEM:  0.13614914347772858
Validation ROEM:  0.13541369900884595

                                                                                

ROEM:  0.14464710808279396

                                                                                

ROEM:  0.1412678623018499

                                                                                

ROEM:  0.14092978688319352

                                                                                

ROEM:  0.14218449267347982

                                                                                

ROEM:  0.14183856914856727
Validation ROEM:  0.14088464964359562

                                                                                

ROEM:  0.1474837286434754

                                                                                

ROEM:  0.1453543190151252

                                                                                

ROEM:  0.14532977859279456

                                                                                

ROEM:  0.14519046579947673

                                                                                

ROEM:  0.1456743446865356
Validation ROEM:  0.14407571555841692

                                                                                

ROEM:  0.14962451343322805

                                                                                

ROEM:  0.14853303474454027

                                                                                

ROEM:  0.14827237118549288

                                                                                

ROEM:  0.1484884995391164

                                                                                

ROEM:  0.14885659551465522
Validation ROEM:  0.14655899139392675

                                                                                

ROEM:  0.13972291094185163

                                                                                

ROEM:  0.13587406645907843

                                                                                

ROEM:  0.13469387369580538

                                                                                

ROEM:  0.13714445626122634

                                                                                

ROEM:  0.1355426420033938
Validation ROEM:  0.1350744047682236

                                                                                

ROEM:  0.14414814152369987

                                                                                

ROEM:  0.14138761417097992

                                                                                

ROEM:  0.14058103215748866

                                                                                

ROEM:  0.14155119897645532

                                                                                

ROEM:  0.14146009287407257
Validation ROEM:  0.13989077516513135

                                                                                

ROEM:  0.14720525709606505

                                                                                

ROEM:  0.1451015107875736

                                                                                

ROEM:  0.14513638496380535

                                                                                

ROEM:  0.14492011668583496

                                                                                

ROEM:  0.14542563219589352
Validation ROEM:  0.1434378863064021

                                                                                

ROEM:  0.1496092741722379

                                                                                

ROEM:  0.148281386450234

                                                                                

ROEM:  0.14794663059499738

                                                                                

ROEM:  0.14822922769500935

                                                                                

ROEM:  0.14843190668939438
Validation ROEM:  0.1463564857954985

                                                                                

ROEM:  0.13796081943628652

                                                                                

ROEM:  0.13526207599481482

                                                                                

ROEM:  0.13409025581671116

                                                                                

ROEM:  0.13677556816198566

                                                                                

ROEM:  0.13499374656016197
Validation ROEM:  0.1343385952686181

                                                                                

ROEM:  0.14228490616005407

                                                                                

ROEM:  0.1397363660003981

                                                                                

ROEM:  0.14122110455848771

                                                                                

ROEM:  0.1415212349066756

                                                                                

ROEM:  0.13981777558580716
Validation ROEM:  0.1391771431529088

                                                                                

ROEM:  0.14621723375671666

                                                                                

ROEM:  0.14310239095583083

                                                                                

ROEM:  0.14561327985699607

                                                                                

ROEM:  0.14399642809519833

                                                                                

ROEM:  0.14408000067334767
Validation ROEM:  0.14356550281596386

                                                                                

ROEM:  0.14790029075754108

                                                                                

ROEM:  0.14647320853340687

                                                                                

ROEM:  0.14734664749892595

                                                                                

ROEM:  0.14706065497571946

                                                                                

ROEM:  0.14718975240583512
Validation ROEM:  0.14568970741407852

                                                                                

ROEM:  0.13712732664765134

                                                                                

ROEM:  0.1338008238685355

                                                                                

ROEM:  0.1342623036071822

                                                                                

ROEM:  0.13485871938600116

                                                                                

ROEM:  0.13492171664698918
Validation ROEM:  0.13471832454985044

                                                                                

ROEM:  0.14224987077882117

                                                                                

ROEM:  0.13947178039683164

                                                                                

ROEM:  0.14057615209005792

                                                                                

ROEM:  0.14078212958163752

                                                                                

ROEM:  0.13955013182459458
Validation ROEM:  0.13909752124898508

                                                                                

ROEM:  0.14594822972586996

                                                                                

ROEM:  0.14295722619789786

                                                                                

ROEM:  0.14520842400430725

                                                                                

ROEM:  0.14397501106230304

                                                                                

ROEM:  0.14368108989261794
Validation ROEM:  0.14245180535870675

                                                                                

ROEM:  0.14768734201509723

                                                                                

ROEM:  0.14638168124685066

                                                                                

ROEM:  0.14727811896047438

                                                                                

ROEM:  0.14677769949371325

                                                                                

ROEM:  0.14729989363321047
Validation ROEM:  0.14547319045041823

                                                                                

ROEM:  0.13614814207316286

                                                                                

ROEM:  0.1338463147968812

                                                                                

ROEM:  0.13440918696538023

                                                                                

ROEM:  0.1348590462766799

                                                                                

ROEM:  0.13274683977530782
Validation ROEM:  0.1338716318423406

                                                                                

ROEM:  0.14184484240333214

                                                                                

ROEM:  0.13848100382759634

                                                                                

ROEM:  0.14015128231613563

                                                                                

ROEM:  0.14068581370803743

                                                                                

ROEM:  0.1397539457417071
Validation ROEM:  0.13804181009567218

                                                                                

ROEM:  0.14585711958614325

                                                                                

ROEM:  0.1421918880227014

                                                                                

ROEM:  0.14489084876556446

                                                                                

ROEM:  0.1439618799075979

                                                                                

ROEM:  0.14376430858845535
Validation ROEM:  0.14224219948426634

                                                                                

ROEM:  0.14771222586350324

                                                                                

ROEM:  0.14609596813380674

                                                                                

ROEM:  0.1474452556523798

                                                                                

ROEM:  0.14686759846464034

                                                                                

ROEM:  0.14690260420899331
Validation ROEM:  0.14500060035674503

                                                                                

ROEM:  0.13630524144915526

                                                                                

ROEM:  0.13303480210571142

                                                                                

ROEM:  0.13439617913746343

                                                                                

ROEM:  0.134522632990394

                                                                                

ROEM:  0.1343472247718771
Validation ROEM:  0.1334067210359182

                                                                                

ROEM:  0.14127081978546785

                                                                                

ROEM:  0.13799625559927614

                                                                                

ROEM:  0.14113872575017403

                                                                                

ROEM:  0.1417371427171356

                                                                                

ROEM:  0.1397773788321236
Validation ROEM:  0.13848925953604233

                                                                                

ROEM:  0.14487488250861086

                                                                                

ROEM:  0.14295316540788502

                                                                                

ROEM:  0.14457743712579982

                                                                                

ROEM:  0.1440196703068042

                                                                                

ROEM:  0.1428436740974294
Validation ROEM:  0.1422252570175789

                                                                                

ROEM:  0.14618164878349324

                                                                                

ROEM:  0.14696765948241153

                                                                                

ROEM:  0.14706688105837082

                                                                                

ROEM:  0.14644857431806016

                                                                                

ROEM:  0.14656384051123583
Validation ROEM:  0.14494204575719402

                                                                                

ROEM:  0.13513358048844662

                                                                                

ROEM:  0.13322432657380942

                                                                                

ROEM:  0.13502744053708216

                                                                                

ROEM:  0.13304393960156752

                                                                                

ROEM:  0.13401702680083136
Validation ROEM:  0.13347049351007884

                                                                                

ROEM:  0.14129340255814768

                                                                                

ROEM:  0.13801230477223284

                                                                                

ROEM:  0.14007605893587596

                                                                                

ROEM:  0.14106504726780925

                                                                                

ROEM:  0.13858765814168955
Validation ROEM:  0.1390813667010956

                                                                                

ROEM:  0.14442436747312118

                                                                                

ROEM:  0.14249171822740536

                                                                                

ROEM:  0.1443935038096058

                                                                                

ROEM:  0.14365960703476846

                                                                                

ROEM:  0.14243201680710446
Validation ROEM:  0.14168486896867866

                                                                                

ROEM:  0.1473325382394709

                                                                                

ROEM:  0.14659636012060434

                                                                                

ROEM:  0.14709282289548076

                                                                                

ROEM:  0.14617223505881488

                                                                                

ROEM:  0.14647170681040608
Validation ROEM:  0.14430813562044825

                                                                                

ROEM:  0.13466912698880706

                                                                                

ROEM:  0.13232663870587177

                                                                                

ROEM:  0.1350393888144444

                                                                                

ROEM:  0.13380892312741813

                                                                                

ROEM:  0.1323875362992172
Validation ROEM:  0.13213061178669902

                                                                                

ROEM:  0.14123878523184089

                                                                                

ROEM:  0.13739883013888368

                                                                                

ROEM:  0.1385883203851163

                                                                                

ROEM:  0.14077100623400096

                                                                                

ROEM:  0.1379183026702101
Validation ROEM:  0.13787015974315495

                                                                                

ROEM:  0.14468226297919803

                                                                                

ROEM:  0.14159150427403006

                                                                                

ROEM:  0.14422902754129166

                                                                                

ROEM:  0.1434371301044384

                                                                                

ROEM:  0.14210798565264746
Validation ROEM:  0.14159465659159928

                                                                                

ROEM:  0.14735317470734158

                                                                                

ROEM:  0.14618544979284318

                                                                                

ROEM:  0.14707934930421399

                                                                                

ROEM:  0.1461067169749615

                                                                                

ROEM:  0.14632106007668105
Validation ROEM:  0.14385549802664638

                                                                                

ROEM:  0.13482531638852066

                                                                                

ROEM:  0.1317508241242193

                                                                                

ROEM:  0.13436232199034456

                                                                                

ROEM:  0.13382551936456996

                                                                                

ROEM:  0.13446683364007714
Validation ROEM:  0.13309966729757927

                                                                                

ROEM:  0.14086442985731615

                                                                                

ROEM:  0.13726199827730248

                                                                                

ROEM:  0.14056327507114325

                                                                                

ROEM:  0.14121763768468198

                                                                                

ROEM:  0.13948570843126262
Validation ROEM:  0.13776394257702881

                                                                                

ROEM:  0.14427914484717405

                                                                                

ROEM:  0.14243989262001763

                                                                                

ROEM:  0.14410531054740522

                                                                                

ROEM:  0.14380280349474836

                                                                                

ROEM:  0.14303453502473734
Validation ROEM:  0.14275087018928698

                                                                                

ROEM:  0.14551372043393454

                                                                                

ROEM:  0.1468200795213993

                                                                                

ROEM:  0.14698714054110132

                                                                                

ROEM:  0.1464906347828224

                                                                                

ROEM:  0.14617534701219623
Validation ROEM:  0.1443891257838943

                                                                                

ROEM:  0.13426856957367048

                                                                                

ROEM:  0.13215008096151645

                                                                                

ROEM:  0.13533184320439007

                                                                                

ROEM:  0.13394302648582174

                                                                                

ROEM:  0.1342537653545996
Validation ROEM:  0.132037111036605

                                                                                

ROEM:  0.14112805315955637

                                                                                

ROEM:  0.13740898514864355

                                                                                

ROEM:  0.13893053561042604

                                                                                

ROEM:  0.14087872608817734

                                                                                

ROEM:  0.1382047057329449
Validation ROEM:  0.13906390564772544

                                                                                

ROEM:  0.1440623003983431

                                                                                

ROEM:  0.14167190859386414

                                                                                

ROEM:  0.1450252423894533

                                                                                

ROEM:  0.14342171369098033

                                                                                

ROEM:  0.14238282128271068
Validation ROEM:  0.14160038153815754

                                                                                

ROEM:  0.1473883819032361

                                                                                

ROEM:  0.14621074425577743

                                                                                

ROEM:  0.14656703476031185

                                                                                

ROEM:  0.14622460012395486

                                                                                

ROEM:  0.14617332673745204
Validation ROEM:  0.14411560615286237

                                                                                

ROEM:  0.13493774709030285

                                                                                

ROEM:  0.1314396871093259

                                                                                

ROEM:  0.13553851299039862

                                                                                

ROEM:  0.13351820744020726

                                                                                

ROEM:  0.13273544448624452
Validation ROEM:  0.13100922346243624

                                                                                

ROEM:  0.1412759495266229

                                                                                

ROEM:  0.13574772876910032

                                                                                

ROEM:  0.13812731534429284

                                                                                

ROEM:  0.1404529726562612

                                                                                 10]

ROEM:  0.13778241938855273
Validation ROEM:  0.13756080332977205

                                                                                

ROEM:  0.1444476041139634

                                                                                

ROEM:  0.1414237254730001

                                                                                

ROEM:  0.14388797530617428

                                                                                

ROEM:  0.14329700398464415

                                                                                

ROEM:  0.14225741552822907
Validation ROEM:  0.1414115412080316

                                                                                

ROEM:  0.1473432609582149

                                                                                

ROEM:  0.14615981109803297

                                                                                

ROEM:  0.14645039079316927

                                                                                

ROEM:  0.14610911568407534

                                                                                

ROEM:  0.146030561165105
Validation ROEM:  0.14352995077920838

                                                                                

ROEM:  0.14062174182653855

                                                                                

ROEM:  0.1381385459165038

                                                                                

ROEM:  0.14042326342659514

                                                                                

ROEM:  0.14032011131158326

                                                                                

ROEM:  0.1416335775424265

                                                                                

Validation ROEM:  0.1377601344451865

                                                                                

ROEM:  0.14475442444761058

                                                                                

ROEM:  0.1432294374712842

                                                                                

ROEM:  0.14528969565320635

                                                                                

ROEM:  0.1443605507698997

                                                                                

ROEM:  0.1456729290819688
Validation ROEM:  0.14262421166592165

                                                                                

ROEM:  0.1481757608047826

                                                                                

ROEM:  0.14676726290450354

                                                                                

ROEM:  0.14723309129516451

                                                                                

ROEM:  0.1468012503282945

                                                                                

ROEM:  0.14721795480473637
Validation ROEM:  0.1454819414730046

                                                                                

ROEM:  0.1511769593614862

                                                                                / 10]

ROEM:  0.14829585803180634

                                                                                

ROEM:  0.148896252290622

                                                                                

ROEM:  0.1487365436523227

                                                                                

ROEM:  0.1493184411731114
Validation ROEM:  0.1475648868494274

                                                                                

ROEM:  0.1403502358773718

                                                                                / 10]

ROEM:  0.1376942686177383

                                                                                

ROEM:  0.14009278830211294

                                                                                 10]

ROEM:  0.1404493589741552

                                                                                

ROEM:  0.14109589964394512
Validation ROEM:  0.1366749374667511

                                                                                

ROEM:  0.14454477911283045

                                                                                

ROEM:  0.14275127207061922

                                                                                

ROEM:  0.14502951395391814

                                                                                

ROEM:  0.1439432350591918

                                                                                

ROEM:  0.145409072214155
Validation ROEM:  0.1421168091153328

                                                                                

ROEM:  0.14778241996289304

                                                                                

ROEM:  0.14639462771149886

                                                                                / 10]

ROEM:  0.146813212084954

                                                                                

ROEM:  0.1464167673387454

                                                                                

ROEM:  0.1471167969452916
Validation ROEM:  0.1453298318451925

                                                                                 10]

ROEM:  0.1507645327859672

                                                                                

ROEM:  0.14829225469810267

                                                                                

ROEM:  0.14851388759388479

                                                                                

ROEM:  0.1484997775860503

                                                                                

ROEM:  0.14923064039921852
Validation ROEM:  0.14730199092615556

                                                                                

ROEM:  0.13970881497676546

                                                                                

ROEM:  0.1371373952728534

                                                                                

ROEM:  0.13938859930232914

                                                                                

ROEM:  0.1400936142673354

                                                                                

ROEM:  0.14080921369559335
Validation ROEM:  0.13595356065213066

                                                                                

ROEM:  0.14432985605092197

                                                                                

ROEM:  0.14266840469491898

                                                                                

ROEM:  0.14481737047551022

                                                                                

ROEM:  0.143606357047121

                                                                                

ROEM:  0.14511111325519194
Validation ROEM:  0.14170326635056904

                                                                                

ROEM:  0.14759668382139546

                                                                                

ROEM:  0.14581754186044532

                                                                                

ROEM:  0.1464932286873134

                                                                                

ROEM:  0.14626077201100046

                                                                                / 10]

ROEM:  0.1469395468544492
Validation ROEM:  0.14495838427521485

                                                                                 10]

ROEM:  0.1504139618182735

                                                                                 10]

ROEM:  0.14804548149780344

                                                                                 10]

ROEM:  0.148166770280866

                                                                                

ROEM:  0.14836644173448352

                                                                                

ROEM:  0.14909750921864737
[11279.031s][warning][gc,alloc] Executor task launch worker for task 5.0 in stage 306542.0 (TID 1267484): Retried waiting for GCLocker too often allocating 524290 words

23/05/08 20:40:47 ERROR Executor: Exception in task 5.0 in stage 306542.0 (TID 1267484)
java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)
23/05/08 20:40:47 ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker for task 5.0 in stage 306542.0 (TID 1267484),5,main]
java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)
23/05/08 20:40:47 WARN TaskSetManager: Lost task 5.0 in stage 306542.0 (TID 1267484) (192.168.0.102 executor driver): java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)

23/05/08 20:40:47 ERROR TaskSetManager: Task 5 in stage 306542.0 failed 1 times; aborting job
23/05/08 20:40:47 ERROR Instrumentation: org.apache.spark.SparkException: Job aborted due to stage failure: Task 5 in stage 306542.0 failed 1 times, most recent failure: Lost task 5.0 in stage 306542.0 (TID 1267484) (192.168.0.102 executor driver): java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)

Driver stacktrace:
	at org.apache.spark.scheduler.DAGScheduler.failJobAndIndependentStages(DAGScheduler.scala:2785)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2(DAGScheduler.scala:2721)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2$adapted(DAGScheduler.scala:2720)
	at scala.collection.mutable.ResizableArray.foreach(ResizableArray.scala:62)
	at scala.collection.mutable.ResizableArray.foreach$(ResizableArray.scala:55)
	at scala.collection.mutable.ArrayBuffer.foreach(ArrayBuffer.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.abortStage(DAGScheduler.scala:2720)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1$adapted(DAGScheduler.scala:1206)
	at scala.Option.foreach(Option.scala:407)
	at org.apache.spark.scheduler.DAGScheduler.handleTaskSetFailed(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.doOnReceive(DAGScheduler.scala:2984)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2923)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2912)
	at org.apache.spark.util.EventLoop$$anon$1.run(EventLoop.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.runJob(DAGScheduler.scala:971)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2263)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2284)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2303)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2328)
	at org.apache.spark.rdd.RDD.count(RDD.scala:1266)
	at org.apache.spark.ml.recommendation.ALS$.train(ALS.scala:995)
	at org.apache.spark.ml.recommendation.ALS.$anonfun$fit$1(ALS.scala:737)
	at org.apache.spark.ml.util.Instrumentation$.$anonfun$instrumented$1(Instrumentation.scala:191)
	at scala.util.Try$.apply(Try.scala:213)
	at org.apache.spark.ml.util.Instrumentation$.instrumented(Instrumentation.scala:191)
	at org.apache.spark.ml.recommendation.ALS.fit(ALS.scala:714)
	at jdk.internal.reflect.GeneratedMethodAccessor281.invoke(Unknown Source)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at py4j.reflection.MethodInvoker.invoke(MethodInvoker.java:244)
	at py4j.reflection.ReflectionEngine.invoke(ReflectionEngine.java:374)
	at py4j.Gateway.invoke(Gateway.java:282)
	at py4j.commands.AbstractCommand.invokeMethod(AbstractCommand.java:132)
	at py4j.commands.CallCommand.execute(CallCommand.java:79)
	at py4j.ClientServerConnection.waitForCommands(ClientServerConnection.java:182)
	at py4j.ClientServerConnection.run(ClientServerConnection.java:106)
	at java.base/java.lang.Thread.run(Thread.java:829)
Caused by: java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	... 1 more

---------------------------------------------------------------------------
Py4JJavaError                             Traceback (most recent call last)
Cell In[12], line 13
     10     print ("ROEM: ", r)
     12 # Fits model to all of training data and generates preds for test data
---> 13 v_fitted_model = model.fit(training)
     14 v_predictions = v_fitted_model.transform(test)
     15 v_ROEM = roem(spark, v_predictions, 'userId', 'viewed')

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/pyspark/ml/base.py:205, in Estimator.fit(self, dataset, params)
    203         return self.copy(params)._fit(dataset)
    204     else:
--> 205         return self._fit(dataset)
    206 else:
    207     raise TypeError(
    208         "Params must be either a param map or a list/tuple of param maps, "
    209         "but got %s." % type(params)
    210     )

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/pyspark/ml/wrapper.py:381, in JavaEstimator._fit(self, dataset)
    380 def _fit(self, dataset: DataFrame) -> JM:
--> 381     java_model = self._fit_java(dataset)
    382     model = self._create_model(java_model)
    383     return self._copyValues(model)

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/pyspark/ml/wrapper.py:378, in JavaEstimator._fit_java(self, dataset)
    375 assert self._java_obj is not None
    377 self._transfer_params_to_java()
--> 378 return self._java_obj.fit(dataset._jdf)

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/py4j/java_gateway.py:1322, in JavaMember.__call__(self, *args)
   1316 command = proto.CALL_COMMAND_NAME +\
   1317     self.command_header +\
   1318     args_command +\
   1319     proto.END_COMMAND_PART
   1321 answer = self.gateway_client.send_command(command)
-> 1322 return_value = get_return_value(
   1323     answer, self.gateway_client, self.target_id, self.name)
   1325 for temp_arg in temp_args:
   1326     if hasattr(temp_arg, "_detach"):

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/pyspark/errors/exceptions/captured.py:169, in capture_sql_exception.<locals>.deco(*a, **kw)
    167 def deco(*a: Any, **kw: Any) -> Any:
    168     try:
--> 169         return f(*a, **kw)
    170     except Py4JJavaError as e:
    171         converted = convert_exception(e.java_exception)

File ~/miniconda3/envs/dev/lib/python3.10/site-packages/py4j/protocol.py:326, in get_return_value(answer, gateway_client, target_id, name)
    324 value = OUTPUT_CONVERTER[type](answer[2:], gateway_client)
    325 if answer[1] == REFERENCE_TYPE:
--> 326     raise Py4JJavaError(
    327         "An error occurred while calling {0}{1}{2}.\n".
    328         format(target_id, ".", name), value)
    329 else:
    330     raise Py4JError(
    331         "An error occurred while calling {0}{1}{2}. Trace:\n{3}\n".
    332         format(target_id, ".", name, value))

Py4JJavaError: An error occurred while calling o194.fit.
: org.apache.spark.SparkException: Job aborted due to stage failure: Task 5 in stage 306542.0 failed 1 times, most recent failure: Lost task 5.0 in stage 306542.0 (TID 1267484) (192.168.0.102 executor driver): java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:829)

Driver stacktrace:
	at org.apache.spark.scheduler.DAGScheduler.failJobAndIndependentStages(DAGScheduler.scala:2785)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2(DAGScheduler.scala:2721)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$abortStage$2$adapted(DAGScheduler.scala:2720)
	at scala.collection.mutable.ResizableArray.foreach(ResizableArray.scala:62)
	at scala.collection.mutable.ResizableArray.foreach$(ResizableArray.scala:55)
	at scala.collection.mutable.ArrayBuffer.foreach(ArrayBuffer.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.abortStage(DAGScheduler.scala:2720)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGScheduler.$anonfun$handleTaskSetFailed$1$adapted(DAGScheduler.scala:1206)
	at scala.Option.foreach(Option.scala:407)
	at org.apache.spark.scheduler.DAGScheduler.handleTaskSetFailed(DAGScheduler.scala:1206)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.doOnReceive(DAGScheduler.scala:2984)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2923)
	at org.apache.spark.scheduler.DAGSchedulerEventProcessLoop.onReceive(DAGScheduler.scala:2912)
	at org.apache.spark.util.EventLoop$$anon$1.run(EventLoop.scala:49)
	at org.apache.spark.scheduler.DAGScheduler.runJob(DAGScheduler.scala:971)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2263)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2284)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2303)
	at org.apache.spark.SparkContext.runJob(SparkContext.scala:2328)
	at org.apache.spark.rdd.RDD.count(RDD.scala:1266)
	at org.apache.spark.ml.recommendation.ALS$.train(ALS.scala:995)
	at org.apache.spark.ml.recommendation.ALS.$anonfun$fit$1(ALS.scala:737)
	at org.apache.spark.ml.util.Instrumentation$.$anonfun$instrumented$1(Instrumentation.scala:191)
	at scala.util.Try$.apply(Try.scala:213)
	at org.apache.spark.ml.util.Instrumentation$.instrumented(Instrumentation.scala:191)
	at org.apache.spark.ml.recommendation.ALS.fit(ALS.scala:714)
	at jdk.internal.reflect.GeneratedMethodAccessor281.invoke(Unknown Source)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at py4j.reflection.MethodInvoker.invoke(MethodInvoker.java:244)
	at py4j.reflection.ReflectionEngine.invoke(ReflectionEngine.java:374)
	at py4j.Gateway.invoke(Gateway.java:282)
	at py4j.commands.AbstractCommand.invokeMethod(AbstractCommand.java:132)
	at py4j.commands.CallCommand.execute(CallCommand.java:79)
	at py4j.ClientServerConnection.waitForCommands(ClientServerConnection.java:182)
	at py4j.ClientServerConnection.run(ClientServerConnection.java:106)
	at java.base/java.lang.Thread.run(Thread.java:829)
Caused by: java.lang.OutOfMemoryError: Java heap space
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:145)
	at scala.reflect.ManifestFactory$IntManifest.newArray(Manifest.scala:143)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:101)
	at org.apache.spark.util.collection.OpenHashSet.<init>(OpenHashSet.scala:57)
	at org.apache.spark.ml.recommendation.ALS$.$anonfun$makeBlocks$1(ALS.scala:1631)
	at org.apache.spark.ml.recommendation.ALS$$$Lambda$4477/0x0000000841749040.apply(Unknown Source)
	at scala.collection.Iterator$$anon$10.next(Iterator.scala:461)
	at org.apache.spark.shuffle.sort.BypassMergeSortShuffleWriter.write(BypassMergeSortShuffleWriter.java:169)
	at org.apache.spark.shuffle.ShuffleWriteProcessor.write(ShuffleWriteProcessor.scala:59)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:101)
	at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:53)
	at org.apache.spark.TaskContext.runTaskWithListeners(TaskContext.scala:161)
	at org.apache.spark.scheduler.Task.run(Task.scala:139)
	at org.apache.spark.executor.Executor$TaskRunner.$anonfun$run$3(Executor.scala:554)
	at org.apache.spark.executor.Executor$TaskRunner$$Lambda$2657/0x0000000841155840.apply(Unknown Source)
	at org.apache.spark.util.Utils$.tryWithSafeFinally(Utils.scala:1529)
	at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:557)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	... 1 more

</pre>