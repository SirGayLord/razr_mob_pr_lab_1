# Лабораторная работа №1. Создание Activity и передача параметров между ними.
* Выполнил: Кастырин Сергей
* Язык программирования: Java

# Что делает приложение?
Этот проект демонстрирует простой пример перехода между двумя экранами (Activity) в Android-приложении. 
Чтобы запустить проект можно прочитать ["Как запустить"](#как-запустить)

# Функциональность:
Приложение содержит две Activity:
  * MainActivity: 
    На первом экране находится кнопка "Перейти к Activity 2".
    

  * SecondActivity:
     На втором экране отображается текст "Переданный параметр: Кастырин", где Кастырин* - это строка, переданная из MainActivity.


# Дополнительные сведения:
* Проект использует стандартные компоненты Android: Activity, Intent, Button, TextView.
* Переход между Activity осуществляется с помощью Intent - объекта, который содержит информацию о том, какую Activity нужно запустить.
* Параметр передается с помощью putExtra("Фамилия", "Кастырин"), а затем извлекается в SecondActivity с помощью getIntent().getStringExtra("Фамилия").

# Как запустить:
1. Импортируйте проект: 
  * Загрузите или клонируйте этот репозиторий.
  * Откройте проект в Android Studio.
2. Запустите приложение:
  * Нажмите кнопку "Run" в Android Studio.
  * Выберите эмулятор или устройство для запуска приложения.
3. Нажмите кнопку:
  * На экране MainActivity нажмите кнопку "Перейти к Activity 2".
  * Вы перейдете на экран SecondActivity, где увидите фамилию Кастырин, переданную из MainActivity.

# Код:
* **MainActivity.java:**
```package com.example.myapplication;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {

    private Button btn1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        btn1 = findViewById(R.id.btn1);
        btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // Переход на Activity 2
                Intent intent = new Intent(MainActivity.this, SecondActivity.class);
                // Передача фамилии в качестве параметра
                intent.putExtra("familyName", "Кастырин"); 
                startActivity(intent);
            }
        });

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```
* **SecondActivity.java:**
```package com.example.myapplication;

import android.os.Bundle;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        TextView textView = findViewById(R.id.textView);

        // Получение переданного параметра
        String familyName = getIntent().getStringExtra("familyName");

        // Вывод переданного параметра в TextView
        textView.setText("Переданный параметр: " + familyName);

    }
}

```
* **activity_main.xml:**
```<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical"
    android:id="@+id/main">

    <Button
        android:id="@+id/btn1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/activity_2" />

</LinearLayout>
```
* **activity_second.xml:**
```<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/second"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

  <TextView
      android:id="@+id/textView"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="Кастырин" />

</LinearLayout>
```
