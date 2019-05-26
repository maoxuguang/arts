1. algorithem

2. review

   <https://blog.packagecloud.io/eng/2015/07/20/yum-repository-internals/>

   koji里面，我改了repo里文件的版本号，编包的时候会选更大的版本号，但我改了之后并没有生效，包里还是老的版本。同事说我要重新createrepo，这样配置文件里的版本才能一起改掉，才会用改过的版本。参考了这个文章，重新createrepo，依然没用。最后还是改spec里的版本号才生效的。

3. tips 

   用API更新数据库里的记录的时候总是报错：

   ```
    "This field is required."
   ```

   我刚开始以为这个字段是外键，所以必须带上，后来跟同事讨论，即使是外键，更新的时候这个字段也已经有值了啊，google下，发现用PATCH代替PUT就可以了。因为put会更新所有字段，而patch是partial update.

4. share  关于google搜索

   想在jquery的datatables中添加编辑按钮，查了下jquery自己带的editor要付费。搜素下面google自动补全的关键字：

```
   jquery datatables edit row button
```

   没有找到想要的，搜索下面的关键字找到了想要的答案， inline table edit

```
   jquery datatables edit row
```

   https://stackoverflow.com/questions/42491910/jquery-datatables-editing-row

   搜索的时候可以略微扩大关键字搜索的范围，可以找到不同的答案。其实这样说也不太准确，因为我想要的是edit row的功能，而button只是实现这个功能的一种具体方法。

========================================我是分割线======================================

​    Django在这段代码报错：

```javascript
var rcp_version = {% get_env "RCP_SYSTEM_VERSION" %};
```



```
Invalid block tag:  expected 'endblock'
```

​    我以为这个get_env是Django自带的一个函数之类的，搜了下没不是，搜出来的都是getenv，再搜报错的信息，搜索结果好像和Django都没啥关系，别的程序也会有这种报错信息，加上了Django的关键字之后发现这个是template tag的问题，现在问题已的方向已经找到了，但搜了下Django template tag里面好像也没有这个tag，那可能就是我们自己写的标签，看了下项目目录下果然有templatetags目录，里面有这个标签。那现在问题就清楚了，就是自己定制的标签没有生效，就搜了：

```
django use custom template tag
```

搜出来的第一个答案的第一段就是：

https://docs.djangoproject.com/en/2.1/howto/custom-template-tags/

```
Django’s template language comes with a wide variety of built-in tags and filters designed to address the presentation logic needs of your application. Nevertheless, you may find yourself needing functionality that is not covered by the core set of template primitives. You can extend the template engine by defining custom tags and filters using Python, and then make them available to your templates using the {% load %} tag.
```

但因为我没仔细看，拉着扫了下好像没有地方讲怎么让定制的标签生效的，最后还是在别的地方找到的答案。

总结起来就是:

```
搜索的时候要先弄清楚问题的本质，也可以在搜索的过程中理清楚。
```



​    









