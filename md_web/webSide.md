# Web前端问题笔记

1. Q：获取select选中的值
A：`var selected = $('#selecter option:selected').val();`
2. Q：jQuery赋值给`<input id='id' type='hidden' value='' />`用`$("#id").val(value)`有时会失效
A：可以尝试用这种方法`$("input[id='id']").val(value)`
