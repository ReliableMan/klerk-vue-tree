# tree_vue 
### cтраница с vue-js компонентом для вывода дерева рубрик сайта.

## Project setup
```
npm install
```
### Compiles and hot-reloads for development
```
npm run serve
```
####  Имеется АПИ *** возвращающее дерево рубрик мероприятий и параметр ?allowEmpty=1 который позволяет вернуть больше рубрик (в том числе и рубрики в которых нет мероприятий).
<br/>
<h2>Компонент должен: <h2/>

- выводить дерево
![tree-vue-klerk-1](https://user-images.githubusercontent.com/93074634/210871188-d725809e-0449-4914-b31d-475c16c14483.gif)
<br/>

- позволять сворачивать визуально ветки на любом уровне включая корень
![tree-vue-klerk-2](https://user-images.githubusercontent.com/93074634/210869428-4af6a58d-60d7-499d-a1d9-777786157171.gif)
<br/>

- должна быть галочка Отображать пустые рубрики, которая влияет на параметр allowEmpty, 
![tree-vue-klerk-3](https://user-images.githubusercontent.com/93074634/210869623-274154ef-fa9e-4bdb-94c6-a7271079d125.gif)
<br/>

- каждая рубрика должна быть ссылкой (в АПИ передаётся относительный адрес на [klerk](https://www.klerk.ru)), 
![tree-vue-klerk-4](https://user-images.githubusercontent.com/93074634/210871773-1b0f85a1-b0ca-46df-8000-48f0d36b9199.gif)
<br/>

-	рядом с каждой рубрикой надо отобразить в скобках два числа: count - есть в АПИ и сумму count-ов данного элемента и всех его дочерних элементов. 
![tree-vue-klerk-5](https://user-images.githubusercontent.com/93074634/210870449-1fb82320-0569-499d-9dd4-f5c939c9d5b0.gif)
<br/>

- возле каждого элемента также должен быть чекбокс, и выше дерева должна выводиться сумма count-ов всех элементов, отмеченных чекбоксами (вместе с дочерними элементами отмеченных элементов). Каждая рубрика не может участвовать в подсчёте более одного раза.
![tree-vue-klerk-6](https://user-images.githubusercontent.com/93074634/210870776-98c4f59a-0d01-42a4-8cfc-8af79aa830e8.gif)
<br/>

#### В процессе разработки на Vue 3 использовалось Options API

