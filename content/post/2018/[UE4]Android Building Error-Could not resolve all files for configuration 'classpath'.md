+++
title= "[UE4]Android Building Error-Could not resolve all files for configuration 'classpath'"
date= "2018-09-05T22:43:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Materials"]
+++

##### Error 1

Error Log:

    A problem occurred configuring root project 'app'.
     > Could not resolve all files for configuration ':classpath'.
        > Could not download kotlin-reflect.jar (org.jetbrains.kotlin:kotlin-reflect:1.1.3-2)
           > Could not get resource 'https://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-reflect/1.1.3-2/kotlin-reflect-1.1.3-2.jar'.
              > Could not GET 'https://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-reflect/1.1.3-2/kotlin-reflect-1.1.3-2.jar'.
                 > Software caused connection abort: recv failed
    > Could not download protobuf-java.jar (com.google.protobuf:protobuf-java:3.0.0)
       > Could not get resource 'https://jcenter.bintray.com/com/google/protobuf/protobuf-java/3.0.0/protobuf-java-3.0.0.jar'.
          > Could not GET 'https://jcenter.bintray.com/com/google/protobuf/protobuf-java/3.0.0/protobuf-java-3.0.0.jar'.
             > Software caused connection abort: recv failed
    
Solution:  
modify config file `UE_4.20\Engine\Build\Android\Java\gradle\build.gradle`,  
add these into `build.gradle`

    jcenter() {
            url "http://jcenter.bintray.com/"
        }

all content:

    // Top-level build file where you can add configuration options common to all sub-projects/modules.

    buildscript {
        repositories {
            google()
            jcenter() {
                url "http://jcenter.bintray.com/"
            }
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:3.0.1'

            // NOTE: Do not place your application dependencies here; they belong
            // in the individual module build.gradle files
        }
        apply from: 'buildscriptAdditions.gradle', to: buildscript
    }

    apply from: 'baseBuildAdditions.gradle'

    allprojects {
        repositories {
            google()
            jcenter()
        }
    }

    task clean(type: Delete) {
        delete rootProject.buildDir
    }


##### Error 2
    
Error Log:
    
    A problem occurred configuring root project 'app'.
     > Could not resolve all files for configuration ':classpath'.
        > Could not download kotlin-reflect.jar (org.jetbrains.kotlin:kotlin-reflect:1.1.3-2)
           > Could not get resource 'http://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-reflect/1.1.3-2/kotlin-reflect-1.1.3-2.jar'.
              > Could not GET 'http://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-reflect/1.1.3-2/kotlin-reflect-1.1.3-2.jar'.
                 > Remote host closed connection during handshake
        > Could not download kotlin-stdlib.jar (org.jetbrains.kotlin:kotlin-stdlib:1.1.3-2)
           > Could not get resource 'http://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-stdlib/1.1.3-2/kotlin-stdlib-1.1.3-2.jar'.
              > Could not HEAD 'http://jcenter.bintray.com/org/jetbrains/kotlin/kotlin-stdlib/1.1.3-2/kotlin-stdlib-1.1.3-2.jar'.
                 > Remote host closed connection during handshake
        > Could not download protobuf-java.jar (com.google.protobuf:protobuf-java:3.0.0)
           > Could not get resource 'http://jcenter.bintray.com/com/google/protobuf/protobuf-java/3.0.0/protobuf-java-3.0.0.jar'.
              > Could not GET 'http://jcenter.bintray.com/com/google/protobuf/protobuf-java/3.0.0/protobuf-java-3.0.0.jar'.
                 > Remote host closed connection during handshake
        > Could not download bcpkix-jdk15on.jar (org.bouncycastle:bcpkix-jdk15on:1.56)
           > Could not get resource 'http://jcenter.bintray.com/org/bouncycastle/bcpkix-jdk15on/1.56/bcpkix-jdk15on-1.56.jar'.
              > Could not HEAD 'http://jcenter.bintray.com/org/bouncycastle/bcpkix-jdk15on/1.56/bcpkix-jdk15on-1.56.jar'.
                 > Remote host closed connection during handshake
        > Could not download bcprov-jdk15on.jar (org.bouncycastle:bcprov-jdk15on:1.56)
           > Could not get resource 'http://jcenter.bintray.com/org/bouncycastle/bcprov-jdk15on/1.56/bcprov-jdk15on-1.56.jar'.
              > Could not HEAD 'http://jcenter.bintray.com/org/bouncycastle/bcprov-jdk15on/1.56/bcprov-jdk15on-1.56.jar'.
                 > Remote host closed connection during handshake
        > Could not download fastutil.jar (it.unimi.dsi:fastutil:7.2.0)
           > Could not get resource 'http://jcenter.bintray.com/it/unimi/dsi/fastutil/7.2.0/fastutil-7.2.0.jar'.
              > Could not HEAD 'http://jcenter.bintray.com/it/unimi/dsi/fastutil/7.2.0/fastutil-7.2.0.jar'.
                 > Remote host closed connection during handshake
     * Try:
     Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.
     * Get more help at https://help.gradle.org
    
Solution:  
Project Settings -> Platforms -> Android -> Uncheck "Enable Gradle instead of Ant"
