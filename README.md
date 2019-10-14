<div align="center">
  <a href="https://github.com/VKCOM">
    <img width="100" height="100" src="https://avatars3.githubusercontent.com/u/1478241?s=200&v=4" alt="VK Logo"/>
  </a>
  <br>
  <br>
</div>

# VKUI Navigator
Данный модуль позволяет быстро и просто создать базовую логику навигации
для сервиса на платформе VK Mini Apps. Поддерживает все необходимые
функции и инкапсулирует в себе базовое поведение на всех платформах (такое как
свайпы на iOS и кнопка "назад" на Android)

## Установка 📦
Выполните `yarn add vkui-navigator` или `npm i vkui-navigator`

## Быстрый старт 🚀
```javascript
import { Page } from "vkui-navigator/dist";

// simple usage
<Page id="page1" homePanel="welcome">
    <Welcome id="welcome"/>
</Page>
```

## Принцип работы
Вокруг ваших панелей создается View со втроенной базовой логикой.
Каждой панели передается в props объект `navigator`. В нем содержаться
методы и параметры, который вы передали из предыдущей панели. Также
есть поддержка модальных окон и попапов

## API Справочник
___
### <a id="page" name="page"></a>  Page

▸ Основная единица модуля. Включает в себя логику навигации между панелями 

**Props:**

Название | Тип | Описание |
------ | ------ | ------ |
`id` | string, required | Идентификатор, который передается View внутри компонента |
`homePanel` | string | Идентификатор начальной панели |
`modals` | array | Массив модальных окон  |
`goView` | func | Коллбек, который вызывается из панелей для смены текущего View(Page) на верхнем порядке
___
### <a id="navigator" name="navigator"></a>  Navigator

▸ Объект, передаваемый в props всем панелям и модальным окнам.

**Structure:**

Название | Тип | Описание |
------ | ------ | ------ |
`go(id:String, params={})` | func | Переход на панель с идентификатором `id`|
`goView(id:String)` | func | Вызывает коллбек, который передался в Page |
`goBack` | func | Возвращает на одну панель назад  |
`showModal(id:String, params={})` | func | Показывает модальное окно с идентификатором `id`|
`hideModal` | func | Скрывает все активные модальные окна |
`showPopout(popout:Node)` | func | Показывает переданный попаут |
`hidePopout` | func | Скрывает все активные попауты |
`showLoader` | func | Показывает спиннер загрузки |
`hideLoader` | func | Скрывает спиннер загрузки |
`params` | object | Параметры, которые передаются через `go` или `showModal` |
___

## Примеры 📚
### Пример с панелью
```
const Panel1 = ({ id, navigator }) => (
    <Panel id={id}>
        <PanelHeader>
            Панель 1
        <PanelHeader/>
        <Group>
            <Button onClick={() => navigator.go("panel2")}>
                Вперед
            </Button>
        </Group>
    </Panel>
);

const Panel2 = ({ id, navigator }) => (
    <Panel id={id}>
        <PanelHeader>
            Панель 2
        <PanelHeader/>
        <Group>
            <Button onClick={() => navigator.goBack()}>
                Назад
            </Button>
        </Group>
    </Panel>
);

<Page homePanel="panel1">
    <Panel1 id="panel1"/>
    <Panel2 id="panel2"/>
</Page>
```

## Авторы 🎨
*   [Степан Новожилов](https://vk.me/this.state.user)