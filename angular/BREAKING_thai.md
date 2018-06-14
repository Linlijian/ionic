
# รายการ code ที่เปลี่ยนใน Ionic 4, Breaking Changes (เทียบจาก Ionic 3)

รายการโค้ดในส่วนต่างๆ 

- [Action Sheet](#action-sheet)
- [Alert](#alert)
- [Back Button](#back-button)
- [Button](#button)
- [Chip](#chip)
- [Colors](#colors)
- [Datetime](#datetime)
- [Dynamic Mode](#dynamic-mode)
- [FAB](#fab)
- [Fixed Content](#fixed-content)
- [Icon](#icon)
- [Input](#Input)
- [Item](#item)
- [Item Divider](#item-divider)
- [Item Options](#item-options)
- [Item Sliding](#item-sliding)
- [List Header](#list-header)
- [Menu Toggle](#menu-toggle)
- [Nav](#nav)
- [Navbar](#navbar)
- [Option](#option)
- [Radio](#radio)
- [Range](#range)
- [Segment](#segment)
- [Select](#select)
- [Spinner](#spinner)
- [Tabs](#tabs)
- [Text / Typography](#text--typography)
- [Theming](#theming)
- [Toolbar](#toolbar)


## Action Sheet

ค่า `title` และ `subTitle` เปลี่ยนเป็น `header` และ `subHeader` ตามลำดับ.

**ตัวอย่างการใช้งานแบบเก่า:**

```js
const actionSheet = await actionSheetCtrl.create({
  title: 'This is the title',
  subTitle: 'this is the sub title'
});
await actionSheet.present();
```

**ตัวอย่างการใช้งานแบบใหม่:**

```js
const actionSheet = await actionSheetCtrl.create({
  header: 'This is the title',
  subHeader: 'this is the sub title'
});
await actionSheet.present();
```


## Alert

ค่า `title` และ `subTitle` เปลี่ยนชื่อเป็น `header` และ `subHeader` ตามลำดับ

**ตัวอย่างการใช้งานแบบเก่า:**

```js
const alert = await alertCtrl.create({
  title: 'This is the title',
  subTitle: 'this is the sub title'
});
await alert.present();
```

**ตัวอย่างการใช้งานแบบใหม่:**

```js
const alert = await alertCtrl.create({
  header: 'This is the title',
  subHeader: 'this is the sub title'
});
await alert.present();
```


## Back Button

ปุ่มย้อนกลับ (Back Button) จะไม่ถูกใส่ให้ใน Navigation Bar อัตโนมัติแล้ว แต่เราต้องกำหนดเอง

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-navbar>
  <ion-title>Back Button Example</ion-title>
</ion-navbar>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-toolbar>
  <ion-buttons slot="start">
    <ion-back-button></ion-back-button>
  </ion-buttons>
  <ion-title>Back Button Example</ion-title>
</ion-toolbar>
```

ดูตัวอย่างการใช้งานเพิ่มเติมได้ใน [back button documentation](https://github.com/ionic-team/ionic/blob/master/core/src/components/back-button) 

## Button

### Markup Changed

ปุ่มสามารถกำหนดได้โดยใช้ `<ion-button>` แทน `<button>` แบบเดิม. Ionic จะพิจารณาแสดงผลเป็น link ปกติ จากการกำหนดค่า `href` ดังตัวอย่าง

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<button ion-button (click)="doSomething()">
  Default Button
</button>

<a ion-button href="#">
  Default Anchor
</a>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-button (click)="doSomething()">
  Default Button
</ion-button>

<ion-button href="#">
  Default Anchor
</ion-button>
```

### Attributes ที่มีการเปลี่ยนชื่อ

ก่อนหน้านี้ เรากำหนดตำแหน่งของ Icon ในปุ่มของเราด้วยชื่อ attribute อย่างเข่น `icon-left`, `icon-right`, `icon-start`, `icon-end`.

These have been renamed to the following, and moved from the button element to the icon itself:

| Old Property              | New Property   | Property Behavior                                                     |
|---------------------------|----------------|-----------------------------------------------------------------------|
| `icon-left`, `icon-start` | `slot="start"` | Positions to the left of the button in LTR, and to the right in RTL.  |
| `icon-right`, `icon-end`  | `slot="end"`   | Positions to the right of the button in LTR, and to the left in RTL.  |

In addition, several sets of mutually exclusive boolean attributes have been combined into a single string attribute.

The `small` and `large` attributes are now combined under the `size` attribute. The `clear`, `outline`, and `solid` attributes have been combined under `fill`. And, lastly, the `full` and `block` attributes have been combined under `expand`.

| Old Property                | New Property | Property Behavior           |
| --------------------------- | ------------ | --------------------------- |
| `small`, `large`            | `size`       | Sets the button size.       |
| `clear`, `outline`, `solid` | `fill`       | Sets the button fill style. |
| `full`, `block`             | `expand`     | Sets the button width.      |


**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-button icon-left>
  <ion-icon name="home"></ion-icon>
  Icon Left
</ion-button>

<ion-button icon-start>
  <ion-icon name="home"></ion-icon>
  Icon Left on LTR, Right on RTL
</ion-button>

<ion-button icon-right>
  Icon Right
  <ion-icon name="home"></ion-icon>
</ion-button>

<ion-button icon-end>
  Icon Right on LTR, Left on RTL
  <ion-icon name="home"></ion-icon>
</ion-button>

<ion-button large>
  Large Button
</ion-button>

<ion-button outline>
  Outline Button
</ion-button>

<ion-button full>
  Full-width Button
</ion-button>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-button>
  <ion-icon slot="start" name="home"></ion-icon>
  Icon Left on LTR, Right on RTL
</ion-button>

<ion-button>
  Icon Right on LTR, Left on RTL
  <ion-icon slot="end" name="home"></ion-icon>
</ion-button>

<ion-button size="large">
  Large Button
</ion-button>

<ion-button fill="outline">
  Outline Button
</ion-button>

<ion-button expand="full">
  Full-width Button
</ion-button>
```

## Chip

### Markup Changed

ปุ่มที่ใส่ไว้ใน `<ion-chip>` จะต้องถูกเขียนใหม่เป็น `<ion-chip-button>` 
โดย Ionic จะพิจารณาแสดงผลเป็น link ปกติ จากการกำหนดค่า `href` ดังตัวอย่าง

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-chip>
  <ion-label>Default</ion-label>
  <ion-button clear color="light">
    <ion-icon name="close-circle"></ion-icon>
  </ion-button>
</ion-chip>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-chip>
  <ion-label>Default</ion-label>
  <ion-chip-button fill="clear" color="light">
    <ion-icon name="close-circle"></ion-icon>
  </ion-chip-button>
</ion-chip>
```


## สีใน Ionic: Colors

ค่าเริ่มต้นจองธีมสี มีการปรับปรุงอีกครั้ง จากแบบเดิมคือ

```
primary:         #327eff
secondary:       #32db64
danger:          #f53d3d
light:           #f4f4f4
dark:            #222
```

ตอนนี้เปลี่ยนใหม่ แถม มีเพิ่มมาให้ด้วย

```
primary:         #3880ff
secondary:       #0cd1e8
tertiary:        #7044ff
success:         #10dc60
warning:         #ffce00
danger:          #f04141
light:           #f4f5f8
medium:          #989aa2
dark:            #222428
```

สีรองอย่าง `secondary` จะเปลี่ยนไปมากที่สุด หากมีการกำหนดใช้สีกลุ่ม `secondary` เราแนะนำให้เปลี่ยนเป็น `success` แทน


## Datetime

ชื่อคลาส  Datetime และ interface เปลี่ยนจากตัวพิมพ์ใหญ่ในคำว่า `Time` (ใน `DateTime`) to `Datetime`. ซึ่งจะทำให้ชื่อเหมือนกับกลุ่ม component อื่นๆ ไม่ดูแปลกแยกอีกต่อไป 

(พล: แล้วตอนแรกใครตั้งมา?! ก้มหน้า migrate ต่อไป) 

**ตัวอย่างการใช้งานแบบเก่า:**

```javascript
import { DateTime } from 'ionic-angular';
```

**ตัวอย่างการใช้งานแบบใหม่:**

```javascript
import { Datetime } from 'ionic-angular';
```


## Dynamic Mode

Components are no longer able to have their mode changed dynamically. You can change the mode before the first render, but after that it will not style properly because only the initial mode's styles are included.


## FAB

### Markup Changed

ปุ่มที่อยู่ใน `<ion-fab>` ควรเขียนใหม่เป็น จาก `<button ion-fab>` เป็น `<ion-fab-button>` . Ionic จะพิจารณาแสดงผลเป็น link ปกติ จากการกำหนดค่า `href` ดังตัวอย่าง

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-fab top right edge>
  <button ion-fab>
    <ion-icon name="add"></ion-icon>
  </button>
  <ion-fab-list>
    <button ion-fab>
      <ion-icon name="logo-facebook"></ion-icon>
    </button>
    <button ion-fab>
      <ion-icon name="logo-twitter"></ion-icon>
    </button>
    <button ion-fab>
      <ion-icon name="logo-vimeo"></ion-icon>
    </button>
    <button ion-fab>
      <ion-icon name="logo-googleplus"></ion-icon>
    </button>
  </ion-fab-list>
</ion-fab>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-fab vertical="top" horizontal="end" edge>
  <ion-fab-button>
    <ion-icon name="add"></ion-icon>
  </ion-fab-button>
  <ion-fab-list>
    <ion-fab-button>
      <ion-icon name="logo-facebook"></ion-icon>
    </ion-fab-button>
    <ion-fab-button>
      <ion-icon name="logo-twitter"></ion-icon>
    </ion-fab-button>
    <ion-fab-button>
      <ion-icon name="logo-vimeo"></ion-icon>
    </ion-fab-button>
    <ion-fab-button>
      <ion-icon name="logo-googleplus"></ion-icon>
    </ion-fab-button>
  </ion-fab-list>
</ion-fab>
```

### Attributes Renamed

ค่า Booleans ที่ไว้กำหนดการวางตำแหน่งของปุ่ม fab จะถูกรวมเป็น attribute เพียง 2 ชื่อ เพื่อให้อ่านง่ายขึ้น

ค่า attibutes ที่ใช้ในการวางตำแหน่งแนวนอน ถูกรวมเป็นค่า attribute ที่ชื่อว่า `horizontal` และค่า attibutes ที่ใช้ในการวางตำแหน่งแนวตั้ง ถูกรวมเป็นค่า attribute ที่ชื่อว่า `vertical`:

| ชื่อ Property เก่า | ชื่อ Property ใหม่        | Property Behavior                                                       |
|--------------|----------------------|-------------------------------------------------------------------------|
| left         | ลบออก              |                                                                         |
| right        | ลบอกก              |                                                                         |
| center       | `horizontal="center"`| Positions to the center of the viewport.                                |
| start        | `horizontal="start"` | Positions to the left of the viewport in LTR, and to the right in RTL.  |
| end          | `horizontal="end"`   | Positions to the right of the viewport in LTR, and to the left in RTL.  |
| top          | `vertical="top"`     | Positions at the top of the viewport.                                   |
| bottom       | `vertical="bottom"`  | Positions at the bottom of the viewport.                                |
| middle       | `vertical="center"`  | Positions at the center of the viewport.                                |

_เพิ่มเติมว่า ค่า `middle` จะถูกเรียกใหม่เป็น `center` สำหรับการจัดวางในแนวดิ่ง_

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-fab top right edge>
  <!-- fab buttons and lists -->
</ion-fab>

<ion-fab center middle>
  <!-- fab buttons and lists -->
</ion-fab>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-fab vertical="top" horizontal="end" edge>
  <!-- fab buttons and lists -->
</ion-fab>

<ion-fab vertical="center" horizontal="center">
  <!-- fab buttons and lists -->
</ion-fab>
```

## Fixed Content

ในเวอร์ชั่นก่อนหน้านี้ container ของ `<ion-fab>`  จะถูกวางในไว้ในส่วนที่ลอยอยู่เหนือ component อื่นเป็นค่าเริ่มต้น (เรียกว่า fixed content). ในเวอร์ชั่นนี้ และเวอร์ชั่นต่อไป เราต้องกำหนดค่า slot เป็น `fixed` โดยตรง

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-content>
  <ion-fab top right edge>
    <!-- fab buttons and lists -->
  </ion-fab>
  Scrollable Content
</ion-content>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-fab vertical="top" horizontal="end" edge slot="fixed">
  <!-- fab buttons and lists -->
</ion-fab>
<ion-content>
  Scrollable Content
</ion-content>
```

## Icon

### Fonts Removed

Icons have been refactored to use SVGs instead of fonts. Ionic will only fetch the SVG for the icon when it is needed, instead of having a large font file that is always loaded in.

If any `CSS` is being overridden for an icon it will need to change to override the SVG itself. Below is a usage example of the differences in changing the icon color.

**ตัวอย่างการใช้งานแบบเก่า:**

```css
.icon {
  color: #000;
}
```

**ตัวอย่างการใช้งานแบบใหม่:**

```css
.icon {
  fill: #000;
}
```

### Property Removed

The `isActive` property has been removed. It only worked for `ios` icons previously. If you would like to switch between an outline and solid icon you should set it in the `name`, or `ios`/`md` attribute and then change it when needed.

## Input

The Sass variables were all renamed from having `$text-input` as the prefix to `$input`.

**ตัวอย่างการใช้งานแบบเก่า:**

```css
$text-input-highlight-color-valid:       #32db64;
```

**ตัวอย่างการใช้งานแบบใหม่:**

```css
$input-highlight-color-valid:       #32db64;
```


## Item

### Markup Changed

Item should now be written as an `<ion-item>` element. Ionic will determine when to render an anchor tag based on the presence of an `href` attribute, and a button tag based on the presence of an `onclick` or `button` attribute. Otherwise, it will render a div.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-item>
  Default Item
</ion-item>

<button ion-item (click)="doSomething()">
  Button Item
</button>

<a ion-item href="#">
  Anchor Item
</a>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-item>
  <ion-label>
    Default Item
  </ion-label>
</ion-item>

<ion-item button (click)="doSomething()">
  <ion-label>
    Button Item
  </ion-label>
</ion-item>

<ion-item href="#">
  <ion-label>
    Anchor Item
  </ion-label>
</ion-item>
```

### Label Required

Previously an `ion-label` would automatically get added to an `ion-item` if one wasn't provided. Now an `ion-label` should always be added if the component is used to display text.

```html
<ion-item>
  <ion-label>
    Item Label
  </ion-label>
</ion-item>
```

### Attributes Renamed

Previously to position elements inside of an `ion-item` the following attributes were used: `item-left`, `item-right`, (and with the added support of RTL) `item-start`, `item-end`.

These have been renamed to the following:

| Old Property              | New Property   | Property Behavior                                                   |
|---------------------------|----------------|---------------------------------------------------------------------|
| `item-left`, `item-start` | `slot="start"` | Positions to the left of the item in LTR, and to the right in RTL.  |
| `item-right`, `item-end`  | `slot="end"`   | Positions to the right of the item in LTR, and to the left in RTL.  |


**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-item>
  <div item-left>Left</div>
  <ion-label>Item Label</ion-label>
  <div item-right>Right</div>
</ion-item>

<ion-item>
  <div item-start>Left on LTR, Right on RTL</div>
  <ion-label>Item Label</ion-label>
  <div item-end>Right on LTR, Left on RTL</div>
</ion-item>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-item>
  <div slot="start">Left on LTR, Right on RTL</div>
  <ion-label>Item Label</ion-label>
  <div slot="end">Right on LTR, Left on RTL</div>
</ion-item>
```

### Detail Push

The attributes to show/hide the detail arrows on items have been converted to a single property and value. Instead of writing `detail-push` or `detail-none` to show/hide the arrow, it should be written `detail`/`detail="true"` or `detail="false"`.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<button ion-item detail-none>
  <ion-label>Item Label</ion-label>
</button>

<ion-item detail-push>
  <ion-label>Item Label</ion-label>
</ion-item>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-item button detail="false">
  <ion-label>Item Label</ion-label>
</ion-item>

<ion-item detail>
  <ion-label>Item Label</ion-label>
</ion-item>
```

By default, items that render buttons or anchor tags will show the arrow in `ios` mode.

## Item Divider

### Label Required

Previously an `ion-label` would automatically get added to an `ion-item-divider` if one wasn't provided. Now an `ion-label` should always be added if the component is used to display text.

```html
<ion-item-divider>
  <ion-label>Item Divider Label</ion-label>
</ion-item-divider>
```


## Item Options

### Attributes Renamed

Previously to position the item options inside of an `ion-item-sliding` the `side` attribute would be used with one of the following values: `"left"`, `"right"`.

These values have been renamed to `"start"` and `"end"` to better align with our support for RTL.


| Old Value       | New Value       |
|-----------------|-----------------|
| `side="left"`   | `side="start"`  |
| `side="right"`  | `side="end"`    |


## Item Sliding

### Markup Changed

The option component should not be written as a `button` with an `ion-button` directive anymore. It should be written as an `ion-item-option`. This will render a native button element inside of it.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-item-sliding>
  <ion-item>
    Item 1
  </ion-item>
  <ion-item-options side="right">
    <button ion-button expandable>
      <ion-icon name="star"></ion-icon>
    </button>
  </ion-item-options>
</ion-item-sliding>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-item-sliding>
  <ion-item>
    <ion-label>Item 1</ion-label>
  </ion-item>
  <ion-item-options side="end">
    <ion-item-option expandable>
      <ion-icon name="star"></ion-icon>
    </ion-item-option>
  </ion-item-options>
</ion-item-sliding>
```

### Method Renamed

The `getSlidingPercent` method has been renamed to `getSlidingRatio` since the function is returning a ratio of the open amount of the item compared to the width of the options.


## List Header

### Label Required

Previously an `ion-label` would automatically get added to an `ion-list-header` if one wasn't provided. Now an `ion-label` should always be added if the component is used to display text.

```html
<ion-list-header>
  <ion-label>List Header Label</ion-label>
</ion-list-header>
```

## Menu Toggle

### Markup Changed

The `menuToggle` attribute should not be added to an element anymore. Elements that should toggle a menu should be wrapped in an `ion-menu-toggle` element.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<button ion-button menuToggle>
  Toggle Menu
</button>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-menu-toggle>
  <ion-button>
    Toggle Menu
  </ion-button>
</ion-menu-toggle>
```


## Nav

### Method renamed

The `remove` method has been renamed to `removeIndex` to avoid conflicts with HTML and be more descriptive as to what it does.

The `getActiveChildNavs` method has been renamed to `getChildNavs`.


## Navbar

The `<ion-navbar>` component has been removed in favor of always using an `<ion-toolbar>` with an added back button:

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-navbar>
  <ion-title>My Navigation Bar</ion-title>
</ion-navbar>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-toolbar>
  <ion-buttons slot="start">
    <ion-back-button></ion-back-button>
  </ion-buttons>
  <ion-title>My Navigation Bar</ion-title>
</ion-toolbar>
```

See the [back button](#back-button) changes for more information.

## Option

### Markup Changed

Select's option element should now be written as `<ion-select-option>`. This makes it more obvious that the element should only be used with a Select.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-select>
  <ion-option>Option 1</ion-option>
  <ion-option>Option 2</ion-option>
  <ion-option>Option 3</ion-option>
</ion-select>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-select>
  <ion-select-option>Option 1</ion-select-option>
  <ion-select-option>Option 2</ion-select-option>
  <ion-select-option>Option 3</ion-select-option>
</ion-select>
```

### Class Changed

The class has been renamed from `Option` to `SelectOption` to keep it consistent with the element tag name.

## Radio

### Slot Required

Previously radio was positioned inside of an item automatically or by using `item-left`/`item-right`. It is now required to have a `slot` to be positioned properly.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-item>
  <ion-label>Apple</ion-label>
  <ion-radio value="apple"></ion-radio>
</ion-item>

<ion-item>
  <ion-label>Grape, checked, disabled</ion-label>
  <ion-radio item-left value="grape" checked disabled></ion-radio>
</ion-item>

<ion-item>
  <ion-label>Cherry</ion-label>
  <ion-radio item-right color="danger" value="cherry"></ion-radio>
</ion-item>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-item>
  <ion-label>Apple</ion-label>
  <ion-radio slot="start" value="apple"></ion-radio>
</ion-item>

<ion-item>
  <ion-label>Grape, checked, disabled</ion-label>
  <ion-radio slot="start" value="grape" checked disabled></ion-radio>
</ion-item>

<ion-item>
  <ion-label>Cherry</ion-label>
  <ion-radio slot="end" color="danger" value="cherry"></ion-radio>
</ion-item>
```

### Radio Group

Radio group has been changed to an element. It should now be wrapped around any `<ion-radio>` elements as `<ion-radio-group>`.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-list radio-group>
  <ion-item>
    <ion-label>Apple</ion-label>
    <ion-radio value="apple"></ion-radio>
  </ion-item>

  <ion-item>
    <ion-label>Grape, checked, disabled</ion-label>
    <ion-radio value="grape" checked disabled></ion-radio>
  </ion-item>

  <ion-item>
    <ion-label>Cherry</ion-label>
    <ion-radio color="danger" value="cherry"></ion-radio>
  </ion-item>
</ion-list>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-list>
  <ion-radio-group>
    <ion-item>
      <ion-label>Apple</ion-label>
      <ion-radio slot="start" value="apple"></ion-radio>
    </ion-item>

    <ion-item>
      <ion-label>Grape, checked, disabled</ion-label>
      <ion-radio slot="start" value="grape" checked disabled></ion-radio>
    </ion-item>

    <ion-item>
      <ion-label>Cherry</ion-label>
      <ion-radio slot="start" color="danger" value="cherry"></ion-radio>
    </ion-item>
  </ion-radio-group>
</ion-list>
```


## Range

### Attributes Renamed

Previously to place content inside of a range the following attributes were used: `range-left`, `range-right`, (and with the added support of RTL) `range-start`, `range-end`.

These have been renamed to the following:

| Old Property                | New Property   | Property Behavior                                                     |
|-----------------------------|----------------|-----------------------------------------------------------------------|
| `range-left`, `range-start` | `slot="start"` | Positions to the left of the range in LTR, and to the right in RTL.   |
| `range-right`, `range-end`  | `slot="end"`   | Positions to the right of the range in LTR, and to the left in RTL.   |


**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-range>
  <ion-icon name="sunny" range-left></ion-icon>
  <ion-icon name="sunny" range-right></ion-icon>
</ion-range>

<ion-range>
  <ion-icon name="sunny" range-start></ion-icon>
  <ion-icon name="sunny" range-end></ion-icon>
</ion-range>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-range>
  <ion-icon name="sunny" slot="start"></ion-icon>
  <ion-icon name="sunny" slot="end"></ion-icon>
</ion-range>
```


## Segment

The markup hasn't changed for Segments, but now writing `<ion-segment-button>` will render a native button element inside of it.


## Select

The `selectOptions` property was renamed to `interfaceOptions` since it directly correlates with the `interface` property.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-select [selectOptions]="customOptions">
  ...
</ion-select>
```

```ts
this.customOptions = {
  title: 'Pizza Toppings',
  subTitle: 'Select your toppings'
};
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-select [interfaceOptions]="customOptions">
  ...
</ion-select>
```

```ts
this.customOptions = {
  title: 'Pizza Toppings',
  subTitle: 'Select your toppings'
};
```

## Spinner

### Name Changed

The `ios` and `ios-small` spinner's have been renamed to `lines` and `lines-small`, respectively. This also applies to any components that use spinner: `ion-loading`, `ion-infinite-scroll`, `ion-refresher`.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-spinner name="ios"></ion-spinner>

<ion-spinner name="ios-small"></ion-spinner>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-spinner name="lines"></ion-spinner>

<ion-spinner name="lines-small"></ion-spinner>
```


## Tabs

Some properties in `ion-tab` changed:

- [tabTitle] -> [label]
- [tabIcon] -> [icon]
- [tabBadge] -> [badge]
- [tabBadgeStyle] -> [badgeStyle]

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-tabs>
  <ion-tab tabTitle="Schedule" tabIcon="add"></ion-tab>
  <ion-tab tabTitle="Map" tabIcon="mao" tabBadge="2"></ion-tab>
</ion-tabs>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-tabs>
  <ion-tab label="Schedule" icon="add"></ion-tab>
  <ion-tab label="Map" icon="mao" badge="2"></ion-tab>
</ion-tabs>
```


## Text / Typography

### Markup Changed

Typography should now be written as an `<ion-text>` element. Previously the `ion-text` attribute could be added to any HTML element to set its color. It should now be used as a wrapper around the HTML elements to style.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<h1 ion-text color="secondary">H1: The quick brown fox jumps over the lazy dog</h1>

<h2 ion-text color="primary">H2: The quick brown fox jumps over the lazy dog</h2>

<h3 ion-text color="light">H3: The quick brown fox jumps over the lazy dog</h3>

<p>
  I saw a werewolf with a Chinese menu in his hand.
  Walking through the <sub ion-text color="danger">streets</sub> of Soho in the rain.
  He <i ion-text color="primary">was</i> looking for a place called Lee Ho Fook's.
  Gonna get a <a ion-text color="secondary">big dish of beef chow mein.</a>
</p>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-text color="secondary">
  <h1>H1: The quick brown fox jumps over the lazy dog</h1>
</ion-text>

<ion-text color="primary">
  <h2>H2: The quick brown fox jumps over the lazy dog</h2>
</ion-text>

<ion-text color="light">
  <h3>H3: The quick brown fox jumps over the lazy dog</h3>
</ion-text>

<p>
  I saw a werewolf with a Chinese menu in his hand.
  Walking through the <ion-text color="danger"><sub>streets</sub></ion-text> of Soho in the rain.
  He <ion-text color="primary"><i>was</i></ion-text> looking for a place called Lee Ho Fook's.
  Gonna get a <ion-text color="secondary"><a>big dish of beef chow mein.</a></ion-text>
</p>
```


## Theming

### Including Sass

Previously all `scss` files in the `src` directory were imported. Now each `scss` file should be included for the component via Angular's `styleUrls` metadata. View [Angular's Component Styles](https://angular.io/guide/component-styles) for more information.

This means that any styles wrapped with a page should now be removed since they will automatically be scoped to the component.

**ตัวอย่างการใช้งานแบบเก่า:**

```scss
page-schedule {
  p {
    color: red;
  }
}
```

**ตัวอย่างการใช้งานแบบใหม่:**

```scss
p {
  color: red;
}
```


### Sass Variables

Sass variables for changing the cordova statusbar have been renamed to app:

**ตัวอย่างการใช้งานแบบเก่า:**

```css
$cordova-ios-statusbar-padding:   20px;
$cordova-md-statusbar-padding:    20px;
```

**ตัวอย่างการใช้งานแบบใหม่:**

```css
$app-ios-statusbar-padding:   20px;
$app-md-statusbar-padding:    20px;
```


## Toolbar

### Menu Toggle

Previously if a `menuToggle` directive was added to an Ionic `button` in a toolbar, it would be positioned outside of the `ion-buttons` element. Since menu toggle is simply a wrapper to a button now, it should be placed inside of the `ion-buttons` element.

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-toolbar>
  <button ion-button menuToggle>
    <ion-icon name="menu"></ion-icon>
  </button>
  <ion-title>Left side menu toggle</ion-title>
</ion-toolbar>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-toolbar>
  <ion-buttons slot="start">
    <ion-menu-toggle>
      <ion-button>
        <ion-icon slot="icon-only" name="menu"></ion-icon>
      </ion-button>
    </ion-menu-toggle>
  </ion-buttons>
  <ion-title>Left side menu toggle</ion-title>
</ion-toolbar>
```

### Attributes Renamed

Previously to positions buttons inside of a toolbar the following attributes were used: `start`, `left`, `right`, `end`.

These have been renamed to the following:

| Old Property | New Property       | Property Behavior                                                                                        |
|--------------|--------------------|----------------------------------------------------------------------------------------------------------|
| `start`      | `slot="secondary"` | Positions element to the `left` of the content in `ios` mode, and directly to the `right` in `md` mode.  |
| `end`        | `slot="primary"`   | Positions element to the `right` of the content in `ios` mode, and to the far `right` in `md` mode.      |
| `left`       | `slot="start"`     | Positions to the `left` of the content in LTR, and to the `right` in RTL.                                |
| `right`      | `slot="end"`       | Positions to the `right` of the content in LTR, and to the `left` in RTL.                                |

**ตัวอย่างการใช้งานแบบเก่า:**

```html
<ion-toolbar>
  <ion-buttons left>
    <button ion-button>Left</button>
  </ion-buttons>
  <ion-buttons start>
    <button ion-button>Secondary</button>
  </ion-buttons>

  <ion-title>
    Title
  </ion-title>

  <ion-buttons end>
    <button ion-button>Primary</button>
  </ion-buttons>
  <ion-buttons right>
    <button ion-button>Right</button>
  </ion-buttons>
</ion-toolbar>
```

**ตัวอย่างการใช้งานแบบใหม่:**

```html
<ion-toolbar>
  <ion-buttons slot="start">
    <ion-button>Left</ion-button>
  </ion-buttons>
  <ion-buttons slot="secondary">
    <ion-button>Secondary</ion-button>
  </ion-buttons>

  <ion-title>
    Title
  </ion-title>

  <ion-buttons slot="primary">
    <ion-button>Primary</ion-button>
  </ion-buttons>
  <ion-buttons slot="end">
    <ion-button>Right</ion-button>
  </ion-buttons>
</ion-toolbar>
```