# 1.Typora的使用

它可以像**浏览器**一样检查元素，修改样式,慢慢研究哈

![image-20220829105505345](D:%5Cmy-project%5Cnotes.github.io%5Cdocs%5Cxia_sister%5Cimg%5Cimage-20220829105505345.png)

程序猿，你真的会用Typora吗？

# 2.员工管理系统之JSP的学习

## 2.1pom.xml

JDK编译等级    mysql驱动   lombok工具   taglibs标准标签库   jstl标签库

```xml
 <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.30</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.24</version>
            <scope>provided</scope>
        </dependency>

        <!-- https://mvnrepository.com/artifact/taglibs/standard -->
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.1.2</version>
        </dependency>
    </dependencies>

```

## 2.2实体类的快捷操作

```sql
DESC `user`;
user_id
username
password
```

## 2.3下拉框

循环  判断   函数

```jsp
<%-- 当发生用户选择单选框导致了值发生变化的时候，那么： --%>
    <%-- select标签的name和某一个被选中的option的value，这两个将会作为一个键值对提交给后台 --%>
    <select name="officeId" onchange="submitOffice(event)">
        <option value="-1">---请选择---</option>
        <c:forEach var="office" items="${officeList}">
            <%-- option有2处需要填写： --%>
            <%-- 第一处：用户看到的文本值 --%>
            <%-- 第二处：提交给后端使用的逻辑值 --%>

            <%-- 下拉框要保留上一次用户选中的那个部门 --%>
            <option value="${office.officeId}" <c:if test="${selectedId == office.officeId}">selected</c:if>>${office.city}</option>

            
        </c:forEach>
    </select>
```

```jsp
   <script>
    
    function submitOffice(e) {
        location.href = "/emp?method=findByOfficeId&officeId=" + e.target.value;
    }

    </script>
```

