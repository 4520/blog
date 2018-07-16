---
layout: post
title: spring data jpa一对多，save之后，子表新增了一条数据，老的数据没有删除，而是更新成为null
date: 2018-03-28 12:41:56
tags: ['jpa', 'hibernate']

---

![](https://blog.xlinyu.com/assets/images/2018-03-28/01.jpg)

> 问题：使用了jpa的@OneToMany注解，当更新子表中的数据时，子表中新增了一条新纪录，并将旧的数据的外键id设置为null，因此产生了孤儿数据，于是查找资料找到了``orphanRemoval``设置为true可以删除孤儿数据

<!--more-->

添加了``orphanRemoval=true``又跳进了另一个坑

```java
org.springframework.orm.jpa.JpaSystemException: A collection with cascade="all-delete-orphan" was no longer referenced by the owning entity instance: io.arukas.entity.Post.imgs; nested exception is org.hibernate.HibernateException: A collection with cascade="all-delete-orphan" was no longer referenced by the owning entity instance: io.arukas.entity.Post.imgs

	at org.springframework.orm.jpa.vendor.HibernateJpaDialect.convertHibernateAccessException(HibernateJpaDialect.java:333)
	at org.springframework.orm.jpa.vendor.HibernateJpaDialect.translateExceptionIfPossible(HibernateJpaDialect.java:244)
	at org.springframework.orm.jpa.JpaTransactionManager.doCommit(JpaTransactionManager.java:521)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:761)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:730)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.commitTransactionAfterReturning(TransactionAspectSupport.java:518)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:292)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:673)
	at io.arukas.service.PostService$$EnhancerBySpringCGLIB$$bb9beb55.update(<generated>)
	at io.arukas.service.PostServiceTests.updatePost(PostServiceTests.java:40)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(FrameworkMethod.java:50)
	at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
	at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMethod.java:47)
	at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMethod.java:17)
	at org.springframework.test.context.junit4.statements.RunBeforeTestMethodCallbacks.evaluate(RunBeforeTestMethodCallbacks.java:75)
	at org.springframework.test.context.junit4.statements.RunAfterTestMethodCallbacks.evaluate(RunAfterTestMethodCallbacks.java:86)
	at org.springframework.test.context.junit4.statements.SpringRepeat.evaluate(SpringRepeat.java:84)
	at org.junit.runners.ParentRunner.runLeaf(ParentRunner.java:325)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:252)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:94)
	at org.junit.runners.ParentRunner$3.run(ParentRunner.java:290)
	at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:71)
	at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:288)
	at org.junit.runners.ParentRunner.access$000(ParentRunner.java:58)
	at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:268)
	at org.springframework.test.context.junit4.statements.RunBeforeTestClassCallbacks.evaluate(RunBeforeTestClassCallbacks.java:61)
	at org.springframework.test.context.junit4.statements.RunAfterTestClassCallbacks.evaluate(RunAfterTestClassCallbacks.java:70)
	at org.junit.runners.ParentRunner.run(ParentRunner.java:363)
	at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.run(SpringJUnit4ClassRunner.java:191)
	at org.junit.runner.JUnitCore.run(JUnitCore.java:137)
	at com.intellij.junit4.JUnit4IdeaTestRunner.startRunnerWithArgs(JUnit4IdeaTestRunner.java:68)
	at com.intellij.rt.execution.junit.IdeaTestRunner$Repeater.startRunnerWithArgs(IdeaTestRunner.java:47)
	at com.intellij.rt.execution.junit.JUnitStarter.prepareStreamsAndStart(JUnitStarter.java:242)
	at com.intellij.rt.execution.junit.JUnitStarter.main(JUnitStarter.java:70)
Caused by: org.hibernate.HibernateException: A collection with cascade="all-delete-orphan" was no longer referenced by the owning entity instance: io.arukas.entity.Post.imgs
	at org.hibernate.engine.internal.Collections.processDereferencedCollection(Collections.java:99)
	at org.hibernate.engine.internal.Collections.processUnreachableCollection(Collections.java:50)
	at org.hibernate.event.internal.AbstractFlushingEventListener.flushCollections(AbstractFlushingEventListener.java:243)
	at org.hibernate.event.internal.AbstractFlushingEventListener.flushEverythingToExecutions(AbstractFlushingEventListener.java:86)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:38)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1282)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:465)
	at org.hibernate.internal.SessionImpl.flushBeforeTransactionCompletion(SessionImpl.java:2963)
	at org.hibernate.internal.SessionImpl.beforeTransactionCompletion(SessionImpl.java:2339)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.beforeTransactionCompletion(JdbcCoordinatorImpl.java:485)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.beforeCompletionCallback(JdbcResourceLocalTransactionCoordinatorImpl.java:147)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.access$100(JdbcResourceLocalTransactionCoordinatorImpl.java:38)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl$TransactionDriverControlImpl.commit(JdbcResourceLocalTransactionCoordinatorImpl.java:231)
	at org.hibernate.engine.transaction.internal.TransactionImpl.commit(TransactionImpl.java:65)
	at org.hibernate.jpa.internal.TransactionImpl.commit(TransactionImpl.java:61)
	at org.springframework.orm.jpa.JpaTransactionManager.doCommit(JpaTransactionManager.java:517)
	... 37 more
```



``PostImage.java``

```java
@Data
@Entity
@Table(name = "post_imgs")
@EntityListeners(AuditingEntityListener.class)
public class PostImage {

    @Id
    @GeneratedValue(generator = "uuid")
    @GenericGenerator(name = "uuid", strategy = "org.hibernate.id.UUIDGenerator")
    private String id;

    private String imageUrl;

    @CreatedDate
    private Date createAt;

    @LastModifiedDate
    private Date updateAt;

    @Version
    private long version;
}
```

``Post.java``

```java
@Data
@Entity
@Table(name = "posts")
@EntityListeners(AuditingEntityListener.class)
public class Post {

    @Id
    @GeneratedValue(generator = "uuid")
    @GenericGenerator(name = "uuid", strategy = "org.hibernate.id.UUIDGenerator")
    private String id;

    private String title;

    private String summary;

    private String content;

    @ManyToOne
    @JoinColumn(name = "author_id",
            foreignKey = @ForeignKey(name = "fk_author_id"),
            referencedColumnName = "id")
    private User author;

    @CreatedDate
    private Date createAt;

    @LastModifiedDate
    private Date updateAt;

    @ManyToMany
    @JoinTable(
            name = "posts_tags",
            joinColumns = @JoinColumn(name = "post_id"),
            inverseJoinColumns = @JoinColumn(name = "tag_id"))
    private Set<Tag> tags;

    @OneToMany
    @JoinColumn(name = "post_id")
    private Set<Comment> comments = new HashSet<>();

    @OneToMany(cascade = CascadeType.ALL, orphanRemoval = true)
    // 一定要指定这个 不然就成了多对多了
    @JoinColumn(name = "post_id")
    private Set<PostImage> imgs = new HashSet<>();

    // 查找点评数量
    // 注意这里是标准的sql，not HQL
    @Formula("(select count(t.id) from comments t where t.post_id = id)")
    private Integer commentNum;

    @Version
    private long version;
}
```

``PostService.java``

```java
@Transactional
public Post update(Post post) {

    // db取出原始数据
    String id = post.getId();
    Post dbPost = postRepository.findOne(id);
    Set<PostImage> imgs = dbPost.getImgs();
    imgs.clear();
    imgs.addAll(post.getImgs());
    post.setImgs(imgs);

    // 将新增数据copy到db的模型中
    BeanUtilsAssembler.merge(post, dbPost);
    return postRepository.save(dbPost);
}
```

最终执行sql，看sql还是需要优化呢，以后有空解决吧。。。

```mysql
Hibernate: select post0_.id as id1_2_0_, post0_.title as title2_2_0_, post0_.summary as summary3_2_0_, post0_.content as content4_2_0_, post0_.author_id as author_i8_2_0_, post0_.create_at as create_a5_2_0_, post0_.update_at as update_a6_2_0_, post0_.version as version7_2_0_, (select count(t.id) from comments t where t.post_id = post0_.id) as formula0_0_, user1_.id as id1_7_1_, user1_.username as username2_7_1_, user1_.password as password3_7_1_, user1_.birthday as birthday4_7_1_, user1_.gender as gender5_7_1_, user1_.unionid as unionid6_7_1_, user1_.create_at as create_a7_7_1_, user1_.update_at as update_a8_7_1_, user1_.version as version9_7_1_ from posts post0_ left outer join users user1_ on post0_.author_id=user1_.id where post0_.id=?
Hibernate: select post0_.id as id1_2_0_, post0_.title as title2_2_0_, post0_.summary as summary3_2_0_, post0_.content as content4_2_0_, post0_.author_id as author_i8_2_0_, post0_.create_at as create_a5_2_0_, post0_.update_at as update_a6_2_0_, post0_.version as version7_2_0_, (select count(t.id) from comments t where t.post_id = post0_.id) as formula0_0_, user1_.id as id1_7_1_, user1_.username as username2_7_1_, user1_.password as password3_7_1_, user1_.birthday as birthday4_7_1_, user1_.gender as gender5_7_1_, user1_.unionid as unionid6_7_1_, user1_.create_at as create_a7_7_1_, user1_.update_at as update_a8_7_1_, user1_.version as version9_7_1_ from posts post0_ left outer join users user1_ on post0_.author_id=user1_.id where post0_.id=?
Hibernate: select imgs0_.post_id as post_id6_1_0_, imgs0_.id as id1_1_0_, imgs0_.id as id1_1_1_, imgs0_.image_url as image_ur2_1_1_, imgs0_.create_at as create_a3_1_1_, imgs0_.update_at as update_a4_1_1_, imgs0_.version as version5_1_1_ from post_imgs imgs0_ where imgs0_.post_id=?
Hibernate: insert into post_imgs (image_url, create_at, update_at, version, id) values (?, ?, ?, ?, ?)
Hibernate: update posts set title=?, summary=?, content=?, author_id=?, create_at=?, update_at=?, version=? where id=? and version=?
Hibernate: update post_imgs set post_id=null where post_id=? and id=?
Hibernate: update post_imgs set post_id=? where id=?
Hibernate: delete from post_imgs where id=? and version=?
```

> https://stackoverflow.com/questions/9430640/a-collection-with-cascade-all-delete-orphan-was-no-longer-referenced-by-the-ow