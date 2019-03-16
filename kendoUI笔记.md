1.MVVM(Model View View-Model)

* **查询表单数据一般需要绑定在viewModel中,在查询数据时，将viewModel中的值通过DataSource的query传递到后台去**,例子：

  ``` js
  #定义viewModel
  #方式一：
  var viewModel = kendo.observable({
                 model : {},
      XXXFunction:function(){},
      ...
  });
  #方式二：Hap.createGridViewModel返回的就是一个kendo.observable(),并且已经封装了基本的CRUD和其他的基本操作。详情请看createGridViewModel里面的内容。
  var viewModel = Hap.createGridViewModel("#grid");
  
  ```

  ​	

  ```js
  #单个表单数据绑定到viewModel
  #1.定义表单
  <input type="text" id="promptCode" data-bind="value:model.promptCode">
  #2.绑定到viewModel
  <script>
      kendo.bind($('promptCode'), viewModel);
  </script>
  
  ```

  ```js
  #多个表单数据绑定到viewModel
  #1.定义表单
  <form id="form01">
  	<input type="text" id="CompanyID" data-bind="value:model.CompanyID">
      <input type="text" id="CompanyName" data-bind="value:model.CompanyName">
  #2.绑定到viewModel
  <script>
      kendo.bind($('form01'), viewModel);
  </script>
  </form>
  ```

* ##### DataSource是为表格和表单提供数据的数据源，其中的数据从后台获得，
