---
title: A. Qt Projects
permalink: /books/cmake-by-examples/chapter-16
---

- **Example 1. Basic Qt Application**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.5)

  project(QtBasicApp)

  set(CMAKE_CXX_STANDARD 11)

  find_package(Qt5 COMPONENTS Widgets REQUIRED)

  add_executable(QtBasicApp main.cpp)

  target_link_libraries(QtBasicApp Qt5::Widgets)
  ```

  ```cpp
  // main.cpp
  #include <QApplication>
  #include <QPushButton>

  int main(int argc, char *argv[]) {
      QApplication app(argc, argv);

      QPushButton button("Hello, Qt!");
      button.show();

      return app.exec();
  }
  ```

- **Example 2. Qt Application with Custom Widgets**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.5)

  project(QtCustomWidgetApp)

  set(CMAKE_CXX_STANDARD 11)

  find_package(Qt5 COMPONENTS Widgets REQUIRED)

  add_executable(QtCustomWidgetApp main.cpp customwidget.cpp)

  target_link_libraries(QtCustomWidgetApp Qt5::Widgets)
  ```

  ```cpp
  // main.cpp
  #include <QApplication>
  #include "customwidget.h"

  int main(int argc, char *argv[]) {
      QApplication app(argc, argv);

      CustomWidget widget;
      widget.show();

      return app.exec();
  }
  ```

  ```cpp
  // customwidget.h
  #ifndef CUSTOMWIDGET_H
  #define CUSTOMWIDGET_H

  #include <QWidget>

  class CustomWidget : public QWidget {
      Q_OBJECT

  public:
      CustomWidget(QWidget *parent = nullptr);
  };

  #endif // CUSTOMWIDGET_H
  ```

  ```cpp
  // customwidget.cpp

  #include "customwidget.h"
  #include <QPushButton>
  #include <QVBoxLayout>

  CustomWidget::CustomWidget(QWidget *parent) : QWidget(parent) {
      QVBoxLayout *layout = new QVBoxLayout(this);
      QPushButton *button = new QPushButton("Custom Widget Button", this);
      layout->addWidget(button);
      setLayout(layout);
  }
  ```

- **Example 3. Qt Application with Resources**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.5)

  project(QtResourceApp)

  set(CMAKE_CXX_STANDARD 11)

  find_package(Qt5 COMPONENTS Widgets REQUIRED)

  qt5_add_resources(RESOURCES resources.qrc)

  add_executable(QtResourceApp main.cpp ${RESOURCES})

  target_link_libraries(QtResourceApp Qt5::Widgets)
  ```

  ```cpp
  // main.cpp

  #include <QApplication>
  #include <QLabel>
  #include <QPixmap>

  int main(int argc, char *argv[]) {
      QApplication app(argc, argv);

      QLabel label;
      label.setPixmap(QPixmap(":/images/logo.png"));
      label.show();

      return app.exec();
  }
  ```

  ```xml
  <!-- resources.qrc -->

  <RCC>
      <qresource prefix="/">
          <file alias="logo.png">images/logo.png</file>
      </qresource>
  </RCC>
  ```

- **Example 4. Qt Application with Translation**

  ```cmake
  # CMakeLists.txt
  cmake_minimum_required(VERSION 3.5)

  project(QtTranslationApp)

  set(CMAKE_CXX_STANDARD 11)

  find_package(Qt5 COMPONENTS Widgets LinguistTools REQUIRED)

  set(TS_FILES translations_en.ts translations_fr.ts)

  qt5_add_translation(QM_FILES ${TS_FILES})

  add_executable(QtTranslationApp main.cpp ${QM_FILES})

  target_link_libraries(QtTranslationApp Qt5::Widgets)
  ```

  ```cpp
  // main.cpp

  #include <QApplication>
  #include <QTranslator>
  #include <QLocale>
  #include <QPushButton>
  #include <QVBoxLayout>
  #include <QWidget>

  int main(int argc, char *argv[]) {
      QApplication app(argc, argv);

      QTranslator translator;
      QString locale = QLocale::system().name();
      translator.load(QString("translations_") + locale);
      app.installTranslator(&translator);

      QWidget window;
      QVBoxLayout layout(&window);

      QPushButton button(QObject::tr("Hello, Qt!"));
      layout.addWidget(&button);

      window.show();

      return app.exec();
  }
  ```

  ```xml
  <!-- translations_en.ts -->
  <?xml version="1.0" encoding="utf-8"?>
  <!DOCTYPE TS>
  <TS version="2.1" language="en">
  <context>
      <name>MainWindow</name>
      <message>
          <location filename="main.cpp" line="15"/>
          <source>Hello, Qt!</source>
          <translation>Hello, Qt!</translation>
      </message>
  </context>
  </TS>
  ```

  ```xml
  <!-- translations_fr.ts -->
  <?xml version="1.0" encoding="utf-8"?>
  <!DOCTYPE TS>
  <TS version="2.1" language="fr">
  <context>
      <name>MainWindow</name>
      <message>
          <location filename="main.cpp" line="15"/>
          <source>Hello, Qt!</source>
          <translation>Bonjour, Qt!</translation>
      </message>
  </context>
  </TS>
  ```
