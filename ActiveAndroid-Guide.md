#ActiveAndroid Guide

##概述

使用ActiveAndroid ORM使得管理客户端Model在通常情况下变得非常容易。对于更高级的或自定义的情况下，你可以使用SQLiteOpenHelper直接管理数据库的通信。但是从JSON简单的模型映射上看，ActiveAndroid保持简单。

ActiveAndroid像任何对象关系映射通过映射Java类到数据库表和映射Java类的成员变量表列。通过这一过程，每个表映射到一个Java模型和列在表中表示的各数据字段。同样地，在数据库中的每一行代表一个特定的对象。这使我们能够创建，修改，删除和使用模型对象，而不是原始的SQL查询我们的SQLite数据库。

例如，“Tweet”的模式将被映射到一个“Tweet”表在数据库中。Tweet模型可能有一个“body”字段映射到一个机构列在表和一个“timestamp”字段映射到一个时间戳列。通过这个过程中，每一行将映射到一个特定的Tweet。

##安装

```
repositories {
    mavenCentral()
    maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
}

compile 'com.michaelpardo:activeandroid:3.1.0-SNAPSHOT'
```

##配置

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    ...>
    <!- adjust the name property of your application node ->
    <application
        android:name="com.activeandroid.app.Application"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >

        <!- add the following metadata for version and database name ->
        <meta-data
            android:name="AA_DB_NAME"
            android:value="RestClient.db" />
        <meta-data
            android:name="AA_DB_VERSION"
            android:value="1" />

        <activity
            android:name="com.codepath.apps.activities.MainActivity"
            android:noHistory="true"
            android:label="@string/app_name" >
            <!- ... ->
        </activity>
    </application>
</manifest>
```