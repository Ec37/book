# Web前端问题笔记

1. 获取select选中的值
A:`var selected = $('#selecter option:selected').val();`
2. jQuery赋值给`<input id='id' type='hidden' value='' />`用`$("#id").val(value)`有时会失效
A:可以尝试用这种方法`$("input[id='id']").val(value)`
3. 兼容IE的Ajax上传表单文件方法
A:可以使用Jquery.form.js的ajaxSubmit方法解决：

    1.导入jquery.form.js

    2.然后使用ajaxSubmit

    ```javascript

    $("#exForm").ajaxSubmit({
        url: "${base}/system/upload",
          type: "post",
          dataType: "json",
          success: function(result){
            //TODO:你要做啥的
          },
          error:function(result){}
    });

    ````

4. 有时候IE会在返回JSON字符串的时候提示下载，要怎么解决？
A:不同平台的web框架有不同的解决方，共同点是都和 `text/html` 相关。
    * struts2可以在返回的Action里加上result参数 `text/html`:

      ```xml
        <action name="loadDemos" class="com.load.demos" method="loadDemos">
          <result type="json">
            <param name="contentType">text/html</param>
          </result>
        </action>
      ```

    * springMvc的话可以从springMvc配置文件中加入以下的bean:

      ```xml
        <bean id="mappingJacksonHttpMessageConverter" class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
          <property name="supportedMediaTypes">
            <list>
              <value>text/html;charset=UTF-8</value>
            </list>
          </property>
        </bean>
      ```

    * 其他后端平台出现同样问题估计也是和text/html设置有关。
