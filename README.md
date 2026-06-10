1. `git clone` this project
2. Download GraalVM for JDK 25 Community : https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-25.0.2/graalvm-community-jdk-25.0.2_linux-x64_bin.tar.gz
3. Add it to your PATH and export JAVA_HOME

```bash
export JAVA_HOME=/path/to/graalvm/untared
export PATH=$JAVA_HOME/bin:$PATH
```

4. `cd /path/to/cloned/repo`
5. `./mvnw clean -Pnative spring-boot:build-image` or `./mvnw -e -X clean -Pnative spring-boot:build-image` for more logging
6. `podman run --net=podman docker.io/library/cortex:0.0.1-SNAPSHOT`
7. Error :  
```text
2026-06-10T10:01:31.762Z  WARN 1 --- [cortex] [           main] o.s.c.support.GenericApplicationContext  : Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.aop.config.internalAutoProxyCreator': java.panw.PanwHooks.HookArgs2(Ljava/lang/Object;Ljava/lang/Object;)V [symbol: Java_java_panw_PanwHooks_HookArgs2 or Java_java_panw_PanwHooks_HookArgs2__Ljava_lang_Object_2Ljava_lang_Object_2]
Application run failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.aop.config.internalAutoProxyCreator': java.panw.PanwHooks.HookArgs2(Ljava/lang/Object;Ljava/lang/Object;)V [symbol: Java_java_panw_PanwHooks_HookArgs2 or Java_java_panw_PanwHooks_HookArgs2__Ljava_lang_Object_2Ljava_lang_Object_2]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:610)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:525)
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:333)
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:371)
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:331)
        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:201)
        at org.springframework.context.support.PostProcessorRegistrationDelegate.registerBeanPostProcessors(PostProcessorRegistrationDelegate.java:265)
        at org.springframework.context.support.AbstractApplicationContext.registerBeanPostProcessors(AbstractApplicationContext.java:812)
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:605)
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:756)
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:445)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:321)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1365)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1354)
        at com.example.cortex.CortexApplication.main(CortexApplication.java:10)
        at java.base@25.0.3/java.lang.invoke.LambdaForm$DMH/sa346b79c.invokeStaticInit(LambdaForm$DMH)
Caused by: java.lang.UnsatisfiedLinkError: java.panw.PanwHooks.HookArgs2(Ljava/lang/Object;Ljava/lang/Object;)V [symbol: Java_java_panw_PanwHooks_HookArgs2 or Java_java_panw_PanwHooks_HookArgs2__Ljava_lang_Object_2Ljava_lang_Object_2]
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.jni.access.JNINativeLinkage.getOrFindEntryPoint(JNINativeLinkage.java:152)
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.jni.JNIGeneratedMethodSupport.nativeCallAddress(JNIGeneratedMethodSupport.java:41)
        at java.panw.PanwHooks.HookArgs2(Native Method)
        at org.springframework.beans.AbstractPropertyAccessor.setPropertyValues(AbstractPropertyAccessor.java)
        at org.springframework.beans.AbstractPropertyAccessor.setPropertyValues(AbstractPropertyAccessor.java:79)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyPropertyValues(AbstractAutowireCapableBeanFactory.java:1744)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1461)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:602)
        ... 15 more
```
