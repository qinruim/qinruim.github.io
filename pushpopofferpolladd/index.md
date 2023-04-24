# push()、pop()、offer()、poll()、add()



# push()、pop()、offer()、poll()、add()

以前以为Deque的push（）跟offer（）方法一样，pop（）跟poll（）方法一样，没有太关注过其具体实现。

今天在做LeetCode P102 二叉树的层序遍历时，用了LinkedList（Deque）作为队列实现，使用push（）方法将元素加入队列时出现了奇怪的结果，改成offer（）方法则没有问题。原因是push是将对象当作栈使用，这题要的是队列

因此记录一下LinkedList的push，offer，add操作的区别；以及poll和pop操作的区别

![img](push()、pop()、offer()、poll()、add().assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmdfY2hhb2NoZW4=,size_16,color_FFFFFF,t_70-16818044103472.png)

![img](push()、pop()、offer()、poll()、add().assets/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dhbmdfY2hhb2NoZW4=,size_16,color_FFFFFF,t_70.png)

1.add（不带索引默认添加到链表的最后）与offer一样都是添加操作，唯一的区别就是offer没有带索引参数的方法，并且如果队列满了add会抛出异常，而offer不会。

上面这两种操作方式是将LinkedList当作链表或队列来使用。

2.push、pop操作是将LinkedList当作栈来使用。


