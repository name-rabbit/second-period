## JQuery-Ajax的增删改查DEMO

## 1.基础的一些操作

>选中某个元素,获取某个元素的值
>
>​	$(selector) .val()

```js
//获取用户名的值
const username = $("#username").val();
```

>清空
>
>元素.empty

```js
  // 定位到select标签
    let select = $("#officeId");
    // 清空下拉框
   // select.html("");
select.empty();
```

>创建元素节点
>
>​	document.createElement("元素")

```js 
 const td = document.createElement("td");
```

>追加元素节点
>
>​	元素.append(元素)

```js
   const tb = $("#tb");
   tb.append(tr);
```

>ajax实现异步提交异步请求
>
>​	$.get/post(url,data,function(e参数后台值))

```js
 $.post(
        // 参数1：请求路径
        "/user",
        // 提交的数据
        {
            method: "checkLogin",
            username,
            password
        },
        // 成功的callback
        (data) => {
            if (data === "SUCCESS") {              
                location.href = "/index.jsp";
            } else {
                //提示用户名密码错误
                $("#tips").text("用户名或密码错误");
            }
        }
    );
```

## 2.demo核心代码

> 登录模块

```js
//login.js
let checkLogin = () => {
    // 获取用户名和密码
    const username = $("#username").val();
    const password = $("#password").val();

    $.post(
        // 参数1：请求路径
        "/user",
        // 提交的数据
        {
            method: "checkLogin",
            username,
            password
        },
        // 成功的callback
        (data) => {
            if (data === "SUCCESS") {              
                location.href = "/index.jsp";
            } else {
                //提示用户名密码错误
                $("#tips").text("用户名或密码错误");
            }
        }
    );

};
```

```jsp
//login.jsp 
 <script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
    <script src="./js/login.js"></script>
<table>
      <span id="tips"></span>
      <tr>
        <td>用户名</td>
        <td><input type="text" id="username" name="username" /></td>
      </tr>
      <tr>
        <td>密码</td>
        <td><input type="password" id="password" name="password" /></td>
      </tr>
      <tr>
        <td colspan="3">
          <input type="reset" value="重置" />
          <button type="button" onclick="checkLogin()">登录</button>
          <button
            type="button"
            onclick="javascript:location.href='/register.jsp'"
          >
            注册
          </button>
        </td>
      </tr>
    </table>

```

>员工管理模块

```js
//index.js
let loadEmpList = () => {
  const tb = $("#tb");
  console.log(tb);
  $.get("/emp", { method: "findAll" }, (empList) => {
    console.log(empList);
    tb.empty();

    for (const emp of empList) {
      const tr = document.createElement("tr");
      tb.append(tr);
      tr.appendTd = function (value, isHtml) {
        const td = document.createElement("td");
        if (!isHtml) td.innerText = value;
        else td.innerHTML = value;
        tr.appendChild(td);
      };
      tr.appendTd(emp.employeeId);
      tr.appendTd(`${emp.firstName} . ${emp.lastName}`);
      tr.appendTd(emp.jobTitle);
      tr.appendTd(emp.salary);
      tr.appendTd(emp.reportsTo);
      tr.appendTd(emp.officeId);
      tr.appendTd(
        `<button type="button">删除</button><button type="button" onclick="toUpdate(${emp.employeeId})">更新</button>`,
        true
      );
    }
  });
};
loadEmpList();
```

```java
 private void findAll(HttpServletRequest req, HttpServletResponse resp) {
        try {
            List<Emp> empList = empDao.findAll();
            JsonUtils.writeJSon(empList,resp);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }


    }
```

>部门管理模块

```js 
//office.js
let fillOfficeSelect = (officeList) => {
    // 定位到select标签
    let select = $("#officeId");

    // 清空下拉框
    select.html("");

    // 用for填充数据
    //select.html("<option>---请选择---</option>");

    select.append(`<option value="-1">---请选择---</option>`);

    for (const office of officeList) {
        // 添加select标签的子元素
        select.append(`<option value="${office.officeId}">${office.city}</option>`);
    }
};


let loadOfficeList = () => {
    // 以GET方式提交异步请求
    $.get({
        // 后台地址
        url: "/user?method=findOffices",
        success: (data) => {
            fillOfficeSelect(data);
        }
    }
    );
};

loadOfficeList();
```

