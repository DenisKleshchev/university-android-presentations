# Anroid User Interface
### Android
#### Денис Клещев

---

## UI Overview

* Весь графический интерфейс строится из объектов классов View и ViewGroup
* View - нечто, что может быть нарисованно на экране и с чем пользователь может взаимодействовать
* ViewGroup - наследник View, содержит в себе другие View и определяет как они будут расположенны относительно друг друга
* AdapterView - особый наследник ViewGroup, дочерние элементы которого задаются с помощью Adapter’a

---

## UI Overview

![Views hierarchy](http://i.stack.imgur.com/vYsMp.png)

---

## Declaring Views

* Дерево View может быть создано прямо в коде
* Более простой и предпочтительный способ - использовать XML
* Это декларативно (говорим что делать, а не как)
* Позволяет отделить графический интерфейс и логику
* Меньше усилий и более читабельно
* Переиспользуемо
* Для разных конфигураций могут быть созданы разные XML файлы, при этом коду знать об этом не обязательно

---

## Common Views

* TextView - нередактируемое текстовое поле
* EditText - редактируемое текстовое поле
* ImageView – картинка
* Button – кнопочка
* CheckBox - галочка

---

## Attributes

* В xml поведение отдельного View можно настраивать с помощью аттрибутов
* Существует набор аттрибутов общих для всех View
* Почти каждый наследник View имеет свой собственный набор специфичных для него аттрибутов
* Можно создавать свои собственные аттрибуты
* Часто для каждого аттрибута существуют соответствующие ему методы

---

## Common Attributes

* android:id - уникальный идентификатор
* android:layout_width - ширина элемента
* android:layout_height - высота элемента
* android:layout_margin - отступы снаружи элемента
* android:padding - отступы внутри элемента
* android:layout_gravity - расположение элемента внутри родителя
* android:gravity - расположение контента внутри элемента
* android:visibility - показывать элемент или нет
* android:background - фоновое изображение
* ...

---

## Unique Attributes

* TextView
    * android:text – текст
    * android:textSize – размер
    * android:textColor – цвет
    * android:textStyle - стиль (bold, italic, monospace)
    * android:singleLine - максимум одна строка текста
    * android:maxLines - максимальное число строк текста
    * android:ellipsize - что делать, если текст слишком длинный
--- 

## Unique Attributes

* EditText
    * android:hint - подсказка, видна пока EditText пустой
    * android:textColorHint - цвет подсказки
    * android:inputType - тип клавиатуры (email, телефон и т.д.)
    * android:digits - список допустимых символов
* ImageView
    * android:src - что показывать
    * android:scaleType - как масштабировать
    * android:adjustViewBounds - меняем размеры View в зависимости от размеров картинки

---

## Dimension Units

* px - реальные пиксели на экране
* pt - points, 1/72 дюйма
* mm – миллиметры
* in – дюймы
* dip - density independent pixels. Количество пикселей одном dip зависит от плотности экрана
* sp - scaled pixels. Аналогичны dip + размер зависит от выбранного размера шрифта пользователем
* процентов нет

---

## Dimension Units: PX vs DP

![Bad practice](http://developer.android.com/images/screens_support/density-test-bad.png)

![Good practice](http://developer.android.com/images/screens_support/density-test-good.png)

---

## Drawable Types

* ColorDrawable - просто цвет
* BitmapDrawable - просто картинка
* NinePatchDrawable - картинка, которая умеет правильно растягиваться
* StateListDrawable - меняет свой контент в зависимости от состояния
* ShapeDrawable - набор свойств таких как: просто цвет, радиус скругления, градиент, обводка.

---

## Drawable Types

`drawable/view_selector.xml` :

    !xml
    <?xml version="1.0" encoding="utf-8"?>
    <selector xmlns:android="http://schemas.android.com/apk/res/android">
        <item android:drawable="@drawable/icon" 
                                android:state_enabled="true" />
        <item android:drawable="@drawable/icon_inactive" 
                                android:state_enabled="false" />
    </selector>

`drawable/view_bg_shape.xml` :

    !xml
    <shape xmlns:android="http://schemas.android.com/apk/res/android"
        android:shape="rectangle">
        <solid android:color="@color/blue" />
        <corners android:radius="2dp" />
    </shape>

---

## Input Handling

* View.setOnClickListener
* View.setOnLongClickListener
* View.setOnFocusChangeListener
* View.setOnTouchListener
* TextView.addTextChangedListener
* CompoundButton.setOnCheckedChangeListener
* AdapterView.setOnItemClickListener

---

## Common Layouts

* FrameLayout - рисует дочерние View поверх друг друга
* LinearLayout - выстраивает свои элементы в одну линию
* RelativeLayout - хитро располагает элементы относительно друг друга
* ListView - список
* GridLayout - дочерние View располагаются по сеточке
* ScrollView - добавляет скролл, если контент слишком большой
* TableLayout - таблица для статичных данных

---

## Take a look

    !xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
                  android:orientation="vertical"
                  android:layout_width="match_parent"
                  android:layout_height="match_parent">
        <ImageView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:adjustViewBounds="true"
            android:src="@drawable/android_logo"/>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="15dp"
            android:layout_marginBottom="10dp"
            android:orientation="horizontal">
            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:gravity="center"
                android:textSize="18sp"
                android:text="Hi there..."/>
    
            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:gravity="center"
                android:textSize="18sp"
                android:text="... and here!"/>
        </LinearLayout>

        <Button
                android:id="@+id/rtn_proceed"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="Proceed"/>
    </LinearLayout>

---

## Take a look

![](img/layot_demo.png)

---

## Linear vs Relative


<table>
    <tr>
        <td><img title="LinearLayout" src="img/linear_layout.png" alt=""width="250"/></td>
        <td><img title="RelativeLayout" src="img/relative_layout.png" alt=""width="250"/></td>
    </tr>
</table>

---

## ListView

* Отображение вертикального списка однотипных данных
* Переиспользует созданные вьюхи
* Можно добавлять хедеры и футеры
* Необходимо использовать класс Adapter

---

## BaseAdapter

Необходимо переопределить:

* int getCount()
* getItem(int position)
* getItemId(int position)
* getView(int position, View convertView, ViewGroup parent)

---

## ListView Example
    !java
    public class DemoAdapter extends BaseAdapter {
        private LayoutInflater inflater;
        private String[] data = {"Написать список", "Выполнить пункт #1",
                "Выполнить пункт #2", "Сделать половину списка", "О_О",
                "Забыть что-нибудь", "Пойти довольным отдыхать"};
    
        public DemoAdapter(Context context) {
            inflater = LayoutInflater.from(context);
        }
    
        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            View view;
            if(convertView == null) {
                view = inflater.inflate(R.layout.list_item, parent, false);
            } else {
                view = convertView;
            }
    
            TextView titleView = (TextView) view.findViewById(R.id.title);
            titleView.setText(getItem(position).toString());
    
            return view;
        }
    
        @Override
        public Object getItem(int position) {
            return data.[position];
        }
    
        @Override
        public int getCount() {
            return data.lenght;
        }
    
        @Override
        public long getItemId(final int position) {
            return position;
        }
    }

---

## ListView example
    !xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                  android:orientation="vertical"
                  android:layout_width="match_parent"
                  android:layout_height="70dp">
    
        <TextView
            android:id="@+id/title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textColor="#000"
            android:text="@string/default_title"
            android:layout_centerVertical="true"
            android:layout_alignParentLeft="true"/>
    
        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_alignParentRight="true"/>
    
    </RelativeLayout>

---

## ListView example
    !java
    public class MainActivity extends Activity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
    
            ListView listView = (ListView) findViewById(R.id.list_view);
    
            DemoAdapter adapter = new DemoAdapter(getApplicationContext());
            listView.setAdapter(adapter);
        }
    }

---

## ListView demo

![](img/list_demo.png)

---

## Header & footer

    !java
    View header = getLayoutInflater().inflate(R.layout.header, listView, false);
    ImageView image = (ImageView) header.findViewById(R.id.image);
    listView.addHeaderView(header);

Пара нюансов:

1. Header устанавливается до того, как задается адаптер.
2. Каждый Header становится нулевым элементом, увеличивает позицию элемента списка на 1. Для получиния нормальноай позиции элемента можно воспользоваться методом `listView.getItemAtPosition(position)`. Также можно вручную узнать количество хедеров `listView.getHeaderViewsCount()`.

---

## Common Adapters

* ArrayAdapter
* CursorAdapter
* SimpleAdapter

---

## ViewHolder pattern

Вызов `findViewById` может быть дорогим. ViewHolder позволяет закешировать результаты:

    !java
    public class ViewHolder {
        TextView title;

        public ViewHolder(View view) {
            title = (TextView) view.findViewById(R.id.title);
        }
    }

И использование:

    !java
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View view;
        if (convertView == null) {
            view = inflater.inflate(R.layout.list_item parent, false);
            view.setTag(new ViewHolder(view));
        } else {
            view = convertView;
        }
        ViewHolder holder = (ViewHolder) view.getTag();
        holder.title.setText("Hello");
    }



---

## RecyclerView

ListView 80го уровня. Особенности:

* Обязательное использование паттерна `ViewHolder`
* `LayoutManager`
    - `LinearLayoutManager`
    - `GridLayoutManager`
    - `StaggeredGridLayoutManager`
    - Custom   

---

## RecyclerView

Анимация операций со списком:

    !java
    RecyclerView.ItemAnimator itemAnimator = new DefaultItemAnimator();
        recyclerView.setItemAnimator(itemAnimator);

---

## CardView
    !xml
    <android.support.v7.widget.CardView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:id="@+id/cardView"
        card_view:cardCornerRadius="6dp"
        card_view:cardBackgroundColor="@android:color/holo_blue_dark">

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/info_text"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Test CardView"
                android:layout_centerInParent="true"
                android:textSize="18sp"
                android:textColor="#fff"/>
        </RelativeLayout>
    </android.support.v7.widget.CardView>

---

## CardView

<img src="img/card_view.png" style="width: 300px">

---

## Custom Views

* Добавление атрибутов
* Расширение существующей View
* Переопределение методов базового класса

---

## Custom Views: атрибуты

Описание атрибутов в res/values/attrs.xml

* declare-styleable
    * name - имя класса
* attr
    * name - имя атрибута, который будет использоваться в разметке
    * format - тип атрибута
        * integer
        * float
        * string
        * color
        * dimension
        * reference
        * ...        

---

## Custom Views: атрибуты

    !xml
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <declare-styleable name="CustomImageView">
            <attr name="foreground_image" format="reference"/>
            <attr name="foreground_image_margin" format="dimension|reference"/>
        </declare-styleable>
    </resources>

---

## Custom Views: Наследование

1. Получить атрибуты в конструкторе

        !java
        TypedArray a = 
            context.obtainStyledAttributes(attrs, R.styleable.CustomImageView);

2. Получить нужные значения

        !java
        Drawable foregroundDrawable = 
            a.getDrawable(R.styleable.CustomImageView_foreground_image);

        float margin = 
            a.getDimension(R.styleable.CustomImageView_foreground_image_margin, 0);

    
3. Не забыть освободить ресуры обратно

        !java
        a.recycle();

---
## Custom Views: Наследование

4. Использовать полученные параметры

        !java
        @Override
        protected void onDraw(final Canvas canvas) {
            super.onDraw(canvas);

            if(foregroundDrawable != null) {
                foregroundDrawable.draw(canvas);
            }
        }

5. При изменении состояния запросить отрисовку

        !java
        public void setForegroundDrawable(Drawable drawable) {
           this.drawable = drawable;
           invalidate();
           requestLayout();
        }

---

## Custom Views: Наследование

* onDraw
* onTouchEvent
* onMeasure
* onSizeChanged
* ...

---

## Custom Views: Использование

Для использования своих атрибутов необходимо добавить пространство имен `http://schemas.android.com/apk/res-auto`

Важно также помнить, что использовании созданного компонента указывается полное имя класса.

    !xml
    <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
             xmlns:app="http://schemas.android.com/apk/res-auto"
             android:layout_width="match_parent"
             android:layout_height="match_parent">

        <com.noveogroup.internship.ui.view.CustomImageView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:foreground_image="@drawable/abc_btn_check_material"
            app:foreground_image_margin="15dp"/>
    
    </FrameLayout>


---

## ConstraintLayout

![](img/constraint_studio.png)

---

## ConstraintLayout

* Resize Handle

![](img/resize_handle.gif)

---

## ConstraintLayout

* Size Constraint Handle

![](img/size_constraint_handle.gif)

---

## ConstraintLayout

* Baseline Constraint Handle

![](img/baseline_constraint_handle.gif)

---

## ConstraintLayout

* Bias

![](img/bias.gif)

---

## ConstraintLayout

* Управление размерами виджета

![](img/size_params.gif)

---

## ConstraintLayout

* Autoconnect

![](img/autoconnect.gif)

---

## ConstraintLayout

* Constraints, заданные вручную

![](img/manual_constraints.gif)

---

## ConstraintLayout

* Inference

![](img/inference.gif)

---

## Дополнительные ссылки

* [http://developer.android.com/guide/topics/ui/index.html](http://developer.android.com/guide/topics/ui/index.html)
* [http://developer.android.com/training/best-ui.html](http://developer.android.com/training/best-ui.html)
* [http://developer.android.com/training/improving-layouts/index.html](http://developer.android.com/training/improving-layouts/index.html)
* [http://developer.android.com/training/custom-views/index.html](http://developer.android.com/training/custom-views/index.html)
* [http://developer.android.com/reference/android/view/View.html](http://developer.android.com/reference/android/view/View.html)
* [http://developer.android.com/guide/topics/ui/custom-components.html](http://developer.android.com/guide/topics/ui/custom-components.html)
* [http://developer.android.com/guide/topics/resources/drawable-resource.html](http://developer.android.com/guide/topics/resources/drawable-resource.html)
* [http://developer.android.com/training/improving-layouts/optimizing-layout.html](http://developer.android.com/training/improving-layouts/optimizing-layout.html)
