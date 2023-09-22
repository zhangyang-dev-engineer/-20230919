
1，启动ApplicationContext
2,创建BeanFactory
3,初始化BeanFactory
4，执行BeanFactory 后置处理器 
5，进行扫描
扫描的流程：
   包路径-》得到包路径下所有class文件对象，注意不是Class对象，而是文件对象（可以理解为file对象）-》利用ASM技术解析每个class文件对象，得到class元数据信息
   如果当前类和某个excludeFilter匹配，那就排除这个类
   如果当前类和某个includeFilter匹配，那就通过这个类-》进一步进行条件注解@Conditional匹配筛选-》都匹配成功以后会生成一个ScannedGenercBeanDefinition
      如果不是顶级类，或静态内部类，则不通过
      如果是抽象类或接口，则不通过
      如果是抽象类，但是有@Lookup注解的方法则通过
   最终扫描到某些BeanDefinion
   遍历每个BeanDefinition
   调用AnnotationBeanNameGenerator 生成BeanName (解析@Component注解所指定的beanName，没有指定则默认生成)
   给BeanDefinition对象中的属性赋默认值
   解析@Lazy,@Primary,@DependsOn,@Role,@Description 等注解并赋值给BeanDefinition对应的属性
   判断当前beanName是否在Spring容器中已经存在，如果不存在则把beanName以及BeanDefinition注册到Spring容器中，如果存在则报错



6，生成BeanDefinition
7,合并BeanDefinition
8,加载类
9，实例化前
10，推断构造方法
11，实例化
12，BeanDefinition后置处理
13，实例化后
14，填充属性
15，填充属性后
16，执行Aware
17,初始化前
18，初始化
19，初始化后
